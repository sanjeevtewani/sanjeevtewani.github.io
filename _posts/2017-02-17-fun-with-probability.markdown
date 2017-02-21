---
layout: post
title:  "Fun with Probability"
date:   2017-02-17 12:00:00 -0500
categories: [Puzzles]
---
{% include katex_import.html %}

Here are two fun puzzles to entertain oneself with over the long weekend: one a bit more elementary, and one that I think was a Putnam problem sometime in the 80s.

1. Clearly, $$3$$ random variables could all have correlation $$1$$, but they couldn't all have correlation $$-1$$.  By the same logic, if $$n$$ random variables all have the same cross-correlations $$(\rho_{i,j}=\rho)$$ for $$i \ne j$$, then there must be some lower bound on $$\rho$$ to ensure that the variables have a valid correlation matrix.  What bound lower bound can we place on $$? \le \rho \le 1$$ for $$n$$ assets?


2. Choose $$x,y \sim unif[0,1]$$ and independent.  What is the probability that the integer closest to $$x/y$$ is even?

#1 above requires some definition of what constitutes a valid correlation matrix.  It turns out that the matrix needs to be positive semi-definite (remember that covariance matrices must be positive semi-definite, and a covariance matrix $$\Sigma=\sigma^{-1} R \sigma^{-1}$$ where $$\sigma = diag(\sigma_1,..,\sigma_n)$$ are the volatilities for each variable).  So we really just need to find bounds on $$\rho$$ such that $$R^n_\rho$$, the $$n \times n$$ matrix with $$1s$$ on the diagonal and $$\rho$$ else where, is positive semi-definite.  For example,

<div class="equation" data-expr="
R^4_\rho = \begin{vmatrix} 1 & \rho & \rho & \rho \\
\rho & 1 & \rho & \rho \\
\rho & \rho & 1 & \rho \\
\rho & \rho & \rho & 1 \end{vmatrix}.
"></div>

To be positive semi-definite, we need to demonstate that all of the eigenvalues are at least zero.  It turns out that, in this case, it's very easy to guess the eigenvectors/values:

Firstly, all of the columns have the same sum of $$1 + (n - 1)\rho$$.  And since multiplying a matrix by $$\bold{1}_n$$ sums the columns, we see that $$R^n_{\rho} \bold{1}_n = (1 + (n-1)\rho) \bold{1}_n$$, so $$1 + (n-1)\rho$$ is an eigenvalue.

Now, we still want to guess the other eigenvalues.  These are a little bit trickier, but it turns out that $$\lambda^n_j = (-1, 0, .. , 1, 0, .. 0)$$, which is $$-1$$ for the first index, $$1$$ for the $$j$$th index, and $$0$$ elsewhere, is a good choice.  For column $$1$$ this vector picks out $$-(1-\rho)$$, for column $$j$$ it picks out $$1-\rho$$, and elsewhere it picks out $$0$$, so $$R^n_\rho \lambda^n_j = (1-\rho) \lambda^n_j$$.  

Our final system of equations then is $$n-1$$ equations where $$1-\rho \ge 0 \Rightarrow \rho \le 1$$, (which isn't much of a surprise given that it's a correlation coefficient), and $$1 + (n-1)\rho \ge 0 \rightarrow \rho \ge - \frac{1}{n-1}$$.  For three variables, then $$\rho > -\frac{1}{2}$$ will be enough to ensure a correlation matrix!

#2 is a bit more involved (and the problem as it was stated gave a big hint which I left out), but the answer is coming!

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
