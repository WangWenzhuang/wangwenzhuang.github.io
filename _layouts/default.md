<!DOCTYPE html>
<html>
  <head>
    <meta http-equiv="content-type" content="text/html; charset=utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>{{ page.title }}</title>
    <link rel="fluid-icon" href="/fluidicon.png" />
    <link rel="apple-touch-icon" sizes="57x57" href="/images/apple-touch-icon-114.png" />
    <link rel="apple-touch-icon" sizes="114x114" href="/images/apple-touch-icon-114.png" />
    <link rel="apple-touch-icon" sizes="72x72" href="/images/apple-touch-icon-144.png" />
    <link rel="apple-touch-icon" sizes="144x144" href="/images/apple-touch-icon-144.png" />
    <link rel="icon" type="image/x-icon" href="/images/favicon.ico" />
    <link rel="stylesheet" href="/plugins/font-awesome-4.7.0/css/font-awesome.min.css" />
    <link rel="stylesheet" href="/plugins/bootstrap-3.3.7/css/bootstrap.min.css">
    <link rel="stylesheet" href="/plugins/prism/prism.css" />
    <link rel="stylesheet" href="/css/style.css" />
    <script src="/plugins/jquery-3.1.1.min.js"></script>
    <script src="/plugins/bootstrap-3.3.7/js/bootstrap.min.js"></script>
    <script src="/plugins/prism/prism.js"></script>
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
