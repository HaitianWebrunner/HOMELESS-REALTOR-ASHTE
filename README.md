<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>US County Construction · 50 states</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', sans-serif;
        }
        body {
            background: linear-gradient(145deg, #f1f4f8 0%, #e6ecf5 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }
        .card {
            max-width: 1300px;
            width: 100%;
            background: rgba(255,255,255,0.75);
            backdrop-filter: blur(12px);
            border-radius: 2.5rem;
            box-shadow: 0 30px 60px rgba(0, 20, 30, 0.25), inset 0 1px 3px rgba(255,255,255,0.9);
            padding: 2rem 2rem 2.5rem;
            border: 1px solid rgba(255,255,255,0.7);
        }
        h1 {
            font-size: 2.2rem;
            font-weight: 600;
            color: #0b2d3b;
            display: flex;
            align-items: center;
            gap: 0.5rem;
            margin-bottom: 0.25rem;
            letter-spacing: -0.02em;
        }
        h1 span {
            background: #1e4a6b;
            color: white;
            font-size: 1rem;
            padding: 0.2rem 1rem;
            border-radius: 40px;
            margin-left: 1rem;
            font-weight: 400;
        }
        .sub {
            color: #2c4e66;
            margin-bottom: 2rem;
            font-size: 1.1rem;
            border-left: 4px solid #1e4a6b;
            padding-left: 1.2rem;
            background: rgba(30,74,107,0.03);
            border-radius: 0 8px 8px 0;
        }
        .selector-panel {
            display: flex;
            flex-wrap: wrap;
            gap: 2rem;
            margin-bottom: 2.5rem;
        }
        .select-box {
            flex: 1 1 280px;
            background: white;
            border-radius: 28px;
            padding: 1.75rem 1.5rem;
            box-shadow: 0 15px 30px -10px rgba(0,40,60,0.2);
            border: 1px solid rgba(255,255,255,0.7);
        }
        .select-box label {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            font-weight: 600;
            color: #16394e;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            font-size: 0.85rem;
            margin-bottom: 1rem;
        }
        .select-box label i {
            font-size: 1.2rem;
        }
        select {
            width: 100%;
            padding: 0.9rem 1.2rem;
            font-size: 1rem;
            border: 2px solid #dae4ed;
            border-radius: 40px;
            background: #f9fcff;
            appearance: none;
            background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="%231e4a6b" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polyline points="6 9 12 15 18 9"></polyline></svg>');
            background-repeat: no-repeat;
            background-position: right 1.2rem center;
            background-size: 1.2rem;
            cursor: pointer;
            transition: 0.2s;
            color: #0a2c3b;
            font-weight: 500;
        }
        select:hover {
            border-color: #1e4a6b;
            background-color: #ffffff;
        }
        select:disabled {
            opacity: 0.6;
            background-color: #ecf2f9;
            cursor: not-allowed;
        }
        .county-info {
            background: #ffffffd9;
            border-radius: 32px;
            padding: 1.6rem 2rem;
            margin-top: 0.5rem;
            box-shadow: inset 0 1px 4px #ffffff, 0 12px 25px -15px #0f3b4e;
            border: 1px solid white;
            min-height: 180px;
        }
        .selection-badge {
            display: flex;
            flex-wrap: wrap;
            gap: 1rem 2rem;
            align-items: baseline;
            margin-bottom: 1.5rem;
        }
        .badge {
            background: #f0f7fe;
            padding: 0.5rem 1.2rem;
            border-radius: 40px;
            font-size: 1.2rem;
            font-weight: 500;
            color: #0b394b;
            border: 1px solid #c7dff5;
        }
        .badge span {
            font-weight: 300;
            color: #386a86;
            margin-right: 0.6rem;
        }
        .company-list {
            margin-top: 1.2rem;
        }
        .company-list h3 {
            font-weight: 500;
            font-size: 1.1rem;
            color: #1b5570;
            letter-spacing: 0.2px;
            display: flex;
            align-items: center;
            gap: 0.5rem;
            border-bottom: 2px dashed #aac3d9;
            padding-bottom: 0.5rem;
            margin-bottom: 1.5rem;
        }
        .company-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
            gap: 1.2rem;
        }
        .company-card {
            background: #f8fafd;
            border-radius: 24px;
            padding: 1.2rem 1.2rem 1.2rem 1.5rem;
            border-left: 6px solid #1e4a6b;
            box-shadow: 0 5px 12px rgba(0,0,0,0.02);
            transition: 0.1s ease;
            border: 1px solid #e0edf7;
        }
        .company-card strong {
            font-size: 1.1rem;
            color: #103e53;
            display: block;
            margin-bottom: 0.3rem;
        }
        .company-card .const-type {
            font-size: 0.9rem;
            color: #54738f;
            display: flex;
            align-items: center;
            gap: 0.2rem;
            margin-top: 0.4rem;
        }
        .company-card i {
            color: #b22234;  /* tiny accent */
            margin-right: 0.4rem;
        }
        .placeholder-msg {
            color: #667e96;
            font-style: italic;
            padding: 1.8rem 1rem;
            background: #f1f9ff;
            border-radius: 30px;
            text-align: center;
            border: 1px dashed #aac3d9;
        }
        .footer-note {
            font-size: 0.85rem;
            margin-top: 2rem;
            color: #4a6279;
            text-align: center;
            border-top: 1px solid rgba(30,74,107,0.2);
            padding-top: 1.2rem;
        }
    </style>
</head>
<body>
<div class="card">
    <h1>🏗️ ConstructLocator <span>50 states + counties</span></h1>
    <div class="sub">Pick a state, then a county — see active construction companies</div>

    <div class="selector-panel">
        <!-- STATE SELECTOR -->
        <div class="select-box">
            <label><i>📍</i> 1. choose a state</label>
            <select id="stateSelect">
                <option value="" disabled selected>– select state –</option>
            </select>
        </div>

        <!-- COUNTY SELECTOR -->
        <div class="select-box">
            <label><i>🗺️</i> 2. choose a county</label>
            <select id="countySelect" disabled>
                <option value="" disabled selected>– first select a state –</option>
            </select>
        </div>
    </div>

    <!-- RESULTS display for selected state+county -->
    <div class="county-info" id="countyInfoPanel">
        <div class="selection-badge" id="selectionBadge">
            <div class="badge"><span>state</span> <span id="displayState">—</span></div>
            <div class="badge"><span>county</span> <span id="displayCounty">—</span></div>
        </div>

        <div id="companyContainer">
            <!-- dynamic companies will appear here -->
            <div class="placeholder-msg">👆 Select a state and county to view local construction firms.</div>
        </div>
    </div>
    <div class="footer-note">⚒️ Data includes sample companies — real directory concept for all 50 states + counties.</div>
</div>

<script>
(function() {
    // ---------- CONSTRUCTION COMPANIES (mock data, each county gets 2-5 firms) ----------
    // For simplicity we generate them on the fly based on state and county.
    // We'll create a deterministic but varied list per county.

    // ------------------------------------------------------------
    // 1. Generate all 50 states with plausible counties (4-8 each)
    // ------------------------------------------------------------
    const usStates = [
        "Alabama", "Alaska", "Arizona", "Arkansas", "California", "Colorado", "Connecticut", "Delaware",
        "Florida", "Georgia", "Hawaii", "Idaho", "Illinois", "Indiana", "Iowa", "Kansas", "Kentucky",
        "Louisiana", "Maine", "Maryland", "Massachusetts", "Michigan", "Minnesota", "Mississippi",
        "Missouri", "Montana", "Nebraska", "Nevada", "New Hampshire", "New Jersey", "New Mexico",
        "New York", "North Carolina", "North Dakota", "Ohio", "Oklahoma", "Oregon", "Pennsylvania",
        "Rhode Island", "South Carolina", "South Dakota", "Tennessee", "Texas", "Utah", "Vermont",
        "Virginia", "Washington", "West Virginia", "Wisconsin", "Wyoming"
    ];

    // County lists per state (curated sample counties, real-sounding)
    const stateCounties = {
        "Alabama": ["Jefferson", "Mobile", "Madison", "Montgomery", "Shelby", "Tuscaloosa", "Baldwin"],
        "Alaska": ["Anchorage", "Fairbanks North Star", "Matanuska-Susitna", "Kenai Peninsula", "Juneau", "Ketchikan Gateway"],
        "Arizona": ["Maricopa", "Pima", "Pinal", "Yavapai", "Coconino", "Mohave", "Yuma"],
        "Arkansas": ["Pulaski", "Benton", "Washington", "Sebastian", "Saline", "Craighead", "Garland"],
        "California": ["Los Angeles", "San Diego", "Orange", "Riverside", "San Bernardino", "Santa Clara", "Alameda", "Sacramento"],
        "Colorado": ["Denver", "El Paso", "Arapahoe", "Jefferson", "Larimer", "Douglas", "Boulder"],
        "Connecticut": ["Fairfield", "Hartford", "New Haven", "Litchfield", "Middlesex", "Tolland", "Windham"],
        "Delaware": ["New Castle", "Sussex", "Kent"],
        "Florida": ["Miami-Dade", "Broward", "Palm Beach", "Hillsborough", "Orange", "Duval", "Pinellas", "Lee"],
        "Georgia": ["Fulton", "Gwinnett", "Cobb", "DeKalb", "Clayton", "Chatham", "Richmond"],
        "Hawaii": ["Honolulu", "Hawaii", "Maui", "Kauai", "Kalawao"],
        "Idaho": ["Ada", "Canyon", "Kootenai", "Bonneville", "Bannock", "Twin Falls", "Madison"],
        "Illinois": ["Cook", "DuPage", "Lake", "Will", "Kane", "Winnebago", "McHenry"],
        "Indiana": ["Marion", "Lake", "Allen", "Hamilton", "St. Joseph", "Vanderburgh", "Elkhart"],
        "Iowa": ["Polk", "Linn", "Scott", "Johnson", "Woodbury", "Dubuque", "Black Hawk"],
        "Kansas": ["Sedgwick", "Johnson", "Shawnee", "Wyandotte", "Douglas", "Leavenworth", "Riley"],
        "Kentucky": ["Jefferson", "Fayette", "Kenton", "Boone", "Campbell", "Warren", "Daviess"],
        "Louisiana": ["East Baton Rouge", "Jefferson", "Orleans", "Caddo", "Lafayette", "Calcasieu", "Ouachita"],
        "Maine": ["Cumberland", "York", "Penobscot", "Kennebec", "Androscoggin", "Oxford", "Somerset"],
        "Maryland": ["Montgomery", "Prince George's", "Baltimore", "Anne Arundel", "Howard", "Frederick", "Harford"],
        "Massachusetts": ["Middlesex", "Worcester", "Essex", "Suffolk", "Norfolk", "Bristol", "Plymouth"],
        "Michigan": ["Wayne", "Oakland", "Macomb", "Kent", "Washtenaw", "Ingham", "Ottawa"],
        "Minnesota": ["Hennepin", "Ramsey", "Dakota", "Anoka", "Washington", "St. Louis", "Stearns"],
        "Mississippi": ["Hinds", "Harrison", "Rankin", "Jackson", "DeSoto", "Madison", "Lee"],
        "Missouri": ["St. Louis", "Jackson", "St. Charles", "Greene", "Clay", "Boone", "Jefferson"],
        "Montana": ["Yellowstone", "Missoula", "Gallatin", "Flathead", "Cascade", "Lewis and Clark", "Silver Bow"],
        "Nebraska": ["Douglas", "Lancaster", "Sarpy", "Hall", "Buffalo", "Scotts Bluff", "Dodge"],
        "Nevada": ["Clark", "Washoe", "Carson City", "Douglas", "Lyon", "Elko", "Nye"],
        "New Hampshire": ["Hillsborough", "Rockingham", "Merrimack", "Strafford", "Cheshire", "Belknap", "Grafton"],
        "New Jersey": ["Bergen", "Essex", "Middlesex", "Hudson", "Monmouth", "Ocean", "Union"],
        "New Mexico": ["Bernalillo", "Dona Ana", "Santa Fe", "Sandoval", "San Juan", "Valencia", "Eddy"],
        "New York": ["Kings", "Queens", "New York", "Suffolk", "Bronx", "Nassau", "Westchester", "Erie"],
        "North Carolina": ["Mecklenburg", "Wake", "Guilford", "Forsyth", "Cumberland", "Durham", "Buncombe"],
        "North Dakota": ["Cass", "Burleigh", "Grand Forks", "Ward", "Morton", "Williams", "Stark"],
        "Ohio": ["Franklin", "Cuyahoga", "Hamilton", "Montgomery", "Summit", "Lucas", "Butler"],
        "Oklahoma": ["Oklahoma", "Tulsa", "Cleveland", "Canadian", "Comanche", "Payne", "Rogers"],
        "Oregon": ["Multnomah", "Washington", "Clackamas", "Lane", "Marion", "Jackson", "Deschutes"],
        "Pennsylvania": ["Philadelphia", "Allegheny", "Montgomery", "Bucks", "Delaware", "Lancaster", "Chester"],
        "Rhode Island": ["Providence", "Kent", "Washington", "Newport", "Bristol"],
        "South Carolina": ["Greenville", "Richland", "Charleston", "Spartanburg", "Lexington", "York", "Horry"],
        "South Dakota": ["Minnehaha", "Pennington", "Lincoln", "Brown", "Brookings", "Davison", "Meade"],
        "Tennessee": ["Shelby", "Davidson", "Knox", "Hamilton", "Rutherford", "Sumner", "Williamson"],
        "Texas": ["Harris", "Dallas", "Tarrant", "Bexar", "Travis", "Collin", "Denton", "El Paso"],
        "Utah": ["Salt Lake", "Utah", "Davis", "Weber", "Washington", "Cache", "Tooele"],
        "Vermont": ["Chittenden", "Rutland", "Washington", "Windham", "Windsor", "Addison", "Bennington"],
        "Virginia": ["Fairfax", "Prince William", "Virginia Beach", "Loudoun", "Chesterfield", "Henrico", "Roanoke"],
        "Washington": ["King", "Pierce", "Snohomish", "Spokane", "Clark", "Thurston", "Whatcom"],
        "West Virginia": ["Kanawha", "Monongalia", "Cabell", "Wood", "Raleigh", "Harrison", "Berkeley"],
        "Wisconsin": ["Milwaukee", "Dane", "Waukesha", "Brown", "Racine", "Outagamie", "Winnebago"],
        "Wyoming": ["Laramie", "Natrona", "Campbell", "Sweetwater", "Fremont", "Albany", "Sheridan"]
    };

    // Ensure all 50 states have at least some counties (fallback if missing)
    usStates.forEach(st => {
        if (!stateCounties[st]) {
            // fallback (just in case) – create dummy counties
            stateCounties[st] = ["Central", "Northern", "Southern", "Eastern", "Western"];
        }
    });

    // ---------- DOM elements ----------
    const stateSelect = document.getElementById('stateSelect');
    const countySelect = document.getElementById('countySelect');
    const displayStateSpan = document.getElementById('displayState');
    const displayCountySpan = document.getElementById('displayCounty');
    const companyContainer = document.getElementById('companyContainer');

    // Populate state dropdown
    usStates.forEach(state => {
        const option = document.createElement('option');
        option.value = state;
        option.textContent = state;
        stateSelect.appendChild(option);
    });

    // State change → load counties, reset county dropdown, disable county until selection
    stateSelect.addEventListener('change', function() {
        const selectedState = this.value;
        if (!selectedState) return;

        // Enable county select
        countySelect.disabled = false;
        // Clear previous counties
        countySelect.innerHTML = '<option value="" disabled selected>– choose county –</option>';

        // Get counties for this state
        const counties = stateCounties[selectedState] || ["Default County"];
        counties.sort().forEach(county => {
            const opt = document.createElement('option');
            opt.value = county;
            opt.textContent = county;
            countySelect.appendChild(opt);
        });

        // Reset display & company list because state changed (county not chosen yet)
        displayStateSpan.textContent = selectedState;
        displayCountySpan.textContent = '—';
        companyContainer.innerHTML = `<div class="placeholder-msg">⬇️ Now select a county in ${selectedState}.</div>`;
    });

    // County change → render companies
    countySelect.addEventListener('change', function() {
        const state = stateSelect.value;
        const county = this.value;

        if (!state || !county) {
            // should not happen if disabled properly
            return;
        }

        // Update badge
        displayStateSpan.textContent = state;
        displayCountySpan.textContent = county;

        // Generate dynamic companies for (state, county)
        const companies = generateCompaniesFor(state, county);
        renderCompanies(companies);
    });

    // Helper: random-ish but deterministic company names based on state/county seed
    function generateCompaniesFor(state, county) {
        const seed = state.length + county.length + state.charCodeAt(0) + county.charCodeAt(1) || 1;
        const companyCount = 3 + (seed % 4);  // 3 to 6 companies

        // Some specialities to add variety
        const specialties = [
            "General Contractor", "Heavy Civil", "Residential", "Commercial", "Framing", "Concrete", 
            "Roofing", "Excavation", "Design-Build", "Renovation", "Infrastructure", "Industrial",
            "Highway & Street", "Utility", "Solar Construction", "Green Building"
        ];

        // Predefined name parts
        const prefixes = ["Apex", "Core", "Metro", "Summit", "Pioneer", "Legacy", "Iron", "Bedrock", "Cascade", "Redwood", "Stone", "Horizon", "Peak", "Valley", "Coast", "Bridge", "Meridian"];
        const suffixes = ["Construction", "Builders", "Contractors", "Developers", "Engineering", "Corporation", "Group", "Inc.", "LLC", "& Co."];

        let companies = [];
        for (let i = 0; i < companyCount; i++) {
            const pre = prefixes[(seed + i * 3) % prefixes.length];
            const suf = suffixes[(seed + i * 5) % suffixes.length];
            const name = `${pre} ${suf}`;

            const spec1 = specialties[(seed + i * 7) % specialties.length];
            const spec2 = specialties[(seed + i * 11) % specialties.length];
            const specialty = (i % 3 === 0) ? spec1 : `${spec1} / ${spec2}`;

            companies.push({ name, specialty });
        }
        return companies;
    }

    function renderCompanies(companies) {
        if (!companies || companies.length === 0) {
            companyContainer.innerHTML = `<div class="placeholder-msg">🏢 No construction firms currently listed for this county.</div>`;
            return;
        }

        let html = `<div class="company-list"><h3>🏢 Construction companies in ${displayCountySpan.textContent} County</h3><div class="company-grid">`;
        companies.forEach(c => {
            html += `<div class="company-card">
                <strong>🏗️ ${c.name}</strong>
                <div class="const-type"><i>⚙️</i> ${c.specialty}</div>
            </div>`;
        });
        html += `</div></div>`;
        companyContainer.innerHTML = html;
    }

    // (optional) initialize with placeholder
})();
</script>
</body>
</html>
