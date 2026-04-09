<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hinlu-Laba | The Smart Laundry Ecosystem</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;800&display=swap" rel="stylesheet">
    
    <style>
        /* CSS Reset & Base Variables */
        :root {
            --primary: #2b3a67; /* Deep Navy Blue */
            --action: #ff6b35; /* Vibrant Orange for Action */
            --bg-light: #f4f7f6;
            --text-dark: #2d3142;
            --text-muted: #666;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Inter', sans-serif; }
        body { background-color: var(--bg-light); color: var(--text-dark); line-height: 1.6; }

        /* Navigation */
        header {
            background-color: #ffffff;
            padding: 15px 5%;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 2px 10px rgba(0,0,0,0.05);
            position: sticky;
            top: 0;
            z-index: 1000;
        }

        .logo { font-size: 26px; font-weight: 800; color: var(--primary); cursor: pointer; letter-spacing: -0.5px;}
        .logo span { color: var(--action); }

        .nav-links { display: flex; gap: 15px; }
        .nav-btn {
            background: none;
            border: none;
            font-size: 1rem;
            font-weight: 600;
            color: var(--text-muted);
            cursor: pointer;
            padding: 8px 16px;
            border-radius: 5px;
            transition: all 0.3s;
        }
        .nav-btn:hover { color: var(--action); }
        .nav-btn.active { background-color: var(--primary); color: white; }

        /* Section Containers */
        .page-section { display: none; padding: 60px 5%; max-width: 1200px; margin: 0 auto; animation: fadeIn 0.4s ease-in-out; }
        .page-section.active { display: block; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        /* General Typography */
        h1 { font-size: 2.8rem; color: var(--primary); margin-bottom: 20px; text-align: center; line-height: 1.2;}
        .subtitle { font-size: 1.2rem; color: var(--text-muted); text-align: center; margin-bottom: 50px; max-width: 800px; margin-left: auto; margin-right: auto;}
        h2 { font-size: 2rem; color: var(--primary); margin-bottom: 20px; }

        /* Grid Layouts */
        .grid-3 { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 30px; margin-bottom: 40px; }
        .grid-2 { display: grid; grid-template-columns: repeat(auto-fit, minmax(400px, 1fr)); gap: 40px; margin-bottom: 40px; align-items: center; }

        /* Cards & Interactive Elements */
        .card { background: white; padding: 30px; border-radius: 12px; box-shadow: 0 5px 15px rgba(0,0,0,0.05); }
        .card-icon { font-size: 2.5rem; margin-bottom: 15px; }
        .card h3 { color: var(--primary); margin-bottom: 15px; font-size: 1.3rem; }
        
        .interactive-box { background: white; padding: 30px; border-radius: 12px; border-top: 4px solid var(--action); box-shadow: 0 10px 30px rgba(0,0,0,0.08); margin-bottom: 40px;}
        input, select { padding: 12px; border: 1px solid #ddd; border-radius: 6px; font-size: 1rem; outline: none;}
        input:focus, select:focus { border-color: var(--action); }

        /* Video Container */
        .video-wrapper { position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 12px; box-shadow: 0 10px 30px rgba(0,0,0,0.15); margin-bottom: 50px; background-color: #000; }
        .video-wrapper iframe { position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: none; }

        /* Process Sync Timeline */
        .sync-process { background: white; padding: 40px; border-radius: 12px; border-left: 5px solid var(--action); box-shadow: 0 5px 20px rgba(0,0,0,0.08); }
        .sync-step { display: flex; margin-bottom: 30px; }
        .step-number { background: var(--primary); color: white; width: 40px; height: 40px; display: flex; align-items: center; justify-content: center; border-radius: 50%; font-weight: 800; font-size: 1.2rem; flex-shrink: 0; margin-right: 20px; }
        .step-content h3 { color: var(--primary); margin-bottom: 5px; }
        .step-tags span { display: inline-block; font-size: 0.8rem; padding: 3px 8px; border-radius: 12px; font-weight: 600; margin-right: 5px; margin-top: 10px;}
        .tag-app { background: #e6eaf5; color: var(--primary); }
        .tag-iot { background: #ffeae0; color: var(--action); }
        .tag-sms { background: #e8f5e9; color: #2e7d32; }

        /* Call to Action Buttons */
        .cta-box { text-align: center; margin-top: 40px; padding: 40px; background: var(--primary); color: white; border-radius: 12px; }
        .btn-main { background-color: var(--action); color: white; padding: 15px 30px; border: none; font-size: 1.1rem; font-weight: 600; border-radius: 8px; cursor: pointer; transition: 0.2s; }
        .btn-main:hover { background-color: #e35a28; transform: translateY(-2px);}

        /* Footer */
        footer { background-color: #171f36; color: #9bb6bb; padding: 40px 5%; text-align: center; margin-top: 60px; }
    </style>
</head>
<body>

    <header>
        <div class="logo" onclick="switchTab('action')">Hinlu<span>Laba</span></div>
        <nav class="nav-links">
            <button class="nav-btn active" onclick="switchTab('action')" id="btn-action">See It In Action</button>
            <button class="nav-btn" onclick="switchTab('customers')" id="btn-customers">For Customers</button>
            <button class="nav-btn" onclick="switchTab('shops')" id="btn-shops">For Shops</button>
            <button class="nav-btn" onclick="switchTab('runners')" id="btn-runners">For Runners</button>
        </nav>
    </header>

    <section id="action" class="page-section active">
        <h1>Built for Fast-Growing Communities.</h1>
        <p class="subtitle">In today's fast-paced world of career, family, and traffic, your time is your most valuable asset. Watch how the Hinlu-Laba ecosystem synchronizes customers, runners, and smart machines.</p>
        
        <div class="video-wrapper">
            <iframe src="https://www.youtube.com/embed/dQw4w9WgXcQ?rel=0" title="Hinlu-Laba Process Review" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
        </div>

        <h2 style="text-align: center; margin-top: 40px;">The Flow of Orders in Action</h2>
        <div class="sync-process">
            <div class="sync-step">
                <div class="step-number">1</div>
                <div class="step-content">
                    <h3>The Customer Tap (Order Generation)</h3>
                    <p>The busy professional opens the mobile app, selects a 5kg package, and taps book. The Hinlu-Laba Cloud calculates the nearest active partner shop via geo-fencing.</p>
                    <div class="step-tags"><span class="tag-app">Customer App</span> <span class="tag-app">Cloud AI</span></div>
                </div>
            </div>
            <div class="sync-step">
                <div class="step-number">2</div>
                <div class="step-content">
                    <h3>The SMS Dispatch & Hardware Audit</h3>
                    <p>An SMS instantly pings the nearest Runners. A runner drops off the bag. Staff loads it. The IoT sensors detect the drum spinning and track utility usage for exact cost calculation.</p>
                    <div class="step-tags"><span class="tag-sms">SMS Gateway</span> <span class="tag-iot">IoT Hardware</span> <span class="tag-app">Shop Dashboard</span></div>
                </div>
            </div>
        </div>
    </section>

    <section id="customers" class="page-section">
        <h1>Your Wardrobe, Handled.</h1>
        <p class="subtitle">For busy professionals, parents, and students. Don't let laundry day consume your weekend.</p>
        
        <div class="grid-3">
            <div class="card">
                <div class="card-icon">📱</div>
                <h3>One-Tap Booking</h3>
                <p>Select your package, from standard Wash-Dry-Fold to comforter care. We instantly find the best-rated shop near you.</p>
            </div>
            <div class="card">
                <div class="card-icon">📍</div>
                <h3>Live GPS Tracking</h3>
                <p>Never wonder where your clothes are. Watch your laundry's journey from your doorstep to the dryer and back again.</p>
            </div>
            <div class="card">
                <div class="card-icon">🛡️</div>
                <h3>The Fresh Guarantee</h3>
                <p>Every load is transported in weather-proof bags and sealed with tamper-proof tags.</p>
            </div>
        </div>

        <div class="interactive-box">
            <h2>Calculate Your Cost</h2>
            <p style="color: var(--text-muted); margin-bottom: 20px;">Estimate your laundry bill instantly before booking.</p>
            <div style="display: flex; gap: 15px; flex-wrap: wrap; align-items: center;">
                <input type="number" id="weightInput" placeholder="Weight in Kg (e.g., 5)" style="width: 200px;" min="1">
                <select id="serviceSelect">
                    <option value="40">Standard Wash-Dry-Fold (₱40/kg)</option>
                    <option value="60">Comforter Care (₱60/kg)</option>
                    <option value="80">Express Rush 3-Hours (₱80/kg)</option>
                </select>
                <button class="btn-main" onclick="calculatePrice()">Calculate</button>
            </div>
            <h1 id="priceResult" style="color: var(--action); margin-top: 20px;">₱0.00</h1>
            <p id="errorText" style="color: red; display: none; margin-top: 5px;">Please enter a valid weight number.</p>
        </div>

        <div class="cta-box">
            <h2>Take Back Your Time.</h2>
            <p style="margin-bottom: 20px;">Join thousands of busy residents automating their chores with Hinlu-Laba.</p>
            <button class="btn-main" onclick="alert('App Store links coming soon! Thank you for your interest.')">Download App (Get ₱100 Off)</button>
        </div>
    </section>

    <section id="shops" class="page-section">
        <h1>Stop Guessing. Start Monitoring.</h1>
        <p class="subtitle">Transform your laundromat into a smart business with IoT sensors and automated delivery orders.</p>
        
        <div class="grid-2">
            <div>
                <h2>The Smart Hardware Shield</h2>
                <p style="margin-bottom: 15px;">We protect your margins. Our non-invasive IoT hardware attaches to any commercial machine to combat utility leaks and "sideline" theft.</p>
                <ul style="list-style-position: inside; margin-bottom: 20px; color: var(--text-muted);">
                    <li><b>Vibration Sensors:</b> Get an alert if staff runs an unrecorded wash.</li>
                    <li><b>Water Flow Meters:</b> Track every drop to identify leaky valves instantly.</li>
                    <li><b>CT Power Clamps:</b> Monitor electricity costs per load to calculate true profit.</li>
                </ul>
            </div>
            <div class="card" style="background: var(--primary); color: white;">
                <h3 style="color: white;">The Revenue Split</h3>
                <p style="color: #9bb6bb; margin-bottom: 10px;">For every Hinlu-Laba order processed:</p>
                <h1 style="color: var(--action); margin-bottom: 5px;">70%</h1>
                <p style="color: white; margin-bottom: 20px; text-align: center;">Goes directly to your shop ledger.</p>
                <p style="font-size: 0.9rem; color: #9bb6bb; text-align: center;">Zero marketing spend. Let our app find the customers while you focus on quality.</p>
            </div>
        </div>
        <div class="cta-box">
            <h2>Join the Fast-Track Pilot</h2>
            <button class="btn-main" onclick="alert('Pilot Program form opening shortly. Please email rambo.xmcl@gmail.com to reserve your spot.')">Apply as Partner Shop</button>
        </div>
    </section>

    <section id="runners" class="page-section">
        <h1>Turn Your Motor into a Money-Maker.</h1>
        <p class="subtitle">Join the Hinlu-Laba Trust Network. Be the essential link in your fast-growing community.</p>
        
        <div class="grid-3">
            <div class="card">
                <div class="card-icon">💸</div>
                <h3>20% Commission</h3>
                <p>Earn a solid cut on every bag. Instant cashouts to GCash or Maya daily.</p>
            </div>
            <div class="card">
                <div class="card-icon">📶</div>
                <h3>Low-Data SMS Ping</h3>
                <p>Our system dispatches jobs via fast SMS so you never miss an order in traffic.</p>
            </div>
            <div class="card">
                <div class="card-icon">🛵</div>
                <h3>Clean & Easy Work</h3>
                <p>Unlike food, laundry doesn't spill, and it doesn't get cold.</p>
            </div>
        </div>
        <div class="cta-box">
            <h2>Ready to ride?</h2>
            <button class="btn-main" onclick="alert('Runner onboarding portal will open during Beta launch.')">Sign Up as a Runner</button>
        </div>
    </section>

    <footer>
        <p style="color: white; font-weight: 800; font-size: 1.2rem; margin-bottom: 10px;">Hinlu-Laba Tech Solutions</p>
        <p style="margin-bottom: 5px;">Metro Manila, Philippines</p>
        <p>Randell Mark Borja • 0966 845 2667 • rambo.xmcl@gmail.com</p>
    </footer>

    <script>
        // 1. Navigation Logic (Switching Tabs)
        function switchTab(tabId) {
            //
