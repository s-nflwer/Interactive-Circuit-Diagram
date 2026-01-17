<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Series vs. Parallel Circuits | Grade 9 Science</title>
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
        <p>Grade 9 Science: Comparing Electrical Circuit Configurations</p>
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
                        <filter id="bright-glow" x="-50%" y="-50%" width="200%" height="200%">
                            <feGaussianBlur stdDeviation="4" result="blur"/>
                            <feFlood flood-color="#ffeb3b" flood-opacity="0.7" result="color"/>
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
