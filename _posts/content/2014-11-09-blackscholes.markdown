---
layout: post
author: Nathan Epstein
title:  "Ito’s Lemma & Black-Scholes"
categories: jekyll update, content
---

###Ito’s Lemma (Informal Derivation)

Much like we use derivatives to examine how deterministic functions change with their underlying variables, Ito’s lemma lets us examine how functions of stochastic variables change over the evolution of the underlying stochastic process. More formally, Ito’s lemma is used to find the differential of a time-dependent function of a stochastic process.

If x is an Ito drift-diffusion process, we may represent it as follows:

<div class='eqtn' id='img1'></div>
<script type="text/javascript">
  var html = $.parseHTML(katex.renderToString("dx = adt + bdW"));
  $('#img1').append(html);
</script>

Note: Alpha and beta are deterministic functions, W is a Wiener process.

Let f be a function of x and t. Perform a Taylor expansion to get an expression for df.

<div class='eqtn' id='img2'></div>
<script type="text/javascript">
  var string = 'f(t+dt,x+dx) = f(t,x)+f_x dx + f_t dt + 0.5f_{xx} dx^2 + 0.5 f_{tt} dt^2 + HOT'
  var html = $.parseHTML(katex.renderToString(string));
  $('#img2').append(html);
</script>

Note: Subscripts indicate partial derivatives, HOT refers to higher order terms.

From the <a href="http://books.google.com/books?id=H06xzeRQgV4C&pg=PA124&lpg=PA124&dq=stochastic+calculus+box+algebra&source=bl&ots=6PZm0mxQjG&sig=lKsLvHRArHhgCLtgZOehv6Hin7c&hl=en&sa=X&ei=rsBzU9rKF4fgsASfgILAAQ&ved=0CDIQ6AEwAQ#v=onepage&q=stochastic%20calculus%20box%20algebra&f=false">box algebra</a>, we know (dt)(dt) = (dW)(dt) = 0 and that (dW)(dW) = dt. All higher order terms go to zero as they will contain at least one of (dt)(dt) or (dW)(dt). Plug dx into the expression above and remove cancel all zero terms. This gives us the final statement of Ito’s lemma:

<div class='eqtn' id='img3'></div>
<script type="text/javascript">
  var string = 'df = f_tdt + f_xdx + 0.5f_{xx}b^2dt'
  var html = $.parseHTML(katex.renderToString(string));
  $('#img3').append(html);
</script>

###The Black-Scholes PDE

The goal of the Black-Scholes PDE is to let us determine the value of a derivative on an underlying stock. We get the PDE by examining the returns on a portfolio of the derivative (call it V) and the underlying stock (denoted S). We go long 1 unit of the derivative and short dV/dS shares of the stock.

Our portfolio at time t is as follows:

<div class='eqtn' id='img4'></div>
<script type="text/javascript">
  var string = 'P(t,S,V) = V(t,S) - V_SS(t)'
  var html = $.parseHTML(katex.renderToString(string));
  $('#img4').append(html);
</script>

We assume that the stock follows geometric Brownian motion.

<div class='eqtn' id='img5'></div>
<script type="text/javascript">
  var string = 'dS = \\mu Sdt + \\sigma SdW'
  var html = $.parseHTML(katex.renderToString(string));
  $('#img5').append(html);
</script>

Note: W is a standard Wiener process

The choice of how many shares of S to short is made so that the portfolio does not depend on the random part of S (see below). To see how the value of the portfolio changes over time, we apply Ito’s lemma (note that S is an Ito drift-diffusion process and V is a function of S).

<div class='eqtn' id='img6'></div>
<div class='eqtn' id='img7'></div>
<div class='eqtn' id='img8'></div>

<script type="text/javascript">
  var string1 = 'dP = dV - V_SdS';
  var string2 = '=(V_tdt + V_sdS + 0.5V_{SS}\\sigma ^2S^2dt) - (V_sdS)'
  var string3 = '=V_tdt + 0.5V_SS\\sigma ^2S^2dt'
  var html = $.parseHTML(katex.renderToString(string1));
  var html2 = $.parseHTML(katex.renderToString(string2));
  var html3 = $.parseHTML(katex.renderToString(string3));

  $('#img6').append(html);
  $('#img7').append(html2);
  $('#img8').append(html3);
