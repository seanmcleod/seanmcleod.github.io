---
title: "Live Photo Gallery People Tags"
date: 2008-10-08T17:30:57+02:00
---

I've used the tagging feature in the original Windows Vista Photo Gallery and the Windows Live Photo Gallery 
versions for tagging people in photos and the location of the photo.

![image alt text](/images/live-photo-gallery-people-tags/image_thumb4.jpg)

The latest version of Windows Live Photo Gallery now includes a specific 'People' category separate from the 
generic tags category for identifying people in photos. In addition it includes a feature to automatically 
identify faces in photos and to associate the 'People' tags with specific faces in the photo.

The sample below taken from the Windows Live Photo blog shows the new face tagging features. You can also 
manually draw a rectangle over a face and tag it if the Photo Gallery doesn't automatically detect the face.

xx

One issue I've noticed is that the new people tags aren't indexed by Windows Search. I often use Windows Search 
to search for photos based on my people and location tags and the new people tags aren't found. So at the moment 
you have to search or filter photos based on the new people tags in Live Photo Gallery itself.

I took a look at the XMP meta-data that is stored by the new people tagging feature in the associated photos.

In the snippet below you can see how the rectangular region for the relevant face is stored if there is one plus 
the **PersonDisplayName**. There are APIs in WIC plus associated .Net wrappers in the .Net Framework that allow you to 
read this meta-data so you could make use of the rectangular regions in your own application that may want to display 
photos and show the tagged faces etc.

```xml
<rdf:Description xmlns:prefix0="http://ns.microsoft.com/photo/1.2/">
  <prefix0:RegionInfo>
    <rdf:Description xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#">
      <prefix1:Regions xmlns:prefix1="http://ns.microsoft.com/photo/1.2/t/RegionInfo#">
        <rdf:Bag xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#">
          <rdf:li>
            <rdf:Description xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#">
              <prefix2:Rectangle xmlns:prefix2="http://ns.microsoft.com/photo/1.2/t/Region#">0.209985, 0.526367, 0.167401, 0.111328</prefix2:Rectangle>
              <prefix3:PersonDisplayName xmlns:prefix3="http://ns.microsoft.com/photo/1.2/t/Region#">Sarah McLeod</prefix3:PersonDisplayName>
            </rdf:Description>
          </rdf:li>
          <rdf:li>
            <rdf:Description xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#">
              <prefix4:Rectangle xmlns:prefix4="http://ns.microsoft.com/photo/1.2/t/Region#">0.430250, 0.148438, 0.284875, 0.189453</prefix4:Rectangle>
              <prefix5:PersonDisplayName xmlns:prefix5="http://ns.microsoft.com/photo/1.2/t/Region#">Gwen De Roubaix</prefix5:PersonDisplayName>
            </rdf:Description>
          </rdf:li>
          <rdf:li>
            <rdf:Description xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#">
              <prefix6:PersonDisplayName xmlns:prefix6="http://ns.microsoft.com/photo/1.2/t/Region#">Marcelle De Roubaix</prefix6:PersonDisplayName>
            </rdf:Description>
          </rdf:li>
        </rdf:Bag>
      </prefix1:Regions>
    </rdf:Description>
  </prefix0:RegionInfo>
</rdf:Description>
```

The following snippet shows the XMP meta-data that is stored if you tag one of your Messenger contacts as a People tag.

```xml
<rdf:Description rdf:about="uuid:faf5bdd5-ba3d-11da-ad31-d33d75182f1b" xmlns:prefix0="http://ns.microsoft.com/photo/1.2/">
  <prefix0:RegionInfo>
    <rdf:Description xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#">
      <prefix1:Regions xmlns:prefix1="http://ns.microsoft.com/photo/1.2/t/RegionInfo#">
        <rdf:Bag xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#">
          <rdf:li>
            <rdf:Description xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#">
              <prefix2:PersonDisplayName xmlns:prefix2="http://ns.microsoft.com/photo/1.2/t/Region#">gerhard</prefix2:PersonDisplayName>
              <prefix3:PersonEmailDigest xmlns:prefix3="http://ns.microsoft.com/photo/1.2/t/Region#">89C386678731AB3D7DEE0E14E11E633387FBDBCD</prefix3:PersonEmailDigest>
              <prefix4:PersonLiveIdCID xmlns:prefix4="http://ns.microsoft.com/photo/1.2/t/Region#">8765613456339678115</prefix4:PersonLiveIdCID>
            </rdf:Description>
          </rdf:li>
        </rdf:Bag>
      </prefix1:Regions>
    </rdf:Description>
  </prefix0:RegionInfo>
</rdf:Description>
```

And lastly a snippet showing how the regular tags which are indexed by Windows Search are stored, basically in a 
**\<dc:subject\>** element and in a **\<MicrosoftPhoto:LastKeywordXMP\>** element.

```xml
<rdf:Description xmlns:dc="http://purl.org/dc/elements/1.1/">
  <dc:subject>
    <rdf:Bag xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#">
      <rdf:li>Party</rdf:li>
      <rdf:li>People/Sarah McLeod</rdf:li>
    </rdf:Bag>
  </dc:subject>
</rdf:Description>
<rdf:Description xmlns:MicrosoftPhoto="http://ns.microsoft.com/photo/1.0">
  <MicrosoftPhoto:LastKeywordXMP>
    <rdf:Bag xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#">
      <rdf:li>Party</rdf:li>
      <rdf:li>People/Sarah McLeod</rdf:li>
    </rdf:Bag>
  </MicrosoftPhoto:LastKeywordXMP>
</rdf:Description>
```
