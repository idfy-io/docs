{% runkit %}

// GeoJSON!

var google = "https://storage.googleapis.com/maps-devrel/google.json";

JSON.parse\(await require\("request-promise"\)\(google\)\);

{% endrunkit %}

