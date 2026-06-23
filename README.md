<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cricket, Tracking & Finance Hub</title>
    <style>
        :root {
            --primary-cricket: #1e3d59;
            --primary-car: #ff6e40;
            --primary-finance: #2e7d32;
            --bg-light: #f5f7fa;
            --text-dark: #333333;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: var(--bg-light);
            color: var(--text-dark);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 20px;
        }

        .app-container {
            width: 100%;
            max-width: 850px;
            background: #ffffff;
            border-radius: 12px;
            box-shadow: 0 8px 24px rgba(0,0,0,0.1);
            overflow: hidden;
        }

        /* Tabs Navigation */
        .tabs-nav {
            display: flex;
            background: #eaeaea;
            border-bottom: 2px solid #ddd;
        }

        .tab-btn {
            flex: 1;
            padding: 15px;
            font-size: 16px;
            font-weight: 600;
            background: none;
            border: none;
            cursor: pointer;
            text-align: center;
            transition: all 0.3s ease;
            color: #555;
        }

        .tab-btn:hover {
            background: #f0f0f0;
        }

        .tab-btn.active[data-tab="cricket"] { background: #fff; color: var(--primary-cricket); border-top: 4px solid var(--primary-cricket); }
        .tab-btn.active[data-tab="car"] { background: #fff; color: var(--primary-car); border-top: 4px solid var(--primary-car); }
        .tab-btn.active[data-tab="finance"] { background: #fff; color: var(--primary-finance); border-top: 4px solid var(--primary-finance); }

        /* Tab Content Panel styling */
        .tab-content {
            display: none;
            padding: 30px;
            min-height: 500px;
        }

        .tab-content.active {
            display: block;
        }

        h2 {
            margin-bottom: 20px;
            font-size: 24px;
            text-align: center;
        }

        .form-group {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 15px;
            margin-bottom: 25px;
            flex-wrap: wrap;
        }

        label {
            font-weight: 600;
        }

        select, input[type="text"], input[type="number"] {
            padding: 10px;
            font-size: 15px;
            border: 1px solid #ccc;
            border-radius: 6px;
            outline: none;
        }

        button {
            padding: 10px 20px;
            font-size: 15px;
            font-weight: bold;
            color: white;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            transition: opacity 0.2s;
        }

        button:hover {
            opacity: 0.9;
        }

        /* Module Specific Styling */
        /* 1. Cricket */
        #cricket h2 { color: var(--primary-cricket); }
        #cricket button { background-color: var(--primary-cricket); }
        .display-box {
            width: 100%;
            max-width: 600px;
            margin: 0 auto;
            padding: 20px;
            border: 1px solid #ccc;
            border-radius: 6px;
            background: #fafafa;
            white-space: pre-wrap;
            min-height: 120px;
        }

        /* 2. Car Tracker */
        #car h2 { color: var(--primary-car); }
        #car button { background-color: var(--primary-car); }
        .car-display {
            max-width: 600px;
            margin: 0 auto 10px auto;
            padding: 20px;
            background-color: #fff3e0;
            border: 2px groove #ffe0b2;
            border-radius: 6px;
            min-height: 120px;
            white-space: pre-wrap;
        }
        .note {
            text-align: center;
            color: gray;
            font-size: 13px;
            font-style: italic;
        }

        /* 3. Finance Layout */
        #finance h2 { color: var(--primary-finance); }
        #finance button { background-color: var(--primary-finance); }
        
        .finance-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            margin-top: 20px;
        }
        
        @media (max-width: 680px) {
            .finance-grid { grid-template-columns: 1fr; }
        }

        .finance-card {
            background: #edf7ed;
            border: 1px solid #c8e6c9;
            padding: 20px;
            border-radius: 6px;
        }
        
        .finance-card h3 {
            margin-bottom: 10px;
            color: var(--primary-finance);
        }
        
        .sub-active {
            background: #f1f8ff;
            border-color: #bee3f8;
        }
        .sub-active h3 {
            color: #2b6cb0;
        }
    </style>
</head>
<body>

<div class="app-container">
    <nav class="tabs-nav">
        <button class="tab-btn active" data-tab="cricket">Cricket Info</button>
        <button class="tab-btn" data-tab="car">Car Tracker</button>
        <button class="tab-btn" data-tab="finance">Finance Hub</button>
    </nav>

    <section id="cricket" class="tab-content active">
        <h2>Cricket Live Statistics</h2>
        <div class="form-group">
            <label for="team-select">Select Team:</label>
            <select id="team-select">
                <option value="India">India</option>
                <option value="Australia">Australia</option>
                <option value="England">England</option>
            </select>
            <button onclick="getCricketData()">Fetch Report</button>
        </div>
        <div id="cricket-output" class="display-box">Select a team to parse real-time standings data.</div>
    </section>

    <section id="car" class="tab-content">
        <h2>Vehicle Tracking Terminal</h2>
        <div class="form-group">
            <label for="car-id">Vehicle ID:</label>
            <input type="text" id="car-id" placeholder="e.g. CAR-99X">
            <button onclick="trackVehicle()">Locate Fleet</button>
        </div>
        <div id="car-output" class="car-display">Awaiting terminal telemetry tracking inputs...</div>
        <p class="note">Data streams sync via secure localized GPS node relays.</p>
    </section>

    <section id="finance" class="tab-content">
        <h2>Personal Finance Engine</h2>
        <div class="form-group">
            <label for="budget-amount">Monthly Budget (₹):</label>
            <input type="number" id="budget-amount" value="15000" placeholder="15000">
            <button onclick="calculateBudget()">Process Ledgers</button>
        </div>
        
        <div class="finance-grid">
            <div class="finance-card">
                <h3>Balance Sheet</h3>
                <p id="finance-output">Provide standard variables to balance net values.</p>
            </div>
            <div class="finance-card sub-active">
                <h3>Active Subscriptions</h3>
                <p id="subscription-output"><strong>Phone:</strong> +91 8805823686<br><strong>Cost:</strong> ₹1,000.00 / mo</p>
            </div>
            <div class="finance-card" style="grid-column: span 2;">
                <h3>Savings & Liquidity Insights</h3>
                <p id="savings-output">Target limits and risk rules safely manifest here.</p>
            </div>
        </div>
    </section>
</div>

<script>
    // Tab Navigation Logic
    const tabs = document.querySelectorAll('.tab-btn');
    const contents = document.querySelectorAll('.tab-content');

    tabs.forEach(tab => {
        tab.addEventListener('click', () => {
            tabs.forEach(t => t.classList.remove('active'));
            contents.forEach(c => c.classList.remove('active'));

            tab.classList.add('active');
            const targetId = tab.getAttribute('data-tab');
            document.getElementById(targetId).classList.add('active');
        });
    });

    function getCricketData() {
        const team = document.getElementById('team-select').value;
        document.getElementById('cricket-output').innerText = 
            `Parsing statistics for [${team}]...\n• Recent Form: W-W-L-W\n• Current Group Standing: #1\n• Next Match Scheduled: Thursday 14:00 UTC`;
    }

    function trackVehicle() {
        const id = document.getElementById('car-id').value || "UNKNOWN-ID";
        document.getElementById('car-output').innerText = 
            `Telemetry Ping for [${id}]:\n• Coordinates: 34.0522° N, 118.2437° W\n• Status: In Transit (Moving)\n• Fuel Level: 74%`;
    }

    function calculateBudget() {
        const amount = parseFloat(document.getElementById('budget-amount').value) || 0;
        const subCost = 1000; // Fixed Subscription Cost in INR
        
        if(amount <= 0) {
            alert("Please enter a valid monetary amount.");
            return;
        }

        const fixedOverhead = amount * 0.5;
        let liquidity = amount * 0.3;
        const savings = amount * 0.2;

        // Deduct subscription from liquidity pool
        const remainingLiquidity = liquidity - subCost;

        document.getElementById('finance-output').innerHTML = `
            Total Budget Evaluated: <strong>₹${amount.toFixed(2)}</strong><br><br>
            • Fixed Overhead (50%): ₹${fixedOverhead.toFixed(2)}<br>
            • Total Liquidity/Flex Allocation (30%): ₹${liquidity.toFixed(2)}
        `;
        
        if (remainingLiquidity >= 0) {
            document.getElementById('savings-output').innerHTML = `
                • High-Yield Savings Pool (20%): <strong>₹${savings.toFixed(2)}</strong><br>
                • Remaining Disposable Liquidity (After ₹${subCost} Subscription): <strong style="color: green;">₹${remainingLiquidity.toFixed(2)}</strong>
            `;
        } else {
            document.getElementById('savings-output').innerHTML = `
                • High-Yield Savings Pool (20%): <strong>₹${savings.toFixed(2)}</strong><br>
                • <span style="color: red; font-weight: bold;">Warning:</span> Subscription expenses (₹${subCost}) exceed your designated 30% flexible liquidity pool by ₹${Math.abs(remainingLiquidity).toFixed(2)}!
            `;
        }
    }
    
    // Auto-calculate on initial load
    window.onload = calculateBudget;
</script>

</body>
</html>
