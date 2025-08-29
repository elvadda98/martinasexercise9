<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vocabulary Game: Everyday & Specialized Terms</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #8e44ad 0%, #3498db 100%);
            min-height: 100vh;
            padding: 20px;
            color: #333;
        }

        .container {
            max-width: 1100px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #8e44ad, #3498db);
            color: white;
            padding: 30px;
            text-align: center;
            position: relative;
        }

        .header::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><circle cx="20" cy="20" r="2" fill="rgba(255,255,255,0.1)"/><circle cx="80" cy="30" r="1.5" fill="rgba(255,255,255,0.1)"/><circle cx="40" cy="70" r="1" fill="rgba(255,255,255,0.1)"/><circle cx="90" cy="80" r="2.5" fill="rgba(255,255,255,0.1)"/></svg>');
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            position: relative;
            z-index: 1;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        .header p {
            font-size: 1.2em;
            opacity: 0.9;
            position: relative;
            z-index: 1;
        }

        .nav-buttons {
            display: flex;
            justify-content: center;
            gap: 10px;
            padding: 20px;
            background: #f8f9fa;
            flex-wrap: wrap;
        }

        .nav-btn {
            padding: 12px 24px;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }

        .nav-btn.active {
            background: linear-gradient(135deg, #8e44ad, #3498db);
            color: white;
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(142,68,173,0.4);
        }

        .nav-btn:not(.active) {
            background: white;
            color: #666;
        }

        .nav-btn:hover:not(.active) {
            background: #e9ecef;
            transform: translateY(-1px);
        }

        .game-section {
            display: none;
            padding: 30px;
            min-height: 400px;
        }

        .game-section.active {
            display: block;
            animation: fadeIn 0.5s ease-in;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .word-bank {
            background: linear-gradient(135deg, #f5f7fa, #e8f4f2);
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 25px;
            border: 2px solid #8e44ad;
            box-shadow: 0 4px 15px rgba(142,68,173,0.2);
        }

        .word-bank h3 {
            color: #8e44ad;
            margin-bottom: 15px;
            text-align: center;
            font-size: 1.4em;
        }

        .word-options {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            justify-content: center;
        }

        .word-option {
            background: linear-gradient(135deg, #8e44ad, #3498db);
            color: white;
            padding: 10px 18px;
            border-radius: 20px;
            font-weight: bold;
            font-size: 16px;
            box-shadow: 0 3px 10px rgba(142,68,173,0.3);
            transition: all 0.3s ease;
            cursor: default;
        }

        .word-option:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(142,68,173,0.4);
        }

        .question {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 20px;
            border-left: 5px solid #8e44ad;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
        }

        .question h3 {
            color: #8e44ad;
            margin-bottom: 15px;
            font-size: 1.3em;
        }

        .fill-blank {
            background: #fff;
            border: 2px solid #ddd;
            border-radius: 8px;
            padding: 8px 12px;
            font-size: 16px;
            margin: 0 5px;
            min-width: 120px;
            transition: border-color 0.3s ease;
        }

        .fill-blank.correct {
            border-color: #4CAF50;
            background: #e8f5e8;
        }

        .fill-blank.incorrect {
            border-color: #f44336;
            background: #ffeaea;
        }

        .options {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }

        .option {
            padding: 15px 20px;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .option:hover {
            border-color: #8e44ad;
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(142,68,173,0.2);
        }

        .option.selected {
            background: #8e44ad;
            color: white;
            border-color: #8e44ad;
        }

        .option.correct {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
        }

        .option.incorrect {
            background: #f44336;
            color: white;
            border-color: #f44336;
        }

        .matching-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-top: 20px;
        }

        .match-column h4 {
            text-align: center;
            margin-bottom: 15px;
            color: #8e44ad;
            font-size: 1.2em;
        }

        .match-item {
            padding: 15px;
            margin: 8px 0;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .match-item:hover {
            border-color: #8e44ad;
            transform: translateY(-1px);
            box-shadow: 0 4px 15px rgba(142,68,173,0.2);
        }

        .match-item.selected {
            background: #e8f4f2;
            border-color: #8e44ad;
            transform: translateY(-1px);
        }

        .match-item.matched {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
            cursor: default;
        }

        .check-btn {
            background: linear-gradient(135deg, #8e44ad, #3498db);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 20px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(142,68,173,0.3);
        }

        .check-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(142,68,173,0.4);
        }

        .feedback {
            margin-top: 15px;
            padding: 15px;
            border-radius: 10px;
            font-weight: bold;
            text-align: center;
            animation: slideIn 0.3s ease;
        }

        @keyframes slideIn {
            from { transform: translateX(-20px); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        .feedback.correct {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }

        .feedback.incorrect {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }

        .score {
            position: fixed;
            top: 20px;
            right: 20px;
            background: linear-gradient(135deg, #8e44ad, #3498db);
            color: white;
            padding: 15px 20px;
            border-radius: 25px;
            font-weight: bold;
            box-shadow: 0 4px 15px rgba(142,68,173,0.3);
            z-index: 1000;
        }

        @media (max-width: 768px) {
            .matching-container {
                grid-template-columns: 1fr;
                gap: 20px;
            }
            
            .nav-buttons {
                flex-direction: column;
                align-items: center;
            }
            
            .nav-btn {
                width: 200px;
            }
            
            .score {
                position: static;
                margin: 20px auto;
                display: block;
                width: fit-content;
            }
        }
    </style>
</head>
<body>
    <div class="score">Score: <span id="score">0</span>/36</div>
    
    <div class="container">
        <div class="header">
            <h1>🌟 Everyday & Specialized Vocabulary</h1>
            <p>Practice these useful English expressions!</p>
        </div>

        <div class="nav-buttons">
            <button class="nav-btn active" onclick="showSection('fill-gaps')">Fill in the Gaps</button>
            <button class="nav-btn" onclick="showSection('matching')">Match Meanings</button>
            <button class="nav-btn" onclick="showSection('multiple-choice')">Multiple Choice</button>
        </div>

        <!-- Fill in the Gaps Section -->
        <div id="fill-gaps" class="game-section active">
            <div class="word-bank">
                <h3>📝 Word Bank - Choose from these words:</h3>
                <div class="word-options">
                    <span class="word-option">backpack</span>
                    <span class="word-option">roommate</span>
                    <span class="word-option">pick up</span>
                    <span class="word-option">underground</span>
                    <span class="word-option">empty</span>
                    <span class="word-option">weight</span>
                    <span class="word-option">shelf</span>
                    <span class="word-option">tailor-made</span>
                    <span class="word-option">compulsory</span>
                    <span class="word-option">further away</span>
                    <span class="word-option">at most</span>
                    <span class="word-option">overcome</span>
                </div>
            </div>

            <div class="question">
                <h3>Question 1:</h3>
                <p>Can you <input type="text" class="fill-blank" data-answer="pick up" placeholder="answer"> some milk from the store on your way home?</p>
                <div class="feedback" id="feedback-1" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 2:</h3>
                <p>I packed all my essentials in my <input type="text" class="fill-blank" data-answer="backpack" placeholder="answer"> for the hiking trip.</p>
                <div class="feedback" id="feedback-2" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 3:</h3>
                <p>The <input type="text" class="fill-blank" data-answer="underground" placeholder="answer"> train system in London is called the "Tube".</p>
                <div class="feedback" id="feedback-3" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 4:</h3>
                <p>My <input type="text" class="fill-blank" data-answer="roommate" placeholder="answer"> and I take turns cooking dinner each week.</p>
                <div class="feedback" id="feedback-4" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 5:</h3>
                <p>The refrigerator is completely <input type="text" class="fill-blank" data-answer="empty" placeholder="answer">; we need to go grocery shopping.</p>
                <div class="feedback" id="feedback-5" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 6:</h3>
                <p>The <input type="text" class="fill-blank" data-answer="weight" placeholder="answer"> of this package is 5 kilograms.</p>
                <div class="feedback" id="feedback-6" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 7:</h3>
                <p>I placed the book back on the <input type="text" class="fill-blank" data-answer="shelf" placeholder="answer"> after reading it.</p>
                <div class="feedback" id="feedback-7" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 8:</h3>
                <p>The software solution was <input type="text" class="fill-blank" data-answer="tailor-made" placeholder="answer"> for our company's specific needs.</p>
                <div class="feedback" id="feedback-8" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 9:</h3>
                <p>Attendance at the safety training session is <input type="text" class="fill-blank" data-answer="compulsory" placeholder="answer"> for all employees.</p>
                <div class="feedback" id="feedback-9" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 10:</h3>
                <p>The new office location is <input type="text" class="fill-blank" data-answer="further away" placeholder="answer"> from my apartment than the old one.</p>
                <div class="feedback" id="feedback-10" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 11:</h3>
                <p>The repair should take <input type="text" class="fill-blank" data-answer="at most" placeholder="answer"> two hours to complete.</p>
                <div class="feedback" id="feedback-11" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 12:</h3>
                <p>She managed to <input type="text" class="fill-blank" data-answer="overcome" placeholder="answer"> her fear of public speaking through practice.</p>
                <div class="feedback" id="feedback-12" style="display: none;"></div>
            </div>

            <button class="check-btn" onclick="checkFillBlanks()">Check Answers</button>
        </div>

        <!-- Matching Section -->
        <div id="matching" class="game-section">
            <h2 style="text-align: center; margin-bottom: 20px; color: #8e44ad;">Match the terms with their meanings</h2>
            <div class="matching-container">
                <div class="match-column">
                    <h4>Terms</h4>
                    <div class="match-item" data-word="backpack" onclick="selectMatch(this)">backpack</div>
                    <div class="match-item" data-word="roommate" onclick="selectMatch(this)">roommate</div>
                    <div class="match-item" data-word="pick up" onclick="selectMatch(this)">pick up</div>
                    <div class="match-item" data-word="underground" onclick="selectMatch(this)">underground</div>
                    <div class="match-item" data-word="empty" onclick="selectMatch(this)">empty</div>
                    <div class="match-item" data-word="weight" onclick="selectMatch(this)">weight</div>
                    <div class="match-item" data-word="shelf" onclick="selectMatch(this)">shelf</div>
                    <div class="match-item" data-word="tailor-made" onclick="selectMatch(this)">tailor-made</div>
                    <div class="match-item" data-word="compulsory" onclick="selectMatch(this)">compulsory</div>
                    <div class="match-item" data-word="further away" onclick="selectMatch(this)">further away</div>
                    <div class="match-item" data-word="at most" onclick="selectMatch(this)">at most</div>
                    <div class="match-item" data-word="overcome" onclick="selectMatch(this)">overcome</div>
                </div>
                <div class="match-column">
                    <h4>Meanings</h4>
                    <div class="match-item" data-meaning="pick up" onclick="selectMatch(this)">To collect or acquire something</div>
                    <div class="match-item" data-meaning="backpack" onclick="selectMatch(this)">A bag carried on the back, used for carrying belongings</div>
                    <div class="match-item" data-meaning="underground" onclick="selectMatch(this)">Beneath the surface of the ground; subway system</div>
                    <div class="match-item" data-meaning="roommate" onclick="selectMatch(this)">A person with whom one shares a living facility</div>
                    <div class="match-item" data-meaning="empty" onclick="selectMatch(this)">Containing nothing; not filled or occupied</div>
                    <div class="match-item" data-meaning="weight" onclick="selectMatch(this)">The heaviness of a person or thing</div>
                    <div class="match-item" data-meaning="shelf" onclick="selectMatch(this)">A flat length of wood or other material fixed to a wall for holding objects</div>
                    <div class="match-item" data-meaning="tailor-made" onclick="selectMatch(this)">Made specifically for a particular purpose or person</div>
                    <div class="match-item" data-meaning="compulsory" onclick="selectMatch(this)">Required by law or rules; mandatory</div>
                    <div class="match-item" data-meaning="further away" onclick="selectMatch(this)">At a greater distance; more remote</div>
                    <div class="match-item" data-meaning="at most" onclick="selectMatch(this)">Not more than; indicating a maximum amount</div>
                    <div class="match-item" data-meaning="overcome" onclick="selectMatch(this)">To succeed in dealing with a problem or difficulty</div>
                </div>
            </div>
            <div class="feedback" id="matching-feedback" style="display: none;"></div>
        </div>

        <!-- Multiple Choice Section -->
        <div id="multiple-choice" class="game-section">
            <div class="question">
                <h3>Question 1: What does "pick up" mean in this context?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To lift something</div>
                    <div class="option" onclick="selectOption(this, true)">To collect or acquire something</div>
                    <div class="option" onclick="selectOption(this, false)">To improve gradually</div>
                    <div class="option" onclick="selectOption(this, false)">To learn something without formal instruction</div>
                </div>
                <div class="feedback" id="mc-feedback-1" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 2: A "backpack" is:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A piece of furniture for storing clothes</div>
                    <div class="option" onclick="selectOption(this, true)">A bag carried on the back for carrying belongings</div>
                    <div class="option" onclick="selectOption(this, false)">A type of chair with support for the back</div>
                    <div class="option" onclick="selectOption(this, false)">A protective case for electronic devices</div>
                </div>
                <div class="feedback" id="mc-feedback-2" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 3: "Underground" can refer to:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">An elevated train system</div>
                    <div class="option" onclick="selectOption(this, true)">A subway system beneath the surface</div>
                    <div class="option" onclick="selectOption(this, false)">An airline transportation network</div>
                    <div class="option" onclick="selectOption(this, false)">A bus rapid transit system</div>
                </div>
                <div class="feedback" id="mc-feedback-3" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 4: A "roommate" is:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A person who designs rooms</div>
                    <div class="option" onclick="selectOption(this, false)">A furniture arrangement specialist</div>
                    <div class="option" onclick="selectOption(this, true)">A person with whom one shares a living facility</div>
                    <div class="option" onclick="selectOption(this, false)">A professional room cleaner</div>
                </div>
                <div class="feedback" id="mc-feedback-4" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 5: What does "empty" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Completely full</div>
                    <div class="option" onclick="selectOption(this, true)">Containing nothing; not filled</div>
                    <div class="option" onclick="selectOption(this, false)">Partially filled</div>
                    <div class="option" onclick="selectOption(this, false)">Overflowing with contents</div>
                </div>
                <div class="feedback" id="mc-feedback-5" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 6: "Weight" refers to:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">The lightness of an object</div>
                    <div class="option" onclick="selectOption(this, true)">The heaviness of a person or thing</div>
                    <div class="option" onclick="selectOption(this, false)">The volume of an object</div>
                    <div class="option" onclick="selectOption(this, false)">The density of a material</div>
                </div>
                <div class="feedback" id="mc-feedback-6" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 7: A "shelf" is:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A type of chair without back support</div>
                    <div class="option" onclick="selectOption(this, true)">A flat surface fixed to a wall for holding objects</div>
                    <div class="option" onclick="selectOption(this, false)">A storage unit with doors</div>
                    <div class="option" onclick="selectOption(this, false)">A portable container for belongings</div>
                </div>
                <div class="feedback" id="mc-feedback-7" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 8: "Tailor-made" means:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Mass-produced for general use</div>
                    <div class="option" onclick="selectOption(this, true)">Made specifically for a particular purpose</div>
                    <div class="option" onclick="selectOption(this, false)">Improvised or makeshift</div>
                    <div class="option" onclick="selectOption(this, false)">Repurposed from something else</div>
                </div>
                <div class="feedback" id="mc-feedback-8" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 9: What does "compulsory" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Optional or voluntary</div>
                    <div class="option" onclick="selectOption(this, true)">Required by law or rules; mandatory</div>
                    <div class="option" onclick="selectOption(this, false)">Recommended but not enforced</div>
                    <div class="option" onclick="selectOption(this, false)">Temporarily suspended</div>
                </div>
                <div class="feedback" id="mc-feedback-9" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 10: "Further away" means:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Closer in distance</div>
                    <div class="option" onclick="selectOption(this, true)">At a greater distance; more remote</div>
                    <div class="option" onclick="selectOption(this, false)">At the same distance</div>
                    <div class="option" onclick="selectOption(this, false)">Within walking distance</div>
                </div>
                <div class="feedback" id="mc-feedback-10" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 11: "At most" indicates:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A minimum amount or limit</div>
                    <div class="option" onclick="selectOption(this, true)">A maximum amount or limit</div>
                    <div class="option" onclick="selectOption(this, false)">An exact amount</div>
                    <div class="option" onclick="selectOption(this, false)">An approximate amount</div>
                </div>
                <div class="feedback" id="mc-feedback-11" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 12: To "overcome" means:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To be defeated by a challenge</div>
                    <div class="option" onclick="selectOption(this, true)">To succeed in dealing with a problem</div>
                    <div class="option" onclick="selectOption(this, false)">To avoid dealing with a difficulty</div>
                    <div class="option" onclick="selectOption(this, false)">To ignore a problem</div>
                </div>
                <div class="feedback" id="mc-feedback-12" style="display: none;"></div>
            </div>
        </div>
    </div>

    <script>
        let score = 0;
        let selectedWord = null;
        let selectedMeaning = null;
        let matchedPairs = [];

        function showSection(sectionId) {
            // Hide all sections
            document.querySelectorAll('.game-section').forEach(section => {
                section.classList.remove('active');
            });
            
            // Remove active class from all buttons
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            
            // Show selected section
            document.getElementById(sectionId).classList.add('active');
            
            // Add active class to clicked button
            event.target.classList.add('active');
        }

        function checkFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            let correctCount = 0;
            
            blanks.forEach((blank, index) => {
                const userAnswer = blank.value.toLowerCase().trim();
                const correctAnswer = blank.dataset.answer.toLowerCase();
                
                if (userAnswer === correctAnswer) {
                    blank.classList.remove('incorrect');
                    blank.classList.add('correct');
                    correctCount++;
                } else {
                    blank.classList.remove('correct');
                    blank.classList.add('incorrect');
                }
                
                // Show feedback for each question
                const feedback = document.getElementById(`feedback-${index+1}`);
                if (userAnswer === correctAnswer) {
                    feedback.textContent = '✅ Correct!';
                    feedback.className = 'feedback correct';
                } else {
                    feedback.textContent = `❌ Incorrect. The correct answer is: "${blank.dataset.answer}"`;
                    feedback.className = 'feedback incorrect';
                }
                feedback.style.display = 'block';
            });
            
            updateScore();
        }

        function selectMatch(element) {
            if (element.classList.contains('matched')) return;
            
            if (element.dataset.word) {
                // Word selected
                if (selectedWord) selectedWord.classList.remove('selected');
                selectedWord = element;
                element.classList.add('selected');
            } else {
                // Meaning selected
                if (selectedMeaning) selectedMeaning.classList.remove('selected');
                selectedMeaning = element;
                element.classList.add('selected');
            }
            
            // Check if we have both word and meaning selected
            if (selectedWord && selectedMeaning) {
                checkMatch();
            }
        }

        function checkMatch() {
            const feedback = document.getElementById('matching-feedback');
            
            if (selectedWord.dataset.word === selectedMeaning.dataset.meaning) {
                // Correct match
                selectedWord.classList.remove('selected');
                selectedWord.classList.add('matched');
                selectedMeaning.classList.remove('selected');
                selectedMeaning.classList.add('matched');
                
                matchedPairs.push(selectedWord.dataset.word);
                
                feedback.textContent = '✅ Correct match!';
                feedback.className = 'feedback correct';
                
                // Check if all matches are complete
                if (matchedPairs.length === 12) {
                    feedback.textContent = '🎉 Congratulations! You matched all terms correctly!';
                }
            } else {
                // Incorrect match
                feedback.textContent = '❌ Incorrect match. Try again.';
                feedback.className = 'feedback incorrect';
            }
            
            feedback.style.display = 'block';
            selectedWord = null;
            selectedMeaning = null;
            
            updateScore();
        }

        function selectOption(element, isCorrect) {
            // Remove selection from all options in this question
            const options = element.parentElement.querySelectorAll('.option');
            options.forEach(opt => {
                opt.classList.remove('selected');
                opt.classList.remove('correct');
                opt.classList.remove('incorrect');
            });
            
            // Mark the selected option
            element.classList.add('selected');
            
            const questionNumber = element.closest('.question').querySelector('h3').textContent.match(/\d+/)[0];
            const feedback = document.getElementById(`mc-feedback-${questionNumber}`);
            
            if (isCorrect) {
                element.classList.add('correct');
                feedback.textContent = '✅ Correct!';
                feedback.className = 'feedback correct';
            } else {
                element.classList.add('incorrect');
                feedback.textContent = '❌ Incorrect. Try again.';
                feedback.className = 'feedback incorrect';
                
                // Show the correct answer
                options.forEach(opt => {
                    if (opt.onclick.toString().includes('true')) {
                        opt.classList.add('correct');
                    }
                });
            }
            
            feedback.style.display = 'block';
            updateScore();
        }

        function updateScore() {
            // Calculate score for fill-in-the-blank
            let fillScore = 0;
            document.querySelectorAll('.fill-blank.correct').forEach(blank => {
                if (!blank.classList.contains('counted')) {
                    fillScore++;
                    blank.classList.add('counted');
                }
            });
            
            // Calculate score for matching (each pair is 1 point)
            const matchScore = matchedPairs.length;
            
            // Calculate score for multiple choice (each correct is 1 point)
            let mcScore = 0;
            document.querySelectorAll('.option.correct.selected').forEach(opt => {
                mcScore++;
            });
            
            // Total score
            score = fillScore + matchScore + mcScore;
            document.getElementById('score').textContent = score;
        }
    </script>
</body>
</html>
