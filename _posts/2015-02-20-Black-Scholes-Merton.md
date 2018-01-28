---
title: Black-Scholes-Merton Formula 
---
Black-Scholes, or sometimes Black-Scholes-Merton, is a mathematical model that seeks to explain the behavior of financial derivatives, most commonly options. 
    It was proposed by Black and Scholes in 1973. It gave theoretical support for trading options to hedge positions, 
    which had been practice but lacked solid support. From the model we are able to calculate what the price of an option should be based on a number of 
	different factors. Nowadays there are numerous variations of the Black-Scholes model, each of which seeks to improve the model based on certain criteria, 
	usually at the cost of a significant increase in complexity. This paper will focus on the original model, the basis for all other models.
 
\
	\ C = Call option price 
	\ S = Current stock price
	\ K = Strike price of the option
	\ r = risk-free interest rate (a number between 0 and 1)
	\ $\sigma$ = volatility of the stocks return (a number between 0 and 1)
	\ t = time to option maturity (in years)
	\ N = normal cumulative distribution function
\


## Black-Scholes Equation
The Black-Scholes equation describes the price of an option over time. The derivation of this equation is complex and exceeds the scope of this paper, so we simply provide the equation.

<a href="https://www.codecogs.com/eqnedit.php?latex=\frac{\partial&space;\mathrm&space;C}{&space;\partial&space;\mathrm&space;t&space;}&space;&plus;&space;\frac{1}{2}\sigma^{2}&space;\mathrm&space;S^{2}&space;\frac{\partial^{2}&space;\mathrm&space;C}{\partial&space;\mathrm&space;C^2}&space;&plus;&space;\mathrm&space;r&space;\mathrm&space;S&space;\frac{\partial&space;\mathrm&space;C}{\partial&space;\mathrm&space;S}\&space;=&space;\mathrm&space;r&space;\mathrm&space;C" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\frac{\partial&space;\mathrm&space;C}{&space;\partial&space;\mathrm&space;t&space;}&space;&plus;&space;\frac{1}{2}\sigma^{2}&space;\mathrm&space;S^{2}&space;\frac{\partial^{2}&space;\mathrm&space;C}{\partial&space;\mathrm&space;C^2}&space;&plus;&space;\mathrm&space;r&space;\mathrm&space;S&space;\frac{\partial&space;\mathrm&space;C}{\partial&space;\mathrm&space;S}\&space;=&space;\mathrm&space;r&space;\mathrm&space;C" title="\frac{\partial \mathrm C}{ \partial \mathrm t } + \frac{1}{2}\sigma^{2} \mathrm S^{2} \frac{\partial^{2} \mathrm C}{\partial \mathrm C^2} + \mathrm r \mathrm S \frac{\partial \mathrm C}{\partial \mathrm S}\ = \mathrm r \mathrm C" /></a>

\begin{equation}
	\frac{\partial \mathrm C}{ \partial \mathrm t } + \frac{1}{2}\sigma^{2} \mathrm S^{2} \frac{\partial^{2} \mathrm C}{\partial \mathrm C^2}
	+ \mathrm r \mathrm S \frac{\partial \mathrm C}{\partial \mathrm S}\ =
	\mathrm r \mathrm C 
	\label{eq:1}
\end{equation}

Notice that that equation \eqref{eq:1} is a partial differential equation. The solution of this equation gives us the Black-Scholes formula.


## Black-Scholes formula for European option price
The Black-Scholes formula allows us the calculate the price of European call and put options.
\begin{equation}
	\mathrm C(\mathrm S,\mathrm t)= \mathrm N(\mathrm d_1)\mathrm S - \mathrm N(\mathrm d_2) \mathrm K \mathrm e^{-rt}
	\label{eq:2}
\end{equation}

\begin{equation}
	\mathrm d_1= \frac{1}{\sigma \sqrt{\mathrm t}} \left[\ln{\left(\frac{S}{K}\right)} + t\left(r + \frac{\sigma^2}{2} \right) \right]
\end{equation}

\begin{equation}
	\mathrm d_2= \frac{1}{\sigma \sqrt{\mathrm t}} \left[\ln{\left(\frac{S}{K}\right)} + t\left(r - \frac{\sigma^2}{2} \right) \right]
\end{equation}

\begin{equation}
	N(x)=\frac{1}{\sqrt{2\pi}} \int_{-\infty}^{x} \mathrm e^{-\frac{1}{2}z^2} dz
	\label{eq:5}
\end{equation}


\section{Example}
You want to buy an IBM European call option with a strike price of \$210. The stock is currently trading at a price of \$208.99 . You calculate the volatility of the stock to be 17\%. 
The rate at which you can borrow and lend money is 5\% (this is the risk-free interest rate). 
The time to maturity of the option is 77 days. What price should you pay (per share) for the option contract?

$$\mathrm d_1= \frac{1}{0.17 \sqrt{0.21095}} \left[\ln{\left(\frac{208.99}{210}\right)} + 0.21095\left(0.05 + \frac{0.17^2}{2} \right) \right]=0.1123799$$
$$\mathrm d_2= \frac{1}{0.17 \sqrt{0.21095}} \left[\ln{\left(\frac{208.99}{210}\right)} + 0.21095\left(0.05 - \frac{0.17^2}{2} \right) \right]=0.0343001$$

Now that we've calculated $\mathrm d_1$ and $\mathrm d_2$ we will calculate $\mathrm N(\mathrm d_1)$ and $\mathrm N(\mathrm d_2)$. It should be noted that it's 
not possible to evaluate equation \eqref{eq:5} by normal means so you must use a table or use computer software to evaluate the
following integrals:

$$N(d_1)=N(0.1123799)=\frac{1}{\sqrt{2\pi}} \int_{-\infty}^{0.1123799} \mathrm e^{-\frac{1}{2}z^2} dz = 0.3516077$$
$$N(d_2)=N(0.0343001)=\frac{1}{\sqrt{2\pi}} \int_{-\infty}^{0.0343001} \mathrm e^{-\frac{1}{2}z^2} dz = 0.3135993$$

Now we plug these in equation \eqref{eq:2} to calculate the price of the call option (per share).

$$\mathrm C(208.99,0.21095)= (0.3516077)(208.99) - (0.3135993)(210) \mathrm e^{-(0.05)(0.21095)} \approx 2.3454$$

You should pay around \$2.35 (per share) for the options contract. As a side note, options contracts are sold in lots of 100 shares, 
so this particular contract would sell for roughly \$235.


<img src="https://latex.codecogs.com/svg.latex?\Large&space;x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}" title="\Large x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}" />

 h<sub>&theta;</sub>(x) = &theta;<sub>o</sub> x + &theta;<sub>1</sub>x

![\Large x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}](https://latex.codecogs.com/svg.latex?x%3D%5Cfrac%7B-b%5Cpm%5Csqrt%7Bb%5E2-4ac%7D%7D%7B2a%7D

\[
\alpha 
\frac{\frac{x}{1}}{x - y}
^3/_7
\]

\[
\begin{equation*}
\mathbf{V}_1 \times \mathbf{V}_2 =  \begin{vmatrix}
\mathbf{i} & \mathbf{j} & \mathbf{k} \\
\frac{\partial X}{\partial u} &  \frac{\partial Y}{\partial u} & 0 \\
\frac{\partial X}{\partial v} &  \frac{\partial Y}{\partial v} & 0
\end{vmatrix}
\end{equation*}
\]
