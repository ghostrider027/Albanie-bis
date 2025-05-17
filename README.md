# Albanie-bis
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>Carte Albanie - Itinéraire et Restaurants</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css"
          integrity="sha256-sA+4JDr7fXFmWbrdUc1tQVD8gR8O9F7VtrmYJtA1pH0=" crossorigin=""/>
    <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"
            integrity="sha256-pM0I+3QxEln9vQiyuOr6Kp7q0VfPTHvL9xnu5MYnL6A=" crossorigin=""></script>
    <script src="https://kit.fontawesome.com/a076d05399.js" crossorigin="anonymous"></script>
    <style>
        html, body, #map { height: 100%; margin: 0; }
    </style>
</head>
<body>
<div id="map"></div>
<script>
    const map = L.map('map').setView([41.3275, 19.8189], 7);

    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        maxZoom: 18,
    }).addTo(map);

    const steps = [
        { name: "📍 Tirana", lat: 41.3275, lon: 19.8189, info: "Capitale vibrante de l’Albanie. Place Skanderbeg, Bunk’Art, téléphérique de Dajti." },
        { name: "📍 Theth", lat: 42.3958, lon: 19.7744, info: "Village alpin. Cascade de Grunas, Blue Eye." },
        { name: "📍 Valbona", lat: 42.4700, lon: 19.8800, info: "Randonnée en vallée spectaculaire. Étape Theth–Valbona." },
        { name: "📍 Shkodra", lat: 42.0683, lon: 19.5126, info: "Château de Rozafa, lac de Shkodra." },
        { name: "📍 Berat", lat: 40.7058, lon: 19.9522, info: "Ville UNESCO. Château, musées, vieille ville." },
        { name: "📍 Himarë", lat: 40.1017, lon: 19.7447, info: "Plages : Spile, Livadhi, Jale." },
        { name: "📍 Gjipe", lat: 40.1426, lon: 19.7441, info: "Crique sauvage entre falaises." },
        { name: "📍 Ksamil", lat: 39.7683, lon: 20.0019, info: "Plages paradisiaques avec îlots." },
        { name: "📍 Butrint", lat: 39.7458, lon: 20.0208, info: "Site archéologique gréco-romain." },
        { name: "📍 Gjirokastër", lat: 40.0758, lon: 20.1389, info: "Ville UNESCO en pierre." },
    ];

    const restaurants = [
        { name: "🍽️ Mullixhiu - Tirana", lat: 41.3225, lon: 19.8212, info: 'Cuisine traditionnelle raffinée. <a href="https://www.mullixhiu.al/" target="_blank">Site officiel</a>' },
        { name: "🍽️ Mrizi i Zanave - Fishtë", lat: 41.8783, lon: 19.7200, info: 'Slow food local. <a href="https://mrizizanave.al/" target="_blank">Site officiel</a>' },
        { name: "🍽️ Taverna Tradicionale - Berat", lat: 40.7065, lon: 19.9485, info: 'Cuisine albanaise authentique.' },
        { name: "🍽️ Taverna Vasili - Ksamil", lat: 39.7710, lon: 20.0002, info: 'Fruits de mer et plats traditionnels.' },
    ];

    const linePoints = [];

    steps.forEach(step => {
        L.marker([step.lat, step.lon], {
            icon: L.icon({
                iconUrl: "https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/images/marker-icon.png",
                iconSize: [25, 41], iconAnchor: [12, 41], popupAnchor: [1, -34],
                shadowUrl: "https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/images/marker-shadow.png",
                shadowSize: [41, 41]
            })
        }).addTo(map).bindPopup(`<b>${step.name}</b><br>${step.info}`);
        linePoints.push([step.lat, step.lon]);
    });

    restaurants.forEach(resto => {
        L.marker([resto.lat, resto.lon], {
            icon: L.divIcon({
                html: `<i class="fas fa-utensils" style="color: green; font-size: 20px;"></i>`,
                iconSize: [20, 20],
                className: 'my-div-icon'
            })
        }).addTo(map).bindPopup(`<b>${resto.name}</b><br>${resto.info}`);
    });

    // Trace l'itinéraire entre les étapes
    L.polyline(linePoints, { color: 'red', weight: 3, opacity: 0.7 }).addTo(map);
</script>
</body>
</html>
