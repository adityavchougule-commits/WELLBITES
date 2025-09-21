<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>WellBites</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">    //google apis for fonts
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin> 
    <link href="https://fonts.googleapis.com/css2?family=Manrope:wght@300;400;500;600;700&display=swap" rel="stylesheet"> 
    <style>
        :root {
            --primary-bg: #F4F7F6;
            --container-bg: #FFFFFF;
            --text-color: #1a202c;
            --subtle-text-color: #718096;
            --accent-color: #4CAF50; /* Vibrant Green */
            --accent-hover: #45a049;
            --border-color: #e2e8f0;
            --shadow-color: rgba(0, 0, 0, 0.05);
            --shadow-hover-color: rgba(0, 0, 0, 0.1);
            --success-color: #4CAF50;
            --warning-color: #fbbf24;
            --danger-color: #f44336;
            --caution-color: #f59e0b;
        }

        *, *::before, *::after {
            box-sizing: border-box;
        }

        body {
            font-family: 'Manrope', sans-serif;
            background: linear-gradient(120deg, #f1f8e9 0%, #e8f5e9 100%);
            color: var(--text-color);
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: flex-start; /* Changed for scrolling */
            min-height: 100vh;
            padding: 20px;
        }
        
        /* Floating veggies background */
        .background-veggies {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 0;
            pointer-events: none;
        }

        .veggie {
            position: absolute;
            bottom: -150px; /* Start below the screen */
            animation: float 25s infinite linear;
        }

        .veggie svg {
            stroke: var(--accent-color);
            stroke-width: 1.5;
            fill: rgba(255, 255, 255, 0.8);
            width: 100%;
            height: 100%;
        }

        @keyframes float {
            from {
                transform: translateY(0) translateX(0) rotate(0deg);
            }
            to {
                transform: translateY(-120vh) translateX(20vw) rotate(720deg);
            }
        }
        
        .veggie.v1 { width: 80px; left: 5%; animation-duration: 35s; animation-delay: -5s; }
        .veggie.v2 { width: 40px; left: 15%; animation-duration: 45s; animation-delay: -15s; }
        .veggie.v3 { width: 60px; left: 25%; animation-duration: 30s; animation-delay: -2s; transform: translateX(-20vw); }
        .veggie.v4 { width: 70px; left: 40%; animation-duration: 50s; animation-delay: -25s; }
        .veggie.v5 { width: 30px; left: 60%; animation-duration: 40s; animation-delay: -1s; }
        .veggie.v6 { width: 90px; left: 75%; animation-duration: 28s; animation-delay: -8s; transform: translateX(-30vw); }
        .veggie.v7 { width: 55px; left: 90%; animation-duration: 38s; animation-delay: -20s; }
        .veggie.v8 { width: 45px; left: 50%; animation-duration: 55s; animation-delay: -30s; }


        /* Page containers and transition styles */
        .page {
            width: 100%;
            max-width: 1100px;
            transition: opacity 0.4s ease-in-out, transform 0.4s ease-in-out;
            z-index: 1; /* Make sure content is above background */
            position: relative;
        }
        
        .page.hidden {
            display: none;
        }

        .page-hidden {
            opacity: 0;
            pointer-events: none;
            transform: scale(0.98);
        }

        /* Home Page Styling */
        #home-page .container {
            max-width: 500px;
            margin: auto;
            align-self: center; /* Center vertically on home page */
        }

        #home-page h1 {
            font-size: 2.5rem;
            font-weight: 700;
            color: var(--text-color);
        }

        #home-page p {
            font-size: 1.1rem;
            color: var(--subtle-text-color);
            margin-bottom: 2rem;
        }

        /* App Page Styling */
        #app-page .app-layout {
            display: grid;
            grid-template-columns: 350px 1fr;
            gap: 3rem;
            align-items: flex-start;
        }

        .input-panel {
            position: sticky;
            top: 20px;
        }

        .results-panel {
            max-height: calc(100vh - 40px); /* Adjust based on body padding */
            overflow-y: auto;
            padding-right: 15px; /* space for scrollbar */
        }

        /* Custom scrollbar for results panel */
        .results-panel::-webkit-scrollbar {
            width: 8px;
        }
        .results-panel::-webkit-scrollbar-track {
            background: #f1f1f1;
            border-radius: 10px;
        }
        .results-panel::-webkit-scrollbar-thumb {
            background: #ccc;
            border-radius: 10px;
        }
        .results-panel::-webkit-scrollbar-thumb:hover {
            background: #aaa;
        }
        
        .container {
            background-color: var(--container-bg);
            padding: 2.5rem;
            border-radius: 24px;
            box-shadow: 0 10px 25px -5px var(--shadow-color), 0 10px 10px -5px var(--shadow-color);
        }
        
        h1 {
            margin-top: 0;
            color: var(--text-color);
            font-size: 1.75rem;
            font-weight: 600;
        }

        p {
            color: var(--subtle-text-color);
            margin-bottom: 2rem;
        }
        
        #welcome-message {
            font-weight: 500;
            font-size: 1.1rem;
            color: var(--subtle-text-color);
            margin-bottom: 2rem;
        }
        
        .form-group {
            margin-bottom: 1.75rem;
            text-align: left;
        }
        
        label {
            display: block;
            margin-bottom: 0.75rem;
            font-weight: 500;
            font-size: 0.9rem;
        }

        .conditions-container {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
        }

        .condition-label { display: block; }
        .condition-checkbox { display: none; }

        .condition-checkbox + span {
            display: inline-block;
            padding: 8px 16px;
            border: 1px solid var(--border-color);
            border-radius: 20px;
            cursor: pointer;
            transition: all 0.2s ease;
            font-size: 0.9rem;
            font-weight: 500;
        }
        .condition-checkbox + span:hover {
            border-color: var(--accent-color);
        }

        .condition-checkbox:checked + span {
            background-color: var(--accent-color);
            color: white;
            border-color: var(--accent-color);
        }
        
        .input-wrapper {
            position: relative;
        }
        
        .input-icon {
            position: absolute;
            top: 50%;
            left: 14px;
            transform: translateY(-50%);
            color: var(--subtle-text-color);
            pointer-events: none;
        }

        input[type="text"] {
            width: 100%;
            padding: 0.8rem 1rem 0.8rem 2.5rem; /* Space for icon */
            border: 1px solid var(--border-color);
            border-radius: 12px;
            font-size: 1rem;
            font-family: 'Manrope', sans-serif;
            transition: border-color 0.2s, box-shadow 0.2s;
        }

        input[type="text"]:focus {
            outline: none;
            border-color: var(--accent-color);
            box-shadow: 0 0 0 3px rgba(76, 175, 80, 0.2);
        }

        #food-list-container {
            position: absolute;
            top: 110%;
            left: 0;
            right: 0;
            background-color: var(--container-bg);
            border: 1px solid var(--border-color);
            border-radius: 12px;
            max-height: 200px;
            overflow-y: auto;
            z-index: 100;
            box-shadow: 0 10px 15px -3px var(--shadow-color);
        }
        .food-list-hidden { display: none; }
        .food-list-item {
            padding: 0.75rem 1rem;
            cursor: pointer;
            font-size: 0.95rem;
            transition: background-color 0.2s;
        }
        .food-list-item:hover { background-color: #f9fafb; }

        button {
            width: 100%;
            padding: 0.9rem;
            border: none;
            border-radius: 12px;
            background-color: var(--accent-color);
            color: white;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: background-color 0.2s, transform 0.1s;
        }

        button:hover { background-color: var(--accent-hover); }
        button:active { transform: scale(0.98); }
        
        #showAlternativesBtn {
            background-color: transparent;
            color: var(--accent-color);
            border: 2px solid var(--accent-color);
            margin-top: 1rem;
        }
        #showAlternativesBtn:hover {
            background-color: rgba(76, 175, 80, 0.1);
        }

        #result-container {
            display: grid;
            gap: 1.5rem;
            text-align: left;
        }
        
        #results-placeholder {
            text-align: center;
            padding: 4rem 2rem;
            border: 2px dashed var(--border-color);
            border-radius: 16px;
        }
        
        #results-placeholder .placeholder-icon {
             font-size: 3rem;
             color: var(--border-color);
             margin-bottom: 1rem;
        }
         #results-placeholder p {
            color: var(--subtle-text-color);
            font-weight: 500;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .result-card, #final-summary-card, #alternatives-card {
            padding: 1.5rem;
            border-radius: 16px;
            animation: fadeIn 0.5s ease forwards;
            border: 1px solid var(--border-color);
            transition: transform 0.3s ease, box-shadow 0.3s ease, background-color 0.3s ease, backdrop-filter 0.3s ease;
        }

        .result-card:hover, #final-summary-card:hover, #alternatives-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 12px 20px -8px var(--shadow-hover-color);
            background-color: rgba(255, 255, 255, 0.6);
            backdrop-filter: blur(5px);
        }
        
        #final-summary-card {
            background-color: #f9fafb;
        }

        #final-summary-card.good { border-left: 5px solid var(--success-color); }
        #final-summary-card.bad { border-left: 5px solid var(--danger-color); }
        #final-summary-card.normal { border-left: 5px solid var(--warning-color); }
        #final-summary-card.caution { border-left: 5px solid var(--caution-color); }

        .result-card h3, #final-summary-card h3, #alternatives-card h3 {
            margin: 0 0 0.5rem 0;
            font-size: 1.1rem;
            font-weight: 600;
        }
        
        #alternatives-card .alternative-list {
            list-style: none;
            padding: 0;
            margin: 0.5rem 0 0 0;
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
        }

        #alternatives-card .alternative-item {
            background-color: #e8f5e9;
            color: #2e7d32;
            padding: 6px 12px;
            border-radius: 16px;
            font-size: 0.9rem;
            font-weight: 500;
        }
        
        .recommendation {
            font-weight: 700;
            margin-bottom: 0.5rem;
            font-size: 1rem;
        }
        
        .recommendation.good { color: var(--success-color); }
        .recommendation.bad { color: var(--danger-color); }
        .recommendation.normal { color: var(--warning-color); }
        .recommendation.caution { color: var(--caution-color); }

        .explanation {
            font-size: 0.9rem;
            color: var(--subtle-text-color);
            line-height: 1.6;
        }
        
        .result-card.error .explanation {
            color: var(--danger-color);
            font-weight: 500;
        }

        @media (max-width: 900px) {
            #app-page .app-layout {
                grid-template-columns: 1fr;
            }
             .input-panel {
                position: static; /* Remove sticky positioning on smaller screens */
            }
            .results-panel {
                max-height: none; /* Allow it to grow */
                overflow-y: visible;
            }
        }

        @media (max-width: 600px) {
            body { padding: 10px; }
            .container { padding: 1.5rem; }
            h1 { font-size: 1.6rem; }
            #home-page h1 { font-size: 2rem; }
        }
    </style>
