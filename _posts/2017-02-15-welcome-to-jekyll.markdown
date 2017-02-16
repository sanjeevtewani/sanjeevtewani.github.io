---
layout: post
title:  "Introduction to learning"
date:   2017-02-15 14:31:55 -0500
categories: [Hilbert spaces]
---
{% include katex_import.html %}

The motivating example for neural nets (with non-linear activation function) is the XOR example:

Consider the problem of generating the XOR function using only matrix multiplications and an activation function.  XOR maps the space of $$[0, 1] \times [0, 1] \leftarrow [0, 1]$$ as such:

<div class="equation" data-expr="
\begin{vmatrix}
0 & 0 \\
0 & 1 \\
1 & 0 \\
1 & 1
\end{vmatrix} \longrightarrow
\begin{vmatrix}
0 \\
1 \\
1 \\
0
\end{vmatrix}
"></div>

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
