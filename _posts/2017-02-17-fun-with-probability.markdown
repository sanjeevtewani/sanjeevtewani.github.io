---
layout: post
title:  "Fun with Probability"
date:   2017-02-17 12:00:00 -0500
categories: [Puzzles]
---
{% include katex_import.html %}

Here are two fun puzzles to entertain oneself with over the long weekend: one a bit more elementary, and one that I think was a Putnam problem sometime in the 80s.

1. Clearly, $$n$$ random variables could all have correlation 1, but they couldn't have correlation 1.  That is, if $$n$$ random variables all have the same correlations $$(\rho_{i,j}=\rho)$$ for $$i \ne j$$, then what lower bound can we place on $$? \le \rho \le 1$$?


2. Choose $$x,y \sim unif[0,1]$$ and independent.  What is the probability that the integer closest to $$x/y$$ is even?


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
