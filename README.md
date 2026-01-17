<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Series vs. Parallel Circuits</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Arial, sans-serif;
        }

        body {
            background-color: white;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 30px;
            min-height: 100vh;
        }

        .header {
            text-align: center;
            margin-bottom: 40px;
            width: 100%;
            max-width: 1200px;
        }

        .header h1 {
            color: #1a237e;
            font-size: 2.5rem;
            margin-bottom: 10px;
            font-weight: 600;
        }

        .header p {
            color: #5c6bc0;
            font-size: 1.2rem;
            max-width: 800px;
            margin: 0 auto;
            line-height: 1.5;
        }

        .comparison-container {
            display: flex;
            width: 100%;
            max-width: 1200px;
            height: 850px;
            background: white;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            border-radius: 12px;
            overflow: hidden;
            border: 1px solid #e0e0e0;
        }

        .panel {
            flex: 1;
            padding: 30px;
            display: flex;
            flex-direction: column;
            position: relative;
        }

        .panel::after {
            content: '';
            position: absolute;
            right: 0;
            top: 50px;
            bottom: 50px;
            width: 1px;
            background: linear-gradient(to bottom, transparent, #b0bec5, transparent);
        }

        .parallel-panel::after {
            display: none;
        }

        .panel-header {
            text-align: center;
            margin-bottom: 30px;
            padding-bottom: 15px;
            border-bottom: 2px solid;
        }

        .series-header {
            border-bottom-color: #e53935;
        }

        .parallel-header {
            border-bottom-color: #1e88e5;
        }

        .panel-header h2 {
            font-size: 1.8rem;
            margin-bottom: 8px;
            color: #263238;
        }

        .panel-header .subtitle {
            font-size: 1.1rem;
            color: #546e7a;
            font-weight: 500;
        }

        .circuit-container {
            flex: 1;
            position: relative;
            background: #fafafa;
            border-radius: 8px;
            padding: 20px;
            border: 1px solid #eceff1;
        }

        /* Circuit Styles */
        .wire {
            stroke-width: 4;
            fill: none;
        }

        .series-wire {
            stroke: #d32f2f;
        }

        .parallel-wire {
            stroke: #1976d2;
        }

        .battery {
            stroke-width: 2;
            stroke: #37474f;
        }

        .battery-fill {
            fill: #f5f5f5;
        }

        .terminal {
            font-size: 14px;
            font-weight: bold;
        }

        .series-terminal {
            fill: #d32f2f;
        }

        .parallel-terminal {
            fill: #1976d2;
        }

        .switch-closed {
            stroke-width: 3;
            stroke: #37474f;
        }

        .switch-open {
            stroke-width: 3;
            stroke: #78909c;
        }

        .switch-line-closed {
            stroke-width: 3;
            stroke: #37474f;
        }

        .switch-line-open {
            stroke-width: 3;
            stroke: #78909c;
            stroke-dasharray: 5,5;
        }

        .bulb {
            transition: filter 0.3s;
        }

        .series-bulb-on {
            filter: url(#medium-glow);
        }

        .series-bulb-off {
            filter: none;
        }

        .parallel-bulb-on {
            filter: url(#bright-glow);
        }

        .parallel-bulb-off {
            filter: none;
        }

        .bulb-glass {
            fill: #f5f5f5;
            stroke-width: 2;
        }

        .series-bulb-glass {
            stroke: #d32f2f;
        }

        .parallel-bulb-glass {
            stroke: #1976d2;
        }

        .filament {
            stroke-width: 2;
            fill: none;
        }

        .series-filament-on {
            stroke: #ff8a65;
        }

        .series-filament-off {
            stroke: #b0bec5;
        }

        .parallel-filament-on {
            stroke: #ffb74d;
        }

        .parallel-filament-off {
            stroke: #b0bec5;
        }

        /* Control Panel */
        .control-panel {
            margin-top: 15px;
            padding: 20px;
            background: #f8f9fa;
            border-radius: 8px;
            border: 1px solid #e9ecef;
        }

        .control-section {
            margin-bottom: 15px;
        }

        .control-label {
            font-size: 1rem;
            font-weight: 600;
            color: #37474f;
            margin-bottom: 10px;
            display: block;
        }

        .toggle-row {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-bottom: 10px;
            flex-wrap: wrap;
        }

        .toggle-btn {
            padding: 10px 20px;
            font-size: 0.9rem;
            font-weight: 600;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            transition: all 0.3s;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
            min-width: 120px;
        }

        .master-switch-btn {
            padding: 12px 30px;
            font-size: 1rem;
            font-weight: 600;
            min-width: 150px;
            margin-bottom: 15px;
        }

        .toggle-btn-series {
            background-color: #ffccbc;
            color: #d32f2f;
            border: 2px solid #ffab91;
        }

        .toggle-btn-series:hover:not(:disabled) {
            background-color: #ffab91;
            transform: translateY(-2px);
        }

        .toggle-btn-series.burned {
            background-color: #d32f2f;
            color: white;
            border: 2px solid #b71c1c;
        }

        .toggle-btn-parallel {
            background-color: #bbdefb;
            color: #1976d2;
            border: 2px solid #90caf9;
        }

        .toggle-btn-parallel:hover:not(:disabled) {
            background-color: #90caf9;
            transform: translateY(-2px);
        }

        .toggle-btn-parallel.burned {
            background-color: #1976d2;
            color: white;
            border: 2px solid #0d47a1;
        }

        .master-switch-series {
            background-color: #e53935;
            color: white;
            border: 2px solid #c62828;
        }

        .master-switch-series:hover {
            background-color: #c62828;
            transform: translateY(-2px);
        }

        .master-switch-parallel {
            background-color: #1e88e5;
            color: white;
            border: 2px solid #1565c0;
        }

        .master-switch-parallel:hover {
            background-color: #1565c0;
            transform: translateY(-2px);
        }

        .reset-btn {
            padding: 10px 25px;
            font-size: 0.95rem;
            font-weight: 600;
            background-color: #4caf50;
            color: white;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            transition: all 0.3s;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
            margin-top: 5px;
        }

        .reset-btn:hover {
            background-color: #388e3c;
            transform: translateY(-2px);
        }

        .circuit-status {
            margin-top: 10px;
            padding: 10px;
            background: white;
            border-radius: 6px;
            font-size: 0.9rem;
            color: #546e7a;
            text-align: center;
            border: 1px solid #e0e0e0;
        }

        .status-on {
            color: #2e7d32;
            font-weight: 600;
        }

        .status-off {
            color: #d32f2f;
            font-weight: 600;
        }

        .caption {
            margin-top: 15px;
            padding: 18px;
            background: #f1f8e9;
            border-radius: 8px;
            border-left: 5px solid;
            font-size: 1.1rem;
            line-height: 1.6;
            color: #33691e;
            font-weight: 500;
        }

        .series-caption {
            border-left-color: #e53935;
            background: #ffebee;
            color: #b71c1c;
        }

        .parallel-caption {
            border-left-color: #1e88e5;
            background: #e3f2fd;
            color: #0d47a1;
        }

        .component-label {
            font-size: 14px;
            fill: #455a64;
            font-weight: 500;
        }

        .voltage-label {
            font-size: 16px;
            font-weight: bold;
            fill: #37474f;
        }

        .broken-wire {
            stroke: #78909c;
            stroke-dasharray: 5,5;
            stroke-width: 4;
        }

        .disabled-btn {
            opacity: 0.5;
            cursor: not-allowed !important;
        }

        .disabled-btn:hover {
            transform: none !important;
        }

        /* Responsive Design */
        @media (max-width: 1000px) {
            .comparison-container {
                flex-direction: column;
                height: auto;
            }
            
            .panel {
                height: 800px;
            }
            
            .panel::after {
                display: none;
            }
            
            .parallel-panel {
                border-top: 1px solid #e0e0e0;
            }
            
            .toggle-row {
                flex-direction: column;
                align-items: center;
            }
            
            .toggle-btn {
                width: 80%;
                max-width: 200px;
            }
        }

        @media (max-width: 600px) {
            body {
                padding: 15px;
            }
            
            .header h1 {
                font-size: 2rem;
            }
            
            .panel {
                padding: 20px;
                height: 750px;
            }
            
            .panel-header h2 {
                font-size: 1.5rem;
            }
            
            .toggle-btn {
                padding: 8px 15px;
                font-size: 0.85rem;
                min-width: 100px;
            }
            
            .master-switch-btn {
                padding: 10px 20px;
                font-size: 0.9rem;
                min-width: 120px;
            }
        }
    </style>
</head>
<body>
    <div class="header">
        <h1>Series vs. Parallel Circuits</h1>
        <p>Comparing Electrical Circuit Configurations</p>
    </div>

    <div class="comparison-container">
        <!-- SERIES CIRCUIT PANEL -->
        <div class="panel">
            <div class="panel-header series-header">
                <h2>SERIES CIRCUIT</h2>
                <div class="subtitle">Single Path</div>
            </div>

            <div class="circuit-container">
                <svg width="100%" height="100%" viewBox="0 0 500 400" id="series-circuit">
                    <!-- SVG Filters for Glow Effects -->
                    <defs>
                        <filter id="medium-glow" x="-50%" y="-50%" width="200%" height="200%">
                            <feGaussianBlur stdDeviation="3" result="blur"/>
                            <feFlood flood-color="#ffcc80" flood-opacity="0.6" result="color"/>
                            <feComposite in="color" in2="blur" operator="in" result="glow"/>
                            <feMerge>
                                <feMergeNode in="glow"/>
                                <feMergeNode in="SourceGraphic"/>
                            </feMerge>
                        </filter>
                    </defs>

                    <!-- Corrected Rectangular Series Circuit -->
                    
                    <!-- Battery on left vertical side -->
                    <rect x="50" y="160" width="40" height="80" class="battery battery-fill" rx="3"/>
                    <line x1="50" y1="160" x2="50" y2="240" class="battery" stroke-width="4"/>
                    <line x1="90" y1="160" x2="90" y2="240" class="battery" stroke-width="4"/>
                    <text x="70" y="150" class="voltage-label" text-anchor="middle">9V</text>
                    <text x="45" y="190" class="terminal series-terminal" text-anchor="end">+</text>
                    <text x="95" y="230" class="terminal series-terminal" text-anchor="start">−</text>

                    <!-- Switch on top horizontal side -->
                    <line x1="150" y1="120" x2="170" y2="100" class="switch-closed" id="series-switch-lever"/>
                    <line x1="170" y1="100" x2="190" y2="100" class="switch-closed" id="series-switch-line"/>
                    <circle cx="190" cy="100" r="4" fill="#37474f" id="series-switch-knob"/>
                    <text x="170" y="90" class="component-label" text-anchor="middle">Switch</text>

                    <!-- Perfect rectangular series circuit wiring -->
                    
                    <!-- Left vertical wire from battery positive to top corner -->
                    <path d="M 90 160 L 90 140" class="wire series-wire" id="series-wire1"/>
                    
                    <!-- Top horizontal wire with switch -->
                    <path d="M 90 140 L 150 140 L 150 120" class="wire series-wire" id="series-wire2"/>
                    <line x1="190" y1="100" x2="200" y2="100" class="wire series-wire" id="series-switch-wire"/>
                    
                    <!-- Complete top wire across -->
                    <path d="M 200 100 L 400 100" class="wire series-wire" id="series-wire3"/>
                    
                    <!-- Right vertical wire down -->
                    <path d="M 400 100 L 400 300" class="wire series-wire" id="series-wire4"/>
                    
                    <!-- Bottom horizontal wire left -->
                    <path d="M 400 300 L 90 300" class="wire series-wire" id="series-wire5"/>
                    
                    <!-- Left vertical wire up to battery negative -->
                    <path d="M 90 300 L 90 240" class="wire series-wire" id="series-wire6"/>

                    <!-- Bulb 1 (on top horizontal side, after switch) -->
                    <circle cx="250" cy="100" r="25" class="bulb series-bulb-on bulb-glass series-bulb-glass" id="series-bulb1"/>
                    <path d="M 235 100 L 245 90 L 255 100 L 265 110 L 245 110 L 235 100" class="filament series-filament-on" id="series-filament1"/>
                    <text x="250" y="140" class="component-label" text-anchor="middle">Bulb 1</text>

                    <!-- Bulb 2 (on right vertical side) -->
                    <circle cx="400" cy="200" r="25" class="bulb series-bulb-on bulb-glass series-bulb-glass" id="series-bulb2"/>
                    <path d="M 385 200 L 395 190 L 405 200 L 415 210 L 395 210 L 385 200" class="filament series-filament-on" id="series-filament2"/>
                    <text x="400" y="240" class="component-label" text-anchor="middle">Bulb 2</text>

                    <!-- Bulb 3 (on bottom horizontal side) -->
                    <circle cx="200" cy="300" r="25" class="bulb series-bulb-on bulb-glass series-bulb-glass" id="series-bulb3"/>
                    <path d="M 185 300 L 195 290 L 205 300 L 215 310 L 195 310 L 185 300" class="filament series-filament-on" id="series-filament3"/>
                    <text x="200" y="340" class="component-label" text-anchor="middle">Bulb 3</text>

                </svg>
            </div>

            <div class="control-panel">
                <!-- Master Switch Control -->
                <div class="control-section">
                    <button class="toggle-btn master-switch-btn master-switch-series" id="series-master-switch">
                        TURN SWITCH OFF
                    </button>
                </div>

                <!-- Bulb Burn Out Controls -->
                <div class="control-section">
                    <div class="control-label">Simulate Bulb Burn Out:</div>
                    <div class="toggle-row">
                        <button class="toggle-btn toggle-btn-series" id="series-burn1">
                            BURN OUT BULB 1
                        </button>
                        <button class="toggle-btn toggle-btn-series" id="series-burn2">
                            BURN OUT BULB 2
                        </button>
                        <button class="toggle-btn toggle-btn-series" id="series-burn3">
                            BURN OUT BULB 3
                        </button>
                    </div>
                    <button class="reset-btn" id="series-reset">RESET ALL BULBS</button>
                </div>

                <!-- Circuit Status -->
                <div class="circuit-status" id="series-status">
                    Switch: <span class="status-on">ON</span> • All bulbs: <span class="status-on">WORKING</span>
                </div>
            </div>

            <div class="caption series-caption">
                Current flows through one path only. If one bulb burns out, the circuit is broken and all bulbs go off.
            </div>
        </div>

        <!-- PARALLEL CIRCUIT PANEL -->
        <div class="panel parallel-panel">
            <div class="panel-header parallel-header">
                <h2>PARALLEL CIRCUIT</h2>
                <div class="subtitle">Multiple Paths</div>
            </div>

            <div class="circuit-container">
                <svg width="100%" height="100%" viewBox="0 0 500 400" id="parallel-circuit">
                    <!-- Battery on left vertical side -->
                    <rect x="50" y="160" width="40" height="80" class="battery battery-fill" rx="3"/>
                    <line x1="50" y1="160" x2="50" y2="240" class="battery" stroke-width="4"/>
                    <line x1="90" y1="160" x2="90" y2="240" class="battery" stroke-width="4"/>
                    <text x="70" y="150" class="voltage-label" text-anchor="middle">9V</text>
                    <text x="45" y="190" class="terminal parallel-terminal" text-anchor="end">+</text>
                    <text x="95" y="230" class="terminal parallel-terminal" text-anchor="start">−</text>

                    <!-- Switch on top horizontal side -->
                    <line x1="150" y1="100" x2="170" y2="80" class="switch-closed" id="parallel-switch-lever"/>
                    <line x1="170" y1="80" x2="190" y2="80" class="switch-closed" id="parallel-switch-line"/>
                    <circle cx="190" cy="80" r="4" fill="#37474f" id="parallel-switch-knob"/>
                    <text x="170" y="70" class="component-label" text-anchor="middle">Switch</text>

                    <!-- Perfect rectangular parallel circuit -->
                    
                    <!-- Top horizontal bus bar -->
                    <path d="M 90 160 L 150 160 L 150 100" class="wire parallel-wire"/>
                    <line x1="190" y1="80" x2="400" y2="80" class="wire parallel-wire" id="parallel-switch-wire"/>
                    
                    <!-- Bottom horizontal bus bar -->
                    <path d="M 90 300 L 400 300" class="wire parallel-wire"/>
                    
                    <!-- Left vertical connection -->
                    <path d="M 90 160 L 90 300" class="wire parallel-wire"/>
                    
                    <!-- Right vertical connection (separate from bulb 3 wires) -->
                    <path d="M 400 80 L 400 300" class="wire parallel-wire" id="parallel-right-vertical"/>

                    <!-- Branch 1 (Bulb 1) - Wires touching the bulb -->
                    <line x1="230" y1="80" x2="230" y2="165" class="wire parallel-wire" id="parallel-wire1-top"/>
                    <line x1="230" y1="215" x2="230" y2="300" class="wire parallel-wire" id="parallel-wire1-bottom"/>
                    
                    <!-- Bulb 1 -->
                    <circle cx="230" cy="190" r="25" class="bulb parallel-bulb-on bulb-glass parallel-bulb-glass" id="parallel-bulb1"/>
                    <path d="M 215 190 L 225 180 L 235 190 L 245 200 L 225 200 L 215 190" class="filament parallel-filament-on" id="parallel-filament1"/>
                    <text x="230" y="230" class="component-label" text-anchor="middle">Bulb 1</text>

                    <!-- Branch 2 (Bulb 2) - Wires touching the bulb -->
                    <line x1="315" y1="80" x2="315" y2="165" class="wire parallel-wire" id="parallel-wire2-top"/>
                    <line x1="315" y1="215" x2="315" y2="300" class="wire parallel-wire" id="parallel-wire2-bottom"/>
                    
                    <!-- Bulb 2 -->
                    <circle cx="315" cy="190" r="25" class="bulb parallel-bulb-on bulb-glass parallel-bulb-glass" id="parallel-bulb2"/>
                    <path d="M 300 190 L 310 180 L 320 190 L 330 200 L 310 200 L 300 190" class="filament parallel-filament-on" id="parallel-filament2"/>
                    <text x="315" y="230" class="component-label" text-anchor="middle">Bulb 2</text>

                    <!-- Branch 3 (Bulb 3) - Separate wires not connected to right vertical -->
                    <line x1="400" y1="80" x2="400" y2="165" class="wire parallel-wire" id="parallel-wire3-top"/>
                    <line x1="400" y1="215" x2="400" y2="300" class="wire parallel-wire" id="parallel-wire3-bottom"/>
                    
                    <!-- Bulb 3 -->
                    <circle cx="400" cy="190" r="25" class="bulb parallel-bulb-on bulb-glass parallel-bulb-glass" id="parallel-bulb3"/>
                    <path d="M 385 190 L 395 180 L 405 190 L 415 200 L 395 200 L 385 190" class="filament parallel-filament-on" id="parallel-filament3"/>
                    <text x="400" y="230" class="component-label" text-anchor="middle">Bulb 3</text>

                </svg>
            </div>

            <div class="control-panel">
                <!-- Master Switch Control -->
                <div class="control-section">
                    <button class="toggle-btn master-switch-btn master-switch-parallel" id="parallel-master-switch">
                        TURN SWITCH OFF
                    </button>
                </div>

                <!-- Bulb Burn Out Controls -->
                <div class="control-section">
                    <div class="control-label">Simulate Bulb Burn Out:</div>
                    <div class="toggle-row">
                        <button class="toggle-btn toggle-btn-parallel" id="parallel-burn1">
                            BURN OUT BULB 1
                        </button>
                        <button class="toggle-btn toggle-btn-parallel" id="parallel-burn2">
                            BURN OUT BULB 2
                        </button>
                        <button class="toggle-btn toggle-btn-parallel" id="parallel-burn3">
                            BURN OUT BULB 3
                        </button>
                    </div>
                    <button class="reset-btn" id="parallel-reset">RESET ALL BULBS</button>
                </div>

                <!-- Circuit Status -->
                <div class="circuit-status" id="parallel-status">
                    Switch: <span class="status-on">ON</span> • All bulbs: <span class="status-on">WORKING</span>
                </div>
            </div>

            <div class="caption parallel-caption">
                Current splits into multiple branches. If one bulb burns out, the others stay lit.
            </div>
        </div>
    </div>

    <script>
        // Initialize circuit states
        let seriesMasterSwitch = true; // true = ON, false = OFF
        let seriesBulbs = [true, true, true]; // true = working, false = burned out
        let parallelMasterSwitch = true; // true = ON, false = OFF
        let parallelBulbs = [true, true, true];

        // Get DOM elements for series circuit
        const seriesMasterSwitchBtn = document.getElementById('series-master-switch');
        const seriesBurn1 = document.getElementById('series-burn1');
        const seriesBurn2 = document.getElementById('series-burn2');
        const seriesBurn3 = document.getElementById('series-burn3');
        const seriesReset = document.getElementById('series-reset');
        const seriesStatus = document.getElementById('series-status');

        // Series circuit elements
        const seriesSwitchLever = document.getElementById('series-switch-lever');
        const seriesSwitchLine = document.getElementById('series-switch-line');
        const seriesSwitchKnob = document.getElementById('series-switch-knob');
        const seriesSwitchWire = document.getElementById('series-switch-wire');
        const seriesBulb1 = document.getElementById('series-bulb1');
        const seriesBulb2 = document.getElementById('series-bulb2');
        const seriesBulb3 = document.getElementById('series-bulb3');
        const seriesFilament1 = document.getElementById('series-filament1');
        const seriesFilament2 = document.getElementById('series-filament2');
        const seriesFilament3 = document.getElementById('series-filament3');
        
        // Get wire elements for broken wire effect in series
        const seriesWires = [
            document.getElementById('series-wire1'),
            document.getElementById('series-wire2'),
            seriesSwitchWire,
            document.getElementById('series-wire3'),
            document.getElementById('series-wire4'),
            document.getElementById('series-wire5'),
            document.getElementById('series-wire6')
        ];

        // Get DOM elements for parallel circuit
        const parallelMasterSwitchBtn = document.getElementById('parallel-master-switch');
        const parallelBurn1 = document.getElementById('parallel-burn1');
        const parallelBurn2 = document.getElementById('parallel-burn2');
        const parallelBurn3 = document.getElementById('parallel-burn3');
        const parallelReset = document.getElementById('parallel-reset');
        const parallelStatus = document.getElementById('parallel-status');

        // Parallel circuit elements
        const parallelSwitchLever = document.getElementById('parallel-switch-lever');
        const parallelSwitchLine = document.getElementById('parallel-switch-line');
        const parallelSwitchKnob = document.getElementById('parallel-switch-knob');
        const parallelSwitchWire = document.getElementById('parallel-switch-wire');
        const parallelRightVertical = document.getElementById('parallel-right-vertical');
        const parallelBulb1 = document.getElementById('parallel-bulb1');
        const parallelBulb2 = document.getElementById('parallel-bulb2');
        const parallelBulb3 = document.getElementById('parallel-bulb3');
        const parallelFilament1 = document.getElementById('parallel-filament1');
        const parallelFilament2 = document.getElementById('parallel-filament2');
        const parallelFilament3 = document.getElementById('parallel-filament3');

        // Get wire elements for broken wire effect in parallel
        const parallelWire1Top = document.getElementById('parallel-wire1-top');
        const parallelWire1Bottom = document.getElementById('parallel-wire1-bottom');
        const parallelWire2Top = document.getElementById('parallel-wire2-top');
        const parallelWire2Bottom = document.getElementById('parallel-wire2-bottom');
        const parallelWire3Top = document.getElementById('parallel-wire3-top');
        const parallelWire3Bottom = document.getElementById('parallel-wire3-bottom');

        // Function to update series circuit display
        function updateSeriesCircuit() {
            // Update master switch button text
            seriesMasterSwitchBtn.textContent = seriesMasterSwitch ? 'TURN SWITCH OFF' : 'TURN SWITCH ON';
            
            // Update switch visual appearance
            if (seriesMasterSwitch) {
                seriesSwitchLever.setAttribute('class', 'switch-closed');
                seriesSwitchLine.setAttribute('class', 'switch-closed');
                seriesSwitchKnob.setAttribute('fill', '#37474f');
            } else {
                seriesSwitchLever.setAttribute('class', 'switch-open');
                seriesSwitchLine.setAttribute('class', 'switch-line-open');
                seriesSwitchKnob.setAttribute('fill', '#78909c');
            }

            // Count working bulbs
            const workingBulbs = seriesBulbs.filter(bulb => bulb).length;
            const allBulbsWorking = workingBulbs === 3;
            const anyBulbBurned = workingBulbs < 3;

            // Update status message
            let statusHTML = '';
            if (!seriesMasterSwitch) {
                statusHTML = `Switch: <span class="status-off">OFF</span> • Circuit: <span class="status-off">DISCONNECTED</span>`;
            } else if (allBulbsWorking) {
                statusHTML = `Switch: <span class="status-on">ON</span> • All bulbs: <span class="status-on">WORKING</span>`;
            } else if (workingBulbs === 0) {
                statusHTML = `Switch: <span class="status-on">ON</span> • Circuit: <span class="status-off">BROKEN</span> (all bulbs burned)`;
            } else {
                statusHTML = `Switch: <span class="status-on">ON</span> • Circuit: <span class="status-off">BROKEN</span> (${3 - workingBulbs} bulb(s) burned)`;
            }
            seriesStatus.innerHTML = statusHTML;

            // Update bulb buttons state
            seriesBurn1.disabled = !seriesMasterSwitch;
            seriesBurn2.disabled = !seriesMasterSwitch;
            seriesBurn3.disabled = !seriesMasterSwitch;
            
            if (!seriesMasterSwitch) {
                seriesBurn1.classList.add('disabled-btn');
                seriesBurn2.classList.add('disabled-btn');
                seriesBurn3.classList.add('disabled-btn');
            } else {
                seriesBurn1.classList.remove('disabled-btn');
                seriesBurn2.classList.remove('disabled-btn');
                seriesBurn3.classList.remove('disabled-btn');
            }

            // Update bulb 1 button text and appearance
            if (seriesBulbs[0]) {
                seriesBurn1.textContent = "BURN OUT BULB 1";
                seriesBurn1.classList.remove('burned');
            } else {
                seriesBurn1.textContent = "FIX BULB 1";
                seriesBurn1.classList.add('burned');
            }

            // Update bulb 2 button text and appearance
            if (seriesBulbs[1]) {
                seriesBurn2.textContent = "BURN OUT BULB 2";
                seriesBurn2.classList.remove('burned');
            } else {
                seriesBurn2.textContent = "FIX BULB 2";
                seriesBurn2.classList.add('burned');
            }

            // Update bulb 3 button text and appearance
            if (seriesBulbs[2]) {
                seriesBurn3.textContent = "BURN OUT BULB 3";
                seriesBurn3.classList.remove('burned');
            } else {
                seriesBurn3.textContent = "FIX BULB 3";
                seriesBurn3.classList.add('burned');
            }

            // Determine if bulbs should be on or off
            const bulbsShouldBeOn = seriesMasterSwitch && allBulbsWorking;
            
            // Update bulb visual appearance
            if (bulbsShouldBeOn) {
                // All bulbs ON
                seriesBulb1.setAttribute('class', 'bulb series-bulb-on bulb-glass series-bulb-glass');
                seriesBulb2.setAttribute('class', 'bulb series-bulb-on bulb-glass series-bulb-glass');
                seriesBulb3.setAttribute('class', 'bulb series-bulb-on bulb-glass series-bulb-glass');
                seriesFilament1.setAttribute('class', 'filament series-filament-on');
                seriesFilament2.setAttribute('class', 'filament series-filament-on');
                seriesFilament3.setAttribute('class', 'filament series-filament-on');
                
                // Show normal wires
                seriesWires.forEach(wire => {
                    if (wire) {
                        wire.setAttribute('class', 'wire series-wire');
                    }
                });
            } else {
                // Some or all bulbs OFF
                seriesBulb1.setAttribute('class', 'bulb series-bulb-off bulb-glass series-bulb-glass');
                seriesBulb2.setAttribute('class', 'bulb series-bulb-off bulb-glass series-bulb-glass');
                seriesBulb3.setAttribute('class', 'bulb series-bulb-off bulb-glass series-bulb-glass');
                seriesFilament1.setAttribute('class', 'filament series-filament-off');
                seriesFilament2.setAttribute('class', 'filament series-filament-off');
                seriesFilament3.setAttribute('class', 'filament series-filament-off');
                
                // Show broken wire effect if switch is on but bulbs are burned
                if (seriesMasterSwitch && anyBulbBurned) {
                    seriesWires.forEach(wire => {
                        if (wire) {
                            wire.setAttribute('class', 'broken-wire');
                        }
                    });
                } else if (!seriesMasterSwitch) {
                    // Switch is off - show normal wires (circuit just disconnected)
                    seriesWires.forEach(wire => {
                        if (wire) {
                            wire.setAttribute('class', 'wire series-wire');
                        }
                    });
                }
            }
        }

        // Function to update parallel circuit display
        function updateParallelCircuit() {
            // Update master switch button text
            parallelMasterSwitchBtn.textContent = parallelMasterSwitch ? 'TURN SWITCH OFF' : 'TURN SWITCH ON';
            
            // Update switch visual appearance
            if (parallelMasterSwitch) {
                parallelSwitchLever.setAttribute('class', 'switch-closed');
                parallelSwitchLine.setAttribute('class', 'switch-closed');
                parallelSwitchKnob.setAttribute('fill', '#37474f');
            } else {
                parallelSwitchLever.setAttribute('class', 'switch-open');
                parallelSwitchLine.setAttribute('class', 'switch-line-open');
                parallelSwitchKnob.setAttribute('fill', '#78909c');
            }

            // Count working bulbs
            const workingBulbs = parallelBulbs.filter(bulb => bulb).length;
            const allBulbsWorking = workingBulbs === 3;

            // Update status message
            let statusHTML = '';
            if (!parallelMasterSwitch) {
                statusHTML = `Switch: <span class="status-off">OFF</span> • Circuit: <span class="status-off">DISCONNECTED</span>`;
            } else if (allBulbsWorking) {
                statusHTML = `Switch: <span class="status-on">ON</span> • All bulbs: <span class="status-on">WORKING</span>`;
            } else if (workingBulbs === 0) {
                statusHTML = `Switch: <span class="status-on">ON</span> • All bulbs: <span class="status-off">BURNED OUT</span>`;
            } else {
                statusHTML = `Switch: <span class="status-on">ON</span> • ${workingBulbs} bulb(s): <span class="status-on">WORKING</span>, ${3 - workingBulbs} bulb(s): <span class="status-off">BURNED</span>`;
            }
            parallelStatus.innerHTML = statusHTML;

            // Update bulb buttons state
            parallelBurn1.disabled = !parallelMasterSwitch;
            parallelBurn2.disabled = !parallelMasterSwitch;
            parallelBurn3.disabled = !parallelMasterSwitch;
            
            if (!parallelMasterSwitch) {
                parallelBurn1.classList.add('disabled-btn');
                parallelBurn2.classList.add('disabled-btn');
                parallelBurn3.classList.add('disabled-btn');
            } else {
                parallelBurn1.classList.remove('disabled-btn');
                parallelBurn2.classList.remove('disabled-btn');
                parallelBurn3.classList.remove('disabled-btn');
            }

            // Determine if each bulb should be on or off
            const bulb1ShouldBeOn = parallelMasterSwitch && parallelBulbs[0];
            const bulb2ShouldBeOn = parallelMasterSwitch && parallelBulbs[1];
            const bulb3ShouldBeOn = parallelMasterSwitch && parallelBulbs[2];

            // Update bulb 1
            if (bulb1ShouldBeOn) {
                parallelBulb1.setAttribute('class', 'bulb parallel-bulb-on bulb-glass parallel-bulb-glass');
                parallelFilament1.setAttribute('class', 'filament parallel-filament-on');
                if (parallelWire1Top) parallelWire1Top.setAttribute('class', 'wire parallel-wire');
                if (parallelWire1Bottom) parallelWire1Bottom.setAttribute('class', 'wire parallel-wire');
            } else {
                parallelBulb1.setAttribute('class', 'bulb parallel-bulb-off bulb-glass parallel-bulb-glass');
                parallelFilament1.setAttribute('class', 'filament parallel-filament-off');
                if (parallelMasterSwitch && !parallelBulbs[0]) {
                    // Bulb burned out - show broken wires
                    if (parallelWire1Top) parallelWire1Top.setAttribute('class', 'broken-wire');
                    if (parallelWire1Bottom) parallelWire1Bottom.setAttribute('class', 'broken-wire');
                } else {
                    // Switch is off - show normal wires
                    if (parallelWire1Top) parallelWire1Top.setAttribute('class', 'wire parallel-wire');
                    if (parallelWire1Bottom) parallelWire1Bottom.setAttribute('class', 'wire parallel-wire');
                }
            }

            // Update bulb 2
            if (bulb2ShouldBeOn) {
                parallelBulb2.setAttribute('class', 'bulb parallel-bulb-on bulb-glass parallel-bulb-glass');
                parallelFilament2.setAttribute('class', 'filament parallel-filament-on');
                if (parallelWire2Top) parallelWire2Top.setAttribute('class', 'wire parallel-wire');
                if (parallelWire2Bottom) parallelWire2Bottom.setAttribute('class', 'wire parallel-wire');
            } else {
                parallelBulb2.setAttribute('class', 'bulb parallel-bulb-off bulb-glass parallel-bulb-glass');
                parallelFilament2.setAttribute('class', 'filament parallel-filament-off');
                if (parallelMasterSwitch && !parallelBulbs[1]) {
                    // Bulb burned out - show broken wires
                    if (parallelWire2Top) parallelWire2Top.setAttribute('class', 'broken-wire');
                    if (parallelWire2Bottom) parallelWire2Bottom.setAttribute('class', 'broken-wire');
                } else {
                    // Switch is off - show normal wires
                    if (parallelWire2Top) parallelWire2Top.setAttribute('class', 'wire parallel-wire');
                    if (parallelWire2Bottom) parallelWire2Bottom.setAttribute('class', 'wire parallel-wire');
                }
            }

            // Update bulb 3 (FIXED: Now shows broken wires when burned out)
            if (bulb3ShouldBeOn) {
                parallelBulb3.setAttribute('class', 'bulb parallel-bulb-on bulb-glass parallel-bulb-glass');
                parallelFilament3.setAttribute('class', 'filament parallel-filament-on');
                if (parallelWire3Top) parallelWire3Top.setAttribute('class', 'wire parallel-wire');
                if (parallelWire3Bottom) parallelWire3Bottom.setAttribute('class', 'wire parallel-wire');
                if (parallelRightVertical) parallelRightVertical.setAttribute('class', 'wire parallel-wire');
            } else {
                parallelBulb3.setAttribute('class', 'bulb parallel-bulb-off bulb-glass parallel-bulb-glass');
                parallelFilament3.setAttribute('class', 'filament parallel-filament-off');
                if (parallelMasterSwitch && !parallelBulbs[2]) {
                    // Bulb burned out - show broken wires for bulb 3's connections
                    if (parallelWire3Top) parallelWire3Top.setAttribute('class', 'broken-wire');
                    if (parallelWire3Bottom) parallelWire3Bottom.setAttribute('class', 'broken-wire');
                    // Keep the right vertical wire intact (it's a separate wire now)
                    if (parallelRightVertical) parallelRightVertical.setAttribute('class', 'wire parallel-wire');
                } else {
                    // Switch is off - show normal wires
                    if (parallelWire3Top) parallelWire3Top.setAttribute('class', 'wire parallel-wire');
                    if (parallelWire3Bottom) parallelWire3Bottom.setAttribute('class', 'wire parallel-wire');
                    if (parallelRightVertical) parallelRightVertical.setAttribute('class', 'wire parallel-wire');
                }
            }

            // Update bulb button text and appearance
            if (parallelBulbs[0]) {
                parallelBurn1.textContent = "BURN OUT BULB 1";
                parallelBurn1.classList.remove('burned');
            } else {
                parallelBurn1.textContent = "FIX BULB 1";
                parallelBurn1.classList.add('burned');
            }

            if (parallelBulbs[1]) {
                parallelBurn2.textContent = "BURN OUT BULB 2";
                parallelBurn2.classList.remove('burned');
            } else {
                parallelBurn2.textContent = "FIX BULB 2";
                parallelBurn2.classList.add('burned');
            }

            if (parallelBulbs[2]) {
                parallelBurn3.textContent = "BURN OUT BULB 3";
                parallelBurn3.classList.remove('burned');
            } else {
                parallelBurn3.textContent = "FIX BULB 3";
                parallelBurn3.classList.add('burned');
            }
        }

        // Event handlers for series circuit
        seriesMasterSwitchBtn.addEventListener('click', () => {
            seriesMasterSwitch = !seriesMasterSwitch;
            updateSeriesCircuit();
        });

        seriesBurn1.addEventListener('click', () => {
            if (seriesMasterSwitch) {
                seriesBulbs[0] = !seriesBulbs[0];
                updateSeriesCircuit();
            }
        });

        seriesBurn2.addEventListener('click', () => {
            if (seriesMasterSwitch) {
                seriesBulbs[1] = !seriesBulbs[1];
                updateSeriesCircuit();
            }
        });

        seriesBurn3.addEventListener('click', () => {
            if (seriesMasterSwitch) {
                seriesBulbs[2] = !seriesBulbs[2];
                updateSeriesCircuit();
            }
        });

        seriesReset.addEventListener('click', () => {
            seriesBulbs = [true, true, true];
            updateSeriesCircuit();
        });

        // Event handlers for parallel circuit
        parallelMasterSwitchBtn.addEventListener('click', () => {
            parallelMasterSwitch = !parallelMasterSwitch;
            updateParallelCircuit();
        });

        parallelBurn1.addEventListener('click', () => {
            if (parallelMasterSwitch) {
                parallelBulbs[0] = !parallelBulbs[0];
                updateParallelCircuit();
            }
        });

        parallelBurn2.addEventListener('click', () => {
            if (parallelMasterSwitch) {
                parallelBulbs[1] = !parallelBulbs[1];
                updateParallelCircuit();
            }
        });

        parallelBurn3.addEventListener('click', () => {
            if (parallelMasterSwitch) {
                parallelBulbs[2] = !parallelBulbs[2];
                updateParallelCircuit();
            }
        });

        parallelReset.addEventListener('click', () => {
            parallelBulbs = [true, true, true];
            updateParallelCircuit();
        });

        // Initialize circuits
        updateSeriesCircuit();
        updateParallelCircuit();

        // Add hover effects
        document.addEventListener('DOMContentLoaded', function() {
            const seriesBulbElements = [seriesBulb1, seriesBulb2, seriesBulb3];
            const parallelBulbElements = [parallelBulb1, parallelBulb2, parallelBulb3];
            
            // Highlight bulbs on hover
            seriesBulbElements.forEach((bulb, index) => {
                bulb.addEventListener('mouseenter', function() {
                    if (seriesMasterSwitch && seriesBulbs[index]) {
                        this.style.strokeWidth = '3';
                        this.style.stroke = '#ff5252';
                    }
                });
                
                bulb.addEventListener('mouseleave', function() {
                    this.style.strokeWidth = '2';
                    this.style.stroke = '#d32f2f';
                });
            });
            
            parallelBulbElements.forEach((bulb, index) => {
                bulb.addEventListener('mouseenter', function() {
                    if (parallelMasterSwitch && parallelBulbs[index]) {
                        this.style.strokeWidth = '3';
                        this.style.stroke = '#2196f3';
                    }
                });
                
                bulb.addEventListener('mouseleave', function() {
                    this.style.strokeWidth = '2';
                    this.style.stroke = '#1976d2';
                });
            });
        });
    </script>
</body>
</html>
