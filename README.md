ProspectEye Tracker API
=======================

This is a documentation for ProspectEye Tracker API and it's functions. This documentation is mostly adressed to web-admins
and its main purpose is to explain how our tracker can be called from your javascript to be able to track dynamic webpages.

What is ProspectEye
--------------------

http://www.prospecteye.com is a webbased BI-system that tracks all visitors on your webpage and presents them as prospects.
ProspectEye delivers each visit with company information such as company name, telephone numbers, descision makers etc.

What is a tracker?
--------------------

The tracker makes sure every pageview on your site is tracked into our system. Our system then automatically calculates X pageviews into a company-visit.
This is done by adding a script to your website-footer which calls the tracker with relevant data every time a page loads.
Our tracker is based on Javascript front-end and PHP/MySQL back-end.

Add the script to your footer
--------------------

```
<script type="text/javascript">
  var psSite = "YOUR_SITE_ID"; var psDynamicSite = true;
  var peJsHost = (("https:" == document.location.protocol) ? "https://" : "http://");
  document.write(unescape("%3Cscript src='" + peJsHost + "tr.prospecteye.com/track.js' type='text/javascript'%3E%3C/script%3E"));
</script>
```

Explaination
--------------------

`var psSite = "YOUR_SITE_CODE"; var psDynamicSite = true;`

Be sure to put the correct Site Code in the variable `psSite` or your pageview won't be tracked correctly. If you have a dynamic
webpage and don't want the tracker to be called automatically set `psDynamicSite = true`

`var peJsHost = (("https:" == document.location.protocol) ? "https://" : "http://");`

This code makes sure you want get any javascript warnings based on our protocol.

`document.write(unescape("%3Cscript src='" + peJsHost + "tr.prospecteye.com/track.js' type='text/javascript'%3E%3C/script%3E"));`

This code adds track.js to your site and enables you to call our API.

Async implementation
--------------------

```
<script type="text/javascript">
    var psSite = "YOUR_SITE_CODE"; var psDynamicSite = true;
    (function() {
        var pe = document.createElement('script'); pe.type = 'text/javascript'; pe.async = true;
    	pe.src = ('https:' == document.location.protocol ? 'https://' : 'http://') + "tr.prospecteye.com/track.js";
        var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(pe, s)
    })();
</script>
```

Dynamic tracking API
====================

Functions
--------------------
`ProspectEye.callTracker(jsonSettings, nAppendType, bShouldAppend)`

`Param: jsonSettings = {}`

Optionals:

```
{
  'url': 'Page Url',        //example http://www.prospecteye.com/index.php
  'pagename': 'Page Title', //example ProspectEye Mainpage
  'referer': 'Referer Url', //example http://www.google.se/q=prospecteye%20ab
  'cookie': true|false,     //example Should the tracker set a cookie or not
  'pedata': {
    'type': 'F',
    'email': 'info@prospecteye.com',
    'form_name': 'Newsletter'
  }
}
```

`Param: nAppendType = ProspectEye.kPEAppendScript|ProspectEye.kPEAppendFrame`

`ProspectEye.kPEAppendScript` - This alternative appends the tracker as a script-call

`ProspectEye.kPEAppendFrame` - This alternative appends the tracker as a 1x1-pixel IFrame

`Param: bShouldAppend = true|false`

`true` - The tracker is appended and called automatically

`false` - The tracker is returned as a script-object or a iframe-object for you to append by yourself

PEData
--------------------
PEData is optional and can be sent with the tracker-call. PEData is user-based information that is picked up from
forms on your website.

Types:

 - 'F' Forms

Example 1: You have a form that lets user subscribe to a newsletter. In order to send along this information to the
tracker you extend the `jsonSettings` with the value `pedata`

```
{
  url: 'Page Url',
  ...
  pedata: {
    type: 'F',
    email: 'info@prospecteye.com',
    form_name: 'Newsletter'
  }
}
```

`type` and `form_name` is standard fields. Between those you can put almost any key-pair of string-data. In this example
we add the data `email: 'info@prospecteye.com'

Example 2: You have a login on you webpage and wants to send along this information to be able to exclude login-customers

```
{
  url: 'Page Url',
  ...
  pedata: {
    type: 'F',
    username: 'info@prospecteye.com',
    form_name: 'Login'
  }
}
```

API Call Examples
--------------------

Standard:

`ProspectEye.callTracker({}, ProspectEye.kPEAppendScript, true);`

Custom:

```
ProspectEye.callTracker({
  'url': 'http://www.prospecteye.com/index.php',
  'pagename': 'ProspectEye Mainpage'
}, ProspectEye.kPEAppendScript, true);
```

Custom (with formdata):

```
ProspectEye.callTracker({
  'url': 'http://www.prospecteye.com/index.php',
  'pagename': 'ProspectEye Mainpage',
  'pedata': {
    'type': 'F',
    'email': 'info@prospecteye.com',
    'form_name': 'Newsletter'
  }
}, ProspectEye.kPEAppendScript, true);
```

Custom (Append by yourself):

```
var tracker = ProspectEye.callTracker({
  'url': 'http://www.prospecteye.com/index.php',
  'pagename': 'ProspectEye Mainpage',
  'pedata': {
    'type': 'F',
    'email': 'info@prospecteye.com',
    'form_name': 'Newsletter'
  }
}, ProspectEye.kPEAppendScript, false);

document.getElementsByTagName("head")[0].appendChild(tracker);
```



