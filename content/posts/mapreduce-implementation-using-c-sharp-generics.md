---
title: "MapReduce Implementation Using C# Generics"
url: "/mapreduce-implementation-using-csharp-generics"
date: 2008-01-23T17:57:34+02:00
---

I came across the Google paper on [MapReduce](http://www.usenix.org/events/osdi04/tech/full_papers/dean/dean.pdf) 
again the other day and decided to try a simple implementation using C# generics allowing you to specify specific 
types for the keys and values as opposed to being forced to use strings for all keys and values.

The initial version doesn't include any automatic parallelism across multiple CPUs or clusters 
of machines.

The core implementation below is only about 50-60 lines of code. I've also included sample map 
and reduce functions making use of this library and mirroring some of the sample applications mentioned in the Google paper.

```c#
using System;
using System.Collections.Generic;

// Common shortcut where both keys and both values are strings
using MapReduceAllStrings = MapReduce.MapReduce<string,string,string,string>;

namespace MapReduce
{

// Map delegate
public delegate IEnumerable<KeyValuePair<K2,V2>> Map<K,V,K2,V2>(KeyValuePair<K,V> input);

// Reduce delegate
public delegate IEnumerable<V2> Reduce<K2,V2>(KeyValuePair<K2, IEnumerable<V2>> input);

public class MapReduce<K, V, K2, V2>
{
    // Process input data using user supplied map and reduce delegates
    public IEnumerable<KeyValuePair<K2, IEnumerable<V2>>> Process(IEnumerable<KeyValuePair<K,V>> input, Map<K,V,K2,V2> map, Reduce<K2,V2> reduce)
    {
        // Use dictionary to store intermdiate data - (k2, list(v2))
        Dictionary<K2, IEnumerable<V2>> intermediateData = new Dictionary<K2, IEnumerable<V2>>();

        // Perform map over all input
        foreach (KeyValuePair<K, V> inputItem in input)
        {
            // Add map results to intermediate dictionary
            foreach(KeyValuePair<K2,V2> mapOutput in map(inputItem))
            {
                IEnumerable<V2> enumerableList;

                // If k2 already exists in dictionary then just add this v2 to it's list(v2)
                if (intermediateData.TryGetValue(mapOutput.Key, out enumerableList))
                {
                    List<V2> v2List = (List<V2>)enumerableList;
                    v2List.Add(mapOutput.Value);
                }
                else
                {
                    // Add new k2 to dictionary and create initial list(v2) with this v2 value
                    List<V2> v2List = new List<V2>();
                    v2List.Add(mapOutput.Value);
                    intermediateData.Add(mapOutput.Key, v2List);
                }
            }
        }

        // Setup final output data structure
        List<KeyValuePair<K2, IEnumerable<V2>>> finalOutput = new List<KeyValuePair<K2,IEnumerable<V2>>>();

        // Perform reduce over all intermediate data
        foreach (KeyValuePair<K2, IEnumerable<V2>> intermediateVal in intermediateData)
        {
            // Setup final output value, i.e. k2 and an empty list(v2) in preparation for reduce operation
            KeyValuePair<K2, IEnumerable<V2>> outputVal = new KeyValuePair<K2, IEnumerable<V2>>(intermediateVal.Key, new List<V2>());
            finalOutput.Add(outputVal);

            // Perform reduce over all intermediate data
            foreach (V2 val in reduce(intermediateVal))
            {
                // Add resultant values from reduce to final output list(v2)
                ((List<V2>)(outputVal.Value)).Add(val);
            }
        }

        return finalOutput;
    }

    public static IEnumerable<V2> IdentityReduce(KeyValuePair<K2, IEnumerable<V2>> input)
    {
        List<V2> output = new List<V2>();

        foreach (V2 val in input.Value)
        {
            output.Add(val);
        }

        return output;
    }
}

class MapReduceTest
{
    static void Main(string[] args)
    {
        WordCountTest();

        ReverseWebLinkGraph();
    }

    /////////////////// - WordCount test

    static void WordCountTest()
    {
        List<KeyValuePair<string, string>> input = new List<KeyValuePair<string, string>>
            {
                new KeyValuePair<string,string>("a", "the quick brown fox jumps over the log"),
                new KeyValuePair<string,string>("b", "while the mokey jumps on the fox"),
                new KeyValuePair<string,string>("c", "and the cow jumps over the moon")
            };

        MapReduce<string, string, string, int> WordCount = new MapReduce<string, string, string, int>();

        foreach(KeyValuePair<string,IEnumerable<int>> val in WordCount.Process(input, WordCountMap, WordCountReduce))
        {
            PrintResult<string, int>(val);
        }
    }

    static IEnumerable<KeyValuePair<string, int>> WordCountMap(KeyValuePair<string, string> input)
    {
        List<KeyValuePair<string, int>> output = new List<KeyValuePair<string, int>>();

        string[] words = input.Value.Split(' ');

        foreach (string word in words)
        {
            output.Add(new KeyValuePair<string,int>(word, 1));
        }

        return output;
    }

    static IEnumerable<int> WordCountReduce(KeyValuePair<string, IEnumerable<int>> input)
    {
        List<int> output = new List<int>();

        int total = 0;
        foreach (int wc in input.Value)
        {
            total += wc;
        }

        output.Add(total);

        return output;
    }

    /////////////////// - Reverse web link graph test

    static void ReverseWebLinkGraph()
    {
        List<KeyValuePair<string, string>> input = new List<KeyValuePair<string, string>>
            {
                new KeyValuePair<string,string>("abc.com", "cnn.com ibm.com dti.com"),
                new KeyValuePair<string,string>("cnn.com", "ms.com slashdot.org abc.com iol.com dti.com"),
                new KeyValuePair<string,string>("dti.com", "ibm.com avd.com abc.com")
            };

        MapReduceAllStrings ReverseWebLinks = new MapReduceAllStrings();

        foreach (KeyValuePair<string, IEnumerable<string>> val in ReverseWebLinks.Process(input, ReverseWebLinksMap, MapReduceAllStrings.IdentityReduce))
        {
            PrintResult<string, string>(val);
        }
    }

    static IEnumerable<KeyValuePair<string, string>> ReverseWebLinksMap(KeyValuePair<string, string> input)
    {
        List<KeyValuePair<string, string>> output = new List<KeyValuePair<string, string>>();

        string[] targets = input.Value.Split(' ');

        foreach (string target in targets)
        {
            output.Add(new KeyValuePair<string, string>(target, input.Key));
        }

        return output;
    }

    /////////////////// - Helper

    static void PrintResult<K,V>(KeyValuePair<K, IEnumerable<V>> result)
    {
        Console.Write(result.Key.ToString());
        Console.Write(" - ");
        foreach(V val in result.Value)
        {
            Console.Write(val.ToString());
            Console.Write(" ");
        }
        Console.WriteLine("");
    }

}

}
```