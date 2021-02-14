---
title: "Bitmap Snapshots of WPF Visuals"
date: 2008-10-07T17:46:40+02:00
---

Recently I needed to create a bitmap of some WPF controls to be used in another program. Doing a quick 
search turned up references to the RenderTargetBitmap class in WPF with sample code along the lines of:

```c#
    RenderTargetBitmap bmp = new RenderTargetBitmap((int)element.Width, 
        (int)element.Height, 96, 96, PixelFormats.Pbgra32);
    bmp.Render(element);
```

However if the WPF control had a **margin** then the rendered bitmap had transparent pixels for the margin area. 
As an example here is a button inside a **StackPanel** with a **margin** applied.

![image alt text](/images/bitmap-snapshots-of-wpf-visuals/image_thumb.jpg)

And the following is the bitmap that is created via the sample code above:

![image alt text](/images/bitmap-snapshots-of-wpf-visuals/image_thumb2.jpg)

Doing some more searching turned up the following code which creates a **VisualBrush** from the target **Visual** and 
then renders that into a **DrawingVisual** and then finally uses **RenderTargetBitmap** to take a snapshot of the 
**DrawingVisual**. Using this approach the **margins** are ignored and the bitmap only consists of the target WPF 
control/visual as shown below:

![image alt text](/images/bitmap-snapshots-of-wpf-visuals/image_thumb3.jpg)

```c#
void CreateBitmapFromVisual(Visual target, string filename) 
{ 
    if (target == null) 
        return; 

    Rect bounds = VisualTreeHelper.GetDescendantBounds(target);

    RenderTargetBitmap rtb = new RenderTargetBitmap((Int32)bounds.Width, 
                (Int32)bounds.Height, 96, 96, PixelFormats.Pbgra32); 
    
    DrawingVisual dv = new DrawingVisual(); 
    
    using (DrawingContext dc = dv.RenderOpen()) 
    { 
        VisualBrush vb = new VisualBrush(target); 
        dc.DrawRectangle(vb, null, new Rect(new Point(), bounds.Size)); 
    } 

    rtb.Render(dv);

    PngBitmapEncoder png = new PngBitmapEncoder();

    png.Frames.Add(BitmapFrame.Create(rtb));

    using (Stream stm = File.Create(filename))
    {
        png.Save(stm);
    }
}
```





