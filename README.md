# safelink
the file I need to make safelink


# Auto Safelink
use include to autosafelink specific urls
```html
<script type='text/javascript'>
var setting = {
	includeurl : "drive.google.com,zippyshare.com",
	path : "#?o="
	};
</script>
<script src='https://rawcdn.githack.com/reost/safelink/e9156d98b1dc5afff78426446a3fab5836f7aabb/include.js'></script>
<script src='https://www.blogger.com/feeds/YOUR_SAFELINK_BLOG_ID/posts/default?alt=json-in-script&amp;max-results=150&amp;callback=showurl'></script>
```

use exclude to protect specific urls from autosafelink
```html
<script type='text/javascript'>
var setting = {
	excludeurl : "yoursite.com,facebook.com",
	path : "#?o="
	};
</script>
<script src='https://rawcdn.githack.com/reost/safelink/e9156d98b1dc5afff78426446a3fab5836f7aabb/exclude.js'></script>
<script src='https://www.blogger.com/feeds/YOUR_SAFELINK_BLOG_ID/posts/default?alt=json-in-script&amp;max-results=150&amp;callback=showurl'></script>
```
