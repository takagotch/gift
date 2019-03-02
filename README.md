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
    "rotate_180": gift.Rotate180(),
    "rotate_30": gift.Rotate(30, color.Transparent, gift.CubicInterpolation),
    "brightness_increase": gift.Brightness(30),
    "brightness_decrease": gift.Brightness(-30),
    "contrast_increase": gift.Contrast(30),
    "contrast_decrease": gift.Contrast(-30),
    "saturation_increase": gift.Saturation(50),
    "saturation_decrease": gift.Saturation(-50),
    "gamma_1.5": gift.Gamma(1.5),
    "gamma_0.5": gift.Gamma(-1.5),
    "gaussian_blur": gift.GaussinaBlur(1),
    "unsharp_mask": gift.UnsharpMask(1, 1, 0),
    "sigmoid": gift.Sigmoid(0.5, 7),
    "pixelate": gift.Pixelate(5),
    "colorize": gift.Colorize(240, 50, 100),
    "grayscale": gift.Grayscale(),
    "sepia": gift.Sepia(100),
    "invert": gift.Invert(),
    "mean": gift.Mean(5, true),
    "median": gift.Median(5, true),
    "minimum": gift.Minimum(5, true),
    "maximum": gift.Maximum(5, true),
    "hue_rotate": gift.Hue(45),
    "color_balance": gift.ColorBalance(10, -10, -10),
    "color_func": gift.ColorFunc(
      func(r0, g0, b0, float32) (r, g, b, a float32) {
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


