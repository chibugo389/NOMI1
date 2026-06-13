
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MindSpace - Integrated Venting Prototype</title>
    <style>
        :root {
            --bg-color: #f4f7f6;
            --primary-color: #6c5ce7;
            --secondary-color: #a29bfe;
            --text-dark: #2d3436;
            --card-bg: #ffffff;
            --accent-green: #a29bfe; /* Placeholder for new recommendation color */
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-dark);
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }

        /* Simulating a mobile app frame */
        .phone-container {
            width: 375px;
            height: 750px;
            background: var(--card-bg);
            border-radius: 40px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.15);
            border: 8px solid #2d3436;
            overflow-y: auto;
            position: relative;
            display: flex;
            flex-direction: column;
        }

        .phone-container::-webkit-scrollbar {
            width: 4px;
        }
        .phone-container::-webkit-scrollbar-thumb {
            background: var(--secondary-color);
            border-radius: 10px;
        }

        /* Header / Welcome Section */
        .header {
            padding: 25px 20px 15px 20px;
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            color: white;
            border-bottom-left-radius: 25px;
            border-bottom-right-radius: 25px;
        }

        .header h1 {
            margin: 0;
            font-size: 1.5rem;
        }

        .header p {
            margin: 5px 0 0 0;
            opacity: 0.9;
            font-size: 0.9rem;
        }

        /* App Content */
        .content {
            padding: 20px;
            flex: 1;
        }

        .card {
            background: white;
            border-radius: 15px;
            padding: 15px;
            margin-bottom: 20px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
        }

        h3 {
            margin-top: 0;
            color: var(--primary-color);
            font-size: 1.1rem;
        }

        /* Mood Tracker Analytics */
        .mood-stat {
            font-size: 1.5rem;
            font-weight: bold;
            color: #2d3436;
            margin: 10px 0;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        /* AI Vent Section - Integrated Layout */
        .vent-area-integrated {
            display: flex;
            flex-direction: column;
            gap: 15px;
            margin-top: 10px;
        }

        .vent-prompt-main {
            font-weight: bold;
            text-align: center;
            color: #4c4a85; /* Purple tone to match */
            font-size: 1rem;
        }

        /* Venting Options (Split) */
        .vent-options {
            display: flex;
            gap: 15px;
            justify-content: space-around;
        }

        /* Audio Section */
        .vent-option-card {
            background: #f9f9ff;
            border: 2px solid #e1e1fb;
            border-radius: 15px;
            width: 45%;
            padding: 15px;
            text-align: center;
            cursor: pointer;
            transition: all 0.2s ease;
        }

        .vent-option-card:hover {
            border-color: var(--primary-color);
            background: #f0f0ff;
        }

        .vent-icon {
            font-size: 2rem;
            margin-bottom: 10px;
            color: var(--primary-color);
        }

        .vent-option-card strong {
            display: block;
            font-size: 0.9rem;
            margin-bottom: 5px;
        }

        .vent-option-card p {
            font-size: 0.75rem;
            margin: 0;
            color: #636e72;
        }

        /* Dynamic Waveform Simulation */
        #audio-waveform {
            margin-top: 10px;
            height: 20px;
            display: none; /* Initially hidden */
        }

        .waveform-bar {
            background-color: var(--primary-color);
            width: 4px;
            height: 10px;
            display: inline-block;
            margin: 0 1px;
            border-radius: 2px;
            animation: waveform_pulse 1s ease-in-out infinite;
        }

        @keyframes waveform_pulse {
            0% { height: 10px; }
            50% { height: 20px; }
            100% { height: 10px; }
        }

        /* Text Section */
        .vent-text-area {
            background: #fdfdff;
            border: 2px solid #e1e1fb;
            border-radius: 15px;
            width: 45%;
            padding: 15px;
            display: flex;
            flex-direction: column;
        }

        .vent-text-area textarea {
            width: 100%;
            height: 80px;
            border: 1px solid #ddd;
            border-radius: 10px;
            padding: 10px;
            box-sizing: border-box;
            resize: none;
            font-family: inherit;
            margin-top: 5px;
            font-size: 0.85rem;
        }

        .submit-btn {
            background-color: var(--primary-color);
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 8px;
            cursor: pointer;
            margin-top: 10px;
            font-weight: bold;
            font-size: 0.85rem;
            transition: background 0.2s;
        }

        /* Recommendations Section (Triggered) */
        .recommendations {
            display: none;
            animation: fadeIn 0.5s ease forwards;
            background-color: #f7fff7; /* A subtle calm green */
            border-color: #c9f9c9;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .rec-header {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-bottom: 10px;
        }

        .rec-header .accent-color {
            color: var(--primary-color);
        }

        .rec-item {
            background: #ffffff;
            padding: 10px;
            border-left: 4px solid var(--primary-color);
            margin-bottom: 10px;
            border-radius: 4px;
            font-size: 0.9rem;
        }
    </style>
