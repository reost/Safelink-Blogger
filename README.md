# Safelink
Safelink blogger with CryptoJS

# How to install
1. upload safelink theme to your blogger
2. create new page, use HTML (not Compose)
3. paste this code
```html
<script src="https://www.blogger.com/feeds/YOUR_SAFELINK_BLOG_ID/posts/default?alt=json-in-script&amp;max-results=150&amp;callback=showurl"></script>

<script>
    //<![CDATA[
    $(document).ready(function() {
            $("#btngenerate").on("click", function() {
                var generateurl = $("#generateurl").val(),
                    generatelink = $("#generatelink"),
                    generateloading = $("#generateloading"),
                    resulturl = $('#resulturl');

                if (generateurl == "") {
                    $("#generateurl").focus();
                    return false;
                }
                $("#copytoclipboard").html("<span class='fa fa-floppy-o'></span> Copy URL");
                generateloading.removeClass('hidden');
                generatelink.addClass('hidden');
                $.ajax({
                    url: '/feeds/posts/summary?alt=json-in-script',
                    type: 'get',
                    dataType: 'jsonp',
                    success: function(data) {
                        var link = '',
                            content = data.feed.entry,
                            links = new Array();
                        if (content !== undefined) {
                            for (var i = 0; i < content.length; i++) {
                                for (var j = 0; j < content[i].link.length; j++) {
                                    if (content[i].link[j].rel == "alternate") {
                                        link = content[i].link[j].href;
                                        break;
                                    }
                                }

                                links[i] = link;
                                var randindex = Math.random() * links.length;
                                randindex = parseInt(randindex);
                            }

                            resultgenerate = links[randindex] + "#?o=" + aesCrypto.encrypt(convertstr(generateurl), convertstr('root'));
                            generateloading.addClass('hidden');
                            generatelink.removeClass('hidden');
                            resulturl.val(resultgenerate);
                        } else {
                            resulturl.val('No result!');
                        }
                    },
                    error: function() {
                        resulturl.val('Error loading feed!');
                    }
                });
            });

            var clipboard = new ClipboardJS('.copytoclipboard');
            clipboard.on('success', function(e) {
                $("#copytoclipboard").html("<span class='fa fa-check'></span> Link Copied to Clipboard");
            });
        })
        //]]>
</script>
<br />
<div class="container" style="margin-top: 5%;">
    <div class="col-md-6">
        <div class="panel panel-primary primary-color-border">
            <div class="panel-heading primary-color">
                <div class="panel-title text-center">
                    <h2>
			<i class="fa fa-shield"></i>
			<strong>Generate</strong>
		    </h2>
                </div>
            </div>
            <div class="panel-body">
                <div class="form-group">
                    <div class="input-group">
                        <span class="input-group-addon">
			    <i class="fa fa-link"></i>
			</span>
                        <input class="form-control" id="generateurl" placeholder="http://example.com" type="url" />
                        <span class="input-group-btn">
			    <button class="btn btn-primary primary-color primary-color-border" id="btngenerate" type="button">
			        <i class="fa fa-shield"></i>
			        <strong>Submit</strong>
			    </button>
			 </span>
                    </div>
                </div>
                <div class="hidden text-center" id="generateloading">
                    <i class="fa fa-spinner fa-spin"></i></div>
                <div class="hidden" id="generatelink">
                    <div class="form-group has-success">
                        <div class="input-group">
                            <span class="input-group-addon">
				<strong>Result:</strong>
				<i aria-hidden="true" class="fa fa-check"></i>
			    </span>
                            <input class="form-control" id="resulturl" onclick="this.focus();this.select()" readonly="readonly" type="text" />
                        </div>
                        <br />
                        <div class="text-center">
                            <button class="copytoclipboard btn-sm btn btn-success" data-clipboard-action="copy" data-clipboard-target="#resulturl" id="copytoclipboard"><span class="fa fa-floppy-o"> Copy URL</span></button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>
```


# Auto Safelink
use include to autosafelink specific urls
```html
<script type='text/javascript'>
var setting = {
	includeurl : "drive.google.com,zippyshare.com",
	path : "#?o="
	};
</script>
<script src='https://rawcdn.githack.com/reost/Safelink-Blogger/cafe1e8574677a79632609f4b2b119b1705dbf20/include.js'></script>
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
<script src='https://rawcdn.githack.com/reost/Safelink-Blogger/cafe1e8574677a79632609f4b2b119b1705dbf20/exclude.js'></script>
<script src='https://www.blogger.com/feeds/YOUR_SAFELINK_BLOG_ID/posts/default?alt=json-in-script&amp;max-results=150&amp;callback=showurl'></script>
```

---

> note : change  **YOUR_SAFELINK_BLOG_ID** with your safelink blog id
