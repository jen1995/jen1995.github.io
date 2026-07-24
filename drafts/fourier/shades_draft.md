# All shades of Fourier Transform

TODOs: 

- maybe write some funny intro, using this: [https://angeloyeo.github.io/2019/06/23/Fourier_Series_en.html](https://angeloyeo.github.io/2019/06/23/Fourier_Series_en.html)
- write the formulas for different Fourier coefficients
- write a passage that Fourier Transform works for any integrable function, use page 524 from. here: [https://matan.math.msu.su/media/uploads/2020/03/V.A.Zorich-Kniga-II-9-izdanie-Temp-Corr-3.pdf](https://matan.math.msu.su/media/uploads/2020/03/V.A.Zorich-Kniga-II-9-izdanie-Temp-Corr-3.pdf)
- use Notion AI to improve text quality

Waveforms alone provide limited insight into a recording's pitch and speech content

Fourier analysis breaks down complex signals into their basic frequency components, showing how different frequencies combine to create the original signal.

Think of Fourier analysis like breaking down a song into individual musical notes. It takes a complicated signal (like a piece of music) and splits it into basic parts - showing us all the different frequencies that work together to create the whole signal.

At its core, Fourier analysis breaks down complex signals into their fundamental frequency components.

It's similar to breaking down a song into its individual musical notes.

The amplitudes of these frequency components appear on the frequency axis rather than the time axis, forming what's called the (frequency) **spectrum**.

The usefulness of Fourier analysis:

- It converts a long sequence of time samples into a compact frequency representation.
- It enables analysis of frequency components and filtering of unwanted frequencies.

# Fourier Series → Fourier Transform

Any **periodic** function $x(t)$ that is integrable over the segment  $\left[-\frac{P}{2}, \frac{P}{2}\right]$ with period $P$ can be represented as a **Fourier Series:**

$$
x(t) = a_0 + \sum_{n = 1}^\infty \left( a_n \cos\left( \frac{2 \pi n t}{P} \right)  + b_n \sin \left( \frac{2 \pi n t}{P} \right) \right)
$$

where:

$$
a_0 = \frac{1}{2P} \int_{-P/2}^{P/2} x(t) dt \\
a_n = \frac{1}{P} \int_{-P/2}^{P/2} x(t) \cos \left(2 \pi \frac{n}{P} t \right) dt, \text{ for } n \ge 1 \\
b_n = \frac{1}{P} \int_{-P/2}^{P/2} x(t) \sin \left(2 \pi \frac{n}{P} t \right) dt, \text{ for } n \ge 1
$$

This can be equivalently rewritten in cosine form:

$$
x(t) = \frac{A_0}{2} + \sum_{n = 1}^\infty A_n \cos \left( 2 \pi  \frac{n}{P} t - \phi_n\right)
$$

where:

$$
A_n = \sqrt{a_n^2 + b_n^2} \text{\quad and \quad} \phi_n = \text{arctan} \frac{b_n}{a_n}
$$

Here $A_n$ is called **magnitude,** $\frac{n}{P}$ is called **frequency** and $\phi_n$ is called **phase.**

![                                                 Source: [[YSDA Speech course, 2022, week 2](https://github.com/yandexdataschool/speech_course/tree/2022/week_02)](https://app.notion.com/p/YSDA-Speech-course-2022-week-2-17148130d8968046973cc5902aecab42?pvs=21) ](All%20shades%20of%20Fourier%20Transform/Screenshot_2025-01-03_at_17.43.19.png)

                                                 Source: [[YSDA Speech course, 2022, week 2](https://github.com/yandexdataschool/speech_course/tree/2022/week_02)](https://app.notion.com/p/YSDA-Speech-course-2022-week-2-17148130d8968046973cc5902aecab42?pvs=21) 

Let's explore an even more compact form using Euler's formula:

$$
e^{i t } = \cos t + i \sin t \Longleftrightarrow \cos t = \frac{1}{2} \left(e^{it} + e^{-it} \right)  
$$

Using Euler's formula, we can derive:

$$
x(t) = \frac{A_0}{2} + \sum_{n = 1}^\infty A_n \cos \left( 2 \pi  \frac{n}{P} t - \phi_n\right) = \sum_{n = -\infty}^\infty c_n e^{2 \pi i \frac{n}{P} t}
$$

$$
\cos\left( 2 \pi \frac{n}{P} t - \phi_n \right) = \frac{1}{2} \cdot e^{i\left( 2 \pi \frac{n}{P} t - \phi_n \right)} + \frac{1}{2} \cdot e^{-i\left( 2 \pi \frac{n}{P} t - \phi_n \right)} = \\ = \frac{1}{2} e^{-i \phi_n} \cdot e^{2 \pi i \frac{+n}{P} t} + \frac{1}{2} e^{i \phi_n} \cdot e^{2 \pi i \frac{-n}{P} t}
$$

From this, we can derive the **exponential form** of Fourier Series:

where

$$
c_n = \frac{1}{P} \int_{-P/2}^{P / 2} x(t) e^{-2 \pi i \frac{n}{P} t} dt
$$

The set of Fourier coefficients is also called the **spectrum** of the function $x(t)$ (which we will often refer to as a *signal*).

What about absolutely integrable aperiodic functions (those without a period)? We can think of them as functions with an **infinite** period. Let's visualize this concept with the illustration below:

![Source: [[Angelo’s Notes: Continuous Time Fourier Transform](https://angeloyeo.github.io/2019/07/07/CTFT_en.html#google_vignette)](https://app.notion.com/p/Angelo-s-Notes-Continuous-Time-Fourier-Transform-17148130d8968027a736eb3f2d9a83a7?pvs=21) ](All%20shades%20of%20Fourier%20Transform/Screenshot_2025-01-04_at_16.20.33.png)

Source: [[Angelo’s Notes: Continuous Time Fourier Transform](https://angeloyeo.github.io/2019/07/07/CTFT_en.html#google_vignette)](https://app.notion.com/p/Angelo-s-Notes-Continuous-Time-Fourier-Transform-17148130d8968027a736eb3f2d9a83a7?pvs=21) 

**TODO: нужно поменять обозначения на картинке**

Starting at the top, we see a function with period $P$. As this period increases, wider gaps appear between repetitions of the function. Eventually, when the period becomes infinitely large, we're left with a single instance of the function.

Let's return to the exponential form of Fourier Series and rewrite it:

$$
x(t) = \sum_{n = -\infty}^\infty c_n e^{2 \pi i \frac{n}{P} t} = \sum_{n=-\infty}^\infty c_n P \cdot  e^{2 \pi i \frac{n}{P} t}  \cdot \frac{1}{P}
$$

We know that:

$$
c_n P = \int_{-P/2}^{P / 2} x(t) e^{-2 \pi i \frac{n}{P} t} dt
$$

As $P$ approaches infinity and we consider an [absolutely integrable](https://en.wikipedia.org/wiki/Absolutely_integrable_function) function $x(t)$ in the limit, we can introduce this helper function:

$$
X(f) = \int_{-\infty}^\infty x(t) e^{-2 \pi i f t} dt 
$$

For $f_n = \frac{n}{P}$ and large values of $P$, this function's values approximate $c_n P$:

$$
X(f_n) = X\left( \frac{n}{P} \right) \approx c_n P \text{ for } P \to \infty
$$

Therefore:

$$
x(t) = \sum_{n=-\infty}^\infty c_n P \cdot  e^{2 \pi i \frac{n}{P} t}  \cdot \frac{1}{P} \approx \sum_{n=-\infty}^\infty X(f_n) \cdot  e^{2 \pi i f_n t}  \cdot \frac{1}{P}
$$

This final sum is an integral sum for the function $X(f) e^{2 \pi f t}$ over the partition $f_{n}$ with norm $f_{n + 1} - f_n = \frac{1}{P}$. As the partition's norm approaches $0$ (when $P \to \infty$), we obtain:

$$
x(t) = \int_{-\infty}^{\infty} X(f) e^{2 \pi i f t} df
$$

This integral for $x(t)$ is known as the **Fourier Integral**, and $X(f)$ is the **Fourier Transform**. Both integrals are interpreted as [Cauchy principal value](https://en.wikipedia.org/wiki/Cauchy_principal_value).

Let’s now see a good visualization of what was going on when we were moving on towards an infinite period:

![                                   Source: [[Angelo’s Notes: Continuous Time Fourier Transform](https://angeloyeo.github.io/2019/07/07/CTFT_en.html#google_vignette)](https://app.notion.com/p/Angelo-s-Notes-Continuous-Time-Fourier-Transform-17148130d8968027a736eb3f2d9a83a7?pvs=21) ](All%20shades%20of%20Fourier%20Transform/Screenshot_2025-01-04_at_20.29.22.png)

                                   Source: [[Angelo’s Notes: Continuous Time Fourier Transform](https://angeloyeo.github.io/2019/07/07/CTFT_en.html#google_vignette)](https://app.notion.com/p/Angelo-s-Notes-Continuous-Time-Fourier-Transform-17148130d8968027a736eb3f2d9a83a7?pvs=21) 

The first three rows show the function on the left and its Fourier coefficients on the right, while the last row displays the Fourier Transform. As we progress downward, we can observe how the gaps between Fourier coefficients gradually decrease (each gap having size of $\frac{1}{T}$) until the discrete points merge into a continuous curve.

**TODO: нужно поменять обозначения на картинке**

УТОЧНИ, ЧТО ТУТ НА КАРТИНКЕ, ТОЧНО ЛИ ТАМ КОЭФФИЦИЕНТЫ ФУРЬЕ НЕ УМНОЖЕНЫ НА T

ДА, ОНИ ТОЧНО УМНОЖЕНЫ НА T, НАДО ИСПРАВИТЬ

СКАЗАТЬ, ЧТО ОНИ ИХ АПЛИТУДЫ БЕЗ УМНОЖЕНИЯ СТАНОВЯТСЯ ПОЧТИ НУЛЕВЫМИ: ТУТ ЕСТЬ ПРО ЭТО: [https://ru.dsplib.org/content/fourier_transform/fourier_transform.html](https://ru.dsplib.org/content/fourier_transform/fourier_transform.html)

# Fourier Transform → Fourier Series

Пусть теперь у нас есть апериодический сигнал $x(t)$ с ограниченным носителем, то есть $x(t) = 0$ при $|t| > \tau/2$ для некоторого $\tau$. Рассмотрим сигнал $x_c(t)$, представляющий из себя бесконечную сумму копий сигнала $x(t)$, сдвинутых относительно друг друга по времени на величину $P > \tau$ (чтобы копии не пересекались по времени).

Пример такого $x(t)$ (синий график) и его периодического продолжения (оранжевый пунктирный график) показаны на рисунке ниже:

![                              Source: [[DSPLIB.org](https://ru.dsplib.org): [Fourier Transform of Non-periodic Signals](https://ru.dsplib.org/content/fourier_transform/fourier_transform.html)](https://app.notion.com/p/DSPLIB-org-Fourier-Transform-of-Non-periodic-Signals-17248130d8968048bc65dbf9f6530006?pvs=21) ](All%20shades%20of%20Fourier%20Transform/02b7de05-7446-4188-b641-a29537bf594c.png)

                              Source: [[DSPLIB.org](https://ru.dsplib.org): [Fourier Transform of Non-periodic Signals](https://ru.dsplib.org/content/fourier_transform/fourier_transform.html)](https://app.notion.com/p/DSPLIB-org-Fourier-Transform-of-Non-periodic-Signals-17248130d8968048bc65dbf9f6530006?pvs=21) 

**TODO: нужно поменять обозначения на картинке**

Преобразование Фурье для $x(t)$ равно:

$$
X(f) = \int_{-\infty}^\infty x(t) e^{-2 \pi i f t} dt = \int_{-\tau / 2}^{\tau / 2} x(t) e^{-2 \pi i f t} dt
$$

Периодический сигнал $x_c(t)$ имеет дискретный спектр $c_n$, который равен:

$$
c_n = \frac{1}{P} \int_{\frac{-P}{2}}^{\frac{P}{2}} x_c(t) e^{-2 \pi i \frac{n}{P} t} dt
$$

Сравнивая последние два выражения на дискретной сетке частот $f_n = \frac{n}{P}$ и учитывая, что $\tau < P$, можно заключить, что:

$$
c_n = \frac{1}{P} X(f_n)
$$

Таким образом, если периодический сигнал $x_c(t)$ представляет из себя копии сигнала $x(t)$ с ограниченным носителем, то каждый элемент его спектра $c_n$ равен значению преобразования Фурье сигнала $x(t)$ в точках $f = f_n$, делёному на период повторения $P$.

Получается, что $\frac{1}{P} X(f)$ задаёт огибающую (envelope curve) дискретного спектра.

TODO: картинка

TODO: подметить связь — повторение - дискретность и наоборот

# **Discrete Signals**

A signal $x(t)$ is called **analog** if it is defined on a continuous time axis $t$ and can take arbitrary values at any moment. An analog signal can be represented by a continuous or piecewise-continuous function of variable $t$. 

If a signal $x_d(t)$ takes arbitrary values only at fixed moments in time $t_n$, where $n$ is an integer, such a signal is called **discrete (sampled)**. The most widely used discrete signals are those defined on an equally spaced grid $t_n = nT$, where $T$ is the sampling interval.

The figure below illustrates an analog signal alongside its discrete counterpart.

![          Source: [[DSPLIB.org](https://ru.dsplib.org): [Analog, discrete, and digital signals](https://ru.dsplib.org/content/discrete_introduction/discrete_introduction.html)](https://app.notion.com/p/DSPLIB-org-Analog-discrete-and-digital-signals-17248130d89680adae25c4884846df13?pvs=21) ](All%20shades%20of%20Fourier%20Transform/Screenshot_2025-01-08_at_20.49.24.png)

          Source: [[DSPLIB.org](https://ru.dsplib.org): [Analog, discrete, and digital signals](https://ru.dsplib.org/content/discrete_introduction/discrete_introduction.html)](https://app.notion.com/p/DSPLIB-org-Analog-discrete-and-digital-signals-17248130d89680adae25c4884846df13?pvs=21) 

Can we immediately apply our existing Fourier apparatus to a discrete signal? Let's try the simplest approach — replacing $x_d(t)$ with $\tilde x(t)$, where:

$$
\tilde x(t) = \begin{cases}x(t), t = nT, & n - \text{integers}, \\0,  & \text{all other cases}
\end{cases}
$$

However, if we calculate the Fourier transform of this function, it would equal zero identically (simply from the definition of the Riemann integral). Therefore, we need a more sophisticated definition of a discrete signal.

TODO: remove

As we've discussed earlier, we typically work with **discrete signals**, which take arbitrary values only at fixed moments in time $t_n = nT$ (where $T$ is the **sampling interval**).

Given these samples, can we determine anything about the spectrum of the original signal?

**Can we directly apply Fourier Series?**

Let's explore this by sampling $N$ points from our signal and constructing a new function:

$$
\tilde x(t) = \begin{cases}x(t), & t = nT, n = 0, \ldots N - 1, \\0,  & t \in [0, NT], t \ne nT
\end{cases}
$$

If we periodically extend $\tilde x(t)$ across the entire real axis and attempt to calculate its Fourier coefficients, we encounter a problem — they all equal zero (simply from the definition of the Riemann integral):

$$
c_n = \frac{1}{P} \int_{0}^{P} \tilde x(t) e^{-2 \pi i \frac{n}{P} t} dt \equiv 0
$$

## Dirac’s delta-function

Let's consider a rectangular pulse $r_\tau(t)$ with duration $\tau$:

$$
r_\tau(t) = \begin{cases} 1, & |t| < \tau/2, \\1/2, & |t| = \tau / 2, \\0, & |t| > \tau / 2
\end{cases}
$$

Then, when normalizing the pulse amplitude to the duration $\tau$, we get a rectangular pulse $\frac{1}{\tau} r_\tau(t)$ whose area equals one for any finite value of $\tau$:

$$
\int_{-\infty}^\infty \frac{1}{\tau} r_\tau(t) dt = 1
$$

If we let the duration of the pulse $\frac{1}{\tau} r_\tau(t)$ approach zero, then the rectangular pulse will transform into what is known as the singular function $\delta(t)$:

$$
\delta(t) = \lim_{\tau \to 0} \frac{1}{\tau} r_\tau(t) = \begin{cases}1 \cdot \infty, & t = 0, \\0 & t \ne 0
\end{cases}
$$

Moreover, the unit area property will be preserved for the function $\delta(t)$:

$$
\int_{-\infty}^\infty \delta(t) dt = 1
$$

Here is a visualization of the rectangular pulse:

![Source: [[DSPLIB.org](https://ru.dsplib.org): [Dirac delta function and its properties](https://ru.dsplib.org/content/fourier_transform_delta_func/fourier_transform_delta_func.html)](https://app.notion.com/p/DSPLIB-org-Dirac-delta-function-and-its-properties-17248130d89680b69462d3bc90fbf519?pvs=21) ](All%20shades%20of%20Fourier%20Transform/Screenshot_2025-01-05_at_13.38.40.png)

Source: [[DSPLIB.org](https://ru.dsplib.org): [Dirac delta function and its properties](https://ru.dsplib.org/content/fourier_transform_delta_func/fourier_transform_delta_func.html)](https://app.notion.com/p/DSPLIB-org-Dirac-delta-function-and-its-properties-17248130d89680b69462d3bc90fbf519?pvs=21) 

Note that both in the definition of $\delta(t)$ and in the figure, we used the notation $1 \cdot \infty$ instead of infinity. This was done specifically to emphasize the unit area property of the delta function. If we multiply $\delta(t)$ by an arbitrary constant $\alpha$, we can write: $\alpha \delta(0) = \alpha \cdot \infty$.

Clearly, the definition of the delta function and the calculation of its integral contradict the classical definitions of functions and integrals. Therefore, Dirac's delta function is described within the framework of generalized functions.

### Scalar Product with Delta Function

[The scalar product](https://en.wikipedia.org/wiki/Dot_product#Functions) of a continuous signal $x(t)$ with Dirac's delta function $\delta(t)$ equals the value of $x(t)$ at zero:

$$
\langle x(t), \delta(t) \rangle = \int_{-\infty}^\infty x(t) \delta(t) dt = x(0)
$$

- Proof
    
    Let's consider the scalar product of a continuous signal $x(t)$ with Dirac's delta function $\delta(t)$:
    
    $$
    \langle x(t), \delta(t) \rangle = \int_{-\infty}^\infty x(t) \delta(t) dt
    $$
    
    Now, let's substitute the definition of the delta function as a limit of rectangular pulse sequences:
    
    $$
    \langle x(t), \delta(t) \rangle = \int_{-\infty}^\infty x(t) \delta(t) dt = \int_{-\infty}^\infty x(t) \lim_{\tau \to 0} \frac{1}{\tau} r_\tau(t) dt = \\= \lim_{\tau \to 0} \int_{-\infty}^\infty x(t)  \frac{1}{\tau} r_\tau(t) dt
    $$
    
    Let's represent the integral using Riemann's definition as a limit of the sum of rectangular pulse areas with duration $\tau$ ([Riemann sums](https://en.wikipedia.org/wiki/Riemann_sum)), as shown in the following figure:
    
    ![                               Source: [[DSPLIB.org](https://ru.dsplib.org): [Dirac delta function and its properties](https://ru.dsplib.org/content/fourier_transform_delta_func/fourier_transform_delta_func.html)](https://app.notion.com/p/DSPLIB-org-Dirac-delta-function-and-its-properties-17248130d89680b69462d3bc90fbf519?pvs=21) ](All%20shades%20of%20Fourier%20Transform/Screenshot_2025-01-05_at_14.14.15.png)
    
                                   Source: [[DSPLIB.org](https://ru.dsplib.org): [Dirac delta function and its properties](https://ru.dsplib.org/content/fourier_transform_delta_func/fourier_transform_delta_func.html)](https://app.notion.com/p/DSPLIB-org-Dirac-delta-function-and-its-properties-17248130d89680b69462d3bc90fbf519?pvs=21) 
    
    Then we can express the last equation as:
    
    $$
    \langle x(t), \delta(t) \rangle = \lim_{\tau \to 0} \sum_{n = -\infty}^\infty x(n \tau) \frac{1}{\tau} r_\tau(n \tau) \tau = \lim_{\tau \to 0} \sum_{n = -\infty}^\infty x(n \tau) r_\tau(n \tau)
    $$
    
    Note that $r_\tau(n \tau)$ is nonzero only when $n = 0$. Therefore, the sum reduces to a single term corresponding to $n = 0$:
    
    $$
    \langle x(t), \delta(t) \rangle = \lim_{\tau \to 0} x(0) \underbrace{r_\tau(0)}_1 = x(0)
    $$
    

### **Filtering Property of the Delta Function**

The scalar product of $x(t)$ with a delta function shifted by $t_0$ equals the value of $x(t)$ at point $t_0$:

$$
\langle x(t), \delta(t - t_0) \rangle = \int_{-\infty}^\infty x(t) \delta(t - t_0) dt = x(t_0)
$$

**Proof**. Let's consider the scalar product of $x(t)$ with a delta function shifted by $t_0$:

$$
\langle x(t), \delta(t - t_0) \rangle = \int_{-\infty}^\infty x(t) \delta(t - t_0) dt
$$

Let's make a change of variables $\xi = t - t_0$, then $t = \xi + t_0$, $dt = d\xi$. Since the limits of integration remain unchanged, the last expression becomes:

$$
\int_{-\infty}^\infty x(t) \delta(t - t_0) dt = \int_{-\infty}^\infty x(\xi + t_0) \delta(\xi) d\xi = x(t_0)
$$

## Mathematical Model of a Discrete Signal

How can we measure an analog signal in practice? Clearly, regardless of our measuring device, it takes some time to make a measurement (let's denote this time as $\tau$). Therefore, during measurement, we don't get an exact value at $t = t_n = nT$, but rather an averaged value within the measurement interval $[nT - \tau/2, nT + \tau/2]$, which mathematically can be expressed as:

$$
\hat x_d(nT) = \frac{1}{\tau}\int_{nT - \tau/2}^{nT + \tau/2} x(t) dt
$$

Here, the hat above $x_d$ denotes an approximate estimate.

Recall that earlier we introduced a convenient function $r_\tau(t)$ that equals $1$ on the interval $(- \tau/2, \tau/2)$ and $0$ outside of it. Therefore, we can rewrite the integral as

$$
\hat x_d(nT) = \frac{1}{\tau} \int_{nT - \tau/2}^{nT + \tau/2} x(t) r_\tau(t - nT)dt = \int_{nT - \tau/2}^{nT + \tau/2} x(t) \frac{1}{\tau}r_\tau(t - nT)dt
$$

Taking into account this equality, we can propose the following function as an approximate model of the discrete signal:

$$
\hat x_d(t) = x(t) \sum_{n=-\infty}^{\infty} \frac{1}{\tau}r_\tau(t - nT)
$$

Integrating $\hat x_d(t)$ over the interval $t \in [nT - \tau/2, nT + \tau/2]$, we obtain an approximate estimate of the signal value $\hat x(nT)$. The figure below illustrates this concept:

![         Source: [[DSPLIB.org](https://ru.dsplib.org): [Analog, discrete, and digital signals](https://ru.dsplib.org/content/discrete_introduction/discrete_introduction.html)](https://app.notion.com/p/DSPLIB-org-Analog-discrete-and-digital-signals-17248130d89680adae25c4884846df13?pvs=21) ](All%20shades%20of%20Fourier%20Transform/Screenshot_2025-01-12_at_13.29.11.png)

         Source: [[DSPLIB.org](https://ru.dsplib.org): [Analog, discrete, and digital signals](https://ru.dsplib.org/content/discrete_introduction/discrete_introduction.html)](https://app.notion.com/p/DSPLIB-org-Analog-discrete-and-digital-signals-17248130d89680adae25c4884846df13?pvs=21) 

As the duration $\tau$ decreases, the estimation error will decrease, and in the limit we can obtain the discrete signal as

$$
x_d(t) = \lim_{\tau \to 0} x(t) \sum_{n=-\infty}^{\infty} \frac{1}{\tau}r_\tau(t - nT) = x(t) \sum_{n = -\infty}^\infty \delta(t - nT),
$$

where $\delta(t - nT)$ is the Dirac function shifted by  $t_n$ discussed above.

Note that this obtained model is no longer an approximate estimation, but represents the **true model** of the discrete signal.

An infinite sum of shifted delta functions is called a **lattice function** and is denoted $l_T(t)$:

$$
l_T(t) = \sum_{n = -\infty}^\infty \delta(t - nT)
$$

Then the mathematical model of the discrete signal will be the product of the original analog signal $x(t)$ and the lattice function:

$$
x_d(t) = x(t) l_T(t)
$$

The following figure illustrates the concepts of $l_T(t)$ and $x_d(t)$:

![                       Source: [[DSPLIB.org](https://ru.dsplib.org): [Analog, discrete, and digital signals](https://ru.dsplib.org/content/discrete_introduction/discrete_introduction.html)](https://app.notion.com/p/DSPLIB-org-Analog-discrete-and-digital-signals-17248130d89680adae25c4884846df13?pvs=21) ](All%20shades%20of%20Fourier%20Transform/Screenshot_2025-01-12_at_13.37.04.png)

                       Source: [[DSPLIB.org](https://ru.dsplib.org): [Analog, discrete, and digital signals](https://ru.dsplib.org/content/discrete_introduction/discrete_introduction.html)](https://app.notion.com/p/DSPLIB-org-Analog-discrete-and-digital-signals-17248130d89680adae25c4884846df13?pvs=21) 

**TODO: remove**

Let’s “put” one delta-function to each sampling point and multiply $x(t)$ by the sum of such functions:

$$
x_d(t) = \sum_{n = -\infty}^\infty x(t) \delta(t - nT)
$$

Let's examine what happens when we integrate this sum near a sampling point $t_0 = kT$, $\tau < T$:

$$
\int_{kT - \tau}^{kT + \tau} x(t)\left( \sum_{n = -\infty}^\infty \delta(t - nT) \right) dt = \\= \{ \text{all deltas except for } n = k \text{ are zeros in these limits} \} = \\
= \int_{kT - \tau}^{kT + \tau} x(t) \delta(t - kT)  dt = x(kT)
$$

Perfect! This shows that our sampling points are now preserved during integration.

# Discrete-Time Fourier Transform

Now that we have introduced the discrete signal model, let's calculate its Fourier transform:

$$
X_d(f) = \int_{-\infty}^\infty x_d(t) e^{-2 \pi i f t} dt = \int_{-\infty}^\infty \left(x(t) \sum_{n = -\infty}^\infty \delta(t - n T) \right) e^{-2 \pi i f t} dt
$$

Let's swap the summation and integration operations and apply the filtering property of the delta function:

$$
X_d(f) = \sum_{n=-\infty}^\infty \int_{-\infty}^\infty x(t) \delta(t - nT) e^{-2 \pi i f t} dt = \sum_{n=-\infty}^\infty  x(n T) e^{-2 \pi i f n T}
$$

We obtained $X_d(f)$ as a sum of complex exponentials, which for $n \ne 0$ are periodic functions with period

$$
P(n) = \frac{1}{nT} = \frac{1}{n} f_s
$$

where  $f_s$ is the signal sampling frequency ($\text{Hz}$). When $n = 0$, the complex exponential equals $1$.

The maximum repetition period of $X_d(f)$ occurs when $n = 1$, in which case it equals the sampling frequency:

$$
P(1) = f_s
$$

Thus, $X_d(f)$ is a periodic function with period $P = f_s = 1/T$.

If we set the sampling frequency to $f_s = 1 \text{ Hz}$, the expression for $X_d(f)$ becomes the **discrete-time Fourier transform**:

$$
X_d(f) = \sum_{n=-\infty}^\infty  x[n] e^{-2 \pi i f n}
$$

As a result of the DTFT, we obtain a 1-periodic function. Here, $n$ should be interpreted as an index in the array of signal samples, and $x[n]$ represents the value of the n-th sample.

Note that the indexing in the expressions above runs from negative infinity to positive infinity. Thus, the DTFT is generally valid for infinite-duration discrete signals. If the signal sample is limited to $N$  points, then by setting $x[n] = 0$ for $n < 0$ and $n \ge N$, the DTFT expression takes the form:

$$
X_d(f) = \sum_{n=0}^{N - 1}  x[n] e^{-2 \pi i f n}
$$

In practical applications, we cannot work with infinite-length signal samples, which makes the expression above particularly important.

As an example, the figure below shows a time-limited discrete signal containing $N = 5$ non-zero samples.

![                                            Source: [[DSPLIB.org](https://ru.dsplib.org): [Discrete-Time Fourier Transform](https://ru.dsplib.org/content/dtft/dtft.html)](https://app.notion.com/p/DSPLIB-org-Discrete-Time-Fourier-Transform-17948130d896802581a2cfecdf1b900a?pvs=21) ](All%20shades%20of%20Fourier%20Transform/Screenshot_2025-01-19_at_20.25.57.png)

                                            Source: [[DSPLIB.org](https://ru.dsplib.org): [Discrete-Time Fourier Transform](https://ru.dsplib.org/content/dtft/dtft.html)](https://app.notion.com/p/DSPLIB-org-Discrete-Time-Fourier-Transform-17948130d896802581a2cfecdf1b900a?pvs=21) 

The DTFT result is a complex function, and the figure shows its amplitude spectrum $|X_d(f)|$.

# Discrete Fourier Transform

Above, we derived the Fourier transform of a discrete signal and found that it is a continuous periodic function. However, in practice, we can only work with discrete sets of numbers. How can we obtain a discrete spectrum for our discrete signal?

Let's consider a discrete signal $x_d(t)$ that is time-limited and contains $N$ non-zero samples taken with a sampling period $T$ seconds. This assumption always holds in practice since we cannot obtain an infinite number of signal samples. Therefore, the duration of the discrete signal equals $NT$ seconds, and  $x_d(t)$  can be written as:

$$
x_d(t) = \sum_{n = 0}^{N - 1} x(t) \delta(t - nT)
$$

Earlier we discussed that periodic signals have a discrete spectrum, which is obtained through the Fourier series expansion of a periodic signal. Therefore, to obtain a discrete spectrum, we need to make the original discrete signal periodic by repeating it infinitely in time with a period $P$ that is a multiple of the sampling interval $T$. In this case, we can perform such periodic repetition because the signal has a finite duration equal to $NT$.

The process of signal repetition in time is illustrated in the figure below:

![                                                Source: [[DSPLIB.org](https://ru.dsplib.org): [Discrete Fourier Transform](https://ru.dsplib.org/content/dft/dft.html)](https://app.notion.com/p/DSPLIB-org-Discrete-Fourier-Transform-17948130d896802bbbd9dec0deaefd02?pvs=21) ](All%20shades%20of%20Fourier%20Transform/Screenshot_2025-01-12_at_15.06.00.png)

                                                Source: [[DSPLIB.org](https://ru.dsplib.org): [Discrete Fourier Transform](https://ru.dsplib.org/content/dft/dft.html)](https://app.notion.com/p/DSPLIB-org-Discrete-Fourier-Transform-17948130d896802bbbd9dec0deaefd02?pvs=21) 

The signal can be repeated with different periods $P$, but the repetition period must be greater than or equal to the signal duration $P \ge NT$ to prevent temporal overlap between the signal and its periodic repetitions. The minimum repetition period that prevents overlapping between the signal and its repetitions equals $P_\text{min} = NT$ seconds. The signal repetition with this minimum period is shown in the figure:

![                                            Source: [[DSPLIB.org](https://ru.dsplib.org): [Discrete Fourier Transform](https://ru.dsplib.org/content/dft/dft.html)](https://app.notion.com/p/DSPLIB-org-Discrete-Fourier-Transform-17948130d896802bbbd9dec0deaefd02?pvs=21) ](All%20shades%20of%20Fourier%20Transform/Screenshot_2025-01-12_at_15.08.55.png)

                                            Source: [[DSPLIB.org](https://ru.dsplib.org): [Discrete Fourier Transform](https://ru.dsplib.org/content/dft/dft.html)](https://app.notion.com/p/DSPLIB-org-Discrete-Fourier-Transform-17948130d896802bbbd9dec0deaefd02?pvs=21) 

Now, let's consider that the signal $x_d(t)$ has a periodic extension with the minimum period $P_\text{min} = NT$  (as shown in the figure above). Then, on the interval $[0, NT]$, it can be expanded into a Fourier series:

$$
x_d(t) = \sum_{k = -\infty}^\infty c_k e^{2 \pi i \frac{k}{NT} t},
$$

where

$$
c_k = \frac{1}{NT} \int_{0}^{NT} x_d(t) e^{-2 \pi i \frac{k}{NT} t} dt = \frac{1}{NT} \int_{0}^{NT} \left( \sum_{n = 0}^{N - 1} x(t) \delta(t - nT) \right) e^{-2 \pi i \frac{k}{NT} t} dt
$$

(To calculate $c_k$, we can use any integration period equal to the signal period, and here it's more convenient to use $[0, NT]$ instead of $[-\frac{NT}{2}, \frac{NT}{2}]$ )

Let's interchange the order of integration and summation, and apply the filtering property of the delta function:

$$
c_k = \frac{1}{NT} \sum_{n = 0}^{N - 1} \int_0^{NT} x(t) \delta(t - nT) e^{-2 \pi i \frac{k}{NT} t} dt = \frac{1}{NT} \sum_{n = 0}^{N - 1} x(nT) e^{-2 \pi i \frac{k}{N} n}
$$

$$
c_k = \frac{1}{NT} \sum_{n = 0}^{N - 1} x(nT) e^{-2 \pi i \frac{k}{NT} nT}
$$

Note that the exponents of the complex exponentials in the expression above **do** **not depend** on the sampling interval $T$, but only on the indices $n$ and $k$, which indicate the ordinal numbers of the time and spectral samples.

The expression obtained for $c_k$ is valid for any integer $k$, but recall that the original signal $x_d(t)$ was discrete, so its spectrum is periodic and repeats every $N$ samples. This is very easy to verify:

$$
c_{k + N} = \frac{1}{NT} \sum_{n = 0}^{N - 1} x(nT) e^{-2 \pi i \frac{k + N}{N} n} = \frac{1}{NT} \sum_{n = 0}^{N - 1} x(nT) e^{-2 \pi i \frac{k}{N} n} \cdot \underbrace{e^{-2 \pi i n}}_{=1} = c_k
$$

We can also recall the relationship between the Fourier transform and Fourier coefficients discussed above:

$$
c_k = \frac{1}{P} X(f_k),
$$

where $P$ is the function period, $X$ is the Fourier transform of a signal that equals the periodic signal over one period and zero elsewhere, and $f_k = \frac{k}{P}$. The Fourier transform of the original signal (without periodic extension) is the DTFT we discussed earlier:

$$
X_d(f) = \sum_{n=0}^{N - 1}  x(n T) e^{-2 \pi i f n T}
$$

Therefore, knowing that $P = NT$,

$$
c_k  = \frac{1}{NT} X_d\left ( \frac{k}{NT} \right) = \\ = \frac{1}{NT}  \sum_{n=0}^{N - 1}  x(n T) e^{-2 \pi i \frac{k}{NT} n T} = \frac{1}{NT} \sum_{n=0}^{N - 1}  x(n T) e^{-2 \pi i \frac{k}{N} n},
$$

which matches our earlier result.

If we operate only with indices of the input signal and spectral samples (setting $T = 1$), we obtain the **discrete Fourier transform** expression:

$$
X[k] = \frac{1}{N} \sum_{n=0}^{N - 1}  x[n] e^{-2 \pi i \frac{k}{N} n}
$$

Note: In the literature, the expression for the forward DFT often does not include the factor $\frac{1}{N}$. Looking ahead, we will also move this factor to the expression for the inverse discrete Fourier transform.

**TODO: remove**

Fourier Series for a discrete signal

In practice our time signal is time-limited and contains $N$ non-zero samples taken with a sampling period $T$ seconds:

$$
x_d(t) = \sum_{n = 0}^{N - 1} x(t) \delta(t - nT)
$$

Let's explore what happens when we try to find its Fourier Series.

First, we must extend our signal periodically so it's defined across the entire time axis. The smallest possible period is NT.

$$
x(t) = \sum_{n = -\infty}^\infty c_n e^{2 \pi i \frac{n}{P} t}
$$

The standard formula for calculating Fourier coefficients of a periodic function, which we mentioned earlier, is:

$$
c_k = \frac{1}{P} \int_{0}^{P} x(t) e^{-2 \pi i \frac{k}{P} t} dt
$$

Applying this to our signal:

$$
c_k = \frac{1}{NT} \int_{0}^{NT} x_d(t) e^{-2 \pi i \frac{k}{NT} t} dt = \frac{1}{NT} \int_{0}^{NT} \left( \sum_{n = 0}^{N - 1} x(t) \delta(t - nT) \right) e^{-2 \pi i \frac{k}{NT} t} dt
$$

Let's interchange the order of integration and summation, and apply the filtering property of the delta function:

$$
c_k = \frac{1}{NT} \sum_{n = 0}^{N - 1} \int_0^{NT} x(t) \delta(t - nT) e^{-2 \pi i \frac{k}{NT} t} dt = \frac{1}{NT} \sum_{n = 0}^{N - 1} x(nT) e^{-2 \pi i \frac{k}{N} n}
$$

$$
c_k = \frac{1}{NT} \sum_{n = 0}^{N - 1} x(nT) e^{-2 \pi i \frac{k}{NT} nT} = \frac{1}{NT} \sum_{n = 0}^{N - 1} x(nT) e^{-2 \pi i \frac{k}{N} n}
$$

Note that the exponents of the complex exponentials in the expression above **do** **not depend** on the sampling interval $T$, but only on the indices $n$ and $k$, which indicate the ordinal numbers of the time and spectral samples.

We can also write out the expression for the inverse discrete Fourier transform (we'll skip the complete derivation):

Важно отметить, что на практике гораздо чаще требуется рассчитывать прямое ДПФ, чем обратное. Поэтому принято нормировочный множитель $\frac{1}{N}$ учитывать в обратном преобразовании, а не в прямом. Тогда пару ДПФ можно переписать в виде:

In practice, we usually need to calculate the forward DFT (Direct Fourier Transform) more often than the inverse DFT. Because of this, there's a common convention: we put the scaling factor$\frac{1}{N}$in the inverse transform equations instead of the forward transform. This lets us write the DFT pair in a simpler way:

**The Discrete Fourier Transform (DFT) and Its Inverse**

**DFT properties that follow from math**

**DFT properties that follow from the previous part**

$$
f_k = \frac{k}{NT_s} = k \frac{f_s}{N} = k \Delta f
$$

For $N = 100$, $f_s = 8000$ $\text{Hz}$:

$$
\Delta f = 8000 / 100 = 80 \text{ Hz}
$$

We created a spectrogram to visualize how the signal's spectrum changes over time.

We then compressed the frequencies by applying mel filters.

# Inverse Discrete Fourier Transform

Учтем, что ДПФ возвращает один период дискретного периодического спектра $c_k, k = 0, \ldots, N - 1$. Также мы выяснили выше, что

$$
c_k = \frac{1}{NT} X_d(f_k),
$$

где $f_k = \frac{k}{NT}$. То есть у нас есть есть $N$ отсчётов некоторой непрерывной функции $\frac{1}{NT} X_d(f)$, и расстояние между каждым отсчётом равно $\frac{1}{NT}$. Это наводит на мысль, что, по аналогии с дискретным сигналом, мы можем выразить дискретный спектр ДПФ на одном периоде, используя дельта-функцию:

$$
X_{DFT}(f) = \frac{1}{NT} X_d(f) \sum_{k = 0}^{N - 1}  \delta\left(f - \frac{k}{NT}\right)
$$

Спектр $X_{DFT}(f)$ является $\frac{1}{T}$-периодической функцией (функция $X_d(f)$ — $\frac{1}{T}$-периодическая, дельта-функции в сумме идут с шагом $\frac{1}{NT}$), поэтому он может быть разложен в ряд Фурье:

$$
X_{DFT}(f) = \sum_{m=-\infty}^\infty p_m e^{2 \pi i m T f},
$$

где $p_m$ — коэффициенты Фурье:

$$
p_m = T \int_{0}^{\frac{1}{T}} X_{DFT}(f) e^{-2 \pi i m T f} df = \\
= T \int_{0}^{\frac{1}{T}} \left( \sum_{k = 0}^{N - 1} \frac{1}{NT} X_d(f) \delta\left(f - \frac{k}{NT}\right)\right) e^{-2 \pi i m T f} df
$$

Поменяем местами операции интегрирования и суммирования и применим фильтрующее свойство дельта-функции:

$$
p_m = T \sum_{k=0}^{N - 1} \int_{0}^{\frac{1}{T}} X_d(f) \delta\left(f - \frac{k}{NT}\right) e^{-2 \pi i m T f} df = \\
= \frac{1}{N} \sum_{k=0}^{N - 1} X_d\left( \frac{k}{NT}\right) e^{-2 \pi i m T \cdot \frac{k}{NT}} = \frac{1}{N} \sum_{k=0}^{N - 1} X_d\left( \frac{k}{NT}\right) e^{-2 \pi i \frac{m}{N} k}
$$

Ранее мы получали соотношение $X_d(f) = \sum_{n=0}^{N - 1}  x(n T) e^{-2 \pi i f n T}$. Для $f = \frac{k}{NT}$ оно равно:

$$
X_d\left( \frac{k}{NT}\right) = \sum_{n=0}^{N - 1}  x(n T) e^{-2 \pi i \frac{k}{NT} n T} = \sum_{n=0}^{N - 1}  x(n T) e^{-2 \pi i \frac{k}{N} n}
$$

Подставим его в выражение для $p_m$:

$$
p_m = \frac{1}{N} \sum_{k=0}^{N - 1} \left( \sum_{n=0}^{N - 1}  x(n T) e^{-2 \pi i \frac{k}{N} n}\right) e^{-2 \pi i \frac{m}{N} k} = \\
= \frac{1}{N} \sum_{k = 0}^{N - 1} \sum_{n = 0}^{N - 1} x(nT) e^{- 2 \pi i \frac{n + m}{N} k} = \\
= \frac{1}{N} \sum_{n = 0}^{N - 1} x(nT) \sum_{k = 0}^{N - 1} e^{- 2 \pi i \frac{n + m}{N} k}
$$

Можно заметить, что при $n = -m$ сумма комплексных экспонент равна:

$$
\sum_{k = 0}^{N - 1} e^{- 2 \pi i \frac{n + m}{N} k} = \sum_{k = 0}^{N - 1} 1 = N,
$$

а при $n \ne m$ сумму комплексных экспонент можно рассматривать как сумму первых $N$ членов геометрической прогрессии:

$$
\sum_{k = 0}^{N - 1} e^{- 2 \pi i \frac{n + m}{N} k} = \frac{\left( e^{- 2 \pi i \frac{n + m}{N}} \right)^N - 1}{e^{- 2 \pi i \frac{n + m}{N}} - 1} = \frac{ 1 - 1}{e^{- 2 \pi i \frac{n + m}{N}} - 1} = 0
$$

Это означает, что в выражении для $p_m$ ненулевым окажется лишь одно слагаемое при $n = -m$:

$$
p_m = \frac{1}{N} \cdot x(-mT) \cdot N = x(-mT)
$$

Выше мы получили, что

$$
p_m = \frac{1}{N} \sum_{k=0}^{N - 1} X_d\left( \frac{k}{NT}\right) e^{-2 \pi i \frac{m}{N} k}
$$

Тогда, вспоминая, что $c_k  = \frac{1}{NT} X_d\left ( \frac{k}{NT} \right)$, можно записать:

$$
x(-mT) = \frac{1}{N} \sum_{k=0}^{N - 1} X_d\left( \frac{k}{NT}\right) e^{-2 \pi i \frac{m}{N} k} \\
x(mT) = T \sum_{k=0}^{N - 1} \frac{1}{NT} X_d\left( \frac{k}{NT}\right) e^{2 \pi i \frac{m}{N} k} \\
x(mT) = T \sum_{k=0}^{N - 1} c_k e^{2 \pi i \frac{m}{N} k}
$$

Итого, мы научились выражать cпектр $c_k, k = 0, \ldots, N - 1$, через отсчёты $x(nT), n = 0, \ldots, N - 1$ и наоборот:

$$
c_k = \frac{1}{NT} \sum_{n = 0}^{N - 1} x(nT) e^{-2 \pi i \frac{k}{N} n} \\
x(nT) = T \sum_{k=0}^{N - 1} c_k e^{2 \pi i \frac{n}{N} k}
$$

Если мы будем оперировать только с индексами входного сигнала и спектральных отсчетов (положив $T = 1$), то мы получим:

$$
X[k] = \frac{1}{N} \sum_{n=0}^{N - 1}  x[n] e^{-2 \pi i \frac{k}{N} n} \\
x[n] = \sum_{k=0}^{N - 1} X[k] e^{2 \pi i \frac{n}{N} k}
$$

Важно отметить, что на практике гораздо чаще требуется рассчитывать прямое ДПФ, чем обратное. Поэтому принято нормировочный множитель $\frac{1}{N}$ учитывать в обратном преобразовании, а не в прямом. Тогда пару ДПФ можно переписать в виде:

$$
X[k] = \sum_{n=0}^{N - 1}  x[n] e^{-2 \pi i \frac{k}{N} n} \\
x[n] = \frac{1}{N} \sum_{k=0}^{N - 1} X[k] e^{2 \pi i \frac{n}{N} k}
$$

В ЛЕКЦИИ ЛУЧШЕ ПРОСТО ДАТЬ РЯД ФУРЬЕ, ОТ НЕГО ПЕРЕЙТИ К МОДЕЛИ СИГНАЛА, А ПОТОМ ПОЛУЧИТЬ ДПФ КАК РЯД ФУРЬЕ ДИСКРЕТНОГО СИГНАЛА 

TODO: используй картинки отсюда для следующего блог-поста: [https://colab.research.google.com/drive/1c8QghHf-XifbFMs0K1zMuTyWY8Xs6w5O](https://colab.research.google.com/drive/1c8QghHf-XifbFMs0K1zMuTyWY8Xs6w5O)

TODO: приложи jupyter-нотбуки с:

- демонстрацией асимметрии для n чётных и нечётных
- добавить блог-пост про дискретное преобразование Фурье из лекций
- мб ноутбук какой-то на основе Роминого

# References

- [https://en.wikipedia.org/wiki/Fourier_series](https://en.wikipedia.org/wiki/Fourier_series)
- [YSDA Speech course, 2022, week 2](https://github.com/yandexdataschool/speech_course/tree/2022/week_02)
- [Angelo’s Notes: Continuous Time Fourier Transform](https://angeloyeo.github.io/2019/07/07/CTFT_en.html#google_vignette)
- [Zorich, Calculus, part 2](https://matan.math.msu.su/media/uploads/2020/03/V.A.Zorich-Kniga-II-9-izdanie-Temp-Corr-3.pdf)
- [DSPLIB.org](https://ru.dsplib.org): [Fourier Transform of Non-periodic Signals](https://ru.dsplib.org/content/fourier_transform/fourier_transform.html)
- [DSPLIB.org](https://ru.dsplib.org): [Dirac delta function and its properties](https://ru.dsplib.org/content/fourier_transform_delta_func/fourier_transform_delta_func.html)
- [DSPLIB.org](https://ru.dsplib.org): [Analog, discrete, and digital signals](https://ru.dsplib.org/content/discrete_introduction/discrete_introduction.html)
- [DSPLIB.org](https://ru.dsplib.org): [Discrete-Time Fourier Transform](https://ru.dsplib.org/content/dtft/dtft.html)
- [DSPLIB.org](https://ru.dsplib.org): [Discrete Fourier Transform](https://ru.dsplib.org/content/dft/dft.html)

We built a spectrogram that showed how the signal spectrum evolves through time

we then compressed the frequencies using mel filters