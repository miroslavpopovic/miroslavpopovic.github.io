---
layout: post
title: jQuery UI Autocomplete - Filter words starting with term
tags: [jquery, jqueryui, autocomplete]
redirect_from: "/jqueryui-autocomplete-filter-words-starting-with-term/"
---

I had an interested problem with [jQuery UI Autocomplete](http://jqueryui.com/demos/autocomplete/) yesterday. The client required that the search / filtering should be done from the beginning of the word only. By default, jQuery UI Autocomplete filters through the list matching the term in the middle of the word.

There [are](http://stackoverflow.com/questions/2382497/jquery-autocomplete-plug-in-search-configuration) [solutions](http://forum.jquery.com/topic/select-only-items-that-start-with-jquery-ui-autocomplete) with using function as an Autocomplete source. It would be OK if we weren't using [jqAuto](http://stackoverflow.com/questions/7537002/autocomplete-combobox-with-knockout-js-template-jquery) [Knockout](http://knockoutjs.com/) binding by [RP Niemeyer](http://www.knockmeout.net/) which already takes over the Autocomplete source option.

The solution was pretty easy though. After searching thru jQuery UI's source, I found the `filter` method used just for that. All that needs to be done is replacing that function with this:

```javascript
// Overrides the default autocomplete filter function to
// search only from the beginning of the string
$.ui.autocomplete.filter = function (array, term) {
  var matcher = new RegExp("^" + $.ui.autocomplete.escapeRegex(term), "i");
  return $.grep(array, function (value) {
    return matcher.test(value.label || value.value || value);
  });
};
```

This is actually the copy of the default jQuery UI's `filter` method with a single change. Regex is prefixed with "^" sign which matches the beginning of the string.

Please note that this is a global change. It will affect all autocomplete boxes on your page.

Here's a fiddle for that, if you want to play around (just try commenting / uncommenting the `filter` method):

<iframe style="width: 100%; height: 300px" src="http://jsfiddle.net/miroslav/yLdn3/embedded/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>
