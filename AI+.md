<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>כותב +AI - עוזר כתיבת החיבורים שלך</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            direction: rtl;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        .header {
            text-align: center;
            margin-bottom: 30px;
            color: white;
        }

        .header h1 {
            font-size: 3em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }

        .header p {
            font-size: 1.2em;
            opacity: 0.9;
        }

        .main-content {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.1);
            backdrop-filter: blur(10px);
        }

        .steps-nav {
            display: flex;
            justify-content: center;
            margin-bottom: 30px;
            gap: 10px;
        }

        .step-btn {
            padding: 12px 25px;
            border: none;
            border-radius: 25px;
            background: #f0f0f0;
            cursor: pointer;
            font-size: 16px;
            transition: all 0.3s ease;
            font-weight: bold;
        }

        .step-btn.active {
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }

        .step-btn:hover {
            transform: translateY(-1px);
            box-shadow: 0 3px 10px rgba(0,0,0,0.1);
        }

        .step-content {
            display: none;
            animation: fadeIn 0.5s ease-in;
        }

        .step-content.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .card {
            background: white;
            border-radius: 15px;
            padding: 25px;
            margin-bottom: 20px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.08);
            border-left: 5px solid #667eea;
        }

        .card h3 {
            color: #333;
            margin-bottom: 15px;
            font-size: 1.5em;
        }

        .input-group {
            margin-bottom: 20px;
        }

        .input-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #555;
        }

        .input-group input,
        .input-group select,
        .input-group textarea {
            width: 100%;
            padding: 12px;
            border: 2px solid #e1e1e1;
            border-radius: 10px;
            font-size: 16px;
            transition: border-color 0.3s ease;
        }

        .input-group input:focus,
        .input-group select:focus,
        .input-group textarea:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
        }

        .textarea-large {
            min-height: 200px;
            resize: vertical;
        }

        .btn-primary {
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
            border: none;
            padding: 12px 30px;
            border-radius: 25px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }

        .feedback {
            background: #e8f5e8;
            border: 2px solid #4caf50;
            border-radius: 10px;
            padding: 15px;
            margin-top: 15px;
        }

        .feedback h4 {
            color: #2e7d32;
            margin-bottom: 10px;
        }

        .feedback ul {
            color: #388e3c;
            padding-right: 20px;
        }

        .tips {
            background: linear-gradient(45deg, #fff3e0, #ffcc80);
            border-radius: 10px;
            padding: 20px;
            margin-top: 20px;
        }

        .tips h4 {
            color: #f57c00;
            margin-bottom: 10px;
        }

        .tips-specific {
            background: linear-gradient(45deg, #e3f2fd, #90caf9);
            border-radius: 10px;
            padding: 20px;
            margin-top: 20px;
            border: 2px solid #2196f3;
        }

        .tips-specific h4 {
            color: #1565c0;
            margin-bottom: 15px;
        }

        .tips-specific .tip-section {
            background: rgba(255, 255, 255, 0.7);
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 15px;
        }

        .tips-specific .tip-section h5 {
            color: #0d47a1;
            margin-bottom: 10px;
            font-size: 1.1em;
        }

        .progress-bar {
            width: 100%;
            height: 10px;
            background: #e0e0e0;
            border-radius: 5px;
            margin-bottom: 20px;
            overflow: hidden;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(45deg, #667eea, #764ba2);
            border-radius: 5px;
            transition: width 0.3s ease;
        }

        .emoji {
            font-size: 1.5em;
            margin-left: 10px;
        }

        .example-box {
            background: #f8f9fa;
            border: 1px solid #dee2e6;
            border-radius: 8px;
            padding: 15px;
            margin: 10px 0;
            font-style: italic;
        }

        .warning-tip {
            background: #fff3e0;
            border: 2px solid #ff9800;
            border-radius: 8px;
            padding: 12px;
            margin: 10px 0;
        }

        .success-tip {
            background: #e8f5e8;
            border: 2px solid #4caf50;
            border-radius: 8px;
            padding: 12px;
            margin: 10px 0;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>כותב +AI <span class="emoji">✍️</span></h1>
            <p>העוזר החכם שלך לכתיבת חיבורים מעולים!</p>
        </div>

        <div class="main-content">
            <div class="progress-bar">
                <div class="progress-fill" id="progressBar" style="width: 25%"></div>
            </div>

            <div class="steps-nav">
                <button class="step-btn active" onclick="showStep(1)">1. תכנון <span class="emoji">🎯</span></button>
                <button class="step-btn" onclick="showStep(1.5)" id="reviewBtn" style="display: none;">1.5. סקירה <span class="emoji">📋</span></button>
                <button class="step-btn" onclick="showStep(2)">2. כתיבה <span class="emoji">✏️</span></button>
                <button class="step-btn" onclick="showStep(3)">3. עריכה <span class="emoji">🔍</span></button>
                <button class="step-btn" onclick="showStep(4)">4. סיום <span class="emoji">🎉</span></button>
            </div>

            <!-- שלב 1: תכנון -->
            <div class="step-content active" id="step1">
                <div class="card">
                    <h3>בואו נתכנן את החיבור שלך! <span class="emoji">📝</span></h3>
                    
                    <div class="input-group">
                        <label for="essayType">איזה סוג חיבור אתה כותב?</label>
                        <select id="essayType" onchange="updateTips()">
                            <option value="">בחר סוג חיבור...</option>
                            <option value="argumentative">חיבור טיעוני</option>
                            <option value="descriptive">חיבור תיאור</option>
                            <option value="formal_letter">מכתב רשמי</option>
                            <option value="friendly_letter">מכתב לחבר</option>
                        </select>
                    </div>

                    <div class="input-group">
                        <label for="topic">מה הנושא של החיבור?</label>
                        <input type="text" id="topic" placeholder="למשל: השפעת הטכנולוגיה על החברה המודרנית">
                    </div>

                    <div class="input-group">
                        <label for="mainIdea">מה הרעיון המרכזי שלך?</label>
                        <textarea id="mainIdea" placeholder="תאר בכמה משפטים את הרעיון העיקרי שלך..."></textarea>
                    </div>

                    <div class="input-group" id="argumentsGroup">
                        <label for="arguments">רשום 3 טיעונים עיקריים:</label>
                        <textarea id="arguments" placeholder="טיעון 1: ...&#10;טיעון 2: ...&#10;טיעון 3: ..."></textarea>
                    </div>

                    <div class="input-group" id="counterArgumentGroup" style="display: none;">
                        <label for="counterArgument">טענת נגד שעלולה להיות מועלית:</label>
                        <textarea id="counterArgument" placeholder="למשל: יש הטוענים כי..."></textarea>
                    </div>

                    <div class="input-group" id="counterArgumentRefutationGroup" style="display: none;">
                        <label for="counterArgumentRefutation">ההפרכה שלך לטענת הנגד:</label>
                        <textarea id="counterArgumentRefutation" placeholder="אולם טענה זו שגויה מכיוון ש..."></textarea>
                    </div>

                    <button class="btn-primary" onclick="generateOutline()">צור מתווה לחיבור <span class="emoji">🚀</span></button>

                    <div id="outlineFeedback"></div>
                </div>

                <div class="tips" id="generalTips">
                    <h4>💡 טיפים לתכנון חיבור מוצלח:</h4>
                    <ul>
                        <li>התחיל עם רעיון ברור ומוגדר</li>
                        <li>חשוב על 3 טיעונים חזקים התומכים ברעיון שלך</li>
                        <li>חפש דוגמאות ומקורות לכל טיעון</li>
                        <li>תכנן את סדר הטיעונים - מהחלש לחזק</li>
                    </ul>
                </div>

                <div class="tips-specific" id="specificTips" style="display: none;">
                    <!-- הטיפים הספציפיים יתווספו כאן -->
                </div>
            </div>

            <!-- שלב 1.5: סקירת התכנון -->
            <div class="step-content" id="step1.5">
                <div class="card">
                    <h3>סקירת התכנון שלך <span class="emoji">📋</span></h3>
                    
                    <div id="planReview">
                        <!-- התוכן יתווסף דינמית -->
                    </div>

                    <div style="text-align: center; margin-top: 30px;">
                        <button class="btn-primary" onclick="showStep(2)" style="margin-left: 10px;">
                            מעבר לכתיבה <span class="emoji">✍️</span>
                        </button>
                        <button class="btn-primary" onclick="showStep(1)" style="background: #6c757d;">
                            חזור לתכנון <span class="emoji">🔄</span>
                        </button>
                    </div>
                </div>

                <div class="tips">
                    <h4>💡 לפני שאתה מתחיל לכתוב:</h4>
                    <ul>
                        <li>בדוק שהמתווה הגיוני וזורם טוב</li>
                        <li>וודא שיש לך מספיק דוגמאות לכל טיעון</li>
                        <li>חשוב על מילות המעבר בין הפסקאות</li>
                        <li>זכור: תמיד אפשר לחזור ולשנות את התכנון!</li>
                    </ul>
                </div>
            </div>

            <!-- שלב 2: כתיבה -->
            <div class="step-content" id="step2">
                <div class="card">
                    <h3>עכשיו בואו נכתוב! <span class="emoji">✍️</span></h3>
                    
                    <div class="input-group">
                        <label for="introduction">הקדמה:</label>
                        <textarea id="introduction" class="textarea-large" 
                                placeholder="התחל במשפט מעניין שיושך את הקורא...&#10;הצג את הנושא...&#10;סיים עם המשפט המרכזי (תזה)..."></textarea>
                    </div>

                    <div class="input-group">
                        <label for="body1">פסקת גוף ראשונה:</label>
                        <textarea id="body1" class="textarea-large" 
                                placeholder="הצג את הטיעון הראשון...&#10;הוסף דוגמאות ומקורות...&#10;הסבר למה זה תומך בתזה שלך..."></textarea>
                    </div>

                    <div class="input-group">
                        <label for="body2">פסקת גוף שנייה:</label>
                        <textarea id="body2" class="textarea-large" 
                                placeholder="הצג את הטיעון השני..."></textarea>
                    </div>

                    <div class="input-group">
                        <label for="body3">פסקת גוף שלישית:</label>
                        <textarea id="body3" class="textarea-large" 
                                placeholder="הצג את הטיעון השלישי..."></textarea>
                    </div>

                    <div class="input-group">
                        <label for="conclusion">מסקנה:</label>
                        <textarea id="conclusion" class="textarea-large" 
                                placeholder="סכם את הטיעונים העיקריים...&#10;חזור על התזה במילים אחרות...&#10;סיים עם מחשבה לעתיד או קריאה לפעולה..."></textarea>
                    </div>

                    <button class="btn-primary" onclick="analyzeWriting()">בדוק את הכתיבה שלי <span class="emoji">🔍</span></button>

                    <div id="writingFeedback"></div>
                </div>

                <div class="tips" id="writingTips">
                    <h4>💡 טיפים לכתיבה זורמת:</h4>
                    <ul>
                        <li>כל פסקה צריכה להתחיל במשפט נושא ברור</li>
                        <li>השתמש במילות חיבור: "בנוסף", "לעומת זאת", "לכן"</li>
                        <li>תן דוגמאות קונקרטיות לכל טיעון</li>
                        <li>שמור על זרימה לוגית בין הפסקאות</li>
                    </ul>
                </div>
            </div>

            <!-- שלב 3: עריכה -->
            <div class="step-content" id="step3">
                <div class="card">
                    <h3>בואו נשפר את החיבור! <span class="emoji">🔧</span></h3>
                    
                    <div class="input-group">
                        <label for="fullEssay">הדבק כאן את החיבור המלא לבדיקה:</label>
                        <textarea id="fullEssay" class="textarea-large" 
                                placeholder="הדבק כאן את כל החיבור..."></textarea>
                    </div>

                    <button class="btn-primary" onclick="checkEssay()">בדוק דקדוק ומבנה <span class="emoji">🎯</span></button>

                    <div id="editingFeedback"></div>
                </div>

                <div class="tips">
                    <h4>🔍 רשימת בדיקות לעריכה:</h4>
                    <ul>
                        <li>✅ בדוק שגיאות כתיב ודקדוק</li>
                        <li>✅ וודא שכל פסקה מתחילה במשפט נושא</li>
                        <li>✅ בדוק שהמעברים בין פסקאות חלקים</li>
                        <li>✅ וודא שהמסקנה מסכמת את כל הטיעונים</li>
                        <li>✅ קרא בקול רם לבדיקת זרימה</li>
                    </ul>
                </div>
            </div>

            <!-- שלב 4: סיום -->
            <div class="step-content" id="step4">
                <div class="card">
                    <h3>מזל טוב! החיבור שלך מוכן! <span class="emoji">🎉</span></h3>
                    
                    <div style="text-align: center; padding: 20px;">
                        <div style="font-size: 4em; margin-bottom: 20px;">🏆</div>
                        <h2 style="color: #667eea; margin-bottom: 20px;">עבודה מעולה!</h2>
                        <p style="font-size: 1.2em; margin-bottom: 30px;">
                            עברת את כל השלבים בהצלחה. החיבור שלך מוכן להגשה!
                        </p>
                        
                        <div class="card" style="background: #f8f9fa; margin: 20px 0;">
                            <h4>📊 סיכום התהליך:</h4>
                            <div id="processSummary">
                                <p>✅ תכננת את החיבור שלך</p>
                                <p>✅ כתבת את כל החלקים</p>
                                <p>✅ ערכת ושיפרת</p>
                                <p>✅ החיבור מוכן להגשה!</p>
                            </div>
                        </div>

                        <button class="btn-primary" onclick="downloadEssay()">הורד את החיבור <span class="emoji">💾</span></button>
                        <button class="btn-primary" onclick="startNew()" style="margin-right: 10px;">התחל חיבור חדש <span class="emoji">🔄</span></button>
                    </div>
                </div>

                <div class="tips">
                    <h4>🚀 טיפים לפעם הבאה:</h4>
                    <ul>
                        <li>שמור את המתווה - זה יעזור לך בחיבורים הבאים</li>
                        <li>קרא חיבורים טובים לשיפור הסגנון</li>
                        <li>תרגל כתיבה קצרה יום יום</li>
                        <li>אל תשכח לערוך תמיד לפני הגשה!</li>
                    </ul>
                </div>
            </div>
        </div>
    </div>

    <script>
        let currentStep = 1;
        let essayData = {};

        function showStep(stepNumber) {
            // הסתר את כל השלבים
            const steps = ['step1', 'step1.5', 'step2', 'step3', 'step4'];
            steps.forEach(step => {
                const element = document.getElementById(step);
                if (element) element.classList.remove('active');
            });
            
            // הסתר את כל הכפתורים
            document.querySelectorAll('.step-btn').forEach(btn => btn.classList.remove('active'));
            
            // הצג את השלב הנבחר
            const targetStep = document.getElementById(`step${stepNumber}`);
            if (targetStep) {
                targetStep.classList.add('active');
            }
            
            // הדלק את הכפתור המתאים
            if (stepNumber === 1.5) {
                document.getElementById('reviewBtn').classList.add('active');
            } else {
                const btnIndex = stepNumber === 1 ? 1 : stepNumber === 2 ? 3 : stepNumber === 3 ? 4 : 5;
                const activeBtn = document.querySelector(`.step-btn:nth-child(${btnIndex})`);
                if (activeBtn) activeBtn.classList.add('active');
            }
            
            currentStep = stepNumber;
            updateProgressBar();
        }

        function updateProgressBar() {
            let progress;
            switch(currentStep) {
                case 1: progress = 20; break;
                case 1.5: progress = 35; break;
                case 2: progress = 55; break;
                case 3: progress = 80; break;
                case 4: progress = 100; break;
                default: progress = 20;
            }
            document.getElementById('progressBar').style.width = progress + '%';
        }

        function updateTips() {
            const essayType = document.getElementById('essayType').value;
            const specificTipsElement = document.getElementById('specificTips');
            const argumentsGroup = document.getElementById('argumentsGroup');
            
            if (!essayType) {
                specificTipsElement.style.display = 'none';
                return;
            }

            specificTipsElement.style.display = 'block';
            
            const tips = {
                argumentative: {
                    title: '🎯 טיפים לחיבור טיעוני:',
                    sections: [
                        {
                            title: 'מבנה חזק',
                            content: '• הצג עמדה ברורה בהקדמה<br>• כל פסקה = טיעון אחד + הוכחות<br>• התייחס לעמדה נגדית והפרך אותה<br>• סיים בחיזוק העמדה',
                            example: 'דוגמה: "אף על פי שיש הטוענים כי... אולם טענה זו שגויה מכיוון ש..."'
                        },
                        {
                            title: 'טיפים מעשיים',
                            content: '• השתמש בדוגמאות קונקרטיות ומקורות<br>• מילות קישור: "יתרה מכך", "מצד שני", "לכן"<br>• סדר הטיעונים: מחלש לחזק',
                            example: 'מילות קישור: "ראשית", "שנית", "אמנם... אולם", "לבסוף"'
                        }
                    ]
                },
                descriptive: {
                    title: '🎨 טיפים לחיבור תיאור:',
                    sections: [
                        {
                            title: 'יצירת אטמוספרה',
                            content: '• השתמש בכל החושים (לא רק ראייה)<br>• בנה מכללי לפרטי או הפוך<br>• צור חוויה חושית לקורא',
                            example: 'דוגמה: "הריח החמצמץ של הגשם התערבב עם ניחוח הפרחים..."'
                        },
                        {
                            title: 'כלים ספרותיים',
                            content: '• השתמש במטפורות והשוואות<br>• תאר פרטים שיוצרים רגש<br>• שפה עשירה וחושית',
                            example: 'מטפורות: "הרוח לחשה סודות", "השמש ציירה צללים רוקדים"'
                        }
                    ]
                },
                formal_letter: {
                    title: '📋 טיפים למכתב רשמי:',
                    sections: [
                        {
                            title: 'מבנה נדרש',
                            content: '• כתובת שולח + תאריך<br>• כתובת נמען + נושא<br>• פנייה מנומסת + גוף + סיום',
                            example: 'פתיחה: "הנדון: בקשה לדחיית מועד<br>אני פונה אליכם בעניין..."'
                        },
                        {
                            title: 'שפה וסגנון',
                            content: '• שפה מכובדת ותמציתית<br>• הבהר מטרה בפסקה ראשונה<br>• השתמש בביטויים מקובלים',
                            example: 'ביטויים: "אני פונה אליכם", "אודה לקבל מענה", "בכבוד רב"'
                        }
                    ]
                },
                friendly_letter: {
                    title: '💌 טיפים למכתב לחבר:',
                    sections: [
                        {
                            title: 'טון אישי וחם',
                            content: '• שפה טבעית ורגועה<br>• התחל בשאלה על מצבו<br>• התייחס לאירועים משותפים',
                            example: 'פתיחה: "איך אתה? מזמן לא שמעתי! אתמול קרה לי משהו מצחיק..."'
                        },
                        {
                            title: 'תוכן מעניין',
                            content: '• שתף חוויות אישיות ורגשות<br>• השתמש בהומור מתאים<br>• סיים בחיבה או תוכניות',
                            example: 'סיומים: "מתגעגע אליך", "מחכה לפגישה הבאה", "כתוב בחזרה!"'
                        }
                    ]
                }
            };

            // עדכון לייבל לפי סוג החיבור
            const argumentsLabel = document.querySelector('label[for="arguments"]');
            const counterArgumentGroup = document.getElementById('counterArgumentGroup');
            const counterArgumentRefutationGroup = document.getElementById('counterArgumentRefutationGroup');
            const counterArgWritingGroup = document.getElementById('counterArgWritingGroup');
            
            if (essayType === 'argumentative') {
                argumentsLabel.textContent = 'רשום 3 טיעונים עיקריים:';
                argumentsGroup.style.display = 'block';
                counterArgumentGroup.style.display = 'block';
                counterArgumentRefutationGroup.style.display = 'block';
                counterArgWritingGroup.style.display = 'block';
            } else if (essayType === 'formal_letter' || essayType === 'friendly_letter') {
                argumentsLabel.textContent = 'רשום 3 נקודות עיקריות שברצונך להעביר:';
                argumentsGroup.style.display = 'block';
                counterArgumentGroup.style.display = 'none';
                counterArgumentRefutationGroup.style.display = 'none';
                counterArgWritingGroup.style.display = 'none';
            } else if (essayType === 'descriptive') {
                argumentsLabel.textContent = 'רשום 3 היבטים שברצונך לתאר:';
                argumentsGroup.style.display = 'block';
                counterArgumentGroup.style.display = 'none';
                counterArgumentRefutationGroup.style.display = 'none';
                counterArgWritingGroup.style.display = 'none';
            } else {
                argumentsLabel.textContent = 'רשום 3 טיעונים עיקריים:';
                argumentsGroup.style.display = 'block';
                counterArgumentGroup.style.display = 'none';
                counterArgumentRefutationGroup.style.display = 'none';
                counterArgWritingGroup.style.display = 'none';
            }

            if (tips[essayType]) {
                let tipContent = `<h4>${tips[essayType].title}</h4>`;
                
                tips[essayType].sections.forEach(section => {
                    tipContent += `
                        <div class="tip-section">
                            <h5>${section.title}</h5>
                            <p>${section.content}</p>
                            <div class="example-box">
                                <strong>💡 ${section.example}</strong>
                            </div>
                        </div>
                    `;
                });

                specificTipsElement.innerHTML = tipContent;
            }
        }

        function generateOutline() {
            const topic = document.getElementById('topic').value;
            const mainIdea = document.getElementById('mainIdea').value;
            const arguments = document.getElementById('arguments').value;
            const essayType = document.getElementById('essayType').value;
            const counterArgument = document.getElementById('counterArgument').value;
            const counterArgumentRefutation = document.getElementById('counterArgumentRefutation').value;

            if (!topic || !mainIdea || !arguments || !essayType) {
                alert('אנא מלא את כל השדות כדי לקבל מתווה מותאם!');
                return;
            }

            if (essayType === 'argumentative' && (!counterArgument || !counterArgumentRefutation)) {
                alert('בחיבור טיעוני חובה למלא גם את טענת הנגד וההפרכה!');
                return;
            }

            const feedback = document.getElementById('outlineFeedback');
            let structureTips = '';

            switch(essayType) {
                case 'argumentative':
                    structureTips = `
                        <div class="success-tip">
                            <strong>🎯 מבנה חיבור טיעוני:</strong><br>
                            • הקדמה: הצגת הנושא + תזה ברורה<br>
                            • פסקאות גוף: כל פסקה = טיעון אחד + הוכחות<br>
                            • טענת נגד והפרכה: "${counterArgument || 'הטענה הנגדית שלך'}"<br>
                            • מסקנה: חיזוק התזה + קריאה לפעולה
                        </div>
                    `;
                    break;
                case 'descriptive':
                    structureTips = `
                        <div class="success-tip">
                            <strong>🎨 מבנה חיבור תיאור:</strong><br>
                            • הקדמה: יצירת רושם ראשוני + הצגת הנתאר<br>
                            • פ
