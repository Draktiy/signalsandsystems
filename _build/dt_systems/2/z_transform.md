---
redirect_from:
  - "dt-systems/2/z-transform"
interact_link: content/dt_systems/2/z_transform.ipynb
title: 'The Z-Transform'
prev_page:
  url: /dt_systems/1/sampling
  title: 'Sampling Theory'
next_page:
  url: /dt_systems/3/i_z_transform
  title: 'The Inverse Z-Transform'
comment: "***PROGRAMMATICALLY GENERATED, DO NOT EDIT. SEE ORIGINAL FILES IN /content***"
---

# Discrete-Time Systems and the Z-Transform

## Scope and Background Reading

This session introduces the z-transform which is used in the analysis of discrete time systems. As for the Fourier and Laplace transforms, we present the definition, define the properties and give some applications of the use of the z-transform in the analysis of signals that are represented as sequences and systems represented by difference equations.

The material in this presentation and notes is based on Chapter 10 of [Steven T. Karris, Signals and Systems: with Matlab Computation and Simulink Modelling, 5th Edition](http://site.ebrary.com/lib/swansea/docDetail.action?docID=10547416) from the **Required Reading List**. Additional coverage is to be found in Chapter 13 of [Benoit Boulet, Fundamentals of Signals and Systems](http://site.ebrary.com/lib/swansea/docDetail.action?docID=10228195) from the **Recommended Reading List**.

## Agenda

* Introduction

* The Z-Transform

* Properties of the Z-Transform

* Some Selected Z-Transforms

* Relationship between Laplace and Z-Transform

* Stability Regions

## Introduction

<img src="pictures/ct-to-dt.png">

In the remainder of this course we turn our attention to how we model and analyse the behaviour of the central block in this picture.

### Nature of the signals

<img src="pictures/ct-to-dt-to-sequence.png">

* The signals we process in discrete time systems are *sequences* of values $x[n]$ where $n$ is an index.

A sequence can be obtained in real-time, e.g. as the output of a ADC, or can be stored in digital memory; processed and re-stored; or processed and output in real-time, for example in digital music.

### Nature of the systems

* The input to a discrete time system is a squences of values $x[n]$
* The output is also a sequence $y[n]$
* The block represents the operations that convert $x[n]$ into $y[n]$. 
* This processing takes the form of a *difference equation* 
* This is analogous to the representation of continuous-time operations by differential equations.

### Transfer function model of a DT system

* In CT systems we use the Laplace transform to simplify the analysis of the *differential equations*
* In DT systems the z-Transform allows us to simplify the analysis of the *difference equations*
* In CT systems application of the Laplace transform allows us to represent systems as transfer functions and solve convolution problems by multiplication
* The z-transform provides [analogous](https://www.google.co.uk/search?q=define:analogous) tools for the analysis of DT systems.

## The Z-Transform

$$\mathcal{Z}\left\{f[n]\right\} = F(z) = \sum_{n=0}^{\infty} f[n]z^{-n}$$

$$\mathcal{Z}^{ - 1}\left\{ {F(z)} \right\} = f[n] = \frac{1}{2\pi j}\oint\limits_{} {F(z){z^{k - 1}}\,dz}$$

### Sampling and the Z-Transform

In the last lecture we showed that sampling could be represented as the multiplication of a CT signal by a periodic train of impulses:

$$x_s(t) = x(t)\sum_{n=0}^{\infty}\delta(t-nT_s)$$

By the sampling property of $\delta(t)$

$$x_s(t) = \sum_{n=0}^{\infty}x(nT_s)\delta(t-nT_s)$$

Using the Laplace transform pairs $\delta(t) \Leftrightarrow 1$ and $\delta(t-T) \Leftrightarrow e^{-sT}$ we obtain:

$$X_s(t) = \mathcal{L}\left\{\sum_{n=0}^{\infty}x(nT_s)\delta(t-nT_s)\right\} = \sum_{n=0}^{\infty}x(nT_s)e^{-nsT_s}$$

By substitution of $z = e^{sT_s}$ and representing samples $x(nT_s)$ as sequence $x[n]$:

$$X(z) = \sum_{n=0}^{\infty}x[n]z^{-n}$$


## Properties of the z-Transform

<table>
<thead>
<tr><td>&nbsp;</td><th>Property</th><th>Discrete Time Domain</th><th>$$\mathcal{Z}$$ Transform</th></tr></thead>
<tbody>
<tr><td>1</td><td>Linearity</td><td>$$af_1[n]+bf_2[n]+\cdots$$</td><td>$$aF_1(z)+bF_2(z)+\cdots$$</td></tr>
<tr><td>2</td><td>Shift of $$x[n]u_0[n]$$</td><td>$$f[n-m]u_0[n-m]$$</td><td>$$z^{-m}F(z)$$</td></tr>
<tr><td>3</td><td>Left shift</td><td>$$f[n-m]$$</td><td>$$z^{-m}F(z)+\sum_{n=0}^{m-1}f[n-m]z^{-n}$$</td></tr>
<tr><td>4</td><td>Right shift</td><td>$$f[n+m]$$</td><td>$$z^{m}F(z)+\sum_{n=-m}^{-1}f[n+m]z^{-n}$$</td></tr>
<tr><td>5</td><td>Multiplication by $$a^n$$</td><td>$$a^nf[n]$$</td><td>$$F\left(\frac{z}{a}\right)$$</td></tr>
<tr><td>6</td><td>Multiplication by $$e^{-nsT_s}$$</td><td>$$e^{-nsT_s}f[n]$$</td><td>$$F\left(e^{sT_s}z\right)$$</td></tr>
<tr><td>7</td><td>Multiplication by $$n$$</td><td>$$nf[n]$$</td><td>$$-z\frac{d}{dz}F(z)$$</td></tr>
<tr><td>8</td><td>Multiplication by $$n^2$$</td><td>$$n^2f[n]$$</td><td>$$-z\frac{d}{dz}F(z)+z^2\frac{d^2}{dz^2}F(z)$$</td></tr>
<tr><td>9</td><td>Summation in time</td><td>$$\sum_{m=0}^{n}f[m]$$</td><td>$$\frac{z}{z-1}F(z)$$</td></tr>
<tr><td>10</td><td>Time convolution</td><td>$$f_1[n]*f_2[n]$$</td><td>$$F_1(z)F_2(z)$$</td></tr>
<tr><td>11</td><td>Frequency convolution</td><td>$$f_1[n]f_2[n]$$</td><td>$$\frac{1}{j2\pi }\oint {x{F_1}(v){F_2}\left( {\frac{z}{v}} \right)} {v^{ - 1}}dv$$</td></tr>
<tr><td>12</td><td>Initial value theorem</td><td colspan="2">$$f[0]=\lim_{z\to\infty}F(z)$$</td></tr>
<tr><td>13</td><td>Final value theorem</td><td colspan="2">$$\lim_{n\to\infty}f[n]=\lim_{z\to 1}(z-1)F(z)$$</td></tr>
</tbody>
</table>

For proofs refer to Section 9.2 of Karris.

## Some Selected Common z-Transforms

### The Geometric Sequence

$$f[n] = \left\{ {\begin{array}{*{20}{c}}
0&{n =  - 1, - 2, - 3, \ldots }\\
a^n&{n = 0,1,2,3, \ldots }
\end{array}} \right.$$

$$F(z) = \sum_{n=0}^{\infty}f[n]z^{-n} = \sum_{n=0}^{\infty}a^n z^{-n} = \sum_{n=0}^{\infty}\left(az^{-1}\right)^n$$

After some analysis<sup>1</sup>, this can be shown to have a *closed-form* expression<sup>2</sup>

$$F(z) = \frac{1}{1-az^{-1}}=\frac{z}{z -a}$$

**Notes**

1. See Karris pp 9-12&mdash;9-13 for the details

2. This function converges only if $$|z| < |a|$$ and the region of convergence is outside the cicle centred at $z=0$ with radius $$r=|a|$$

### Region of convergence

<img src="pictures/roc.png">

### The Delta Sequence

$$\delta [n] = \left\{ {\begin{array}{*{20}{c}}
1&{n = 0}\\
0&\mathrm{otherwise}
\end{array}} \right.$$

$$\mathcal{Z}\left\{\delta [n]\right\} = \Delta(z) = \sum_{n=0}^{\infty}\delta[n]z^{-n} = 1 + \sum_{n=1}^{\infty}0z^{-n} =1$$

$$\delta [n] \Leftrightarrow 1$$

### The Unit Step

$${u_0}[n] = {\rm{ }}\left\{ {\begin{array}{*{20}{c}}
0&{n < 0}\\
1&{n \ge 0}
\end{array}} \right.$$

<img src="pictures/unitstep.png">

### Z-Transform of Unit Step

$$\mathcal{Z}\left\{u_0 [n]\right\} U_0(z) = \sum_{n=0}^{\infty}u_0[n]z^{-n} =\sum_{n=0}^{\infty}z^{-n}$$

This is a special case of the geometric sequence with $a = 1$ so

$$U_0(z) = \frac{1}{1-z^{-1}} = \frac{z}{z - 1}$$

Region of convergence is $$|z| > 1$$

### Exponontial Decay Sequence

$$f[n] = e^{naT_s}{u_0}[n]$$

$$F(z) = \sum_{n=0}^{\infty}e^{-nasT_s}z^{-n} =1+e^{-aT_s}z^{-1}+e^{-2aT_s}z^{-2}+e^{-a3T_s}z^{-3}+\cdots$$

This is a geometric sequence with $a = e^{-aT_s}$, so

$$\mathcal{Z}\left\{e^{naT_s}{u_0}[n]\right\} = \frac{1}{1-e^{-aT_s}z^{-1}} = \frac{z}{z-e^{-aT_s}}$$

Region of convergence is $$|e^{-aT_s}z^{-1}| < 1$$

### Ramp Function

$$f[n] = nu_0[n]$$

$$\mathcal{Z}\left\{nu_0[n]\right\}=\sum_{n=0}^{\infty} nz^{-n} = 0 + z^{-1}+2z^{-2}+3z^{-3}+\cdots$$

We recognize this as a signal $u_0[n]$ multiplied by $n$ for which we have the property 
$$nf[n] \Leftrightarrow -z\frac{d}{dz}F(z)$$

After applying the property and some manipulation, we arrive at:

$$nu_0[n] \Leftrightarrow \frac{z}{(z-1)^2}$$

### z-Transform Tables

As usual, we can rely on this and similar analysis to have been tabulated for us and in practice we can rely on tables of transform pairs, such as this one.

<table>
<thead>
<tr><td>&nbsp;</td><th>f[n]</th><th>F(z)</th></tr></thead>
<tbody>
<tr><td>1</td><td>$$\delta[n]$$</td><td>$$1$$</td></tr>
<tr><td>2</td><td>$$\delta[n-m]$$</td><td>$$z^{-m}$$</td></tr>
<tr><td>3</td><td>$$a^nu_0[n]$$</td><td>$$\frac{z}{z-a}\;|z| > a$$</td></tr>
<tr><td>4</td><td>$$u_0[n]$$</td><td>$$\frac{z}{z-1}\;|z| > 1$$</td></tr>
<tr><td>5</td><td>$$(e^{-anT_s})u_0[n]$$</td><td>$$\frac{z}{z-e^{-aT_s}}\;|e^{-aT_s}z^{-1}| < 1$$</td></tr>
<tr><td>6</td><td>$$(\cos naT_s)u_0[n]$$</td><td>$$\frac{z^2 - z\cos aT_s}{z^2 -2z\cos aT_s + 1}\;|z| > 1$$</td></tr>
<tr><td>7</td><td>$$(\sin naT_s)u_0[n]$$</td><td>$$\frac{z\sin aT_s}{z^2 -2z\cos aT_s + 1}\;|z| > 1$$</td></tr>
<tr><td>8</td><td>$$(a^n\cos naT_s)u_0[n]$$</td><td>$$\frac{z^2 - az\cos aT_s}{z^2 -2az\cos aT_s + a^2}\;|z| > 1$$</td></tr>
<tr><td>9</td><td>$$(a^n\sin naT_s)u_0[n]$$</td><td>$$\frac{az\sin aT_s}{z^2 -2az\cos aT_s + a^2}\;|z| > 1$$</td></tr>
<tr><td>10</td><td>$$u_0[n]-u_0[n-m]$$</td><td>$$\frac{z^m-1}{z^{m-1}(z-1)}$$</td></tr>
<tr><td>11</td><td>$$nu_0[n]$$</td><td>$$\frac{z}{(z-1)^2}$$</td></tr>
<tr><td>12</td><td>$$n^2u_0[n]$$</td><td>$$\frac{z(z+1)}{(z-1)^3}$$</td></tr>
<tr><td>13</td><td>$$[n+1]u_0[n]$$</td><td>$$\frac{z^2}{(z-1)^2}$$</td></tr>
<tr><td>14</td><td>$$a^n n u_0[n]$$</td><td>$$\frac{az}{(z-a)^2}$$</td></tr>
<tr><td>15</td><td>$$a^n n^2 u_0[n]$$</td><td>$$\frac{az(z+a)}{(z-a)^3}$$</td></tr>
<tr><td>16</td><td>$$a^n n[n+1] u_0[n]$$</td><td>$$\frac{2az^2}{(z-a)^3}$$</td></tr>

</tbody>
</table>

## Relationship Between the Laplace and Z-Transform

Given that we can represent a sampled signal in the complex frequency domain as the infinite sum of each sequence value delayed by an integer multiple of the sampling time:

$$F(s) = \sum_{n=0}^{\infty}f[n]e^{-nsT_s}$$

And by definition, the z-transform of such a sequence is:

$$F(z) = \sum_{n=0}^{\infty}f[n]z^{-n}$$

It follows that

$$z = e^{sT_s}$$

And

$$s = \frac{1}{T_s}\ln z$$

### Mapping of s to z

Since $s$ and $z$ are both complex variables, $z=e^{sT_s}$ is a mapping from the $s$-domain to the $z$-domain and $z = \ln z/T_s$ is a mapping from the $z$ to $s$-domain.

<img src="pictures/mapping-s-to-z.png"> 

### Mapping of s to z

Now, since

$$s = \sigma + j\omega$$

$$z = e^{\sigma T_s + j\omega T_s} = e^{\sigma T_s}e^{j\omega T_s} = |z|e^{j\theta}$$

where $$|z| = e^{\sigma Ts}$$ and $$\theta = \omega T_s.$$

### Introduction of sampling frequency

Now, since $T_s = 1/f_s$ then $\omega_s = 2\pi/f_s$ or $f_s = \omega_s/(2\pi)$ and $T_s = 2\pi/\omega_s$

We let

$$\theta = \omega T_s = \omega\frac{2\pi}{\omega_s} = 2\pi\frac{\omega}{\omega_s}$$

Hence by substitution:

$$z = e^{\sigma t}e^{j2\pi\omega/\omega_s}$$

### Interpretation of the mapping s to z

* The quantity $e^{j2\pi\omega/\omega_s}$ defines a unit-circle in the $z$-plane centred at the origin. 

* And of course the term $\sigma$ represents the (stability) boundary between the left- and right-half planes of the $s$-plane.

* What are the consequences of this?

### Case I: $\sigma < 0$

* When $\sigma < 0$ we see that from $$|z| = e^{\sigma T_s}$$ that $$|z| < 1$$
* The left-half plane of the $s$-domain maps into the unit circle in the $z$-plane.
* Different negative values of $\sigma$ map onto concentric circles with radius less than unity.

### Case II: $\sigma > 0$

* When $\sigma > 0$ we see that from $$|z| = e^{\sigma T_s}$$ that $$|z| > 1$$
* The right-half plane of the $s$-domain maps outside the unit circle in the $z$-plane.
* Different positive values of $\sigma$ map onto concentric circles with radius greater than unity.

### Case III: $\sigma = 0$

* When $\sigma = 0$, $$|z| = 1$$ and $$\theta = 2\pi\omega/\omega_s$$
* All values of $\omega$ lie on the circumference of the unit circle.

### Stability Region - s-Plane

<img src="pictures/s-plane.png">

### Stability Region - z-Plane

<img src="pictures/z-plane.png">

### Frequencies in the z-Domain

* As a consequence of the result for **Case III** above, we can explore how frequencies (that is is values of $s=\pm j\omega$) map onto the $z$-plane.

* We already know that these frequencies will map onto the unit circle and by $\theta = 2\pi\omega/\omega_s$ the angles are related to the sampling frequency.

* Let's see how

### Mapping of multiples of sampling frequency

<table>
<thead><tr><td>$\omega$ [radians/sec]</td><td>$$|z|$$</td><td>$\theta$ [radians]</td></tr>
</thead>
<tbody>
<tr><td>0</td><td>1</td><td>0</td></tr>
<tr><td>$\omega_s/8$</td><td>1</td><td>$\pi/4$</td></tr>
<tr><td>$\omega_s/4$</td><td>1</td><td>$\pi/2$</td></tr>
<tr><td>$3\omega_s/8$</td><td>1</td><td>$3\pi/4$</td></tr>
<tr><td>$\omega_s/2$</td><td>1</td><td>$\pi$</td></tr>
<tr><td>$5\omega_s/8$</td><td>1</td><td>$5\pi/4$</td></tr>
<tr><td>$3\omega_s/4$</td><td>1</td><td>$3\pi/2$</td></tr>
<tr><td>$7\omega_s/8$</td><td>1</td><td>$7\pi/4$</td></tr>
<tr><td>$\omega_s$</td><td>1</td><td>$2\pi$</td></tr>
</tbody>
</table>

### Mapping of s-plane to z-plane

<img src="pictures/s-to-z-mapping.png">

### Mapping z-plane to s-plane

There is no unique mapping of $z$ to $s$ since

$$s = \frac{1}{T_s} \ln z$$

but for a complex variable

$$\ln z = \ln z \pm j2n\pi$$

This is in agreement with the theoretical idea that in the frequency domain, sampling creates an infinite number of spectra, each of which is centred around $\pm n\omega_s$.

### Frequency aliasing

* It's worth observing that any stable complex pole in the $s$-plane $s=-\sigma + j\omega$ will have complex conjugate pair $s = -\sigma - j\omega$.
* Providing $\omega < \omega_s/2$ these poles will be mapped to the upper and lower half-plane of the $z$-plane respectively.
* If $\omega > \omega_s/2$, an upper-half plane pole will be mapped to the lower-half plane and will have an effective frequency of $\omega_s/2 - \omega$.
* Similarly, its conjugate pair will move into the upper-half plane. 

This is another way of looking at *aliasing*.

* Also, any poles with frequency $\omega > \omega_s$ will also be aliased back into into the unit circle.

## Summary

* Introduction
* The Z-Transform
* Properties of the Z-Transform
* Some Selected Z-Transforms
* Relationship Between Laplace and Z-Transform
* Stability Regions

*Next session*

* The Inverse Z-Transform &ndash; an examples class

## Homework

Problems 1 to 3 in **Section 9.10 Exercises** of Karris explore the z-Transform