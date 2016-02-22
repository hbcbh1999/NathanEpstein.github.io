---
layout: post
author: Nathan Epstein
title:  "Term Structure Equation"
categories: jekyll update, content
tweet: "Understanding the Term Structure Equation"
---

There are many <a href="http://en.wikipedia.org/wiki/Short-rate_model#Particular_short-rate_models">stochastic models</a> which are used to describe the future evolution of the short rate (instantaneous spot rate). Given such a model, we may find it useful to develop an equation which relates the short rate to the yield curve.

Letting the bond price, P, be a function of the short rate, r, we have the following initial conditions.

<div class='eqtn' id='img1'></div>
<div class='eqtn' id='img2'></div>
<div class='eqtn' id='img3'></div>
<div class='eqtn' id='img4'></div>

<script type="text/javascript">
  var string = 'dr = a(t,r)dt + b(t,r)dW';
  var string2 = 'dP = (P_t + aP_r + 0.5b^2P_{rr})dt + bP_rdW';
  var string3 = '\\to dP/P = \\mu dt +\\sigma dW';
  var string4 = '\\ \\mu = P^{-1}(P_t + aP_r + 0.5b^2P_{rr}),\\ \\sigma = P^{-1}(bP_r)'
  var html = $.parseHTML(katex.renderToString(string));
  var html2 = $.parseHTML(katex.renderToString(string2));
  var html3 = $.parseHTML(katex.renderToString(string3));
  var html4 = $.parseHTML(katex.renderToString(string4));
  $('#img1').append(html);
  $('#img2').append(html2);
  $('#img3').append(html3);
  $('#img4').append(html4).prepend('where');

</script>


Note: dP is given by Ito’s lemma and dP/P is the percentage change in the bond price.

We construct a bond portfolio, of value V(t), by going long a bond of maturity T2 and short a bond of maturity T1 (T1 < T2), in amounts V2(t) and V1(t) respectively. Note that this implies V = V2 - V1. The change in the portfolio’s value is given by the following.

<div class='eqtn' id='img5'></div>
<div class='eqtn' id='img6'></div>

<script type="text/javascript">
  var string = 'dV = V_2(dP_2/P_2) - V_1(dP_1/P_1)';
  var string2 = '= (V_2\\mu _2 - V_1\\mu _1)dt + (V_2\\sigma _2 - V_1\\sigma _1)dW';
  var html = $.parseHTML(katex.renderToString(string));
  var html2 = $.parseHTML(katex.renderToString(string2));
  $('#img5').append(html);
  $('#img6').append(html2);
</script>


We can make this portfolio risk free by choosing V1 and V2 such that dV does not depend on dW (by setting the coefficient of dW equal to 0).

<div class='eqtn' id='img7'></div>
<div class='eqtn' id='img8'></div>

<script type="text/javascript">
  var string = 'V_2\\sigma _2 - V_1 \\sigma _1 = 0';
  var string2 = '\\to V_2 = (V_1\\sigma _1/\\sigma _2)';
  var html = $.parseHTML(katex.renderToString(string));
  var html2 = $.parseHTML(katex.renderToString(string2));
  $('#img7').append(html);
  $('#img8').append(html2);
</script>


Note: This is the risk-neutral condition on the portfolio.

Such a portfolio will earn the risk-free rate by the assumption of no arbitrage.

<div class='eqtn' id='img9'></div>
<div class='eqtn' id='img10'></div>
<div class='eqtn' id='img11'></div>

<script type="text/javascript">
  var string = 'dV = (V_2\\mu _2 - V_1\\mu _1)dt = rVdt';
  var string2 = '\\to (V_1\\sigma _1/\\sigma _2)(\\mu _2 - r)= V_1(\\mu _1 - r)';
  var string3 = '\\to (\\mu _2 - r)/(\\sigma _2) = (\\mu _1 - r)/(\\sigma _1) = \\gamma (t,r)';

  var html = $.parseHTML(katex.renderToString(string));
  var html2 = $.parseHTML(katex.renderToString(string2));
  var html3 = $.parseHTML(katex.renderToString(string3));

  $('#img9').append(html);
  $('#img10').append(html2).append(' by the risk-neutral condition.');
  $('#img11').append(html3);

</script>

The bond maturities, T1 and T2, were chosen arbitrarily which implies that gamma does not depend on maturity; it only depends on t and r. Thus, the equation for gamma (frequently referred to as the market price of risk associated with bonds) can be expressed independently of a maturity.

<div class='eqtn' id='img12'></div>

<script type="text/javascript">
  var string = '\\gamma = (\\mu - r)/\\sigma';
  var html = $.parseHTML(katex.renderToString(string));
  $('#img12').append(html);
</script>

Rearranging this equation and substituting our original values for mu and sigma will bring us to a PDE which relates the short rate and yield curve (the term structure equation).

<div class='eqtn' id='img13'></div>
<div class='eqtn' id='img14'></div>
<div class='eqtn' id='img15'></div>

<script type="text/javascript">
  var string = '\\mu - r = \\sigma \\gamma';
  var string2 = '\\to P\\mu - Pr = P\\sigma \\gamma';
  var string3 = '\\to P_t + (a - \\gamma b)P_r + 0.5b^2P_{rr} - rP = 0';

  var html = $.parseHTML(katex.renderToString(string));
  var html2 = $.parseHTML(katex.renderToString(string2));
  var html3 = $.parseHTML(katex.renderToString(string3));

  $('#img13').append(html);
  $('#img14').append(html2);
  $('#img15').append(html3);

</script>


Note: The boundary condition of the PDE is P(t,T,r) = 1