</script>


Note: This step uses the fact that the differential is a linear operator.

The change in the value of our portfolio, dP, does not depend on dS (and therefore does not depend on dW). It is riskless.

Because the portfolio is riskless, it must earn the same return as if we invested the value of our portfolio at the risk free interest rate (no arbitrage). Equating these returns will bring us to the Black-Scholes PDE.

<div class='eqtn' id='img9'></div>
<div class='eqtn' id='img10'></div>

<script type="text/javascript">
  var string = 'V_tdt + 0.5V_{SS}\\sigma ^2S^2dt = (r(V-V_SS)dt';
  var string2 = '\\to V_tdt + V_SrS + 0.5V_{SS}\\sigma ^2S^2 = rV';
  var html = $.parseHTML(katex.renderToString(string));
  var html2 = $.parseHTML(katex.renderToString(string2));
  $('#img9').append(html);
  $('#img10').append(html2)
</script>


The final line is the Black-Scholes PDE. It is important to note that this result depends on several <a href="http://en.wikipedia.org/wiki/Black%E2%80%93Scholes_model#The_Black-Scholes_world">assumptions</a> which may not always be true. Practitioners seeking to apply the model should take note of these limitations.

###Dynamic Hedging

In theory, the Black-Scholes portfolio uses a stock position to hedge away the risk of purchasing a derivative (and collects the risk free rate of return). For investment purposes, this is not particularly exciting; we can earn the risk free rate (with much less difficulty) by buying treasury bonds.

But the Black-Scholes portfolio will only earn the risk free rate *if the derivative is priced fairly*. By looking at the Black-Scholes PDE, we can see that the price of the derivative depends (in general) on the volatility of the stock. Thus, any observed price implicitly assumes a volatility (this is known as the *implied volatility*). What happens if the implied volatility is different than the volatility we observe going forward?

We apply Ito’s lemma and see that the change in value of the Black-Scholes portfolio is given by:

<div class='eqtn' id='img11'></div>
<script type="text/javascript">
  var string = 'dP =  V_tdt + 0.5\\sigma ^2S^2V_{SS}dt'
  var html = $.parseHTML(katex.renderToString(string));
  $('#img11').append(html);
</script>

Note: In this equation sigma indicates the observed volatility

We revisit the Black-Scholes PDE to get a relation in terms of the implied volatility.

<div class='eqtn' id='img12'></div>
<div class='eqtn' id='img13'></div>

<script type="text/javascript">
  var string = 'V_t + V_SrS +0.5V_{SS}\\sigma _i^2S^2 = rV';
  var string2 = '\\to V_tdt = r(V - V_SS)dt - 0.5V_{SS}\\sigma _i^2S^2dt';
  var html = $.parseHTML(katex.renderToString(string));
  var html2 = $.parseHTML(katex.renderToString(string2));
  $('#img12').append(html);
  $('#img13').append(html2)
</script>

Note: The subscript i indicates reference to the implied volatility

Substituting this result into the equation for the portfolio return, we get:

<div class='eqtn' id='img14'></div>
<script type="text/javascript">
  var string = 'dP = r(V - V_SS)dt + 0.5V_{SS}S^2(\\sigma ^2 - \\sigma _i^2)dt'
  var html = $.parseHTML(katex.renderToString(string));
  $('#img14').append(html);
</script>

Thus, the portfolio earns the risk free rate (the first term) plus a premium for the difference in the observed stock variance and implied stock variance (the second term). *Owning the Black-Scholes portfolio is a bet that the observed volatility of the stock will be greater than the implied volatility of the stock.*

Note what happens if the observed volatility equals the implied volatility (i.e. if the derivative is priced fairly). The second term goes to zero and the portfolio earns the risk free rate. If the observed volatility is less than the implied volatility, the holder of the portfolio earns below the risk free rate.
