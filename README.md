# Single image haze removal
#### A Python implementation of single image haze removal
-
The propose of this repository is to implement the image haze removal base on the Zhiming Tan Et al. [paper](https://pdfs.semanticscholar.org/64ca/a24f2cb3fff6d8eb966f90078f0d0b8a7db0.pdf).

##Usage

The code can be executed via `terminal`
>	```python dehaze.py```
> then input the PATH_TO_IMAGE
> ```imagename.png```

---

## Sample input
![Original Image](https://github.com/kindraywind/SingleImageHazeRemover/blob/master/sample/ex_input.jpg?raw=true)

## Sample output
![Clarified image w=0.95, t0=0.55](https://github.com/kindraywind/SingleImageHazeRemover/blob/master/sample/ex_output.jpg?raw=true)

---

## How does it work.
This dehaze algorithm contains three steps,

1) Determine intensity of atmospheric light
2) Estimate transmission map
3) Clarify image

First, the intensity of atmospheric light `A` is estimated form hazed image `I(x)`. Then, the transmission map `t(x)` is estimated using `A` and `I(x)`. Finally, the image is clarified with the image defogging model.

#### Step#1 Estimate intensity of atmospheric light:
Find the top 0.1% brightest pixels in the dark channel then choose one with highest intensity as the representing of atmospheric light.

#### Step#2 Estimate transmission map:
First, find a dark channel based on a local area(coarsemap)
Then, the transmission map `t(x)` is thereby obtained:

```t(x) = 1 – defoggingParam * darkPixelFromCoarseMap / AtmosphericLightIntensity```

The ```defoggingParam``` is a value between 0 to 1. The higher value the lesser amount of fog would be kept for the distant objects.

#### Step#3 Clarify image:
Finally, the image is clarified by: ```J(x)=(I(x)- A)/max(t(x), t0)+A```

Where `J(x)` is output, `I(x)` is input, `t(x)` is transmission map, `A` is atmospheric light and `t0` is set to a constant value to avoid dividing by zero.
