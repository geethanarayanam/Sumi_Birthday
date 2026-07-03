<html lang="te">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>పుట్టినరోజు శుభాకాంక్షలు!</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: #ffe6f2;
            overflow: hidden;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .page {
            position: absolute;
            width: 100%;
            height: 100%;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            padding: 20px;
            transition: opacity 0.5s ease-in-out;
        }

        .hidden {
            display: none !important;
        }

        /* --- PAGE 1: CURTAINS --- */
        #page1 {
            background-color: #333;
            perspective: 1000px;
        }

        .curtain-container {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            display: flex;
            z-index: 10;
        }

        .curtain {
            width: 50%;
            height: 100%;
            background: linear-gradient(to right, #990000, #ff3333, #990000);
            transition: transform 1.5s ease-in-out;
            box-shadow: 0 0 20px rgba(0,0,0,0.5);
        }

        .curtain.left {
            transform-origin: left;
        }

        .curtain.right {
            transform-origin: right;
        }

        /* Curtain open states */
        .open .curtain.left {
            transform: scaleX(0);
        }

        .open .curtain.right {
            transform: scaleX(0);
        }

        .start-btn {
            position: absolute;
            z-index: 20;
            width: 100px;
            height: 100px;
            border-radius: 50%;
            border: 4px solid #fff;
            background: radial-gradient(circle, #ff66cc, #ff0066);
            color: white;
            font-weight: bold;
            font-size: 16px;
            cursor: pointer;
            box-shadow: 0 0 15px rgba(255,255,255,0.8);
            transition: transform 0.3s, opacity 0.5s;
        }

        .start-btn:hover {
            transform: scale(1.1);
        }

        /* --- BUTTON STYLES --- */
        .action-btn {
            margin-top: 30px;
            padding: 15px 30px;
            font-size: 18px;
            font-weight: bold;
            color: white;
            background: linear-gradient(45deg, #ff0066, #ff66cc);
            border: none;
            border-radius: 50px;
            cursor: pointer;
            box-shadow: 0 5px 15px rgba(255, 0, 102, 0.4);
            transition: transform 0.2s, box-shadow 0.2s;
        }

        .action-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(255, 0, 102, 0.6);
        }

        /* --- PAGE 2 & 4: WISHES --- */
        .wishes-title {
            font-size: 2.5rem;
            color: #cc0066;
            margin-bottom: 20px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
        }

        .wishes-text {
            font-size: 1.5rem;
            color: #444;
            max-width: 600px;
            line-height: 1.6;
        }

        /* --- PAGE 3: GIFT BOX --- */
        .gift-container {
            position: relative;
            width: 200px;
            height: 200px;
            cursor: pointer;
            animation: spin 4s linear infinite;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        /* Simple CSS Gift Box */
        .gift-box {
            width: 150px;
            height: 150px;
            background-color: #ff3366;
            position: absolute;
            bottom: 0;
            left: 25px;
            border-radius: 10px;
        }

        .gift-box::before { /* Ribbon */
            content: '';
            position: absolute;
            left: 65px;
            width: 20px;
            height: 100%;
            background-color: #ffcc00;
        }

        .gift-lid {
            width: 170px;
            height: 40px;
            background-color: #e6003d;
            position: absolute;
            top: 20px;
            left: 15px;
            z-index: 2;
            border-radius: 5px;
            box-shadow: 0 5px 5px rgba(0,0,0,0.2);
        }

        .gift-lid::before { /* Ribbon on lid */
            content: '';
            position: absolute;
            left: 75px;
            width: 20px;
            height: 100%;
            background-color: #ffcc00;
        }

        /* Emoji Explosion Particle */
        .particle {
            position: absolute;
            font-size: 30px;
            pointer-events: none;
            animation: explode 1s ease-out forwards;
            z-index: 100;
        }

        @keyframes explode {
            0% {
                transform: translate(0, 0) scale(1);
                opacity: 1;
            }
            100% {
                transform: translate(var(--x), var(--y)) scale(1.5);
                opacity: 0;
            }
        }
    </style>
</head>
<body>

    <!-- Background Music (Using a public copyright-free standard birthday tune) -->
    <audio id="birthday-audio" loop>
        <source src="https://actions.google.com/sounds/v1/ambiences/morning_birds.ogg" type="audio/ogg">
        <!-- Note: Modern browsers require interaction (like clicking your button) to play audio -->
    </audio>

    <!-- PAGE 1: Curtain Slider -->
    <div id="page1" class="page">
        <div class="curtain-container" id="curtain-wrapper">
            <div class="curtain left"></div>
            <div class="curtain right"></div>
        </div>
        <button class="start-btn" id="start-btn">OPEN</button>
    </div>

    <!-- PAGE 2: Initial Birthday Wishes -->
    <div id="page2" class="page hidden">
        <h1 class="wishes-title">Happy Birthday! 🎂</h1>
        <p class="wishes-text">Wishing my wonderful sister-in-law a day filled with love, laughter, and endless happiness!</p>
        <button class="action-btn" id="surprise-btn">Click here for the surprise!</button>
    </div>

    <!-- PAGE 3: Revolving Gift Box -->
    <div id="page3" class="page hidden">
        <h2 class="wishes-title" style="margin-bottom: 50px;">Tap the Gift Box! 🎁</h2>
        <div class="gift-container" id="gift-box">
            <div class="gift-lid"></div>
            <div class="gift-box"></div>
        </div>
        <button class="action-btn hidden" id="blessings-btn" style="margin-top: 50px;">For Blessings, Click Here</button>
    </div>

    <!-- PAGE 4: Telugu Birthday Wishes -->
    <div id="page4" class="page hidden">
        <h1 class="wishes-title">పుట్టినరోజు శుభాకాంక్షలు! 🎉</h1>
        <p class="wishes-text" style="font-size: 1.8rem; color: #b30047; font-weight: bold;">
            నా ప్రియమైన వదినగారికి హృదయపూర్వక పుట్టినరోజు శుభాకాంక్షలు! 💐
        </p>
        <p class="wishes-text" style="margin-top: 20px;">
            మీరు ఎల్లప్పుడూ ఆయురారోగ్యాలతో, సుఖసంతోషాలతో ఉండాలని ఆ దేవుడిని కోరుకుంటున్నాను. ఈ సంవత్సరం మీకు మరిన్ని విజయాలను అందించాలని ఆశిస్తున్నాను! 🌟✨
        </p>
    </div>

    <script>
        // Page Navigation Elements
        const page1 = document.getElementById('page1');
        const page2 = document.getElementById('page2');
        const page3 = document.getElementById('page3');
        const page4 = document.getElementById('page4');

        // Audio element
        const audio = document.getElementById('birthday-audio');
        // fallback to a generic synth birthday trigger if file fails
        audio.src = "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3"; // Placeholder track for music flow

        // Step 1: Curtain Open & Move to Page 2
        document.getElementById('start-btn').addEventListener('click', function() {
            this.style.opacity = '0';
            document.getElementById('curtain-wrapper').classList.add('open');
            
            setTimeout(() => {
                page1.classList.add('hidden');
                page2.classList.remove('hidden');
            }, 1500); // Waits for curtain transition to finish
        });

        // Step 2: Surprise Button -> Page 3
        document.getElementById('surprise-btn').addEventListener('click', function() {
            page2.classList.add('hidden');
            page3.classList.remove('hidden');
        });

        // Step 3: Gift Box Click -> Emojis, Music & Show Blessings Button
        const giftBox = document.getElementById('gift-box');
        const blessingsBtn = document.getElementById('blessings-btn');
        
        giftBox.addEventListener('click', function(e) {
            // Play Birthday Music
            audio.play().catch(err => console.log("Audio play blocked until further interaction."));

            // Stop rotation animation
            giftBox.style.animation = 'none';

            // Pop emojis 🎉 🎊 💎
            const emojis = ['🎉', '🎊', '💎', '🎂', '✨'];
            for (let i = 0; i < 30; i++) {
                createParticle(emojis[Math.floor(Math.random() * emojis.length)]);
            }

            // Show the next button
            blessingsBtn.classList.remove('hidden');
        });

        // Function to generate popping emojis
        function createParticle(emoji) {
            const particle = document.createElement('div');
            particle.classList.add('particle');
            particle.textContent = emoji;

            // Random directions for explosion
            const angle = Math.random() * Math.PI * 2;
            const distance = 100 + Math.random() * 150;
            const x = Math.cos(angle) * distance;
            const y = Math.sin(angle) * distance;

            particle.style.setProperty('--x', `${x}px`);
            particle.style.setProperty('--y', `${y}px`);

            // Center particle on the gift box
            particle.style.left = '50%';
            particle.style.top = '40%';

            page3.appendChild(particle);

            // Remove particle after animation ends
            setTimeout(() => {
                particle.remove();
            }, 1000);
        }

        // Step 4: Blessings Button -> Telugu Wishes
        blessingsBtn.addEventListener('click', function() {
            page3.classList.add('hidden');
            page4.classList.remove('hidden');
        });
    </script>
</body>
</html>
