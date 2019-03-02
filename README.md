### gift
---
https://github.com/disintegration/gift

```go
g := gift.New(
  gift.Resize(800, 0, gift.LanczosResmpling),
  gift.UnshrpMask(1, 1, 0),
)

dst := image.NewRGBA(g.Bounds(src.Bounds()))

g.Draw(dst, src)


g := gift.New(
  gift.Grayscale(),
  gift.Contrast(10),
)

g.Add(GaussianBlur(2))

dst := image.NewRGBA(g.Bounds(src.Bounds()))

g.Draw(dst, src)

g.DrawAt(dst, src, dst.Bounds().Min, gift.CopyOperator)

dstImage := image.NewRGBA(bgImage.Bounds())
gift.New().Draw(dstImage, bgImage)
gift.New().DrawAt(dstImage, fgImage, image.Pt(100, 100), gift.OverOperator)

package main

import (
  "image"
  "image/color"
  "image/png"
  "log"
  "os"
  
  "github.com/disintegration/gift"
)

func main() {
  src := loadImage("testdata/src.png")
  
  filters := map[string]gift.Filter{
    "resize": gift.Resize(100, 0, gift.LanczosResampling),
    "crop_to_size": gift.CropToSize(100, 100, gift.LeftAnchor),
    "rotate_180": gift.(),
    "rotate_30": gift.(),
    "brightness_increase": gift.(),
    "brightness_decrease": gift.(),
    "contrast_increase": gift.(),
    "contrast_decrease": gift.(),
    "saturation_increase": gift.(),
    "saturation_decrease": gift.(),
    "gamma_1.5": gift.(),
    "gamma_0.5": gift.(),
    "gaussian_blur": gift.(),
    "unsharp_mask": gift.(),
    "sigmoid": gift.(),
    "pixelate": gift.(),
    "colorize": gift.(),
    "grayscale": gift.(),
    "sepia": gift.(),
    "invert": gift.(),
    "mean": gift.(),
    "median": gift.(),
    "minimum": gift.(),
    "maximum": gift.(),
    "hue_rotate": gift.(),
    "color_balance": gift.ColorBalance(10, -10, -10),
    "color_func": gift.ColorFunc(
      func() () {
        r = 1 - r0
        g = g0 + 0.1
        b = 0
        a = a0
        return r, g, b, a
      },
    ),
    "convolution_emboss": gift.Convolution(
      []float32{
        -1, -1, 0,
        -1, 1, 1,
        0, 1, 1,
      },
      false, false, false, 0.0,
    ),
  }
  
  for name, filter := range filters {
    g := gift.New(filter)
    dst := image.NewNRGBA(g.Bounds(src.Bounds()))
    g.Draw(dst, src)
    saveImage("testdata/dst_"+name+".png", dst)
  }
}

func loadImage(filename string) image.Image {
  f, err := os.Open(filename)
  if err != nil {
    log.Fatalf("os.Open failed: %v", err)
  }
  img, _, err := image.Decode(f)
  if err != nil {
    log.Fatalf("image.Decode failed: %v", err)
  }
  return img
}

func saveImage(filename string, img image.Image) {
  f, err := os.Create(filename)
  if err != nil {
    log.Fatalf("os.Create failed: %v", err)
  }
  err = png.Encode(f, img)
  if err != nil {
    log.Fatalf("png.Encode failed: %v", err)
  }
}
```

```
```

```
```