</head>
<body>

    <div class="background-veggies">
        <div class="veggie v1">
            <svg viewBox="0 0 100 100"><path d="M69.2,83.4c-9.2,6.9-21.7,9-32.9,5.7c-11.2-3.3-19.9-10.8-24.8-21.1c-4.9-10.3-5.6-22.3-1.9-33 C13.3,24.8,22.2,16,33.4,12c11.2-4,24-3,34,3s16.7,16.5,18.5,28.8c1.8,12.3-3.4,25.2-13.2,33.5C71.1,78.2,70.3,80.4,69.2,83.4z M51.9,13.9c-0.2,0-0.4,0-0.6,0c-0.3,0-0.6,0-0.9,0c-0.3,0-0.6,0-0.9,0c-0.3,0-0.5,0-0.8,0c-0.3,0-0.6,0.1-0.9,0.1c-0.3,0-0.6,0.1-0.8,0.1 c-0.3,0-0.6,0.1-0.9,0.1c-0.3,0.1-0.5,0.1-0.8,0.2c-0.3,0.1-0.6,0.1-0.9,0.2c-0.3,0.1-0.5,0.1-0.8,0.2c-0.3,0.1-0.6,0.2-0.8,0.2 c-0.3,0.1-0.6,0.2-0.8,0.3c-0.3,0.1-0.5,0.2-0.8,0.3c-0.3,0.1-0.5,0.2-0.8,0.3c-0.3,0.1-0.5,0.2-0.8,0.4c-0.2,0.1-0.5,0.2-0.7,0.3 c-0.3,0.1-0.5,0.2-0.7,0.4c-0.2,0.1-0.5,0.2-0.7,0.4c-0.2,0.1-0.5,0.2-0.7,0.4c-0.2,0.1-0.4,0.3-0.7,0.4c-0.2,0.1-0.4,0.3-0.6,0.5 c-0.2,0.1-0.4,0.3-0.6,0.5c-0.2,0.2-0.4,0.3-0.6,0.5c-0.2,0.2-0.4,0.3-0.6,0.5c-0.2,0.2-0.4,0.4-0.5,0.6c-0.2,0.2-0.4,0.4-0.5,0.6c-0.2,0.2-0.3,0.4-0.5,0.6c-0.2,0.2-0.3,0.4-0.5,0.7c-0.1,0.2-0.3,0.4-0.4,0.6c-0.2,0.2-0.3,0.5-0.4,0.7c-0.1,0.2-0.3,0.5-0.4,0.7c-0.1,0.2-0.3,0.5-0.4,0.8c-0.1,0.2-0.2,0.5-0.3,0.8c-0.1,0.2-0.2,0.5-0.3,0.8c-0.1,0.3-0.2,0.5-0.3,0.8c-0.1,0.3-0.2,0.6-0.3,0.9c-0.1,0.3-0.2,0.6-0.2,0.9c-0.1,0.3-0.2,0.6-0.2,0.9c-0.1,0.3-0.1,0.6-0.2,0.9c-0.1,0.3-0.1,0.6-0.2,1c-0.1,0.3-0.1,0.6-0.1,0.9c-0.1,0.3-0.1,0.6-0.1,0.9c0,0.3-0.1,0.6-0.1,0.9c0,0.3,0,0.6-0.1,1c0,0.3,0,0.6-0.1,0.9c0,0.3,0,0.6,0,0.9 c0,0.3,0,0.6,0,0.9c0,0.3,0,0.6,0,1c0,0.3,0,0.6,0,0.9c0,0.3,0,0.7,0,1c0,0.3,0,0.7,0,1c0,0.3,0,0.7,0,1.1c0,0.4,0,0.7,0,1.1 c0,0.4,0,0.7,0,1.1c0,0.4,0,0.8,0,1.2c0,0.4,0,0.8,0,1.2c0,0.4,0,0.8,0,1.2c0,0.4,0.1,0.8,0.1,1.2c0,0.4,0.1,0.8,0.1,1.2c0,0.4,0.1,0.8,0.1,1.2c0.1,0.4,0.1,0.8,0.1,1.2c0.1,0.4,0.1,0.8,0.2,1.2c0.1,0.4,0.2,0.8,0.2,1.2c0.1,0.4,0.2,0.8,0.2,1.2c0.1,0.4,0.2,0.8,0.3,1.2c0.1,0.4,0.2,0.8,0.3,1.1c0.1,0.4,0.3,0.8,0.3,1.2c0.1,0.4,0.3,0.7,0.4,1.1c0.1,0.4,0.3,0.7,0.4,1.1 c0.1,0.4,0.3,0.7,0.4,1.1c0.2,0.4,0.4,0.7,0.5,1.1c0.2,0.4,0.4,0.7,0.5,1.1c0.2,0.4,0.4,0.7,0.6,1c0.2,0.3,0.4,0.7,0.6,1 c0.2,0.3,0.5,0.7,0.6,1c0.2,0.3,0.5,0.6,0.7,0.9c0.2,0.3,0.5,0.6,0.7,0.9c0.2,0.3,0.5,0.6,0.8,0.9c0.3,0.3,0.5,0.6,0.8,0.9 c0.3,0.3,0.6,0.5,0.8,0.8c0.3,0.3,0.6,0.5,0.9,0.8c0.3,0.3,0.6,0.5,0.9,0.7c0.3,0.2,0.6,0.5,0.9,0.7c0.3,0.2,0.7,0.4,1,0.6 c0.3,0.2,0.7,0.4,1,0.6c0.3,0.2,0.7,0.4,1.1,0.6c0.4,0.2,0.7,0.4,1.1,0.5c0.4,0.2,0.8,0.3,1.2,0.5c0.4,0.2,0.8,0.3,1.2,0.4 c0.4,0.1,0.8,0.3,1.2,0.4c0.4,0.1,0.8,0.3,1.2,0.4c0.4,0.1,0.8,0.2,1.2,0.3c0.4,0.1,0.8,0.2,1.2,0.3c0.4,0.1,0.8,0.2,1.2,0.2 c0.4,0.1,0.8,0.1,1.2,0.2c0.4,0.1,0.8,0.1,1.2,0.2c0.4,0.1,0.8,0.1,1.2,0.1c0.4,0,0.8,0.1,1.2,0.1c0.4,0,0.8,0,1.2,0c0.4,0,0.8,0,1.2,0c0.4,0,0.8,0,1.2,0c0.4,0,0.8,0,1.1,0c0.4,0,0.7,0,1.1,0c0.4,0,0.7,0,1.1,0c0.3,0,0.7,0,1,0c0.3,0,0.7-0.1,1-0.1 c0.3,0,0.7-0.1,1-0.1c0.3,0,0.7-0.1,1-0.2c0.3-0.1,0.6-0.1,1-0.2c0.3-0.1,0.6-0.1,0.9-0.2c0.3-0.1,0.6-0.2,0.9-0.2 c0.3-0.1,0.6-0.2,0.9-0.3c0.3-0.1,0.6-0.2,0.8-0.3c0.3-0.1,0.6-0.2,0.8-0.3c0.3-0.1,0.5-0.3,0.8-0.4c0.2-0.1,0.5-0.3,0.7-0.4 c0.2-0.1,0.5-0.3,0.7-0.4c0.2-0.1,0.5-0.3,0.7-0.5c0.2-0.1,0.4-0.3,0.6-0.5c0.2-0.2,0.4-0.4,0.6-0.6c0.2-0.2,0.4-0.4,0.6-0.6 c0.2-0.2,0.3-0.4,0.5-0.6c0.2-0.2,0.3-0.5,0.5-0.7c0.1-0.2,0.3-0.5,0.4-0.7c0.1-0.2,0.3-0.5,0.4-0.7c0.1-0.2,0.3-0.5,0.4-0.8 c0.1-0.3,0.2-0.5,0.3-0.8c0.1-0.3,0.2-0.6,0.3-0.9c0.1-0.3,0.2-0.6,0.2-0.9c0.1-0.3,0.2-0.6,0.2-0.9c0.1-0.3,0.1-0.6,0.2-1 c0.1-0.3,0.1-0.6,0.1-0.9c0.1-0.3,0.1-0.6,0.1-1c0-0.3,0.1-0.6,0.1-0.9c0-0.3,0-0.6,0.1-0.9c0-0.3,0-0.6,0-0.9c0-0.3,0-0.6,0-1 c0-0.3,0-0.6,0-0.9c0-0.3,0-0.7,0-1c0-0.3,0-0.7,0-1c0-0.4,0-0.7,0-1.1c0-0.4,0-0.7,0-1.1c0-0.4,0-0.8,0-1.2c0-0.4-0.1-0.8-0.1-1.2 c0-0.4-0.1-0.8-0.1-1.2c-0.1-0.4-0.1-0.8-0.2-1.2c-0.1-0.4-0.2-0.8-0.2-1.2c-0.1-0.4-0.2-0.8-0.3-1.2c-0.1-0.4-0.2-0.8-0.3-1.2 c-0.1-0.4-0.3-0.8-0.3-1.2c-0.1-0.4-0.3-0.7-0.4-1.1c-0.1-0.4-0.3-0.7-0.4-1.1c-0.2-0.4-0.4-0.7-0.5-1.1c-0.2-0.4-0.4-0.7-0.5-1.1 c-0.2-0.4-0.4-0.7-0.6-1c-0.2-0.3-0.4-0.7-0.6-1c-0.2-0.3-0.5-0.6-0.7-0.9c-0.2-0.3-0.5-0.6-0.7-0.9c-0.2-0.3-0.5-0.6-0.8-0.9 c-0.3-0.3-0.5-0.6-0.8-0.8c-0.3-0.3-0.6-0.5-0.8-0.8c-0.3-0.3-0.6-0.5-0.9-0.7c-0.3-0.2-0.6-0.5-0.9-0.7c-0.3-0.2-0.7-0.4-1-0.6 c-0.3-0.2-0.7-0.4-1-0.6c-0.3-0.2-0.7-0.4-1.1-0.5c-0.4-0.1-0.7-0.3-1.1-0.5c-0.4-0.1-0.8-0.3-1.2-0.4c-0.4-0.1-0.8-0.3-1.2-0.4 c-0.4-0.1-0.8-0.2-1.2-0.3c-0.4-0.1-0.8-0.2-1.2-0.3c-0.4-0.1-0.8-0.2-1.2-0.2c-0.4-0.1-0.8-0.1-1.2-0.2c-0.4,0-0.8-0.1-1.2-0.1 c-0.4,0-0.8-0.1-1.2-0.1c-0.4,0-0.8,0-1.2,0c-0.4,0-0.8,0-1.1,0h-1.1C52.3,13.9,52.1,13.9,51.9,13.9z"/></svg>
        </div>
        <div class="veggie v2">
            <svg viewBox="0 0 100 100"><path d="M50,95C25.2,95,5,74.8,5,50S25.2,5,50,5s45,20.2,45,45S74.8,95,50,95z M50,15c-19.3,0-35,15.7-35,35 s15.7,35,35,35s35-15.7,35-35S69.3,15,50,15z"/><path d="M50,72.5c-12.4,0-22.5-10.1-22.5-22.5S37.6,27.5,50,27.5S72.5,37.6,72.5,50S62.4,72.5,50,72.5z M50,37.5 c-6.9,0-12.5,5.6-12.5,12.5s5.6,12.5,12.5,12.5s12.5-5.6,12.5-12.5S56.9,37.5,50,37.5z"/></svg>
        </div>
        <div class="veggie v3">
            <svg viewBox="0 0 100 100"><path d="M78.6,89.5H21.4c-4.1,0-7.5-3.4-7.5-7.5V18c0-4.1,3.4-7.5,7.5-7.5h57.1c4.1,0,7.5,3.4,7.5,7.5v64 C86.1,86.1,82.7,89.5,78.6,89.5z M21.4,15.5c-1.4,0-2.5,1.1-2.5,2.5v64c0,1.4,1.1,2.5,2.5,2.5h57.1c1.4,0,2.5-1.1,2.5-2.5V18 c0-1.4-1.1-2.5-2.5-2.5H21.4z"/><path d="M68,34.8H32c-1.1,0-2-0.9-2-2s0.9-2,2-2h36c1.1,0,2,0.9,2,2S69.1,34.8,68,34.8z"/><path d="M68,52H32c-1.1,0-2-0.9-2-2s0.9-2,2-2h36c1.1,0,2,0.9,2,2S69.1,52,68,52z"/><path d="M68,69.2H32c-1.1,0-2-0.9-2-2s0.9-2,2-2h36c1.1,0,2,0.9,2,2S69.1,69.2,68,69.2z"/></svg>
        </div>
        <div class="veggie v4">
            <svg viewBox="0 0 100 100"><path d="M50,97.5C23.8,97.5,2.5,76.2,2.5,50S23.8,2.5,50,2.5S97.5,23.8,97.5,50S76.2,97.5,50,97.5z M50,7.5 C26.5,7.5,7.5,26.5,7.5,50S26.5,92.5,50,92.5S92.5,73.5,92.5,50S73.5,7.5,50,7.5z"/><path d="M50,65.2c-8.4,0-15.2-6.8-15.2-15.2s6.8-15.2,15.2-15.2s15.2,6.8,15.2,15.2S58.4,65.2,50,65.2z M50,44.8 c-2.9,0-5.2,2.3-5.2,5.2s2.3,5.2,5.2,5.2s5.2-2.3,5.2-5.2S52.9,44.8,50,44.8z"/></svg>
        </div>
        <div class="veggie v5">
           <svg viewBox="0 0 100 100"><path d="M83.4,69.2c-6.9,9.2-16.1,15.3-26.4,17.4c-10.3,2.1-21.2-0.1-30.7-6c-9.5-6-16.7-15.3-20.3-26.3 c-3.6-11,0.3-23.2,7.8-32.3c7.5-9.1,18.1-14.7,29.6-15.6c11.5-0.9,22.8,2.8,31.4,10.2c8.6,7.4,13.8,17.8,14.6,29.1 C90.1,60.1,87.9,64,83.4,69.2z M82.9,43.2c-0.7-9.5-5-18.2-12.3-24.5c-7.3-6.3-16.9-9.3-26.6-8.5c-9.7,0.8-18.8,5.5-25.2,13.2 c-6.4,7.7-9.5,18-6.5,28c3,10,9,18.1,17.3,23.2c8.3,5,18,6.8,27.1,4.9c9.1-1.9,17.2-7.1,23.1-15.1c3.9-5.3,5.8-10.2,5.8-15.2 C85.6,47.2,84.4,44.7,82.9,43.2z"/></svg>
        </div>
        <div class="veggie v6">
             <svg viewBox="0 0 100 100"><path d="M94.4,50.1L94.4,50.1c0,11.2-9.1,20.3-20.3,20.3H25.9c-11.2,0-20.3-9.1-20.3-20.3v0 c0-11.2,9.1-20.3,20.3-20.3h48.2C85.3,29.8,94.4,38.9,94.4,50.1z"/></svg>
        </div>
        <div class="veggie v7">
            <svg viewBox="0 0 100 100"><path d="M86.1,78.6c-4.1,0-7.5-3.4-7.5-7.5V28.8c0-4.1,3.4-7.5,7.5-7.5s7.5,3.4,7.5,7.5v42.2 C93.6,75.2,90.2,78.6,86.1,78.6z"/><path d="M62.5,78.6c-4.1,0-7.5-3.4-7.5-7.5V28.8c0-4.1,3.4-7.5,7.5-7.5s7.5,3.4,7.5,7.5v42.2 C70,75.2,66.6,78.6,62.5,78.6z"/><path d="M38.9,78.6c-4.1,0-7.5-3.4-7.5-7.5V28.8c0-4.1,3.4-7.5,7.5-7.5s7.5,3.4,7.5,7.5v42.2 C46.4,75.2,43,78.6,38.9,78.6z"/><path d="M15.2,78.6c-4.1,0-7.5-3.4-7.5-7.5V28.8c0-4.1,3.4-7.5,7.5-7.5s7.5,3.4,7.5,7.5v42.2 C22.7,75.2,19.3,78.6,15.2,78.6z"/></svg>
        </div>
        <div class="veggie v8">
            <svg viewBox="0 0 100 100"><path d="M70.3,86.1c-9.1,5.2-20.2,6.4-30.4,3.4C29.6,86.2,21.1,80,16,71.2C10.8,62.4,9.6,51.3,12.6,41 c3-10.3,10-18.7,18.8-23.9c8.8-5.2,19.9-6.4,30.1-3.4c10.3,3,18.8,9.2,23.9,18c5.2,8.8,6.4,19.9,3.4,30.1 C85.8,72.2,79.5,80.8,70.3,86.1z M64.7,82.2c8.1-4.7,13.6-12.4,16.2-21.5c2.6-9.1,1.6-18.9-2.9-27.1c-4.5-8.1-12.2-13.7-21.3-16.3 c-9.1-2.6-18.9-1.6-27.1,2.9c-8.1,4.5-13.7,12.2-16.3,21.3c-2.6,9.1-1.6,18.9,2.9,27.1c4.5,8.1,12.2,13.7,21.3,16.3 C55.3,86.4,62.8,85.6,64.7,82.2z"/></svg>
        </div>
    </div>

    <div id="home-page" class="page">
        <div class="container">
            <h1>Your Personal Nutrition Guide</h1>
            <p>Get instant, personalized food recommendations based on your health conditions. Enter your name to begin.</p>
            <div class="form-group">
                <div class="input-wrapper">
                    <span class="input-icon">
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16">
                            <path d="M3 14s-1 0-1-1 1-4 6-4 6 3 6 4-1 1-1 1H3zm5-6a3 3 0 1 0 0-6 3 3 0 0 0 0 6z"/>
                        </svg>
                    </span>
                    <input type="text" id="userName" placeholder="Your Name" required>
                </div>
            </div>
            <button id="startButton">Get Started</button>
        </div>
    </div>

    <div id="app-page" class="page hidden page-hidden">
        <div class="app-layout">
            <div class="input-panel container">
                 <h1 id="app-title">WellBites</h1>
                <p id="welcome-message"></p>
                <form id="foodForm">
                    <div class="form-group">
                        <label>1. Select Your Health Condition(s)</label>
                        <div id="conditionsContainer" class="conditions-container"></div>
                    </div>
                    <div class="form-group">
                        <label for="foodSearch">2. Find a Food Item</label>
                        <div class="food-search-wrapper input-wrapper">
                            <span class="input-icon">
                                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16">
                                    <path d="M11.742 10.344a6.5 6.5 0 1 0-1.397 1.398h-.001c.03.04.062.078.098.115l3.85 3.85a1 1 0 0 0 1.415-1.414l-3.85-3.85a1.007 1.007 0 0 0-.115-.1zM12 6.5a5.5 5.5 0 1 1-11 0 5.5 5.5 0 0 1 11 0z"/>
                                </svg>
                            </span>
                            <input type="text" id="foodSearch" name="foodItem" placeholder="e.g., Apple, Salmon..." autocomplete="off" required>
                            <div id="food-list-container" class="food-list-hidden"></div>
                        </div>
                    </div>
                    <button type="submit">Get Recommendation</button>
                </form>
            </div>
            <div class="results-panel">
                <div id="result-container">
                    <div id="results-placeholder">
                        <div class="placeholder-icon">🥗</div>
                        <p>Your food recommendations will appear here.</p>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // --- DATASET ---
        const foodData = [
            // Fruits
            { food: "Apple", category: "Fruit", recommendations: { "Diabetes": { status: "Good", explanation: "Low GI, rich in fiber." }, "Hypertension": { status: "Good", explanation: "Contains potassium." }, "Thyroid Disorder": { status: "Good", explanation: "Generally safe." }, "Obesity": { status: "Good", explanation: "Low calorie, high fiber." }, "Fatty Liver (NAFLD)": { status: "Good", explanation: "Supports liver health." } } },
            { food: "Avocado", category: "Fruit", recommendations: { "Diabetes": { status: "Good", explanation: "Low carb, high in healthy fats." }, "Hypertension": { status: "Good", explanation: "Rich in potassium." }, "Thyroid Disorder": { status: "Good", explanation: "Healthy fats are beneficial." }, "Obesity": { status: "Good", explanation: "Promotes satiety." }, "Fatty Liver (NAFLD)": { status: "Good", explanation: "Reduces inflammation." } } },
            { food: "Banana", category: "Fruit", recommendations: { "Diabetes": { status: "Bad", explanation: "High in sugar." }, "Hypertension": { status: "Good", explanation: "Rich in potassium." }, "Thyroid Disorder": { status: "Normal", explanation: "Consume in moderation." }, "Obesity": { status: "Normal", explanation: "Moderate in calories." }, "Fatty Liver (NAFLD)": { status: "Normal", explanation: "Consume in moderation." } } },
            { food: "Berries", category: "Fruit", recommendations: { "Diabetes": { status: "Good", explanation: "Low GI, high in antioxidants." }, "Hypertension": { status: "Good", explanation: "Good for heart health." }, "Thyroid Disorder": { status: "Good", explanation: "Generally safe." }, "Obesity": { status: "Good", explanation: "Low calorie, high fiber." }, "Fatty Liver (NAFLD)": { status: "Good", explanation: "Protects the liver." } } },
            { food: "Orange", category: "Fruit", recommendations: { "Diabetes": { status: "Good", explanation: "Low GI and high fiber." }, "Hypertension": { status: "Good", explanation: "Rich in potassium and vitamin C." }, "Thyroid Disorder": { status: "Good", explanation: "Good source of Vitamin C." }, "Obesity": { status: "Good", explanation: "Low-calorie and high in fiber." }, "Fatty Liver (NAFLD)": { status: "Good", explanation: "May reduce liver inflammation." } } },
            { food: "Grapes", category: "Fruit", recommendations: { "Diabetes": { status: "Normal", explanation: "High in sugar." }, "Hypertension": { status: "Good", explanation: "Contain potassium." }, "Thyroid Disorder": { status: "Good", explanation: "No known issues." }, "Obesity": { status: "Normal", explanation: "High in sugar." }, "Fatty Liver (NAFLD)": { status: "Normal", explanation: "High sugar content." } } },
            
            // Vegetables
            { food: "Leafy Greens", category: "Vegetable", recommendations: { "Diabetes": { status: "Good", explanation: "Extremely low in carbs." }, "Hypertension": { status: "Good", explanation: "Rich in nitrates." }, "Thyroid Disorder": { status: "Good", explanation: "Nutrient-dense." }, "Obesity": { status: "Good", explanation: "Very low in calories." }, "Fatty Liver (NAFLD)": { status: "Good", explanation: "Reduces fat in the liver." } } },
            { food: "Broccoli", category: "Vegetable", recommendations: { "Diabetes": { status: "Good", explanation: "Low carb, high fiber." }, "Hypertension": { status: "Good", explanation: "Rich in potassium." }, "Thyroid Disorder": { status: "Normal", explanation: "Contains goitrogens." }, "Obesity": { status: "Good", explanation: "Low calorie, high fiber." }, "Fatty Liver (NAFLD)": { status: "Good", explanation: "Prevents fat buildup." } } },
            { food: "Sweet Potato", category: "Vegetable", recommendations: { "Diabetes": { status: "Good", explanation: "Lower GI than white potatoes." }, "Hypertension": { status: "Good", explanation: "Rich in potassium." }, "Thyroid Disorder": { status: "Good", explanation: "Provides complex carbs." }, "Obesity": { status: "Good", explanation: "Fiber-rich." }, "Fatty Liver (NAFLD)": { status: "Good", explanation: "Nutrient-dense." } } },
            { food: "Tomatoes", category: "Vegetable", recommendations: { "Diabetes": { status: "Good", explanation: "Low-GI and non-starchy." }, "Hypertension": { status: "Good", explanation: "High in potassium and lycopene." }, "Thyroid Disorder": { status: "Good", explanation: "Good source of vitamins." }, "Obesity": { status: "Good", explanation: "Low in calories." }, "Fatty Liver (NAFLD)": { status: "Good", explanation: "Lycopene can reduce liver inflammation." } } },

            // Proteins
            { food: "Salmon", category: "Lean Protein", recommendations: { "Diabetes": { status: "Good", explanation: "Rich in Omega-3s." }, "Hypertension": { status: "Good", explanation: "Omega-3s lower blood pressure." }, "Thyroid Disorder": { status: "Good", explanation: "Source of selenium." }, "Obesity": { status: "Good", explanation: "Promotes satiety." }, "Fatty Liver (NAFLD)": { status: "Good", explanation: "Reduces liver fat." } } },
            { food: "Chicken Breast", category: "Lean Protein", recommendations: { "Diabetes": { status: "Good", explanation: "Lean protein, no carbs." }, "Hypertension": { status: "Good", explanation: "Low-fat protein." }, "Thyroid Disorder": { status: "Good", explanation: "Provides lean protein." }, "Obesity": { status: "Good", explanation: "High in protein." }, "Fatty Liver (NAFLD)": { status: "Good", explanation: "Essential for liver repair." } } },
            { food: "Eggs", category: "Lean Protein", recommendations: { "Diabetes": { status: "Good", explanation: "High-quality protein." }, "Hypertension": { status: "Good", explanation: "Nutrient-dense." }, "Thyroid Disorder": { status: "Good", explanation: "Source of iodine/selenium." }, "Obesity": { status: "Good", explanation: "Increases fullness." }, "Fatty Liver (NAFLD)": { status: "Good", explanation: "Contains choline." } } },
            { food: "Lentils", category: "Plant Protein", recommendations: { "Diabetes": { status: "Good", explanation: "High fiber, slow sugar release." }, "Hypertension": { status: "Good", explanation: "Rich in potassium." }, "Thyroid Disorder": { status: "Good", explanation: "Plant-based protein." }, "Obesity": { status: "Good", explanation: "Prolonged satiety." }, "Fatty Liver (NAFLD)": { status: "Good", explanation: "Reduces liver strain." } } },
            { food: "Red Meat", category: "Protein", recommendations: { "Diabetes": { status: "Bad", explanation: "High saturated fat." }, "Hypertension": { status: "Bad", explanation: "High in saturated fat." }, "Thyroid Disorder": { status: "Normal", explanation: "Source of iron/B12." }, "Obesity": { status: "Bad", explanation: "High in calories." }, "Fatty Liver (NAFLD)": { status: "Bad", explanation: "Worsens fat accumulation." } } },

            // Grains
            { food: "Oats", category: "Grain", recommendations: { "Diabetes": { status: "Good", explanation: "High in soluble fiber." }, "Hypertension": { status: "Good", explanation: "Lowers cholesterol." }, "Thyroid Disorder": { status: "Good", explanation: "Nutritious whole grain." }, "Obesity": { status: "Good", explanation: "Very filling." }, "Fatty Liver (NAFLD)": { status: "Good", explanation: "Reduces liver strain." } } },
            { food: "Quinoa", category: "Grain", recommendations: { "Diabetes": { status: "Good", explanation: "Complete protein, low GI." }, "Hypertension": { status: "Good", explanation: "High in magnesium." }, "Thyroid Disorder": { status: "Good", explanation: "Gluten-free alternative." }, "Obesity": { status: "Good", explanation: "Promotes satiety." }, "Fatty Liver (NAFLD)": { status: "Good", explanation: "Supports liver health." } } },
            { food: "White Bread", category: "Grain", recommendations: { "Diabetes": { status: "Bad", explanation: "High GI, spikes sugar." }, "Hypertension": { status: "Bad", explanation: "High in sodium." }, "Thyroid Disorder": { status: "Normal", explanation: "Little nutritional benefit." }, "Obesity": { status: "Bad", explanation: "Contributes to weight gain." }, "Fatty Liver (NAFLD)": { status: "Bad", explanation: "Refined carbs." } } },
            
            // Dairy
            { food: "Yogurt", category: "Dairy", recommendations: { "Diabetes": { status: "Good", explanation: "Choose plain Greek yogurt." }, "Hypertension": { status: "Good", explanation: "Source of calcium." }, "Thyroid Disorder": { status: "Good", explanation: "Contains iodine." }, "Obesity": { status: "Good", explanation: "High in protein." }, "Fatty Liver (NAFLD)": { status: "Good", explanation: "Probiotics may help." } } },
            { food: "Milk", category: "Dairy", recommendations: { "Diabetes": { status: "Normal", explanation: "Contains lactose (sugar)." }, "Hypertension": { status: "Good", explanation: "Source of calcium/vitamin D." }, "Thyroid Disorder": { status: "Normal", explanation: "Consume in moderation." }, "Obesity": { status: "Normal", explanation: "Contains calories." }, "Fatty Liver (NAFLD)": { status: "Normal", explanation: "Choose low-fat." } } },

            // Nuts & Seeds
            { food: "Almonds", category: "Nuts & Seeds", recommendations: { "Diabetes": { status: "Good", explanation: "Healthy fats, fiber, magnesium." }, "Hypertension": { status: "Good", explanation: "Rich in magnesium." }, "Thyroid Disorder": { status: "Good", explanation: "Source of selenium/iron." }, "Obesity": { status: "Good", explanation: "Promotes satiety." }, "Fatty Liver (NAFLD)": { status: "Good", explanation: "Protects the liver." } } },
            { food: "Chia Seeds", category: "Nuts & Seeds", recommendations: { "Diabetes": { status: "Good", explanation: "Extremely high in fiber." }, "Hypertension": { status: "Good", explanation: "High in omega-3s." }, "Thyroid Disorder": { status: "Good", explanation: "Provides calcium/magnesium." }, "Obesity": { status: "Good", explanation: "Creates fullness." }, "Fatty Liver (NAFLD)": { status: "Good", explanation: "Benefits the liver." } } },
            
            // Unhealthy
            { food: "French Fries", category: "Unhealthy", recommendations: { "Diabetes": { status: "Bad", explanation: "Refined carbs, unhealthy fats." }, "Hypertension": { status: "Bad", explanation: "High in sodium and fats." }, "Thyroid Disorder": { status: "Bad", explanation: "Promotes inflammation." }, "Obesity": { status: "Bad", explanation: "Extremely high in calories." }, "Fatty Liver (NAFLD)": { status: "Bad", explanation: "Damaging to the liver." } } },
            { food: "Cold Drinks", category: "Unhealthy", recommendations: { "Diabetes": { status: "Bad", explanation: "Loaded with sugar." }, "Hypertension": { status: "Bad", explanation: "Contributes to weight gain." }, "Thyroid Disorder": { status: "Bad", explanation: "Promotes inflammation." }, "Obesity": { status: "Bad", explanation: "Source of empty calories." }, "Fatty Liver (NAFLD)": { status: "Bad", explanation: "Drives fat accumulation." } } }
        ];

        // --- APPLICATION LOGIC ---
        const homePage = document.getElementById('home-page');
        const appPage = document.getElementById('app-page');
        const startButton = document.getElementById('startButton');
        const userNameInput = document.getElementById('userName');
        const welcomeMessage = document.getElementById('welcome-message');

        const form = document.getElementById('foodForm');
        const foodSearchInput = document.getElementById('foodSearch');
        const foodListContainer = document.getElementById('food-list-container');
        const resultContainer = document.getElementById('result-container');
        const conditionsContainer = document.getElementById('conditionsContainer');
        
        const diseases = ["Diabetes", "Hypertension", "Thyroid Disorder", "Obesity", "Fatty Liver (NAFLD)"];
        let currentFood = null;
        let currentConditions = [];

        startButton.addEventListener('click', () => {
            const userName = userNameInput.value.trim();
            if (userName) {
                welcomeMessage.textContent = `Hello, ${userName}!`;
                
                homePage.classList.add('page-hidden');
                
                setTimeout(() => {
                    homePage.classList.add('hidden');
                    appPage.classList.remove('hidden');
                    setTimeout(() => {
                        appPage.classList.remove('page-hidden');
                    }, 50);
                }, 400);

            } else {
                userNameInput.style.borderColor = 'var(--danger-color)';
                setTimeout(() => { userNameInput.style.borderColor = 'var(--border-color)'; }, 2000);
            }
        });

        function populateConditions() {
            conditionsContainer.innerHTML = '';
            diseases.forEach(disease => {
                const label = document.createElement('label');
                label.className = 'condition-label';
                const checkbox = document.createElement('input');
                checkbox.type = 'checkbox';
                checkbox.className = 'condition-checkbox';
                checkbox.value = disease;
                const span = document.createElement('span');
                span.textContent = disease;
                label.appendChild(checkbox);
                label.appendChild(span);
                conditionsContainer.appendChild(label);
            });
        }

        function populateFoodList(foods) {
            foodListContainer.innerHTML = '';
            
            if (foods.length === 0) {
                const noResultItem = document.createElement('div');
                noResultItem.textContent = "No food found";
                noResultItem.style.padding = '0.75rem 1rem';
                noResultItem.style.color = '#a0aec0';
                foodListContainer.appendChild(noResultItem);
            } else {
                 foods.forEach(foodItem => {
                    const item = document.createElement('div');
                    item.className = 'food-list-item';
                    item.textContent = foodItem.food;
                    item.addEventListener('click', () => {
                        foodSearchInput.value = foodItem.food;
                        foodListContainer.classList.add('food-list-hidden');
                    });
                    foodListContainer.appendChild(item);
                });
            }
        }

        form.addEventListener('submit', function(event) {
            event.preventDefault();
            checkFoodRecommendation();
        });

        foodSearchInput.addEventListener('input', function(event) {
            const searchTerm = event.target.value.toLowerCase();
            const filteredFoods = foodData.filter(item => item.food.toLowerCase().includes(searchTerm));
            populateFoodList(filteredFoods);
            if (searchTerm) {
                foodListContainer.classList.remove('food-list-hidden');
            } else {
                foodListContainer.classList.add('food-list-hidden');
            }
        });

        foodSearchInput.addEventListener('focus', function() {
            const searchTerm = this.value.toLowerCase();
            if(searchTerm === '') {
                 populateFoodList(foodData);
                 foodListContainer.classList.remove('food-list-hidden');
            }
        });

        document.addEventListener('click', function(event) {
            if (!event.target.closest('.food-search-wrapper')) {
                foodListContainer.classList.add('food-list-hidden');
            }
        });

        function checkFoodRecommendation() {
            currentConditions = Array.from(document.querySelectorAll('.condition-checkbox:checked')).map(cb => cb.value);
            const foodQuery = foodSearchInput.value.trim().toLowerCase();

            resultContainer.innerHTML = ''; 

            if (currentConditions.length === 0) {
                displayError("Please select at least one health condition.");
                return;
            }
            if (!foodQuery) {
                displayError("Please choose a food from the list.");
                return;
            }

            currentFood = foodData.find(item => item.food.toLowerCase() === foodQuery);

            if (currentFood) {
                if (currentConditions.length > 1) {
                    generateFinalSummary(currentFood, currentConditions);
                }
                displayMultipleResults(currentFood, currentConditions);
                addAlternativesButton();
            } else {
                currentFood = null;
                displayError(`Sorry, "${foodSearchInput.value}" is not in our database.`);
            }
        }

        function generateFinalSummary(food, conditions) {
            const statuses = conditions.map(condition => food.recommendations[condition].status);
            let finalStatus = 'good';
            let summaryText = `This food is generally recommended for all your selected conditions.`;
            let statusText = 'Recommended';
            
            if (statuses.includes('Bad')) {
                finalStatus = 'bad';
                statusText = 'To be Avoided';
                const badFor = conditions.filter(c => food.recommendations[c].status === 'Bad');
                summaryText = `Prioritize this: Avoid this food as it's detrimental for ${badFor.join(', ')}, despite potential benefits for other conditions.`;
            } else if (statuses.includes('Normal')) {
                finalStatus = 'caution';
                statusText = 'Caution Advised';
                const normalFor = conditions.filter(c => food.recommendations[c].status === 'Normal');
                const goodFor = conditions.filter(c => food.recommendations[c].status === 'Good');
                summaryText = `This food is a mixed bag. It's beneficial for ${goodFor.join(', ')} but should only be consumed in moderation for ${normalFor.join(', ')}.`;
            }

            displayFinalSummary(finalStatus, statusText, summaryText);
        }
        
        function displayFinalSummary(statusClass, statusText, explanation) {
            const summaryCard = document.createElement('div');
            summaryCard.id = 'final-summary-card';
            summaryCard.className = statusClass;
            summaryCard.innerHTML = `
                <h3>Overall Recommendation</h3>
                <div class="recommendation ${statusClass}">${statusText}</div>
                <div class="explanation">${explanation}</div>
            `;
            resultContainer.prepend(summaryCard);
        }

        function displayMultipleResults(food, conditions) {
            const resultsWrapper = document.createElement('div');
            resultsWrapper.style.display = 'grid';
            resultsWrapper.style.gap = '1.5rem';

            conditions.forEach(condition => {
                const recommendation = food.recommendations[condition];
                let statusText = '';
                let statusClass = '';

                switch (recommendation.status) {
                    case 'Good': statusText = 'Recommended'; statusClass = 'good'; break;
                    case 'Bad': statusText = 'To be Avoided'; statusClass = 'bad'; break;
                    case 'Normal': statusText = 'Consume in Moderation'; statusClass = 'normal'; break;
                }

                const card = document.createElement('div');
                card.className = `result-card ${statusClass}`;
                card.innerHTML = `
                    <h3>For ${condition}</h3>
                    <div class="recommendation ${statusClass}">${statusText}</div>
                    <div class="explanation">${recommendation.explanation}</div>
                `;
                resultsWrapper.appendChild(card);
            });
            resultContainer.appendChild(resultsWrapper);
        }

        function addAlternativesButton() {
            const existingBtn = document.getElementById('showAlternativesBtn');
            if (existingBtn) existingBtn.remove();

            const alternativesBtn = document.createElement('button');
            alternativesBtn.id = 'showAlternativesBtn';
            alternativesBtn.textContent = 'Find Better Alternatives';
            alternativesBtn.addEventListener('click', showAlternatives);
            resultContainer.appendChild(alternativesBtn);
        }

        function showAlternatives() {
            const existingCard = document.getElementById('alternatives-card');
            if (existingCard) existingCard.remove();
            
            const category = currentFood.category;
            
            const alternatives = foodData.filter(item => {
                if (item.food === currentFood.food || item.category !== category) {
                    return false;
                }
                // Check if the food is "Good" for ALL selected conditions
                return currentConditions.every(condition => item.recommendations[condition]?.status === 'Good');
            });

            const card = document.createElement('div');
            card.id = 'alternatives-card';
            
            let content = `<h3>Healthier Alternatives in the Same Category (${category})</h3>`;

            if (alternatives.length > 0) {
                content += '<ul class="alternative-list">';
                alternatives.forEach(alt => {
                    content += `<li class="alternative-item">${alt.food}</li>`;
                });
                content += '</ul>';
            } else {
                content += `<p class="explanation">No better alternatives found in the ${category} category for your selected conditions.</p>`;
            }
            
            card.innerHTML = content;
            resultContainer.appendChild(card);
            
            const btn = document.getElementById('showAlternativesBtn');
            if (btn) btn.remove(); // Remove button after showing alternatives
        }
        
        function displayError(message) {
            resultContainer.innerHTML = `<div id="results-placeholder" class="result-card error"><p class="explanation">${message}</p></div>`;
        }
        
        document.addEventListener('DOMContentLoaded', () => {
            populateConditions();
            foodData.sort((a, b) => a.food.localeCompare(b.food));
        });
    </script>
</body>
</html>
