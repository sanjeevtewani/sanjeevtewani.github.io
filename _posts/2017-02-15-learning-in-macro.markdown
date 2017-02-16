---
layout: post
title:  "Learning in Macro"
date:   2017-02-15 14:31:55 -0500
categories: [Interest Rates]
---
{% include katex_import.html %}

I've been working through a fantastic [Deep Learning](https://mitpress.mit.edu/books/deep-learning) book since January, and I came across an interesting little topic that caught my attention.  Briefly mentioned in Chapter 13 is the topic of Independent Component Analysis, which concerns itself with the problems like the 'cocktail party problem'.  In particular, the problem is how a machine could separate out $$n$$ voices speaking simultaneously, using only $$n$$ different microphones placed around the room.  Microphone $$i$$ observes a (time-indexed) signal $$x_{i,t}$$ and attempts to recover latent signals (voices), which are denoted $$s_{i,t}$$ and mixed according to a matrix $$A$$.

If you paid attention to interest rates in 2016 -- or if you happen to read a lot of Goldman research -- you may have come across a picture that looks like this:

![My helpful? screenshot]({{site.url}}/public/Goldman Rigobon 2003.png){:height="360px" width="360px"}

Even though the cocktail party problem may seem a bit contrived ($$n$$ microphones?), this is precisely the problem one sees when they're observing interest rates, where there are $$n$$ observable 10y rates and $$n$$ latent variables driving global rates.  A practitioner may augment their information using particular interest rate flies or curves, and therefore try to infer the direction of the latent variables via some derivative of the rates curve, but just knowing the direction of the latent variable it can be difficult to bring information about curves and flies together to a coherent picture like the one above.

Therefore, it's interesting to know what Rigobon does to solve this problem, and how his solution relates to the cocktail party problem.  One primary feature of ICA is that the latent variables cannot be normal Gaussians.  If they were, then a simple linear combination of variables will also be Gaussian and the variances $$\sigma_{as_i+bs_j}^2 = a^2\sigma_{s_i}^2 + b^2\sigma_{s_j}^2$$ will contain no information about the direction of the mixing parameters $$a, b$$.

As with many things in empirical finance, Rigobon wants Gaussianity but also wants to identify the parameters.  His solution is to consider bond yield innovations (residuals from a regression including lags) across two different states, where the variances of the latent variables are different in each state.  Doing so, he finds:

$$
v_{1,t} = \frac{1}{1-\alpha\beta}[\beta\eta_t + \epsilon_t]
$$


$$
v_{2,t} = \frac{1}{1-\alpha\beta}[\eta_t + \alpha\epsilon_t]
$$



Which is the reduced form of $$ v_{1,t} = \beta v_{2,t} + \epsilon_t $$ and $$ v_{2,t} = \alpha v_{1,t} + \eta_t $$.  Rejecting the typical solutions (assume one of $$\alpha$$ or $$\beta$$ is $$0$$ so one latent variable is directly observable, or $$\sigma_\epsilon/\sigma_\eta$$ is a constant) which are very likely violated in the Japan-US example, identification is instead achieved by considering the variance matrix across two different states (say, a tranquil period and volatile period).  Then the covariance matrix has the following form over the states $$s \in (1, 2)$$

<div class="equation" data-expr="
\Omega_s = \begin{vmatrix} \omega_{1,1,s} & \omega_{1,2,s} \\
\omega_{2,1,s} & \omega_{2,2,s} \end{vmatrix}
 = \frac{1}{(1-\alpha\beta)^2}
\begin{vmatrix} \beta\sigma_{\eta,s}^2 + \sigma_{\epsilon,s}^2 & \beta\sigma_{\eta,s}^2 + \alpha\sigma_{\epsilon,s}^2 \\
 & \sigma_{\eta,s}^2 + \alpha\sigma_{\epsilon,s}^2 \end{vmatrix}
"></div>

Yielding six equations (three each per state), six unknowns (two mixing parameters and four variances), and no additional constraints!  Rigobon goes on to discuss various conditions under which identification can fail (such as if only one variance changes across states), but for the case of Japanese and US yields these conditions are unlikely to appear.  The result is a nice way to identify the latent drivers of these yield curves and ultimately, for practitioners, a way to frame early 2016's decline in yields (and its subsequent reversal).

<script type="text/javascript">
    // grab all elements in DOM with the class 'equation'
    var tex = document.getElementsByClassName("equation");

    // for each element, render the expression attribute
    Array.prototype.forEach.call(tex, function(el) {
        katex.render(el.getAttribute("data-expr"), el);
    });

    $("script[type='math/tex']").replaceWith(
      function(){
        var tex = $(this).text();
        return "<span class=\"inline-equation\">" +
               katex.renderToString(tex) +
               "</span>";
    });

    $("script[type='math/tex; mode=display']").replaceWith(
      function(){
        var tex = $(this).text();
        return "<div class=\"equation\">" +
               katex.renderToString("\\displaystyle "+tex) +
               "</div>";
    });

</script>
