# Identification

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Praesent ultrices condimentum elementum. In id placerat eros. Etiam sed arcu sollicitudin, molestie lorem sit amet, ornare massa. Mauris lacus quam, consectetur sed lacinia eu, semper in diam. Fusce vitae metus non neque euismod blandit a vitae ante. Fusce eget tempus velit. Quisque venenatis nec ligula non posuere. Nullam a erat vel felis lobortis pretium non ut felis. Proin commodo porta odio, id faucibus magna ultricies quis.

{% runkit %}
// GeoJSON!
var google = "https://storage.googleapis.com/maps-devrel/google.json"
JSON.parse(await require("request-promise")(google))
{% endrunkit %}