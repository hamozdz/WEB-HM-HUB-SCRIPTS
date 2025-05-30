<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HM HUB Scripts</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@400;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary-text-color: #ffffff;
            --secondary-text-color: #dddddd;
            --accent-color: #009688; /* Teal for buttons */
            --accent-hover-color: #00796b;
            --background-color: #000000;
            --item-bg-color: rgba(255, 255, 255, 0.03);
            --item-hover-bg-color: rgba(255, 255, 255, 0.05);
            --item-border-color: rgba(255, 255, 255, 0.1);
            --code-bg-color: rgba(0,0,0,0.4);
            --code-text-color: #c7f0df; /* Light green for code */
            --disabled-text-color: #aaaaaa;
        }

        body {
            font-family: 'Tajawal', sans-serif;
            margin: 0;
            padding: 0;
            background-color: var(--background-color);
            color: var(--primary-text-color);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            overflow-x: hidden; /* Prevent horizontal scroll */
            position: relative;
        }

        .light-effect {
            position: absolute;
            width: 300px;
            height: 300px;
            border-radius: 50%;
            background: radial-gradient(circle, rgba(255, 255, 255, 0.15) 0%, rgba(255, 255, 255, 0) 70%);
            animation: moveLight 10s infinite linear alternate, pulseLight 5s infinite ease-in-out alternate;
            pointer-events: none;
            z-index: 0;
        }

        @keyframes moveLight {
            0% { transform: translate(-10%, -10%) scale(1); }
            25% { transform: translate(10%, -5%) scale(1.1); }
            50% { transform: translate(5%, 10%) scale(1); }
            75% { transform: translate(-5%, 5%) scale(1.2); }
            100% { transform: translate(-10%, -10%) scale(1); }
        }

        @keyframes pulseLight {
            0% { opacity: 0.6; }
            50% { opacity: 0.9; }
            100% { opacity: 0.6; }
        }

        .content-container {
            position: relative;
            z-index: 1;
            text-align: center;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
            width: 100%;
            max-width: 900px; /* Max width for content area */
        }

        .welcome-message {
            font-size: 1.8rem;
            color: var(--secondary-text-color);
            margin-bottom: 2rem;
            opacity: 0;
            transform: translateY(20px);
            animation: fadeInWelcome 1.5s ease-out forwards;
            font-weight: 400;
        }

        @keyframes fadeInWelcome {
            to { opacity: 1; transform: translateY(0); }
        }

        .welcome-message.move-up {
            animation: moveUpAndFadeWelcome 1s ease-in forwards 0.5s;
        }

        @keyframes moveUpAndFadeWelcome {
            to { opacity: 0; transform: translateY(-80px); }
        }

        .title {
            font-size: 3.2rem;
            font-weight: 700;
            margin-bottom: 1rem;
            text-shadow: 0 0 10px rgba(255, 255, 255, 0.3);
            opacity: 0;
            transform: translateY(20px);
        }

        .title.visible {
            animation: fadeInTitle 1s ease-out forwards;
        }

        @keyframes fadeInTitle {
            to { opacity: 1; transform: translateY(0); }
        }

        .title.move-up-main {
            animation: moveUpMainTitle 1s ease-in forwards;
        }

        @keyframes moveUpMainTitle {
            to { opacity: 0; transform: translateY(-150px); }
        }

        .subtitle, .developer-credit {
            font-size: 1.6rem;
            color: #cccccc;
            font-weight: 400;
            transition: opacity 0.5s ease-out, transform 0.5s ease-out;
        }
        .developer-credit {
             font-size: 1rem;
             color: #bbbbbb;
             margin-top: 1.5rem;
        }

        .subtitle.hidden, .developer-credit.hidden {
            opacity: 0;
            transform: translateY(20px);
        }

        .notification-banner {
            position: fixed;
            bottom: -100px;
            left: 50%;
            transform: translateX(-50%);
            background-color: rgba(0, 150, 50, 0.85);
            color: white;
            padding: 15px 30px;
            border-radius: 8px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
            z-index: 1000;
            font-size: 1.1rem;
            opacity: 0;
            transition: bottom 0.7s cubic-bezier(0.68, -0.55, 0.27, 1.55), opacity 0.7s ease-out;
        }

        .notification-banner.show {
            bottom: 20px;
            opacity: 1;
        }

        /* Scripts Section Styles */
        .scripts-section {
            display: flex; 
            flex-direction: column;
            align-items: center;
            width: 100%;
            opacity: 0;
            transform: translateY(30px);
            transition: opacity 0.8s ease-out 0.2s, transform 0.8s ease-out 0.2s; 
        }
        .scripts-section.visible {
            opacity: 1;
            transform: translateY(0);
        }

        .show-scripts-button {
            background-color: var(--accent-color);
            color: var(--primary-text-color);
            border: none;
            padding: 12px 25px;
            border-radius: 6px;
            font-size: 1.2rem;
            font-weight: 700;
            cursor: pointer;
            transition: background-color 0.3s ease, transform 0.3s ease;
            margin-bottom: 20px;
        }
        .show-scripts-button:hover {
            background-color: var(--accent-hover-color);
            transform: translateY(-2px);
        }
        .show-scripts-button.hidden {
            display: none;
        }

        .scripts-category-title {
            font-size: 1.7rem;
            color: var(--accent-color);
            margin-bottom: 15px;
            margin-top: 10px; /* Added top margin for spacing between button and first title */
            text-align: center;
            opacity: 0;
            font-weight: 700;
            transform: translateY(15px);
            transition: opacity 0.6s ease-out, transform 0.6s ease-out;
        }
        .scripts-category-title.visible {
            opacity: 1;
            transform: translateY(0);
        }


        .scripts-list-container {
            width: 100%;
            max-width: 700px;
            max-height: 60vh; /* Adjusted max-height slightly if two lists are shown */
            overflow-y: auto;
            padding-right: 10px; /* For scrollbar */
            opacity: 0;
            transform: translateY(20px);
            transition: opacity 0.6s ease-out, transform 0.6s ease-out;
        }
        .scripts-list-container.visible {
            opacity: 1;
            transform: translateY(0);
        }
        /* Custom scrollbar for scripts list */
        .scripts-list-container::-webkit-scrollbar {
            width: 8px;
        }
        .scripts-list-container::-webkit-scrollbar-track {
            background: rgba(255,255,255,0.05);
            border-radius: 4px;
        }
        .scripts-list-container::-webkit-scrollbar-thumb {
            background: var(--accent-color);
            border-radius: 4px;
        }
        .scripts-list-container::-webkit-scrollbar-thumb:hover {
            background: var(--accent-hover-color);
        }


        .script-item {
            background-color: var(--item-bg-color);
            border: 1px solid var(--item-border-color);
            border-radius: 8px;
            margin-bottom: 12px;
            overflow: hidden;
        }

        .script-title-button {
            background-color: var(--item-hover-bg-color); 
            color: var(--secondary-text-color);
            padding: 15px;
            width: 100%;
            text-align: right;
            border: none;
            cursor: pointer;
            font-size: 1.1rem;
            font-weight: 700;
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: background-color 0.3s ease;
            border-radius: 8px; 
        }
        .script-title-button:hover {
            background-color: rgba(255, 255, 255, 0.08);
        }
        .script-title-button.expanded {
            border-bottom-left-radius: 0;
            border-bottom-right-radius: 0;
            background-color: rgba(255, 255, 255, 0.09);
        }

        .toggle-icon {
            font-size: 1.5rem;
            line-height: 1;
            transition: transform 0.3s ease;
            color: var(--accent-color);
        }
        .script-title-button.expanded .toggle-icon {
            transform: rotate(45deg);
        }

        .script-details {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.5s ease-in-out, padding 0.5s ease-in-out;
            padding: 0 15px;
            background-color: var(--item-bg-color); 
        }
        .script-details.expanded {
            max-height: 500px; 
            padding: 15px 15px 20px 15px; 
        }

        .script-code-block {
            background-color: var(--code-bg-color);
            color: var(--code-text-color);
            padding: 12px;
            border-radius: 6px;
            margin-bottom: 15px;
            white-space: pre-wrap;
            word-break: break-all;
            text-align: left;
            direction: ltr;
            font-family: 'SFMono-Regular', Consolas, 'Liberation Mono', Menlo, Courier, monospace;
            font-size: 0.9rem;
            border: 1px solid rgba(255,255,255,0.1);
        }
        .script-code-block.not-working {
            color: var(--disabled-text-color); /* Different color for non-working script code */
        }

        .copy-script-button {
            background-color: var(--accent-color);
            color: var(--primary-text-color);
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 1rem;
            font-weight: 500;
            transition: background-color 0.3s ease, transform 0.2s ease;
            display: block;
            margin: 0 auto;
        }
        .copy-script-button:hover {
            background-color: var(--accent-hover-color);
            transform: scale(1.05);
        }
        .copy-script-button:active {
            transform: scale(0.98);
        }


        /* Responsive Styles */
        @media (max-width: 768px) {
            .light-effect { width: 200px; height: 200px; }
            .welcome-message { font-size: 1.5rem; }
            .title { font-size: 2.7rem; }
            .subtitle { font-size: 1.3rem; }
            .developer-credit { font-size: 0.9rem; }
            .notification-banner { font-size: 1rem; padding: 12px 25px; width: 90%; }
            .show-scripts-button { font-size: 1.1rem; padding: 10px 20px;}
            .scripts-category-title { font-size: 1.4rem; }
            .script-title-button {font-size: 1rem; padding: 12px;}
            .script-code-block { font-size: 0.85rem; }
            .copy-script-button { font-size: 0.9rem; padding: 8px 15px;}
        }
        @media (max-width: 480px) {
            .light-effect { width: 150px; height: 150px; }
            .welcome-message { font-size: 1.2rem; }
            .title { font-size: 2.2rem; }
            .subtitle { font-size: 1.1rem; }
            .developer-credit { font-size: 0.8rem; }
            .notification-banner { font-size: 0.9rem; padding: 10px 20px; }
            .scripts-category-title { font-size: 1.2rem; }
            .scripts-list-container { padding-right: 5px; } 
        }
    </style>
