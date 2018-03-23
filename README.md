Skip to content
This repository
Search
Pull requests
Issues
Marketplace
Explore
 @PowerPudu
Sign out
0
0 0 PowerPudu/Clase-23-de-Marzo
 Code  Issues 0  Pull requests 0  Projects 0  Wiki  Insights  Settings
Clase-23-de-Marzo/index.html
9f1be9f  7 minutes ago
@PowerPudu PowerPudu Add files via upload
     
81 lines (76 sloc)  4.66 KB
<!doctype html>
<html>
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css" integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm" crossorigin="anonymous">
<title>Seminario Gráfica Computacional I 2018, Primer Semestre → Clase 1 → Viernes 16 de marzo</title>
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.3.1/dist/leaflet.css"
  integrity="sha512-Rksm5RenBEKSKFjgI3a41vrjkw4EVPlJ3+OiI65vTjIdo9brlAacEuKOiQ5OFh7cOI1bkDwLqdLw3Zg0cRJAAQ=="
  crossorigin=""/>
<script src="https://unpkg.com/leaflet@1.3.1/dist/leaflet.js"
  integrity="sha512-/Nsx9X4HebavoBvEBuyp3I7od5tA0UzAxs+j83KgC8PU0kgB4XiK4Lfe4y4cgBtaRJQEIFCW+oC506aPT2L1zw=="
  crossorigin=""></script>
<link href="https://fonts.googleapis.com/css?family=Bungee+Outline" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css?family=Quicksand:400,700" rel="stylesheet">
<link href="style.css" rel="stylesheet">
</head>
<body>
<div class="container">
	<div class="row">
		<div class="col-sm-12 py-5">
			<h1>Tembló</h1>
			<h3>En alguna parte del mundo</h3>
			<p>Usaré espanglish:</p>
			<p>El <a href="https://earthquake.usgs.gov/">Earthquake Hazards Program</a> del <a href="https://www.usgs.gov/">USGS</a>, tiene un servicio de <a href="https://earthquake.usgs.gov/earthquakes/feed/v1.0/geojson.php">GeoJSON Summary Format</a>, donde pueder is a buscar data sobre los movimientos telúricos alrededor del mundo.</p>
            <p>Mediante consulta a los <a href="https://earthquake.usgs.gov/earthquakes/feed/v1.0/geojson.php">M4.5 Earthquakes del Past Day</a>, podemos enterarnos que el último registro corresponde a un movimiento de M<span id="magnitud"></span> ocurrido a las <span id="hora"></span>GMT en <span id="lugar"></span>, con epicentro en las coordenadas <span id="coords"></span>
		<p></p>
			<div id="mapid"></div>
            
			<p>Si quieren ver la hora a la que ocurrió este movimiento telúrico, métanse a la consola de Javascript del Navegador, allí hay un número raro. Ese número es un Unix Timestamp, que pueden traducir en <a href="https://www.unixtimestamp.com/" target="_blank">https://www.unixtimestamp.com/</a></p>
		</div>
		<div class="col-sm-6 pb-5">
			<p>Antes de continuar, necesito que cada uno de ustedes genere una cuenta en <a href="https://home.openweathermap.org/users/sign_up" target="_blank">OpenWeatherMap</a>. Vamos a usar la <a href="https://openweathermap.org/api">WeatherAPI</a>, y para ello, es mejor que cada cual cuente con su <a href="http://openweathermap.org/appid">APIKey</a>.</p>
		</div>
		<div class="col-sm-6 pb-5">
			<p>¿De qué está hablando?¿Qué es una API? No es nada complicado. De hecho, se trata de algo creado para facilitar la programación, en rigor es una <a href="https://es.wikipedia.org/wiki/Interfaz_de_programaci%C3%B3n_de_aplicaciones" title="Wikipedia">Interfaz de programación de aplicaciones.</a></p>
		</div>
		<div class="col-sm-12" style="border-top:1px solid #eee;">
			<div class="row pt-3 pb-4 small">
				
				<div class="col-sm-3 text-right">
					<p><a href="Londres.html">Continuar</a></p>
				</div>
			</div>		
		</div>
	</div>
</div>
<script>
var request = new XMLHttpRequest();
request.open('GET', 'https://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/4.5_day.geojson', true);
request.onload = function () {
	var data = JSON.parse(this.response);
	var lat = data.features[0].geometry.coordinates[1];
	var lon = data.features[0].geometry.coordinates[0];
	var where = data.features[0].properties.place;
	var when = new Date(data.features[0].properties.time);
    var whenUTC = when.toUTCString();
	var magnitud = data.features[0].properties.mag
    
    document.getElementById("magnitud").innerHTML = magnitud;
      document.getElementById("lugar").innerHTML = where.split(",")[1];
    document.getElementById("hora").innerHTML = whenUTC.split(" ")[4];
      document.getElementById("coords").innerHTML = "("+ lat + ", " + lon+")";
	console.log(data);
	console.log(when);
	//mapa
	var mymap = L.map('mapid').setView([lat, lon], 2);
	L.tileLayer('https://api.tiles.mapbox.com/v4/{id}/{z}/{x}/{y}.png?access_token=pk.eyJ1IjoibWFwYm94IiwiYSI6ImNpejY4NXVycTA2emYycXBndHRqcmZ3N3gifQ.rJcFIG214AriISLbB6B5aw', {
		maxZoom: 18,
		attribution: 'Map data &copy; <a href="http://openstreetmap.org">OpenStreetMap</a> contributors, ' + 'Imagery © <a href="http://mapbox.com">Mapbox</a>',
		id: 'mapbox.streets'
	}).addTo(mymap);
	L.marker([lat, lon]).addTo(mymap)
	.bindPopup("<h5>"+ magnitud + "</h5><p>" + lat + "," + lon + "<p>").openPopup();
}
request.send();
</script>
</body>
</html>

© 2018 GitHub, Inc.
Terms
Privacy
Security
Status
Help
Contact GitHub
API
Training
Shop
Blog
About
Press h to open a hovercard with more details.
