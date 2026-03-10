---
show: true
width: 12
date: 2025-10-01 00:00:00 +0800
group: Visited Places
---
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" integrity="sha256-p4NxAoJBhIIN+hmNHrzRCf9tD/miZyoHS5obTRR9BMY=" crossorigin=""/>
<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js" integrity="sha256-20nQCchB9co0qIjJZRGuk2/Z9VM+kNiyxNV/XN/WLEg=" crossorigin=""></script>

<style>
  #travel-map { height: 450px; border-radius: 12px; z-index: 0; }
  .pulse-marker {
    width: 18px; height: 18px;
    border-radius: 50%;
    background: #e74c3c;
    border: 3px solid #fff;
    box-shadow: 0 0 0 0 rgba(231,76,60,0.6);
    animation: map-pulse 2s infinite;
  }
  @keyframes map-pulse {
    0%   { box-shadow: 0 0 0 0 rgba(231,76,60,0.6); }
    70%  { box-shadow: 0 0 0 12px rgba(231,76,60,0); }
    100% { box-shadow: 0 0 0 0 rgba(231,76,60,0); }
  }
</style>

<div id="travel-map"></div>

<script>
  (function() {
    function initMap() {
      if (typeof L === 'undefined') { setTimeout(initMap, 100); return; }
      var map = L.map('travel-map', { zoomControl: true, scrollWheelZoom: false }).setView([10, 130], 3);
      L.tileLayer('https://{s}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}{r}.png', {
        attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors &copy; <a href="https://carto.com/attributions">CARTO</a>',
        subdomains: 'abcd', maxZoom: 19
      }).addTo(map);

      var places = [
        { name: "New Zealand · 新西兰", lat: -40.9006, lng: 174.8860 },
        { name: "Macao · 澳门",         lat: 22.1987,  lng: 113.5439 },
        { name: "Bali · 巴厘岛",        lat: -8.3405,  lng: 115.0920 },
        { name: "Shengsi Islands · 嵊泗群岛", lat: 30.7263, lng: 122.4444 }
      ];

      var icon = L.divIcon({ className: '', html: '<div class="pulse-marker"></div>', iconSize: [18, 18], iconAnchor: [9, 9] });
      places.forEach(function(p) {
        L.marker([p.lat, p.lng], { icon: icon })
          .addTo(map)
          .bindPopup('<strong>' + p.name + '</strong>');
      });

      setTimeout(function() { map.invalidateSize(); }, 300);
    }
    if (document.readyState === 'loading') {
      document.addEventListener('DOMContentLoaded', initMap);
    } else {
      initMap();
    }
  })();
</script>
