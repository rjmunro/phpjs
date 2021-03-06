---
layout: page
title: "JavaScript date_default_timezone_get function"
comments: true
sharing: true
footer: true
sidebar: false
alias:
- /functions/view/date_default_timezone_get:583
- /functions/view/date_default_timezone_get
- /functions/view/583
- /functions/date_default_timezone_get:583
- /functions/583
---
<!-- Generated by Rakefile:build -->
A JavaScript equivalent of PHP's date_default_timezone_get

{% codeblock datetime/date_default_timezone_get.js lang:js https://raw.github.com/kvz/phpjs/master/functions/datetime/date_default_timezone_get.js raw on github %}
function date_default_timezone_get () {
  // http://kevin.vanzonneveld.net
  // +   original by: Brett Zamir (http://brett-zamir.me)
  // -    depends on: timezone_abbreviations_list
  // %        note 1: Uses global: php_js to store the default timezone
  // *     example 1: date_default_timezone_get();
  // *     returns 1: 'unknown'
  var tal = {},
    abbr = '',
    i = 0,
    curr_offset = -(new Date()).getTimezoneOffset() * 60;

  if (this.php_js) {
    if (this.php_js.default_timezone) { // set by date_default_timezone_set
      return this.php_js.default_timezone;
    }
    if (this.php_js.ENV && this.php_js.ENV.TZ) { // getenv
      return this.php_js.ENV.TZ;
    }
    if (this.php_js.ini && this.php_js.ini['date.timezone']) { // e.g., if set by ini_set()
      return this.php_js.ini['date.timezone'].local_value ? this.php_js.ini['date.timezone'].local_value : this.php_js.ini['date.timezone'].global_value;
    }
  }
  // Get from system
  tal = this.timezone_abbreviations_list();
  for (abbr in tal) {
    for (i = 0; i < tal[abbr].length; i++) {
      if (tal[abbr][i].offset === curr_offset) {
        return tal[abbr][i].timezone_id;
      }
    }
  }
  return 'UTC';
}
{% endcodeblock %}

 - [view on github](https://github.com/kvz/phpjs/blob/master/functions/datetime/date_default_timezone_get.js)
 - [edit on github](https://github.com/kvz/phpjs/edit/master/functions/datetime/date_default_timezone_get.js)

### Example 1
This code
{% codeblock lang:js example %}
date_default_timezone_get();
{% endcodeblock %}

Should return
{% codeblock lang:js returns %}
'unknown'
{% endcodeblock %}


### Other PHP functions in the datetime extension
{% render_partial _includes/custom/datetime.html %}
## Legacy comments
These were imported from our old site. Please use disqus below for new comments
<div style="overflow-y: scroll; max-height: 500px;">
{% render_partial functions/date_default_timezone_get/_comments.html %}
</div>
