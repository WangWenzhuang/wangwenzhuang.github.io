<!DOCTYPE html>
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1" />
		<meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <title>{{ page.title }}</title>
    <meta name="description" content="敏捷实践者，全栈工程师" />
    <link rel="fluid-icon" href="/images/fluidicon.png" />
    <link rel="apple-touch-icon" type="image/png" href="/images/apple-touch-icon.png" />
    <link rel="icon" type="image/x-icon" href="/images/favicon.ico" />
    <link rel="stylesheet" href="https://cdn.bootcss.com/font-awesome/4.7.0/css/font-awesome.min.css" />
    <link href="https://cdn.bootcss.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet"/>
    <link rel="stylesheet" href="/css/monokai.sublime.syntax.css" />
    <link rel="stylesheet" href="/css/blog.css" />
    <script src="https://cdn.bootcss.com/jquery/3.1.1/jquery.min.js"></script>
    <script src="https://cdn.bootcss.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>
    <script>
        var _hmt = _hmt || [];
        (function() {
          var hm = document.createElement("script");
          hm.src = "//hm.baidu.com/hm.js?2647be066b5c11cc8f6a27bd02cb71af";
          var s = document.getElementsByTagName("script")[0]; 
          s.parentNode.insertBefore(hm, s);
        })();
    </script>
  </head>
  <body>
    <div class="menu">
        {% include head.md %}
    </div>
    {{ content }}
    <div class="footer">
      {% include footer.md %}
    </div>
  </body>
</html>
