# raftar-bihar
Raftar Bihar: Bihar's first hyper-local bike taxi service website. Features interactive Leaflet.js maps for narrow lane navigation and local language support
<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Raftar Bihar - Bihar ki Apni Sawari</title>
    
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
    
    <style>
        :root {
            --primary: #ff8c00; 
            --secondary: #1a237e; 
            --light: #f9f9f9;
            --white: #ffffff;
        }

        body { font-family: 'Segoe UI', Arial, sans-serif; margin: 0; padding: 0; scroll-behavior: smooth; background-color: var(--white); }

        /* Navigation Bar */
        header {
            background: var(--white);
            padding: 10px 5%;
            display: flex;
            justify-content: space-between;
            align-items: center;
            position: sticky;
            top: 0;
            z-index: 1000;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }

        .logo-box { display: flex; align-items: center; text-decoration: none; }
        
        /* Header Logo Size */
        .header-logo {
            height: 60px; 
            width: auto;
        }

        nav a { color: var(--secondary); text-decoration: none; margin-left: 20px; font-weight: 700; text-transform: uppercase; font-size: 0.9rem; }

        .btn-app {
            background: var(--primary);
            color: white !important;
            padding: 10px 20px;
            border-radius: 50px;
            box-shadow: 0 4px 15px rgba(255, 140, 0, 0.3);
        }

        /* Hero Section */
        .hero {
            background: linear-gradient(rgba(26, 35, 126, 0.85), rgba(26, 35, 126, 0.85)), url('https://images.unsplash.com/photo-1449495169669-7b118f960237?auto=format&fit=crop&w=1350&q=80');
            background-size: cover;
            background-position: center;
            height: 65vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            color: white;
            padding: 0 20px;
        }

        /* Big Logo in Hero */
        .hero-logo {
            height: 180px; 
            margin-bottom: 20px;
            filter: drop-shadow(0 5px 15px rgba(0,0,0,0.3));
        }

        .hero h1 { font-size: 2.8rem; margin: 0; font-weight: 800; }
        .hero p { font-size: 1.2rem; opacity: 0.9; margin-top: 10px; }

        /* Map styling */
        .map-container { padding: 50px 5%; text-align: center; }
        #map { height: 450px; width: 100%; border-radius: 20px; border: 5px solid var(--secondary); margin-top: 25px; box-shadow: 0 15px 35px rgba(0,0,0,0.1); }

        .btn-confirm {
            background: var(--primary);
            color: white;
            padding: 15px 40px;
            border: none;
            border-radius: 50px;
            font-size: 1.1rem;
            cursor: pointer;
            font-weight: bold;
            margin-top: 20px;
            transition: 0.3s;
        }

        footer { background: #111; color: white; text-align: center; padding: 25px; border-top: 4px solid var(--primary); }
    </style>
</head>
<body>

    <header>
        <a href="#" class="logo-box">
            <img src="5.png" alt="Raftar Bihar" class="header-logo">
        </a>
        <nav>
            <a href="#map-section">Map</a>
            <a href="#" class="btn-app">Download App</a>
        </nav>
    </header>

    <section class="hero">
        <img src="5.png" alt="Raftar Bihar Identity" class="hero-logo">
        <h1>Bihar ka Apna <span style="color:var(--primary)">Raftar</span></h1>
        <p>Gali-Gali, Dagar-Dagar... Surakshit aur Sasta Safar.</p>
    </section>

    <section id="map-section" class="map-container">
        <h2 style="color: var(--secondary); font-size: 2rem;">Kahan Se Pick-up Karein?</h2>
        <p>Map par click karke apna point set karein (Chhoti galiyan bhi map par hain!)</p>
        
        <div id="map"></div>
        
        <div style="background: var(--light); padding: 20px; border-radius: 15px; display: inline-block; margin-top: 20px; border-left: 5px solid var(--primary);">
            <span id="coords" style="font-weight: bold; color: var(--secondary);">Location select karein...</span>
        </div>
        <br>
        <button class="btn-confirm" onclick="confirmRide()">Sawaari Book Karein</button>
    </section>

    <footer>
        <p>&copy; 2026 Raftar Bihar | Bihar ki Pragati ki Nai Pehchan</p>
    </footer>

    <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
    <script>
        // Default center at Patna Junction
        var map = L.map('map').setView([25.6022, 85.1360], 15);
        
        L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
            attribution: '© Raftar Bihar Maps'
        }).addTo(map);

        var marker;
        map.on('click', function(e) {
            if (marker) { map.removeLayer(marker); }
            marker = L.marker([e.latlng.lat, e.latlng.lng]).addTo(map)
                .bindPopup("<b>Raftar Bihar</b> yahan se aapko legi!").openPopup();
            document.getElementById('coords').innerHTML = "Set Location: " + e.latlng.lat.toFixed(5) + ", " + e.latlng.lng.toFixed(5);
        });

        function confirmRide() {
            if (marker) {
                alert("Dhanyawad! Raftar Bihar sathi aapki chuni hui gali mein pahunch raha hai.");
            } else {
                alert("Pehle map par click karke location set karein!");
            }
        }
    </script>
</body>
</html>
