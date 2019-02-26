---
redirect_from:
  - "/laplace-transform/5/worksheet8"
interact_link: content/laplace_transform/5/worksheet8.ipynb
title: 'Worksheet 8 Impulse Response and Time Convolution'
prev_page:
  url: /laplace_transform/4/worksheet7
  title: 'Worksheet 7 Transfer Functions'
next_page:
  url: /fourier_series/1/worksheet9
  title: 'Worksheet 9 Trigonometric Fourier Series'
comment: "***PROGRAMMATICALLY GENERATED, DO NOT EDIT. SEE ORIGINAL FILES IN /content***"
---

# Worksheet 8

## To accompany Chapter 3.5 Convolution and the Impulse Response

We will step through this worksheet in class. 

You are expected to have at least watched the video presentation of [Chapter 3.5](https://cpjobling.github.io/eg-247-textbook/laplace_transform/5/convolution) of the [notes](https://cpjobling.github.io/eg-247-textbook) before coming to class. If you haven't watch it afterwards!

## Agenda

The material to be presented is:

### First Hour

* Even and Odd Functions of Time
* Time Convolution

## Even and Odd Functions of Time

Fill in the Blanks Quiz.

### Even Functions of Time

A function $f(t)$ is said to be an *even function* of time if the following relation holds

<pre style="border: 2px solid blue">




</pre>

Polynomials with even exponents only, and with or without constants, are even functions. For example:

Write down the Taylor-series polynomial expansion of $\cos t$. Is $\cos t$ even or odd?

<pre style="border: 2px solid blue">




</pre>

Odd/Even?

### Odd Functions of Time

A function $f(t)$ is said to be an *odd function* of time if the following relation holds

<pre style="border: 2px solid blue">




</pre>

Polynomials with even exponents only, and with or without constants, are even functions.

Write down the Taylor-series polynomial expansion of $\cos t$. Is $\cos t$ even or odd?

<pre style="border: 2px solid blue">




</pre>

Odd/Even?

### Observations

* For odd functions $f(0) =$
<pre style="border: 2px solid blue">




</pre>

* The product of *two even* or *two odd* functions is an [Even/Odd] function.

* The product of an even and an odd function, is an [Even/Odd] function.

In the following $f_e(t)$ will denote an even function and $f_o(t)$ an odd function.

### Time integrals of even and odd functions

For an even function $f_e(t)$

$$\int_{-T}^{T}f_e(t) dt = 2 \int_{0}^{T}f_e(t) dt$$

For an odd function $f_o(t)$

$$\int_{-T}^{T}f_o(t) dt = 0$$

### Even/Odd Representation of an Arbitrary Function

A function $f(t)$ that is neither even nor odd can be represented as an even function by use of:
    
$$f_e(t) = \frac{1}{2}\left[f(t)+f(-t)\right]$$

or as an odd function by use of:

$$f_o(t) = \frac{1}{2}\left[f(t)-f(-t)\right]$$

Adding these together, an abitrary signal can be represented as

$$f(t) = f_e(t) + f_o(t)$$

That is, any function of time can be expressed as the sum of an even and an odd function.

### Example 1

Is the Dirac delta $\delta(t)$ an even or an odd function of time?

### Solution

Let $f(t)$ be an arbitrary function of time that is continous at $t=t_0$. Then by the sifting property of the delta function

<pre style="border: 2px solid blue">




</pre>

and for $t_0 = 0$

<pre style="border: 2px solid blue">




</pre>

Also for an even function $f_e(t)$

<pre style="border: 2px solid blue">




</pre>

and for an odd function $f_o(t)$

<pre style="border: 2px solid blue">




</pre>

### Even or odd?

An odd function $f_o(t)$ evaluated at $t=0$ is zero, that is $f_o(0) = 0$.

Hence

$$\int_{-\infty}^{\infty} f_o(t)\delta(t) dt = f_o(0) = 0$$

Hence the product $f_o(t)\delta(t)$ is odd function of $t$.

Since $f_o(t)$ is odd, $\delta(t)$ must be even because only an *even* function multiplied by an *odd* function can result in an *odd* function.

(Even times even or odd times odd produces an even function. See earlier slide)

## Time Convolution

Consider a system whose input is the Dirac delta ($\delta(t)$), and its output is the ***impulse response*** $h(t)$. We can represent the input-output relationship as a block diagram

<img src="pictures/conv1.png" width="50%">


### In general

<img src="pictures/conv2.png" width="50%">

### Add an arbitrary input

Let $u(t)$ be any input whose value at $t=\tau$ is $u(\tau)$, Then because of the sampling property of the delta function

<img src="pictures/conv3.png" width="50%">

(output is $u(\tau)h(t-\tau)$)

### Integrate both sides

Integrating both sides over all values of $\tau$ ($-\infty < \tau < \infty$) and making use of the fact that the delta function is even, i.e. 

$$\delta(t-\tau)=\delta(\tau-t)$$

we have:

<img src="pictures/conv4.png">

### Use the sifting property of delta

The second integral on the left side reduces to $u(t)$

<img src="pictures/conv5.png">

### The Convolution Integral

The integral

$${\int_{-\infty}^{\infty} u(\tau)h(t-\tau)d\tau}$$

or

$${\int_{-\infty}^{\infty} u(t-\tau)h(\tau)d\tau}$$

is known as the *convolution integral*; it states that if we know the impulse response of a system, we can compute its time response to any input by using either of the integrals.

The convolution integral is usually written $u(t)*h(t)$ or $h(t)*u(t)$ where the asterisk ($*$) denotes convolution.

### Second Hour

* Graphical Evaluation of the Convolution Integral
* System Response by Laplace

## Graphical Evaluation of the Convolution Integral

The convolution integral is most conveniently evaluated by a graphical evaluation. The text book gives three examples (6.4-6.6) which we will demonstrate using a [graphical visualization tool](http://www.mathworks.co.uk/matlabcentral/fileexchange/25199-graphical-demonstration-of-convolution) developed by Teja Muppirala of the Mathworks.

The tool: [convolutiondemo.m](matlab/convolutiondemo.m) (see [license.txt](matlab/license.txt)).



{:.input_area}
```matlab
clear all
cd ../matlab/convolution_demo
pwd
format compact
```




{:.input_area}
```matlab
convolutiondemo % ignore warnings
```


### Convolution by Graphical Method - Summary of Steps

For simplicity, we give the rules for $u(t)$, but the procedure is the same if we reflect and slide $h(t)$

1. Substitute $u(t)$ with $u(\tau)$ &ndash; this is a simple change of variable. It doesn't change the definition of $u(t)$.

2. Reflect $u(\tau)$ about the vertical axis to form $u(-\tau)$

3. Slide $u(-\tau)$ to the right a distance $t$ to obtain $u(t-\tau)$

4. Multiply the two signals to obtain the product $u(t-\tau)h(\tau)$

5. Integrate the product over all $\tau$ from $-\infty$ to $\infty$.

### Example 2

(This is example 6.4 in the Karris)

The signals $h(t)$ and $u(t)$ are shown below. Compute $h(t)*u(t)$ using the graphical technique.

<img src="pictures/conv_ex1.png">

### h(t)

The signal $h(t)$ is the straight line $f(t)=-t+1$ but this is defined only between $t = 0$ and $t = 1$. We thus need to gate the function by multiplying it by $u_0(t)-u_0(t-1)$ as illustrated below:

<img src="pictures/gate_h.png">

Thus

$$h(t) \Leftrightarrow H(s)$$

$$h(t) = (-t + 1)(u_0(t)-u_0(t-1)) = (-t + 1)u_0(t) - (-(t - 1)u_0(t - 1)) = -t u_0(t) + u_0(t) + (t - 1)u_0(t - 1)$$

$$-t u_0(t) + u_0(t) + (t - 1)u_0(t - 1) \Leftrightarrow - \frac{1}{s^2} + \frac{1}{s} +\frac{e^{-s}}{s^2}$$

$$H(s) = \frac{s + e^{-s} - 1}{s^2}$$

### u(t)

The input $u(t)$ is the gating function:

$$u(t) = u_0(t)-u_0(t-1)$$

so

$$U(s) = \frac{1}{s}-\frac{e^{-s}}{s} = \frac{1 - e^{-s}}{s}$$
    

### Prepare for convolutiondemo

To prepare this problem for evaluation in the `convolutiondemo` tool, we need to determine the Laplace Transforms of $h(t)$ and $u(t)$.

### convolutiondemo settings

* Let `g = (1 - exp(-s))/s`
* Let `h = (s + exp(-s) - 1)/s^2`
* Set range $-2 < \tau < -2$

### Summary of result

1. For $t < 0$: $u(t-\tau)h(\tau) = 0$
2. For $t = 0$: $u(t-\tau) = u(-\tau)$ and $u(-\tau)h(\tau) = 0$
3. For $0 < t \le 1$: $h*u = \int_0^t (1)(-\tau + 1)d\tau = \left.\tau - \tau^2/2\right|_0^t = t-t^2/2$
4. For $1 < t \le 2$: $h*u = \int_{t-1}^1(-\tau + 1)d\tau = \left.\tau - \tau^2/2\right|_{t-1}^{1} = t^2/2-2t+2$
5. For $2 \le t$: $u(t-\tau)h(\tau) = 0$

### Example 3

This is example 6.5 from Karris.

$$h(t) = e^{-t}$$

$$u(t) = u_0(t)-u_0(t-1)$$

<pre style="border: 2px solid blue">















</pre>

### Answer 3

$$y(t) = \left\{ {\begin{array}{*{20}{l}}
{0:t \le 0}\\
1 - e^{ - t}:\;0 < t \le 1\\
e^{ - t}\left( {e - 1} \right):\;1 < t \le 2\\
0:\;2 \le t
\end{array}} \right.$$

#### Check with MATLAB



{:.input_area}
```matlab
syms t tau
x1=int(exp(-tau),tau,0,t)
```




{:.input_area}
```matlab
x2=int(exp(-tau),tau,t-1,t)
```


### Example 4

This is example 6.6 from the text book.

$$h(t) = 2(u_0(t)-u_0(t-1))$$

$$u(t) = u_0(t)-u_0(t-2)$$

<pre style="border: 2px solid blue">















</pre>

### Answer 4

$$y(t) = \left\{ {\begin{array}{*{20}{l}}
{0:t \le 0}\\
{2t:\;0 < t \le 1}\\
{2:\;1 < t \le 2}\\
{-2t+6:\;2 < t \le 3}\\
{0:\;3 \le t}\\
\end{array}} \right.$$

## System Response by Laplace

In the discussion of Laplace, we stated that

$$\mathcal{L} \left\{ f(t)*g(t)\right\} = F(s)G(s)$$

We can use this property to make the solution of convolution problems even simpler.

### Impulse Response and Transfer Functions

Returning to the example we started with

<img src="pictures/conv1.png" width="50%">

Then the impulse response of the system $h(t)$ will be given by:

$$\mathcal{L} \left\{ h(t)*\delta(t)\right\} = H(s)\Delta(s)$$

Where $H(s)$ be the laplace transform of the impulse response of the system $h(t)$. From properties of the Laplace transform we know that

$$\delta(t) \Leftrightarrow 1$$

so that $\Delta(s) = 1$ and

$$h(t)*\delta(t) \Leftrightarrow H(s).1 = H(s)$$

A consequence of this is that the transform of the impulse response $h(t)$ of a system with transfer function $H(s)$ is completely defined by the transfer function itself.

Previously we argued that the response of system with impulse response $h(t)$ was given by the convolution integrals:

$$h(t)*u(t) = {\int_{-\infty}^{\infty} u(\tau)h(t-\tau)d\tau} = {\int_{-\infty}^{\infty} u(t-\tau)h(\tau)d\tau}$$

Thus the Laplace transform of any system subject to an input $u(t)$ is simply

$$Y(s) = H(s)U(s)$$

and 

$$y(t) = \mathcal{L}^{-1} \left\{ G(s) U(s) \right\}$$

Using tables, solution of a convolution problem by Laplace is usually simpler than using convolution directly.

### Example 5

This is example 6.7 from Karris.

<img src="pictures/example4.jpg" width="75%">

For the circuit shown above, show that the transfer function of the circuit is:

$$ H(s) = \frac{V_c(s)}{V_s(s)} = \frac{1/RC}{s + 1/RC} $$

Determine the impulse respone $h(t)$ of the circuit and the response of the capacitor voltage when the input is the unit step function $u_0(t)$ and $v_c(0^-)=0$.

Assume $C=1\; \mathrm{F}$ and $R=1\;\Omega$.

### Solution 5a - Impulse response

<pre style="border: 2px solid blue">















</pre>

### Solution  5b - Step response

<pre style="border: 2px solid blue">




















</pre>


### Homework

Verify this result using the convolution integral

$$h(t)*u(t) = {\int_{-\infty}^{\infty} u(\tau)h(t-\tau)d\tau}$$