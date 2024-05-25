# What Linearly Separable Means
**And why a lot of problems aren't**

*By Cooper Ott - May 25, 2024*

The point of neural networks are to figure out a "good enough" understanding of some data (pictures of numbers, etc) that it can accurately understand something similar that it hasn't seen before (a differently written 4).

But getting that understanding isn't easy, and it's not really the way humans think about it. If you were to explain the difference between an 8 and a 9, you'd probably say something about both having a circle on top, but the bottom circle isn't connected. Computers don't understand shapes, so we have to first teach them what shapes are.

## The Perceptron (1957)

Enter Frank Rosenblatt (building of of the work of Warren McCulloch and Walter Pitts), who built a machine that could do just that. With a 20x20 black-and-white grid of light sensors, it could be given a printed picture that it would make a guess about: square or circle. If it was right, nothing would happen. If it was wrong, it can correct which parts of the picture it associated with each shape. It figured out where the corners of squares were, and if they weren't lit up, the machine called it a circle.

It was relatively simple, and could only learn to tell between two categories of things, and could not form more complex understanding of data. While one part of this problem was that it could only understand one idea at a time (which could and would be fixed by linking multiple, one after another), another issue is how it treats the information from each sensor.

## So, when do lines come in?
**Actually, right now!**

Let's say you have an extremely simple problem to solve, let's say figuring out if a number is greater than zero. On a number line, you could just draw a line and split the two categories. This is a Linearly Separable problem. A more complex one would be figuring out if you have two numbers, and you're trying to classify if both are ones. If you can categorize data points by drawing straight lines between to separate them, it is linearly separable.

The problem is: most problems aren't this simple. If you want to figure out if, with two numbers (think of them like an x and y coordinate for a point), if they are within a certain distance of 0: the ideal separation shape for this is actually a perfect circle. And once other problems (like how text works in something like ChatGPT) are applied to this, it's very clear that just straight lines can't capture the nuances between words in different languages.

So is this it? We just have to chain more and more perceptrons together until we approximate a curve? Thankfully, no. The inner parts of the system don't have to smoothly (and linearly) separate data. **Activation functions** are ways of introducing non-linearity into the separations, by having the values coming in squashed or stretched. Popular examples can be seen below, each with their own unique bends.

![https://www.researchgate.net/figure/Commonly-used-activation-functions-a-Sigmoid-b-Tanh-c-ReLU-and-d-LReLU_fig3_335845675](/blog/2024/5/activation-funcs.png)

There's pros and cons to each, but one thing is certain: since most of our problems being tackled by powerful neural networks can't be solved with lines that are straight, we need to start off with lines that aren't.