<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Find Your Perfect Fitbit!</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <!-- Using Roboto as a proxy for Google Sans for web compatibility -->
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700;900&display=swap" rel="stylesheet">
    <style>
        /* Google Brand Colors: Blue #4285F4, Red #EA4335, Yellow #FBBC05, Green #34A853 */
        body {
            font-family: 'Roboto', sans-serif; /* Changed to Roboto */
            background-color: #F8F9FA; /* Very light gray, almost white */
        }
        .container-card {
            background-color: #ffffff;
            border-radius: 1.5rem; /* More rounded */
            padding: 2.5rem;
            box-shadow: 0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1);
            max-width: 600px;
            margin: 2rem auto;
            min-height: 400px;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
        }
        .question-text {
            font-size: 1.875rem; /* text-3xl */
            font-weight: 700; /* font-bold */
            color: #212121; /* Near-black for strong contrast */
            margin-bottom: 2rem;
            text-align: center;
        }
        .option-button {
            display: block;
            width: 100%;
            padding: 1rem 1.5rem;
            margin-bottom: 1rem;
            border-radius: 0.75rem;
            font-weight: 500; /* font-medium to align with Roboto aesthetic */
            text-align: center;
            transition: all 0.2s ease-in-out;
            cursor: pointer;
            border: 2px solid #D1D5DB; /* Light gray border */
            background-color: #F2F2F2; /* Soft light gray */
            color: #4B5563; /* Darker gray text */
        }
        .option-button:hover {
            border-color: #4285F4; /* Google Blue hover border */
            background-color: #E8F0FE; /* Very light blue hover background */
            color: #1A73E8; /* Slightly darker Google Blue text on hover */
        }
        .option-button.selected {
            background-color: #4285F4; /* Google Blue */
            color: white;
            border-color: #4285F4;
            box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);
            transform: translateY(-2px);
        }
        .action-button {
            background-color: #4285F4; /* Google Blue for primary actions */
            color: white;
            padding: 1rem 2rem;
            border-radius: 0.75rem;
            font-weight: 700; /* font-bold */
            cursor: pointer;
            transition: background-color 0.2s ease-in-out;
            border: none;
            display: inline-flex; /* Use flex to center icon/text */
            align-items: center;
            justify-content: center;
            gap: 0.5rem; /* Space between icon and text */
        }
        .action-button:hover {
            background-color: #1A73E8; /* Darker Google Blue on hover */
        }
        .action-button:disabled {
            background-color: #D1D5DB; /* Grayed out when disabled */
            cursor: not-allowed;
        }
        .text-link-cta {
            color: #4285F4; /* Google Blue for text link CTA */
            font-weight: 600;
            text-decoration: none; /* No underline by default */
            transition: color 0.2s ease-in-out;
            cursor: pointer;
        }
        .text-link-cta:hover {
            color: #1A73E8; /* Darker blue on hover */
            text-decoration: underline;
        }

        .result-section h2 {
            font-size: 2.5rem; /* text-4xl */
            font-weight: 900; /* font-black */
            color: #212121; /* Near-black */
            margin-bottom: 1rem;
            text-align: center;
        }
        .result-section h3 {
            font-size: 2rem; /* text-3xl */
            font-weight: 700; /* font-bold */
            color: #4285F4; /* Changed to Google Blue */
            margin-bottom: 1rem;
            text-align: center;
        }
        .result-section p {
            font-size: 1.125rem; /* text-lg */
            color: #4B5563; /* Darker gray */
            text-align: center;
            margin-bottom: 1.5rem;
        }
        .feature-list {
            list-style: none;
            padding: 0;
            margin: 1.5rem 0;
            text-align: left;
            display: inline-block; /* For centering the list */
        }
        .feature-list li {
            background-color: #E8EAED; /* A bit darker light gray */
            padding: 0.5rem 1rem;
            margin-bottom: 0.5rem;
            border-radius: 0.5rem;
            color: #4B5563;
            font-weight: 400; /* Lighter font weight for list items */
        }
        .credit {
            font-size: 0.875rem; /* text-sm */
            color: #6B7280;
            text-align: center;
            margin-top: 2rem;
        }
        .llm-output-container {
            background-color: #E8F0FE; /* Very light blue for LLM output box */
            border-radius: 0.75rem;
            padding: 1.5rem;
            margin-top: 2rem;
            text-align: left;
            border: 1px dashed #4285F4; /* Google Blue border */
        }
        .loading-spinner {
            border: 4px solid #f3f3f3;
            border-top: 4px solid #4285F4; /* Google Blue */
            border-radius: 50%;
            width: 30px;
            height: 30px;
            animation: spin 1s linear infinite;
            margin: 1rem auto;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
    </style>
</head>
<body class="p-4 md:p-8">
    <!-- Chosen Color Palette: Google Brand Colors (Blue #4285F4, Red #EA4335, Yellow #FBBC05) -->
    <!-- This application does not use Mermaid JS or SVG graphics. All diagrams and visuals are implemented using structured HTML/CSS. -->

    <div id="quiz-container" class="container-card">
        <h1 class="text-4xl font-black text-center mb-6 text-gray-900">Find Your Perfect Fitbit!</h1>

        <div id="start-screen" class="text-center">
            <p class="text-lg text-gray-700 mb-8">
                Answer a few quick questions to discover which Fitbit model is the best match for your lifestyle and goals.
            </p>
            <button id="start-quiz-btn" class="action-button">Start Quiz</button>
        </div>

        <div id="quiz-questions" class="hidden">
            <p id="question-text" class="question-text"></p>
            <div id="options-container" class="grid grid-cols-1 gap-4"></div>
            <div class="flex justify-between mt-6">
                <button id="back-btn" class="option-button w-auto px-6 py-2" disabled>Back</button>
                <button id="next-btn" class="action-button w-auto px-6 py-2" disabled>Next</button>
            </div>
        </div>

        <div id="result-screen" class="hidden result-section text-center">
            <h2 class="mb-4">Your Perfect Fitbit Match:</h2>
            <h3 id="recommended-fitbit" class="mb-4"></h3>
            <p id="fitbit-description" class="text-lg text-gray-700 mb-6"></p>
            <h4 class="text-xl font-bold text-gray-800 mb-4">Key Features:</h4>
            <ul id="fitbit-features" class="feature-list mx-auto"></ul>
            
            <div class="flex flex-col gap-4 mt-8 items-center">
                <a id="google-store-link" href="#" target="_blank" class="action-button no-underline">
                    🛒 View on Google Store
                </a>
                <button id="get-tips-btn" class="text-link-cta mt-4">✨ Get Personalized Tips ✨</button>
            </div>

            <div id="llm-tips-container" class="llm-output-container hidden">
                <p class="font-bold text-lg text-[#4285F4] mb-2">Personalized Advice for You:</p>
                <div id="llm-tips-content"></div>
                <div id="loading-spinner" class="loading-spinner hidden"></div>
            </div>
            <button id="restart-btn" class="action-button mt-8">Start Over</button>
        </div>
    </div>

    <div class="credit">
        <p>&copy; 2025 Fitbit Selector Quiz. All rights reserved.</p>
    </div>

    <script>
        const quizData = [
            {
                question: "What's your primary reason for wanting a Fitbit?",
                options: [
                    { text: "Track daily activity & basic fitness", score: { 'Inspire 3': 1, 'Luxe': 1 } },
                    { text: "Serious fitness tracking & workout insights", score: { 'Charge 6': 1, 'Versa 4': 0.5, 'Sense 2': 0.5 } },
                    { text: "Advanced health monitoring (ECG, stress, skin temp)", score: { 'Sense 2': 1, 'Charge 6': 0.5, 'Versa 4': 0.5 } },
                    { text: "Smartwatch features (apps, calls, payments)", score: { 'Versa 4': 1, 'Sense 2': 1 } },
                ]
            },
            {
                question: "What's your approximate budget?",
                options: [
                    { text: "Under $100", score: { 'Inspire 3': 1, 'Luxe': 0.5 } },
                    { text: "$100 - $200", score: { 'Charge 6': 1, 'Luxe': 1 } },
                    { text: "$200+", score: { 'Sense 2': 1, 'Versa 4': 1 } },
                ]
            },
            {
                question: "Which form factor do you prefer?",
                options: [
                    { text: "Sleek, minimalist tracker band", score: { 'Inspire 3': 1, 'Luxe': 1, 'Charge 6': 1 } },
                    { text: "Traditional smartwatch design", score: { 'Versa 4': 1, 'Sense 2': 1 } },
                ]
            },
            {
                question: "How important is battery life to you?",
                options: [
                    { text: "Very important (multiple days to a week+)", score: { 'Inspire 3': 1, 'Luxe': 1, 'Charge 6': 1, 'Versa 4': 0.5, 'Sense 2': 0.5 } },
                    { text: "Somewhat important (2-4 days is fine)", score: { 'Versa 4': 1, 'Sense 2': 1, 'Charge 6': 0.5 } },
                    { text: "Not a major concern (charge daily if needed)", score: { 'Versa 4': 0.5, 'Sense 2': 0.5 } },
                ]
            },
            {
                question: "Do you need built-in GPS for outdoor activities?",
                options: [
                    { text: "Yes, for tracking runs/rides without phone", score: { 'Charge 6': 1, 'Versa 4': 1, 'Sense 2': 1 } },
                    { text: "No, phone GPS is fine or not needed", score: { 'Inspire 3': 1, 'Luxe': 1 } },
                ]
            },
            {
                question: "How much emphasis do you place on sleep tracking?",
                options: [
                    { text: "Basic sleep stages & score", score: { 'Inspire 3': 1, 'Luxe': 1, 'Charge 6': 0.5 } },
                    { text: "Advanced sleep tools (Sleep Profile, Smart Wake)", score: { 'Charge 6': 1, 'Versa 4': 1, 'Sense 2': 1 } },
                ]
            }
        ];

        const fitbitModels = {
            'Inspire 3': {
                description: "An easy-to-use, stylish tracker for daily activity, sleep, and heart rate, perfect for beginners or those who prefer simplicity.",
                features: ["Daily activity tracking", "24/7 Heart Rate", "Sleep tracking & score", "Up to 10 days battery", "Water resistant"],
                productUrl: "https://store.google.com/product/fitbit_inspire_3?hl=en-US"
            },
            'Luxe': {
                description: "A fashionable fitness and wellness tracker that offers a premium design with core health features, ideal for style-conscious users.",
                features: ["Vibrant AMOLED display", "Stress management score", "24/7 Heart Rate", "Sleep tracking & score", "Up to 5 days battery"],
                productUrl: "https://store.google.com/category/trackers?hl=en-US" // Direct Luxe page not prominently listed on Google Store, linking to general trackers
            },
            'Charge 6': {
                description: "A powerful fitness tracker with advanced health features, including ECG and EDA, designed for serious health and fitness enthusiasts.",
                features: ["ECG app (AFib assessment)", "EDA Scan for stress management", "24/7 Heart Rate & notifications", "Built-in GPS", "Google apps (Maps, Wallet)", "Up to 7 days battery"],
                productUrl: "https://store.google.com/product/fitbit_charge_6?hl=en-US"
            },
            'Versa 4': {
                description: "A balanced smartwatch that combines fitness, health, and smart features, offering a good blend of convenience and insights.",
                features: ["Daily Readiness Score", "24/7 Heart Rate & notifications", "Built-in GPS", "Google apps (Maps, Wallet)", "Calls from wrist (Bluetooth)", "Up to 6 days battery"],
                productUrl: "https://store.google.com/product/fitbit_versa_4?hl=en-US"
            },
            'Sense 2': {
                description: "Fitbit's most advanced health smartwatch, focusing on comprehensive stress management, heart health, and sleep insights.",
                features: ["cEDA sensor for all-day stress detection", "ECG app (AFib assessment)", "Skin temperature sensor", "24/7 Heart Rate & notifications", "Built-in GPS", "Google apps (Maps, Wallet)", "Up to 6 days battery"],
                productUrl: "https://store.google.com/product/fitbit_sense_2?hl=en-US"
            }
        };

        let currentQuestionIndex = 0;
        const userScores = { 'Inspire 3': 0, 'Luxe': 0, 'Charge 6': 0, 'Versa 4': 0, 'Sense 2': 0 };
        let selectedOption = null; // Track selected option per question

        const startScreen = document.getElementById('start-screen');
        const quizQuestions = document.getElementById('quiz-questions');
        const resultScreen = document.getElementById('result-screen');
        const startQuizBtn = document.getElementById('start-quiz-btn');
        const questionText = document.getElementById('question-text');
        const optionsContainer = document.getElementById('options-container');
        const backBtn = document.getElementById('back-btn');
        const nextBtn = document.getElementById('next-btn');
        const recommendedFitbit = document.getElementById('recommended-fitbit');
        const fitbitDescription = document.getElementById('fitbit-description');
        const fitbitFeatures = document.getElementById('fitbit-features');
        const googleStoreLink = document.getElementById('google-store-link'); // New element
        const getTipsBtn = document.getElementById('get-tips-btn');
        const llmTipsContainer = document.getElementById('llm-tips-container');
        const llmTipsContent = document.getElementById('llm-tips-content');
        const loadingSpinner = document.getElementById('loading-spinner');
        const restartBtn = document.getElementById('restart-btn');

        function showScreen(screenId) {
            startScreen.classList.add('hidden');
            quizQuestions.classList.add('hidden');
            resultScreen.classList.add('hidden');
            document.getElementById(screenId).classList.remove('hidden');
        }

        function renderQuestion() {
            const questionData = quizData[currentQuestionIndex];
            questionText.textContent = questionData.question;
            optionsContainer.innerHTML = '';
            nextBtn.disabled = true;

            questionData.options.forEach((option, index) => {
                const button = document.createElement('button');
                button.className = 'option-button';
                button.textContent = option.text;
                button.dataset.index = index;
                button.onclick = () => selectOption(button, index);
                optionsContainer.appendChild(button);
            });

            if (quizData[currentQuestionIndex].selectedAnswerIndex !== undefined) {
                const prevSelectedButton = optionsContainer.children[quizData[currentQuestionIndex].selectedAnswerIndex];
                selectOption(prevSelectedButton, quizData[currentQuestionIndex].selectedAnswerIndex, true);
            }

            backBtn.disabled = currentQuestionIndex === 0;
        }

        function selectOption(button, index, isReloading = false) {
            Array.from(optionsContainer.children).forEach(btn => btn.classList.remove('selected'));
            button.classList.add('selected');

            selectedOption = quizData[currentQuestionIndex].options[index];
            quizData[currentQuestionIndex].selectedAnswerIndex = index;
            nextBtn.disabled = false;
        }

        function calculateScores() {
            for (const key in userScores) {
                userScores[key] = 0;
            }

            quizData.forEach(q => {
                if (q.selectedAnswerIndex !== undefined) {
                    const selectedOpt = q.options[q.selectedAnswerIndex];
                    if (selectedOpt && selectedOpt.score) {
                        for (const model in selectedOpt.score) {
                            userScores[model] += selectedOpt.score[model];
                        }
                    }
                }
            });
        }

        function determineRecommendation() {
            calculateScores();

            let bestFitbit = null;
            let highestScore = -1;

            for (const model in userScores) {
                if (userScores[model] > highestScore) {
                    highestScore = userScores[model];
                    bestFitbit = model;
                }
            }

            if (bestFitbit === null || highestScore === 0) {
                 if (userScores['Charge 6'] > 0) return 'Charge 6';
                 if (userScores['Versa 4'] > 0) return 'Versa 4';
                 return 'Inspire 3';
            }

            const tiedModels = Object.keys(userScores).filter(model => userScores[model] === highestScore);
            if (tiedModels.length > 1) {
                if (tiedModels.includes('Charge 6')) return 'Charge 6';
                if (tiedModels.includes('Versa 4')) return 'Versa 4';
                if (tiedModels.includes('Sense 2')) return 'Sense 2';
                if (tiedModels.includes('Luxe')) return 'Luxe';
                return 'Inspire 3';
            }

            return bestFitbit;
        }

        function displayResult() {
            const recommendation = determineRecommendation();
            const fitbitInfo = fitbitModels[recommendation];

            recommendedFitbit.textContent = recommendation;
            fitbitDescription.textContent = fitbitInfo.description;
            fitbitFeatures.innerHTML = '';
            fitbitInfo.features.forEach(feature => {
                const li = document.createElement('li');
                li.textContent = feature;
                fitbitFeatures.appendChild(li);
            });
            
            // Set the Google Store link
            googleStoreLink.href = fitbitInfo.productUrl;

            llmTipsContainer.classList.add('hidden'); // Hide LLM output until requested
            llmTipsContent.innerHTML = ''; // Clear previous LLM content
            showScreen('result-screen');
        }

        async function fetchGeminiTips(retries = 3, delay = 1000) {
            const recommended = recommendedFitbit.textContent;
            const primaryReasonIndex = quizData[0].selectedAnswerIndex;
            const primaryReason = quizData[0].options[primaryReasonIndex].text;

            llmTipsContainer.classList.remove('hidden');
            llmTipsContent.innerHTML = '<p class="text-center text-gray-500">Generating personalized tips...</p>';
            loadingSpinner.classList.remove('hidden');
            getTipsBtn.disabled = true;

            let chatHistory = [];
            const prompt = `Given that a user is interested in a Fitbit ${recommended} and their primary reason for wanting a Fitbit is to "${primaryReason}", provide 3-5 concise, actionable tips or ideas on how they can best utilize their new Fitbit for their specific goal. Focus on practical usage advice.`;
            chatHistory.push({ role: "user", parts: [{ text: prompt }] });
            const payload = { contents: chatHistory };
            const apiKey = "";
            const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-05-20:generateContent?key=${apiKey}`;

            try {
                const response = await fetch(apiUrl, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });

                if (!response.ok) {
                    if (response.status === 429 && retries > 0) {
                        await new Promise(res => setTimeout(res, delay));
                        return fetchGeminiTips(retries - 1, delay * 2);
                    }
                    throw new Error(`API error: ${response.status} ${response.statusText}`);
                }

                const result = await response.json();
                if (result.candidates && result.candidates.length > 0 &&
                    result.candidates[0].content && result.candidates[0].content.parts &&
                    result.candidates[0].content.parts.length > 0) {
                    const text = result.candidates[0].content.parts[0].text;
                    llmTipsContent.innerHTML = text.replace(/\n/g, '<br>');
                } else {
                    llmTipsContent.innerHTML = '<p class="text-red-500">Could not retrieve tips. Please try again.</p>';
                }
            } catch (error) {
                llmTipsContent.innerHTML = `<p class="text-red-500">Error: ${error.message}. Please try again.</p>`;
            } finally {
                loadingSpinner.classList.add('hidden');
                getTipsBtn.disabled = false;
            }
        }

        startQuizBtn.addEventListener('click', () => {
            showScreen('quiz-questions');
            renderQuestion();
        });

        nextBtn.addEventListener('click', () => {
            if (selectedOption) {
                currentQuestionIndex++;
                selectedOption = null;
                if (currentQuestionIndex < quizData.length) {
                    renderQuestion();
                } else {
                    displayResult();
                }
            }
        });

        backBtn.addEventListener('click', () => {
            if (currentQuestionIndex > 0) {
                currentQuestionIndex--;
                selectedOption = null;
                renderQuestion();
            }
        });

        getTipsBtn.addEventListener('click', fetchGeminiTips);

        restartBtn.addEventListener('click', () => {
            currentQuestionIndex = 0;
            selectedOption = null;
            for (const key in userScores) {
                userScores[key] = 0;
            }
            quizData.forEach(q => q.selectedAnswerIndex = undefined);
            llmTipsContainer.classList.add('hidden');
            llmTipsContent.innerHTML = '';
            showScreen('start-screen');
        });

        showScreen('start-screen');
    </script>
</body>
</html>
```