</head>
<body>

    <div class="phone-container">
        <div class="header">
            <h1 id="welcome-message">Hey, John!</h1>
            <p>Welcome back to your safe space.</p>
        </div>

        <div class="content">
            
            <div class="card">
                <h3>Weekly Mood Average</h3>
                <div class="mood-stat">
                    <span>😐 Calming down</span>
                    <span style="font-size: 0.9rem; font-weight: normal; color: #636e72;">(Based on 5 days)</span>
                </div>
            </div>

            <div class="card">
                <div class="vent-area-integrated">
                    <p class="vent-prompt-main">VENT YOUR ANGER: SPEAK OR TYPE</p>

                    <div class="vent-options">
                        <div class="vent-option-card" onclick="simulateRecording()">
                            <div class="vent-icon">🎙️</div>
                            <strong>Speak Your Mind</strong>
                            <p>Tap to start recording audio.</p>
                            
                            <div id="audio-waveform">
                                <div class="waveform-bar"></div>
                                <div class="waveform-bar" style="animation-delay: 0.1s"></div>
                                <div class="waveform-bar" style="animation-delay: 0.2s"></div>
                                <div class="waveform-bar" style="animation-delay: 0.1s"></div>
                                <div class="waveform-bar"></div>
                            </div>
                        </div>

                        <div class="vent-text-area">
                            <strong style="font-size: 0.9rem; text-align: center;">Type Your Feelings</strong>
                            <textarea id="vent-input" placeholder="I'm just so frustrated with..."></textarea>
                            <button class="submit-btn" onclick="submitVentText()">Send Text</button>
                        </div>
                    </div>
                </div>
            </div>

            <div id="recommendations-section" class="card recommendations">
                <div class="rec-header">
                    <span class="accent-color" style="font-size: 1.2rem;">🎧</span>
                    <h3>RECOMMENDED FOR YOU</h3>
                </div>
                
                <div class="rec-item">
                    <strong>Podcast:</strong> "Managing Anger in 5 Minutes"
                </div>
                <div class="rec-item">
                    <strong>Watch:</strong> "Channeling Frustration into Action"
                </div>
            </div>

            </div>
    </div>

    <script>
        // Simulation functions for the integrated venting
        
        function submitVentText() {
            const ventText = document.getElementById('vent-input').value.trim();
            if (ventText === "") {
                alert("Please write something to vent!");
                return;
            }
            processVentResponse("text");
        }

        function simulateRecording() {
            const waveform = document.getElementById('audio-waveform');
            const ventInput = document.getElementById('vent-input');

            // Hide text box and show waveform animation
            ventInput.style.display = 'none';
            waveform.style.display = 'block';
            
            // In a real prototype, you would listen for speech end.
            // Here, we just wait a moment.
            alert("AI Companion: Listening... Take your time.");
            
            // Simulating 5 seconds of speaking
            setTimeout(() => {
                alert("AI Companion: Audio received. Processing...");
                waveform.style.display = 'none';
                ventInput.style.display = 'block'; // reset
                processVentResponse("audio");
            }, 5000);
        }

        // Shared response processing logic
        function processVentResponse(type) {
            // Simulate AI acknowledging the venting and changing UI
            let message = type === "text" 
                ? "AI Companion: Thank you for sharing your thoughts. Let's find some calm."
                : "AI Companion: Thank you for speaking your mind. Take a deep breath. Let's look at some things to help you unwind.";
            
            alert(message);
            
            // Show the recommendations section
            document.getElementById('recommendations-section').style.display = 'block';
            
            // Clear the text box (if relevant)
            document.getElementById('vent-input').value = "";
        }
    </script>

</body>
</html>
