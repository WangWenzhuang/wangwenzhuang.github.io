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
    <link rel="stylesheet" href="//cdn.bootcss.com/bootstrap/3.3.5/css/bootstrap.min.css">
    <link rel="stylesheet" href="/css/style.css" />
    <link rel="stylesheet" href="/plugins/prism/prism.css" />
    <script type="text/javascript">
        $(function () {
            $(window).scroll(function () {
                var scrolltop = $(this).scrollTop();
                if (scrolltop >= 100) {
                    $("#elevator_item").show();
                } else {
                    $("#elevator_item").hide();
                }
            });
            $("#elevator").click(function () {
                $("html,body").animate({ scrollTop: 0 }, 500);
            });
            $(".qr").hover(function () {
                $(".qr-popup").show();
            }, function () {
                $(".qr-popup").hide();
            });
        });
    </script>
  </head>
  <body>
    <div class="container menu">
      {% include head.md %}
    </div>
    {{ content }}
    <div class="container footer">
      {% include footer.md %}
    </div>
  </body>
</html>
