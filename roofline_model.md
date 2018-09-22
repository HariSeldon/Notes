# The Roofline model

## Intro

The roofline model is a graphical tool to visualize the performance of an application on specific hardware.
The model relates the arithmetic performance of a device with the operational intensity of an application.
The x axis of the plot reports the operational intensity (`I`), which is the ratio between the number of arithmetic operations performed by an application (`F`) and the amount of data transferred from DRAM to the Caches (`D`).
The y axis reports Ops/s, the ratio between `F` and the duration of the computation `T`.
So: `I = F / D`, `Flops / Bytes`.
In most cases Ops are Floating point operations.
The information on the Roofline plot is in part device-specific and in part application-specific.
The line that gives the name to the model is device-specific.
It is composed of two parts:

* The horizontal line represents the maximum floating point performance of the device (`max F`), which cannot be surpassed in any way. Changing `I` does not change `max F`, this is why it is a horizontal line.
* The left side of the plot represents the relationship between `F/T` and `I` when the application is not maxing out the arithmetic intensity of the device.

From dimensionality analysis: `F/T = [Flops/s]`, `I = [Flops/Byte]`, `F/T = x * I` -> `x = [Bytes/s]`, where `x` is memory bandwidth.
The intersection between the horizontal line and the slanted line is at maximum bandwidth and max floating point perf.

The dots below the roofline are instances of applications.
Code transformations like loop tiling can move a dot by reducing `D`, which means to make better use of the memory hierarchy.
The assumption underneath the fact that dots can move around is that `F` does not change (meaning that the application has been optimized already to perform the minimum number of floating point operations possible).
The vertical distance between a dot and the Roofline shows how well the application is using the resources of the machine.

What is the slope of the line ?
To find it out, take two points on the x axis, `A = 1 / 10` and `B = 1 / 5` (assuming that they are both under the slanted part of the graph).
Imagine that an application originally was at point `A` and through compiler optimizations improved to point `B`. 
This means that the transformation halved `D`, which in turns means that the execution time of the application halved too, since the application is memory bound.
This means that `F/T` doubled.
So moving forward by a factor of 2 on the x axis causes to move upwards on the y axis by a factor of 2.
Consequently the slope of the line is `1`.

## How to make the plot

See: <http://spiral.ece.cmu.edu:8080/pub-spiral/pubfile/ispass-2013_177.pdf>

## References

<https://people.eecs.berkeley.edu/~kubitron/cs252/handouts/papers/RooflineVyNoYellow.pdf>
