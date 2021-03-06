---
layout: page
title: "JavaScript array_chunk function"
comments: true
sharing: true
footer: true
alias:
- /functions/view/array_chunk:306
- /functions/view/array_chunk
- /functions/view/306
- /functions/array_chunk:306
- /functions/306
---
<!-- Generated by Rakefile:build -->
A JavaScript equivalent of PHP's array_chunk

{% codeblock array/array_chunk.js lang:js https://raw.github.com/kvz/phpjs/master/functions/array/array_chunk.js raw on github %}
function array_chunk(input, size, preserve_keys) {
  //  discuss at: http://phpjs.org/functions/array_chunk/
  // original by: Carlos R. L. Rodrigues (http://www.jsfromhell.com)
  // improved by: Brett Zamir (http://brett-zamir.me)
  //        note: Important note: Per the ECMAScript specification, objects may not always iterate in a predictable order
  //   example 1: array_chunk(['Kevin', 'van', 'Zonneveld'], 2);
  //   returns 1: [['Kevin', 'van'], ['Zonneveld']]
  //   example 2: array_chunk(['Kevin', 'van', 'Zonneveld'], 2, true);
  //   returns 2: [{0:'Kevin', 1:'van'}, {2: 'Zonneveld'}]
  //   example 3: array_chunk({1:'Kevin', 2:'van', 3:'Zonneveld'}, 2);
  //   returns 3: [['Kevin', 'van'], ['Zonneveld']]
  //   example 4: array_chunk({1:'Kevin', 2:'van', 3:'Zonneveld'}, 2, true);
  //   returns 4: [{1: 'Kevin', 2: 'van'}, {3: 'Zonneveld'}]

  var x, p = '',
    i = 0,
    c = -1,
    l = input.length || 0,
    n = [];

  if (size < 1) {
    return null;
  }

  if (Object.prototype.toString.call(input) === '[object Array]') {
    if (preserve_keys) {
      while (i < l) {
        (x = i % size) ? n[c][i] = input[i] : n[++c] = {}, n[c][i] = input[i];
        i++;
      }
    } else {
      while (i < l) {
        (x = i % size) ? n[c][x] = input[i] : n[++c] = [input[i]];
        i++;
      }
    }
  } else {
    if (preserve_keys) {
      for (p in input) {
        if (input.hasOwnProperty(p)) {
          (x = i % size) ? n[c][p] = input[p] : n[++c] = {}, n[c][p] = input[p];
          i++;
        }
      }
    } else {
      for (p in input) {
        if (input.hasOwnProperty(p)) {
          (x = i % size) ? n[c][x] = input[p] : n[++c] = [input[p]];
          i++;
        }
      }
    }
  }
  return n;
}
{% endcodeblock %}

 - [Raw function on GitHub](https://github.com/kvz/phpjs/blob/master/functions/array/array_chunk.js)

Please note that php.js uses JavaScript objects as substitutes for PHP arrays, they are 
the closest match to this hashtable-like data structure. 

Please also note that php.js offers community built functions and goes by the 
[McDonald's Theory](https://medium.com/what-i-learned-building/9216e1c9da7d). We'll put online 
functions that are far from perfect, in the hopes to spark better contributions. 
Do you have one? Then please just: 

 - [Edit on GitHub](https://github.com/kvz/phpjs/edit/master/functions/array/array_chunk.js)


### Other PHP functions in the array extension
{% render_partial _includes/custom/array.html %}
