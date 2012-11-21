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

Our tracker is based on Javascript front-end and PHP back-end. The tracker makes sure every pageview on your site is tracked
on our system and then calculated as a visit. This is done by adding a script to your website-footer whick calls the tracker
with relevant data every time a page loads.

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
webpage and don't want the tracker to be called automaticlly set `psDynamicSite = true`

`var peJsHost = (("https:" == document.location.protocol) ? "https://" : "http://");`

This code makes sure you want get any javascript warnings based on our protocol.

`document.write(unescape("%3Cscript src='" + peJsHost + "tr.prospecteye.com/track.js' type='text/javascript'%3E%3C/script%3E"));`

This code adds track.js to your site and enables you to call our API.

Dynamic tracking API
====================

Functions
--------------------
`pe_callTracker(jsonSettings, nAppendType, bShouldAppend)`

`Param: jsonSettings`

Standard: `{}`

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

`Param: nAppendType = kPEAppendScript|kPEAppendFrame`

`kPEAppendScript` - This alternative appends the tracker as a script-call

`kPEAppendFrame` - This alternative appends the tracker as a 1x1-pixel IFrame

`Param: bShouldAppend = true|false`

`true` - The tracker is appended and called automaticlly

`false` - The tracker is returned as a script-object or a iframe-object for you to append by yourself





