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

        .essay-type-cards {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }

        .essay-type-card {
            background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
            border: 3px solid #dee2e6;
            border-radius: 15px;
            padding: 25px;
            cursor: pointer;
            transition: all 0.3s ease;
            text-align: center;
        }

        .essay-type-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(0,0,0,0.15);
            border-color: #667eea;
        }

        .essay-type-card.selected {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border-color: #667eea;
        }

        .essay-type-card h4 {
            font-size: 1.4em;
            margin-bottom: 15px;
        }

        .essay-type-card .emoji {
            font-size: 2.5em;
            margin-bottom: 10px;
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
            margin: 5px;
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }

        .btn-secondary {
            background: #6c757d;
            color: white;
            border: none;
            padding: 12px 30px;
            border-radius: 25px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            margin: 5px;
        }

        .tips-box {
            background: linear-gradient(45deg, #e3f2fd, #90caf9);
            border-radius: 15px;
            padding: 25px;
            margin-top: 20px;
            border: 2px solid #2196f3;
        }

        .tips-box h4 {
            color: #1565c0;
            margin-bottom: 20px;
            text-align: center;
            font-size: 1.4em;
        }

        .tip-section {
            background: rgba(255, 255, 255, 0.8);
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 15px;
        }

        .tip-section h5 {
            color: #0d47a1;
            margin-bottom: 12px;
            font-size: 1.1em;
        }

        .tip-section ul {
            padding-right: 20px;
            margin-bottom: 10px;
        }

        .tip-section li {
            margin-bottom: 8px;
            line-height: 1.5;
        }

        .example-box {
            background: #f8f9fa;
            border: 1px solid #dee2e6;
            border-radius: 8px;
            padding: 15px;
            margin-top: 10px;
            font-style: italic;
            color: #495057;
        }

        .back-btn {
            margin-bottom: 20px;
        }

        .progress-indicator {
            text-align: center;
            margin-bottom: 20px;
            font-size: 1.1em;
            color: #667eea;
            font-weight: bold;
        }

        @media (max-width: 768px) {
            .container {
                padding: 10px;
            }
            
            .header h1 {
                font-size: 2em;
            }
            
            .main-content {
                padding: 20px;
            }
            
            .essay-type-cards {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>כותב +AI ✍️</h1>
            <p>העוזר החכם שלך לכתיבת חיבורים מעולים!</p>
        </div>

        <div class="main-content">
            <!-- בחירת סוג חיבור -->
            <div class="step-content active" id="essayTypeSelection">
                <div class="card">
                    <h3>איזה סוג חיבור תרצה לכתוב? 📝</h3>
                    
                    <div class="essay-type-cards">
                        <div class="essay-type-card" onclick="selectEssayType('argumentative')">
                            <div class="emoji">⚖️</div>
                            <h4>חיבור טיעוני</h4>
                            <p>הצגת עמדה עם טיעונים ותמיכה</p>
                        </div>
                        
                        <div class="essay-type-card" onclick="selectEssayType('descriptive')">
                            <div class="emoji">🎨</div>
                            <h4>חיבור תיאור</h4>
                            <p>תיאור חושי ויצירת אטמוספרה</p>
                        </div>
                        
                        <div class="essay-type-card" onclick="selectEssayType('formal_letter')">
                            <div class="emoji">📋</div>
                            <h4>מכתב רשמי</h4>
                            <p>מכתב למוסד או גורם רשמי</p>
                        </div>
                        
                        <div class="essay-type-card" onclick="selectEssayType('friendly_letter')">
                            <div class="emoji">💌</div>
                            <h4>מכתב לחבר</h4>
                            <p>מכתב אישי וחם לחבר או לקרוב</p>
                        </div>
                    </div>
                </div>
            </div>

            <!-- חיבור טיעוני -->
            <div class="step-content" id="argumentative">
                <div class="progress-indicator">שלב 1: תכנון חיבור טיעוני ⚖️</div>
                
                <button class="btn-secondary back-btn" onclick="goBack()">← חזרה לבחירת סוג חיבור</button>
                
                <div class="card">
                    <h3>תכנון החיבור הטיעוני שלך 🎯</h3>
                    
                    <div class="input-group">
                        <label for="argTopic">מה הנושא של החיבור?</label>
                        <input type="text" id="argTopic" placeholder="למשל: השפעת הטכנולוגיה על החברה המודרנית">
                    </div>

                    <div class="input-group">
                        <label for="argPosition">מה העמדה שלך? </label>
                        <textarea id="argPosition" placeholder="הצג בבירור מה העמדה שלך בנושא..."></textarea>
                    </div>

                    <div class="input-group">
                        <label for="argArguments">3 טיעונים עיקריים התומכים בעמדה שלך:</label>
                        <textarea id="argArguments" placeholder="טיעון 1: ...&#10;טיעון 2: ...&#10;טיעון 3: ..."></textarea>
                    </div>

                    <div class="input-group">
                        <label for="argCounterArgument">טענת נגד שעלולה להיות מועלית:</label>
                        <textarea id="argCounterArgument" placeholder="יש הטוענים כי..."></textarea>
                    </div>

                    <div class="input-group">
                        <label for="argRefutation">ההפרכה שלך לטענת הנגד:</label>
                        <textarea id="argRefutation" placeholder="אולם טענה זו שגויה מכיוון ש..."></textarea>
                    </div>

                    <button class="btn-primary" onclick="generateOutline('argumentative')">צור מתווה לחיבור 🚀</button>
                    <div id="argOutline"></div>
                </div>

                <div class="tips-box">
                    <h4>🎯 טיפים לחיבור טיעוני מוצלח</h4>
                    
                    <div class="tip-section">
                        <h5>🏗️ מבנה חזק</h5>
                        <ul>
                            <li>הקדמה: הצג את הנושא ואת העמדה שלך בבירור</li>
                            <li>כל פסקת גוף: טיעון אחד + הוכחות ודוגמאות</li>
                            <li>התייחסות לעמדה נגדית והפרכה שלה</li>
                            <li>מסקנה: חיזוק העמדה וקריאה לפעולה</li>
                        </ul>
                        <div class="example-box">
                            <strong>דוגמה לפתיחה:</strong> "אף על פי שיש הטוענים כי רשתות חברתיות מחברות בין אנשים, למעשה הן מרחיקות אותנו זה מזה יותר מתמיד."
                        </div>
                    </div>

                    <div class="tip-section">
                        <h5>💪 טיפים מעשיים</h5>
                        <ul>
                            <li>השתמש בדוגמאות קונקרטיות ומקורות אמינים</li>
                            <li>סדר הטיעונים: מהחלש לחזק ביותר</li>
                            <li>מילות קישור: "ראשית", "שנית", "יתרה מכך", "לכן"</li>
                            <li>הצג את טענת הנגד בהוגנות לפני ההפרכה</li>
                        </ul>
                        <div class="example-box">
                            <strong>דוגמה למעבר:</strong> "בנוסף לכך, חשוב לציין כי..." או "מצד שני, יש לזכור ש..."
                        </div>
                    </div>
                </div>
            </div>

            <!-- חיבור תיאור -->
            <div class="step-content" id="descriptive">
                <div class="progress-indicator">שלב 1: תכנון חיבור תיאור 🎨</div>
                
                <button class="btn-secondary back-btn" onclick="goBack()">← חזרה לבחירת סוג חיבור</button>
                
                <div class="card">
                    <h3>תכנון החיבור התיאורי שלך 🎨</h3>
                    
                    <div class="input-group">
                        <label for="descTopic">מה אתה רוצה לתאר?</label>
                        <input type="text" id="descTopic" placeholder="למשל: הגן הבוטני בעיר, זכרון ילדות, מקום מיוחד">
                    </div>

                    <div class="input-group">
                        <label for="descMainImpression">איזה רושם כללי אתה רוצה ליצור?</label>
                        <textarea id="descMainImpression" placeholder="תאר את האווירה או הרגש שאתה רוצה להעביר..."></textarea>
                    </div>

                    <div class="input-group">
                        <label for="descAspects">3 היבטים עיקריים לתיאור:</label>
                        <textarea id="descAspects" placeholder="היבט 1: המראה החיצוני...&#10;היבט 2: הקולות והריחות...&#10;היבט 3: התחושות והרגשות..."></textarea>
                    </div>

                    <div class="input-group">
                        <label for="descSenses">רשום חוויות חושיות ספציפיות:</label>
                        <textarea id="descSenses" placeholder="מה רואים, שומעים, מריחים, מרגישים, טועמים..."></textarea>
                    </div>

                    <button class="btn-primary" onclick="generateOutline('descriptive')">צור מתווה לחיבור 🚀</button>
                    <div id="descOutline"></div>
                </div>

                <div class="tips-box">
                    <h4>🎨 טיפים לחיבור תיאור מוצלח</h4>
                    
                    <div class="tip-section">
                        <h5>🌟 יצירת אטמוספרה</h5>
                        <ul>
                            <li>השתמש בכל החושים - לא רק ראייה</li>
                            <li>בנה מהכללי לפרטי או מהפרטי לכללי</li>
                            <li>צור חוויה חושית שהקורא ירגיש אותה</li>
                            <li>השתמש בשפה עשירה ומגוונת</li>
                        </ul>
                        <div class="example-box">
                            <strong>דוגמה חושית:</strong> "הריח החמצמץ של הגשם הראשון התערבב עם ניחוח הפרחים הבשלים, בעוד קולות הציפורים מילאו את האוויר בשיר בוקר עדין."
                        </div>
                    </div>

                    <div class="tip-section">
                        <h5>🎭 כלים ספרותיים</h5>
                        <ul>
                            <li>השתמש במטפורות והשוואות יצירתיות</li>
                            <li>תאר פרטים קטנים שיוצרים רגש</li>
                            <li>השתמש בצבעים, צורות וטקסטורות</li>
                            <li>צור קצב וזרימה בכתיבה</li>
                        </ul>
                        <div class="example-box">
                            <strong>דוגמה מטפורית:</strong> "הרוח לחשה סודות בעלי העצים", "השמש ציירה צללים רוקדים על הרצפה"
                        </div>
                    </div>
                </div>
            </div>

            <!-- מכתב רשמי -->
            <div class="step-content" id="formal_letter">
                <div class="progress-indicator">שלב 1: תכנון מכתב רשמי 📋</div>
                
                <button class="btn-secondary back-btn" onclick="goBack()">← חזרה לבחירת סוג חיבור</button>
                
                <div class="card">
                    <h3>תכנון המכתב הרשמי שלך 📋</h3>
                    
                    <div class="input-group">
                        <label for="formalPurpose">מה המטרה של המכתב?</label>
                        <input type="text" id="formalPurpose" placeholder="למשל: בקשה לדחיית בחינה, תלונה על שירות, בקשה למלגה">
                    </div>

                    <div class="input-group">
                        <label for="formalRecipient">למי אתה פונה?</label>
                        <input type="text" id="formalRecipient" placeholder="למשל: מנהל בית הספר, מחלקת שירות לקוחות, ועדת מלגות">
                    </div>

                    <div class="input-group">
                        <label for="formalMainPoints">3 נקודות עיקריות שברצונך להעביר:</label>
                        <textarea id="formalMainPoints" placeholder="נקודה 1: הבעיה או הבקשה...&#10;נקודה 2: הסיבות והנסיבות...&#10;נקודה 3: מה אתה מבקש לקבל..."></textarea>
                    </div>

                    <div class="input-group">
                        <label for="formalDetails">פרטים רלוונטיים (תאריכים, מספרי אסמכתה וכו'):</label>
                        <textarea id="formalDetails" placeholder="רשום פרטים חשובים שצריך לכלול במכתב..."></textarea>
                    </div>

                    <button class="btn-primary" onclick="generateOutline('formal_letter')">צור מתווה למכתב 🚀</button>
                    <div id="formalOutline"></div>
                </div>

                <div class="tips-box">
                    <h4>📋 טיפים למכתב רשמי מוצלח</h4>
                    
                    <div class="tip-section">
                        <h5>🏗️ מבנה נדרש</h5>
                        <ul>
                            <li>כתובת השולח ותאריך (בראש המכתב)</li>
                            <li>כתובת הנמען ונושא המכתב</li>
                            <li>פנייה מנומסת ("אדון/גברת נכבד/ה")</li>
                            <li>גוף המכתב - הבהרת המטרה ופירוט הבקשה</li>
                            <li>סיום מנומס וחתימה</li>
                        </ul>
                        <div class="example-box">
                            <strong>דוגמה לפתיחה:</strong> "הנדון: בקשה לדחיית מועד בחינה<br>אדון/גברת נכבד/ה,<br>אני פונה אליכם בעניין בקשה לדחיית מועד בחינה..."
                        </div>
                    </div>

                    <div class="tip-section">
                        <h5>💼 שפה וסגנון</h5>
                        <ul>
                            <li>השתמש בשפה מכובדת ותמציתית</li>
                            <li>הבהר את המטרה כבר בפסקה הראשונה</li>
                            <li>היה ברור ומדויק בבקשתך</li>
                            <li>השתמש בביטויים מקובלים ומנומסים</li>
                        </ul>
                        <div class="example-box">
                            <strong>ביטויים מועילים:</strong> "אני פונה אליכם בעניין...", "אודה לקבל מענה בהקדם", "בכבוד רב", "בתודה מראש"
                        </div>
                    </div>
                </div>
            </div>

            <!-- מכתב לחבר -->
            <div class="step-content" id="friendly_letter">
                <div class="progress-indicator">שלב 1: תכנון מכתב לחבר 💌</div>
                
                <button class="btn-secondary back-btn" onclick="goBack()">← חזרה לבחירת סוג חיבור</button>
                
                <div class="card">
                    <h3>תכנון המכתב לחבר שלך 💌</h3>
                    
                    <div class="input-group">
                        <label for="friendlyRecipient">לאיזה חבר אתה כותב?</label>
                        <input type="text" id="friendlyRecipient" placeholder="שם החבר ואיך אתם מכירים...">
                    </div>

                    <div class="input-group">
                        <label for="friendlyPurpose">מה הסיבה לכתיבת המכתב?</label>
                        <textarea id="friendlyPurpose" placeholder="למשל: לספר על חופשה, להזמין לאירוע, לעדכן על חדשות..."></textarea>
                    </div>

                    <div class="input-group">
                        <label for="friendlyContent">3 דברים עיקריים שאתה רוצה לספר:</label>
                        <textarea id="friendlyContent" placeholder="דבר 1: ...&#10;דבר 2: ...&#10;דבר 3: ..."></textarea>
                    </div>

                    <div class="input-group">
                        <label for="friendlyMemories">זכרונות או חוויות משותפים שאתה רוצה להזכיר:</label>
                        <textarea id="friendlyMemories" placeholder="תאר זכרונות או חוויות שהיו לכם ביחד..."></textarea>
                    </div>

                    <div class="input-group">
                        <label for="friendlyPlans">תוכניות או הצעות לעתיד:</label>
                        <textarea id="friendlyPlans" placeholder="מה אתה מציע לעשות ביחד, מתי להיפגש..."></textarea>
                    </div>

                    <button class="btn-primary" onclick="generateOutline('friendly_letter')">צור מתווה למכתב 🚀</button>
                    <div id="friendlyOutline"></div>
                </div>

                <div class="tips-box">
                    <h4>💌 טיפים למכתב חבר מוצלח</h4>
                    
                    <div class="tip-section">
                        <h5>❤️ טון אישי וחם</h5>
                        <ul>
                            <li>השתמש בשפה טבעית ורגועה</li>
                            <li>התחל בשאלה על מצבו של החבר</li>
                            <li>התייחס לאירועים או זכרונות משותפים</li>
                            <li>הראה עניין אמיתי בחייו</li>
                        </ul>
                        <div class="example-box">
                            <strong>דוגמה לפתיחה:</strong> "היי רון! איך אתה? מזמן לא שמעתי ממך! אתמול קרה לי משהו מצחיק שחייב לספר לך..."
                        </div>
                    </div>

                    <div class="tip-section">
                        <h5>😊 תוכן מעניין ואישי</h5>
                        <ul>
                            <li>שתף חוויות אישיות ורגשות</li>
                            <li>השתמש בהומור מתאים וקל</li>
                            <li>תאר אירועים בפירוט ובחיות</li>
                            <li>סיים בביטוי חיבה או תוכניות להיפגש</li>
                        </ul>
                        <div class="example-box">
                            <strong>סיומים חמים:</strong> "מתגעגע אליך המון!", "מחכה לפגישה הבאה שלנו", "כתוב לי בחזרה מהר!"
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        let currentEssayType = '';
        let essayData = {};

        function selectEssayType(type) {
            // הסתר את כל הכרטיסיות
            document.querySelectorAll('.essay-type-card').forEach(card => {
                card.classList.remove('selected');
            });

            // סמן את הכרטיסייה הנבחרת
            event.target.closest('.essay-type-card').classList.add('selected');

            // המתן קצת ואז עבור לדף הרלוונטי
            setTimeout(() => {
                currentEssayType = type;
                showStep(type);
            }, 300);
        }

        function showStep(stepId) {
            // הסתר את כל השלבים
            document.querySelectorAll('.step-content').forEach(step => {
                step.classList.remove('active');
            });

            // הצג את השלב הנבחר
            const targetStep = document.getElementById(stepId);
            if (targetStep) {
                targetStep.classList.add('active');
            }
        }

        function goBack() {
            showStep('essayTypeSelection');
            currentEssayType = '';
        }

        function generateOutline(type) {
            let outlineHtml = '';
            let isValid = true;

            switch(type) {
                case 'argumentative':
                    const argTopic = document.getElementById('argTopic').value;
                    const argPosition = document.getElementById('argPosition').value;
                    const argArguments = document.getElementById('argArguments').value;
                    const argCounterArgument = document.getElementById('argCounterArgument').value;
                    const argRefutation = document.getElementById('argRefutation').value;

                    if (!argTopic || !argPosition || !argArguments || !argCounterArgument || !argRefutation) {
                        alert('אנא מלא את כל השדות כדי לקבל מתווה מותאם!');
                        return;
                    }

                    const argsList = argArguments.split('\n').filter(arg => arg.trim());
                    
                    outlineHtml = `
                        <div style="background: #e8f5e8; border: 2px solid #4caf50; border-radius: 10px; padding: 20px; margin-top: 15px;">
                            <h4 style="color: #2e7d32; margin-bottom: 15px;">🎯 המתווה שלך מוכן!</h4>
                            <div style="background: white; padding: 20px; border-radius: 8px;">
                                <h5 style="color: #1565c0; margin-bottom: 15px;">📝 מבנה החיבור הטיעוני:</h5>
                                <p><strong>🌟 הקדמה:</strong> הצגת הנושא "${argTopic}" והעמדה: "${argPosition}"</p>
                                ${argsList.map((arg, index) => `<p><strong>📍 פסקת גוף ${index + 1}:</strong> ${arg.trim()}</p>`).join('')}
                                <p><strong>⚖️ טענת נגד:</strong> ${argCounterArgument}</p>
                                <p><strong>💪 הפרכה:</strong> ${argRefutation}</p>
                                <p><strong>🎯 מסקנה:</strong> חיזוק העמדה וסיכום הטיעונים</p>
                            </div>
                            <div style="margin-top: 15px; text-align: center;">
                                <button class="btn-primary" onclick="startWriting('argumentative')">התחל לכתוב את החיבור! ✍️</button>
                            </div>
                        </div>
                    `;
                    document.getElementById('argOutline').innerHTML = outlineHtml;
                    break;

                case 'descriptive':
                    const descTopic = document.getElementById('descTopic').value;
                    const descMainImpression = document.getElementById('descMainImpression').value;
                    const descAspects = document.getElementById('descAspects').value;
                    const descSenses = document.getElementById('descSenses').value;

                    if (!descTopic || !descMainImpression || !descAspects || !descSenses) {
                        alert('אנא מלא את כל השדות כדי לקבל מתווה מותאם!');
                        return;
                    }

                    const aspectsList = descAspects.split('\n').filter(aspect => aspect.trim());
                    
                    outlineHtml = `
                        <div style="background: #e8f5e8; border: 2px solid #4caf50; border-radius: 10px; padding: 20px; margin-top: 15px;">
                            <h4 style="color: #2e7d32; margin-bottom: 15px;">🎨 המתווה שלך מוכן!</h4>
                            <div style="background: white; padding: 20px; border-radius: 8px;">
                                <h5 style="color: #1565c0; margin-bottom: 15px;">📝 מבנה חיבור התיאור:</h5>
                                <p><strong>🌟 הקדמה:</strong> יצירת רושם ראשוני של "${descTopic}"</p>
                                <p><strong>💫 הרושם הכללי:</strong> ${descMainImpression}</p>
                                ${aspectsList.map((aspect, index) => `<p><strong>🎭 פסקת תיאור ${index + 1}:</strong> ${aspect.trim()}</p>`).join('')}
                                <p><strong>👁️ חוויות חושיות:</strong> ${descSenses}</p>
                                <p><strong>🎯 מסקנה:</strong> חזרה לרושם הכללי ועמקת התיאור</p>
                            </div>
                            <div style="margin-top: 15px; text-align: center;">
                                <button class="btn-primary" onclick="startWriting('descriptive')">התחל לכתוב את החיבור! ✍️</button>
                            </div>
                        </div>
                    `;
                    document.getElementById('descOutline').innerHTML = outlineHtml;
                    break;

                case 'formal_letter':
                    const formalPurpose = document.getElementById('formalPurpose').value;
                    const formalRecipient = document.getElementById('formalRecipient').value;
                    const formalMainPoints = document.getElementById('formalMainPoints').value;
                    const formalDetails = document.getElementById('formalDetails').value;

                    if (!formalPurpose || !formalRecipient || !formalMainPoints) {
                        alert('אנא מלא את השדות החובה כדי לקבל מתווה מותאם!');
                        return;
                    }

                    const pointsList = formalMainPoints.split('\n').filter(point => point.trim());
                    
                    outlineHtml = `
                        <div style="background: #e8f5e8; border: 2px solid #4caf50; border-radius: 10px; padding: 20px; margin-top: 15px;">
                            <h4 style="color: #2e7d32; margin-bottom: 15px;">📋 המתווה שלך מוכן!</h4>
                            <div style="background: white; padding: 20px; border-radius: 8px;">
                                <h5 style="color: #1565c0; margin-bottom: 15px;">📝 מבנה המכתב הרשמי:</h5>
                                <p><strong>📍 כתובת ותאריך</strong></p>
                                <p><strong>📮 נמען:</strong> ${formalRecipient}</p>
                                <p><strong>📋 נושא:</strong> ${formalPurpose}</p>
                                <p><strong>🌟 פתיחה מנומסת</strong></p>
                                ${pointsList.map((point, index) => `<p><strong>📍 נקודה ${index + 1}:</strong> ${point.trim()}</p>`).join('')}
                                ${formalDetails ? `<p><strong>📄 פרטים נוספים:</strong> ${formalDetails}</p>` : ''}
                                <p><strong>🎯 סיום וחתימה מנומסת</strong></p>
                            </div>
                            <div style="margin-top: 15px; text-align: center;">
                                <button class="btn-primary" onclick="startWriting('formal_letter')">התחל לכתוב את המכתב! ✍️</button>
                            </div>
                        </div>
                    `;
                    document.getElementById('formalOutline').innerHTML = outlineHtml;
                    break;

                case 'friendly_letter':
                    const friendlyRecipient = document.getElementById('friendlyRecipient').value;
                    const friendlyPurpose = document.getElementById('friendlyPurpose').value;
                    const friendlyContent = document.getElementById('friendlyContent').value;
                    const friendlyMemories = document.getElementById('friendlyMemories').value;
                    const friendlyPlans = document.getElementById('friendlyPlans').value;

                    if (!friendlyRecipient || !friendlyPurpose || !friendlyContent) {
                        alert('אנא מלא את השדות החובה כדי לקבל מתווה מותאם!');
                        return;
                    }

                    const contentList = friendlyContent.split('\n').filter(item => item.trim());
                    
                    outlineHtml = `
                        <div style="background: #e8f5e8; border: 2px solid #4caf50; border-radius: 10px; padding: 20px; margin-top: 15px;">
                            <h4 style="color: #2e7d32; margin-bottom: 15px;">💌 המתווה שלך מוכן!</h4>
                            <div style="background: white; padding: 20px; border-radius: 8px;">
                                <h5 style="color: #1565c0; margin-bottom: 15px;">📝 מבנה המכתב לחבר:</h5>
                                <p><strong>💌 פתיחה חמה:</strong> בירורי שלום ל${friendlyRecipient}</p>
                                <p><strong>🎯 מטרת המכתב:</strong> ${friendlyPurpose}</p>
                                ${contentList.map((item, index) => `<p><strong>📍 נושא ${index + 1}:</strong> ${item.trim()}</p>`).join('')}
                                ${friendlyMemories ? `<p><strong>💭 זכרונות משותפים:</strong> ${friendlyMemories}</p>` : ''}
                                ${friendlyPlans ? `<p><strong>🚀 תוכניות לעתיד:</strong> ${friendlyPlans}</p>` : ''}
                                <p><strong>❤️ סיום חם וביטוי געגועים</strong></p>
                            </div>
                            <div style="margin-top: 15px; text-align: center;">
                                <button class="btn-primary" onclick="startWriting('friendly_letter')">התחל לכתוב את המכתב! ✍️</button>
                            </div>
                        </div>
                    `;
                    document.getElementById('friendlyOutline').innerHTML = outlineHtml;
                    break;
            }

            // שמירת הנתונים
            essayData[type] = {
                topic: document.getElementById(type === 'argumentative' ? 'argTopic' : 
                                             type === 'descriptive' ? 'descTopic' : 
                                             type === 'formal_letter' ? 'formalPurpose' : 'friendlyRecipient').value,
                allData: Array.from(document.querySelectorAll(`#${type} input, #${type} textarea`)).reduce((acc, input) => {
                    if (input.value) acc[input.id] = input.value;
                    return acc;
                }, {})
            };
        }

        function startWriting(type) {
            alert(`🎉 מעולה! עכשיו אתה מוכן להתחיל לכתוב את ${type === 'argumentative' ? 'החיבור הטיעוני' : 
                                                                    type === 'descriptive' ? 'חיבור התיאור' :
                                                                    type === 'formal_letter' ? 'המכתב הרשמי' : 'המכתב לחבר'} שלך!
            
💡 טיפ: שמור את המתווה בצד וכתוב לפיו את החיבור במחברת או במחשב.
            
בהצלחה! 🚀`);
        }

        // הוספת אנימציות נוספות
        document.addEventListener('DOMContentLoaded', function() {
            // אנימציה לכפתורים
            const buttons = document.querySelectorAll('.btn-primary, .btn-secondary');
            buttons.forEach(button => {
                button.addEventListener('click', function() {
                    this.style.transform = 'scale(0.95)';
                    setTimeout(() => {
                        this.style.transform = '';
                    }, 150);
                });
            });

            // הוספת גבולות מעוגלים לשדות קלט בפוקוס
            const inputs = document.querySelectorAll('input, textarea');
            inputs.forEach(input => {
                input.addEventListener('focus', function() {
                    this.style.borderColor = '#667eea';
                    this.style.boxShadow = '0 0 0 3px rgba(102, 126, 234, 0.1)';
                });

                input.addEventListener('blur', function() {
                    this.style.borderColor = '#e1e1e1';
                    this.style.boxShadow = 'none';
                });
            });
        });
    </script>
</body>
</html>
