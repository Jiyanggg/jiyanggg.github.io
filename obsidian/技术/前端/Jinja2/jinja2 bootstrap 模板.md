
```html
<!doctype html>
<html>
    <head>
        {% block css %}
        <!-- Bootstrap core CSS -->
        <link rel="stylesheet" href="{{ url_for('static', filename='css/bootstrap.min.css') }}">
        <!-- Custom styles for this template -->
        <link href="{{ url_for('static', filename='css/offcanvas.css') }}" rel="stylesheet">
        {% endblock %}
    </head>
    <body>




        {% block js %}
        <!-- Placed at the end of the document so the pages load faster -->
        <script src="{{ url_for('static', filename='jquery-3.3.1.min.js') }}"></script>
        <script src="{{ url_for('static', filename='js/bootstrap.min.js') }}"></script>
        {% endblock %}
    </body>
</html>
```