</head>
<body>
    <div class="light-effect"></div>

    <div class="content-container">
        <p id="welcomeText" class="welcome-message">مرحبا بك في موقع سكربتات HM HUB نرحب بك</p>
        <h1 id="mainTitle" class="title">HM HUB Scripts</h1>
        <p id="subtitleText" class="subtitle">مركزك المفضل للسكربتات</p>
        <p id="developerCredit" class="developer-credit">تم تطويره من قبل HM HUB</p>

        <div id="scriptsSection" class="scripts-section" style="display: none;">
            <button id="showScriptsButton" class="show-scripts-button">اظهار سكربتات الحالية</button>
            
            <h2 id="workingScriptsTitle" class="scripts-category-title" style="display: none;">سكربتات مدعومة وشغالة</h2>
            <div id="scriptsListContainer" class="scripts-list-container" style="display: none;">
                </div>

            <h2 id="nonWorkingScriptsTitle" class="scripts-category-title" style="display: none; margin-top: 30px;">سكربتات غير مدعومة أو غير شغالة</h2>
            <div id="nonWorkingScriptsListContainer" class="scripts-list-container" style="display: none;">
                </div>
        </div>
    </div>

    <div id="notificationBanner" class="notification-banner">
        تم تحميل بيانات موقع بنجاح
    </div>

    <script>
        // DOM Elements
        const welcomeText = document.getElementById('welcomeText');
        const mainTitle = document.getElementById('mainTitle');
        const subtitleText = document.getElementById('subtitleText');
        const developerCredit = document.getElementById('developerCredit');
        const notificationBanner = document.getElementById('notificationBanner');
        const scriptsSection = document.getElementById('scriptsSection');
        const showScriptsButton = document.getElementById('showScriptsButton');
        
        const workingScriptsTitle = document.getElementById('workingScriptsTitle');
        const scriptsListContainer = document.getElementById('scriptsListContainer');
        
        const nonWorkingScriptsTitle = document.getElementById('nonWorkingScriptsTitle');
        const nonWorkingScriptsListContainer = document.getElementById('nonWorkingScriptsListContainer');

        let mainTitleHasAppeared = false;

        // Script Data
        const workingScriptsData = [
            { title: "bloxfruit|🔥working✅️", code: 'loadstring(game:HttpGet("https://raw.githubusercontent.com/acsu123/HOHO_H/main/Loading_UI"))()' },
            { title: "MM2(SCRIPT1)yarhem|working✅️", code: 'loadstring(game:HttpGet("https://raw.githubusercontent.com/Joystickplays/psychic-octo-invention/main/yarhm.lua", false))()' },
            { title: "MM2(SCRIPT2)overdrive|working✅️", code: 'loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-Overdrive-H-21567"))()' },
            { title: "MM2(SCRIPT3)xhub|🔥working✅️", code: 'loadstring(game:HttpGet("https://raw.githubusercontent.com/Au0yX/Community/main/XhubMM2"))()' },
            { title: "Dex(explorer)|working✅️", code: 'loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-Keyless-Mobile-Dex-Reupload-22707"))()' },
            { title: "roships|working✅️", code: 'loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-rochips-universal-18294"))()' },
            { title: "AFEM(animation)|working(erreur)⚠️", code: 'loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-AFEM-14048"))()' },
            { title: "animation all R6|WORKING✔️", code: 'loadstring(game:HttpGet("https://rawscripts.net/raw/PLACEHOLDER_ANIMATION_R6_URL"))()' }, // New working script
            { title: "game draw|working!", code: 'loadstring(game:HttpGet("https://rawscripts.net/raw/PLACEHOLDER_GAME_DRAW_URL"))()' } // New working script
        ];

        const nonWorkingScriptsData = [
            { title: "Pillar chase|not working⛔️", code: '-- Script for Pillar Chase (Currently not working) --', isWorking: false },
            { title: "betterbypasser|not working⛔️", code: '-- Script for betterbypasser (Currently not working) --', isWorking: false },
            { title: "Brookhaven|not working⛔️", code: '-- Script for Brookhaven (Currently not working) --', isWorking: false },
            { title: "prison life|not working⛔️", code: '-- Script for prison life (Currently not working) --', isWorking: false }
        ];

        // Functions
        function copyToClipboard(text, buttonElement) {
            const textarea = document.createElement('textarea');
            textarea.value = text;
            textarea.style.position = 'fixed'; // Prevent scrolling to bottom of page
            textarea.style.top = '0';
            textarea.style.left = '0';
            textarea.style.opacity = '0'; // Make it invisible
            document.body.appendChild(textarea);
            textarea.focus();
            textarea.select();
            try {
                document.execCommand('copy');
                const originalText = buttonElement.textContent;
                buttonElement.textContent = 'تم النسخ!';
                buttonElement.style.backgroundColor = '#4CAF50'; // Green for success
                setTimeout(() => {
                    buttonElement.textContent = originalText;
                    buttonElement.style.backgroundColor = ''; // Revert color
                }, 2000);
            } catch (err) {
                console.error('Failed to copy: ', err);
                const originalText = buttonElement.textContent;
                buttonElement.textContent = 'فشل النسخ';
                buttonElement.style.backgroundColor = '#F44336'; // Red for error
                setTimeout(() => {
                    buttonElement.textContent = originalText;
                    buttonElement.style.backgroundColor = ''; // Revert color
                }, 2000);
            }
            document.body.removeChild(textarea);
        }

        function createScriptItem(script) {
            const item = document.createElement('div');
            item.className = 'script-item';

            const titleButton = document.createElement('button');
            titleButton.className = 'script-title-button';
            
            const titleSpan = document.createElement('span');
            titleSpan.textContent = script.title;
            
            const toggleIcon = document.createElement('span');
            toggleIcon.className = 'toggle-icon';
            toggleIcon.textContent = '+';
            
            titleButton.appendChild(titleSpan);
            titleButton.appendChild(toggleIcon);

            const details = document.createElement('div');
            details.className = 'script-details';

            const codeBlock = document.createElement('pre');
            const codeElement = document.createElement('code');
            codeElement.className = 'script-code-block';
            if (script.isWorking === false) { // Check if script is explicitly marked as not working
                codeElement.classList.add('not-working');
            }
            codeElement.textContent = script.code;
            codeBlock.appendChild(codeElement);

            const copyButton = document.createElement('button');
            copyButton.className = 'copy-script-button';
            copyButton.textContent = 'نسخ السكربت';
            copyButton.onclick = () => copyToClipboard(script.code, copyButton);

            details.appendChild(codeBlock);
            details.appendChild(copyButton);
            item.appendChild(titleButton);
            item.appendChild(details);

            titleButton.onclick = () => {
                details.classList.toggle('expanded');
                titleButton.classList.toggle('expanded');
                toggleIcon.textContent = details.classList.contains('expanded') ? '×' : '+';
            };
            return item;
        }

        function populateScriptsList(container, data) {
            container.innerHTML = ''; // Clear previous items
            data.forEach(script => {
                container.appendChild(createScriptItem(script));
            });
        }

        // Event Listeners & Initial Load Logic
        window.addEventListener('load', () => {
            // 1. Welcome message animations
            setTimeout(() => {
                if (welcomeText) welcomeText.classList.add('move-up');
            }, 2500);

            // 2. Main title appears
            setTimeout(() => {
                if (mainTitle) mainTitle.classList.add('visible');
                mainTitleHasAppeared = true;
                if (subtitleText) {
                    subtitleText.style.opacity = '1';
                    subtitleText.style.transform = 'translateY(0)';
                }
                if (developerCredit) {
                    developerCredit.style.opacity = '1'; 
                    developerCredit.style.transform = 'translateY(0)';
                }
            }, 3500);

            // 3. Main title moves up, subtitles & dev credit hide
            setTimeout(() => {
                if (mainTitleHasAppeared) {
                    if (mainTitle) mainTitle.classList.add('move-up-main');
                    if (subtitleText) subtitleText.classList.add('hidden');
                    if (developerCredit) developerCredit.classList.add('hidden');

                    setTimeout(() => {
                        if (welcomeText) welcomeText.style.display = 'none';
                        if (mainTitle) mainTitle.style.display = 'none';
                        if (subtitleText) subtitleText.style.display = 'none';
                        if (developerCredit) developerCredit.style.display = 'none';
                    }, 1000); 
                }
            }, 5500);

            // 4. Notification banner appears and then hides
            setTimeout(() => {
                if (mainTitleHasAppeared && notificationBanner) { 
                    notificationBanner.classList.add('show');
                    setTimeout(() => {
                        notificationBanner.classList.remove('show');
                    }, 3000);
                }
            }, 7000);

            // 5. Show the "Scripts Section" (initially just the button) after banner hides
            setTimeout(() => {
                if (scriptsSection) {
                    scriptsSection.style.display = 'flex'; 
                    setTimeout(() => { 
                        scriptsSection.classList.add('visible');
                    }, 20); 
                }
            }, 10000); 
        });

        if (showScriptsButton) {
            showScriptsButton.addEventListener('click', () => {
                showScriptsButton.classList.add('hidden'); 
                
                // Show and populate working scripts
                if (workingScriptsTitle) {
                    workingScriptsTitle.style.display = 'block';
                    setTimeout(() => workingScriptsTitle.classList.add('visible'), 50);
                }
                if (scriptsListContainer) {
                    scriptsListContainer.style.display = 'block'; 
                    populateScriptsList(scriptsListContainer, workingScriptsData);
                    setTimeout(() => scriptsListContainer.classList.add('visible'), 100); 
                }

                // Show and populate non-working scripts after a delay
                setTimeout(() => {
                    if (nonWorkingScriptsTitle) {
                        nonWorkingScriptsTitle.style.display = 'block';
                        setTimeout(() => nonWorkingScriptsTitle.classList.add('visible'), 50);
                    }
                    if (nonWorkingScriptsListContainer) {
                        nonWorkingScriptsListContainer.style.display = 'block'; 
                        populateScriptsList(nonWorkingScriptsListContainer, nonWorkingScriptsData);
                        setTimeout(() => nonWorkingScriptsListContainer.classList.add('visible'), 100);
                    }
                }, 400); // Delay for the second section to appear after the first
            });
        }
        console.log("HM HUB Scripts page loaded with interactive scripts list (v2).");
    </script>
</body>
</html>

