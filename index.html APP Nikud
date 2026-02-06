<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>נקודות טובות - ניהול כיתה</title>
    <!-- Google Fonts: Heebo for modern Hebrew typography -->
    <link href="https://fonts.googleapis.com/css2?family=Heebo:wght@300;400;700;900&display=swap" rel="stylesheet">
    <!-- Chart.js for progress reports -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        :root {
            --primary-yellow: #FFD54F;
            --primary-teal: #4DB6AC;
            --bg-light: #f4f7f6;
            --text-dark: #37474f;
            --white: #ffffff;
            --shadow: 0 4px 6px rgba(0,0,0,0.1);
            --transition: all 0.3s ease;
            --success: #66bb6a;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Heebo', sans-serif;
        }

        body {
            background-color: var(--bg-light);
            color: var(--text-dark);
            line-height: 1.6;
            padding-bottom: 50px;
        }

        /* Layout Sections */
        header {
            background: linear-gradient(135deg, var(--primary-teal), #26a69a);
            color: white;
            padding: 1.5rem 1rem;
            text-align: center;
            box-shadow: var(--shadow);
            margin-bottom: 1rem;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 1rem;
        }

        /* Controls Bar */
        .controls-bar {
            background: var(--white);
            padding: 1rem;
            border-radius: 12px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1rem;
            box-shadow: var(--shadow);
            flex-wrap: wrap;
            gap: 1rem;
        }

        /* Bulk Actions Bar */
        .bulk-actions {
            background: #e0f2f1;
            padding: 0.8rem;
            border-radius: 12px;
            margin-bottom: 1.5rem;
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            align-items: center;
            justify-content: center;
            border: 1px solid var(--primary-teal);
        }

        .bulk-btn {
            padding: 5px 12px;
            background: white;
            border: 1px solid var(--primary-teal);
            border-radius: 20px;
            font-size: 0.85rem;
            cursor: pointer;
            transition: var(--transition);
        }

        .bulk-btn:hover {
            background: var(--primary-teal);
            color: white;
        }

        .date-picker-wrapper {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        input[type="date"] {
            padding: 8px 12px;
            border: 2px solid var(--primary-teal);
            border-radius: 8px;
            font-size: 1rem;
            outline: none;
        }

        .btn {
            padding: 10px 20px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 700;
            transition: var(--transition);
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .btn-primary { background-color: var(--primary-yellow); color: #5f4b00; }
        .btn-primary:hover { background-color: #ffca28; transform: translateY(-2px); }
        .btn-teal { background-color: var(--primary-teal); color: white; }
        .btn-teal:hover { background-color: #00897b; transform: translateY(-2px); }

        /* Student Grid */
        .student-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 1.5rem;
        }

        .student-card {
            background: var(--white);
            border-radius: 15px;
            padding: 1.2rem;
            box-shadow: var(--shadow);
            transition: var(--transition);
            position: relative;
            overflow: hidden;
            border-top: 5px solid transparent;
        }

        .student-card.perfect-score {
            border-top-color: var(--primary-yellow);
            background: #fffdf5;
        }

        .student-name {
            font-size: 1.3rem;
            font-weight: 900;
            margin-bottom: 0.8rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .score-badge {
            background: var(--primary-teal);
            color: white;
            padding: 2px 10px;
            border-radius: 20px;
            font-size: 0.85rem;
        }

        .criteria-list {
            list-style: none;
        }

        .criteria-item {
            display: flex;
            align-items: center;
            margin-bottom: 6px;
            padding: 8px 12px;
            border-radius: 8px;
            background: #f9f9f9;
            cursor: pointer;
            user-select: none;
            transition: background 0.2s, transform 0.1s;
        }

        .criteria-item:hover { background: #f0f0f0; }
        .criteria-item:active { transform: scale(0.98); }
        
        .criteria-item input[type="checkbox"] {
            width: 20px;
            height: 20px;
            margin-left: 12px;
            cursor: pointer;
            accent-color: var(--primary-teal);
            pointer-events: none; /* Allows click to pass through to item */
        }

        .criteria-label {
            flex-grow: 1;
            font-size: 1rem;
        }

        /* Stars Container */
        .stars-container {
            display: flex;
            gap: 6px;
            margin-top: 12px;
            padding-top: 10px;
            border-top: 1px dashed #ddd;
            justify-content: center;
        }

        .star { 
            color: #e0e0e0; 
            font-size: 1.5rem; 
            transition: transform 0.2s cubic-bezier(0.175, 0.885, 0.32, 1.275), color 0.2s;
        }
        
        .star.active { 
            color: var(--primary-yellow); 
            transform: scale(1.15);
            text-shadow: 0 0 8px rgba(255, 213, 79, 0.6);
        }

        /* Animation */
        @keyframes celebrate {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
        .animate-celebrate { animation: celebrate 0.5s ease-in-out; }

        /* Reports Section */
        .reports-section {
            display: none;
            margin-top: 2rem;
            background: white;
            padding: 2rem;
            border-radius: 15px;
            box-shadow: var(--shadow);
        }

        .chart-container {
            position: relative;
            height: 400px;
            width: 100%;
        }

        /* Read Only Mode Overlay */
        .readonly-overlay {
            position: absolute;
            top: 0; left: 0; right: 0; bottom: 0;
            background: rgba(255,255,255,0.1);
            z-index: 10;
            cursor: not-allowed;
            display: none;
        }
        .student-card.readonly .readonly-overlay { display: block; }

        /* Modal Styles */
        .modal {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.5);
            display: none;
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }
        .modal-content {
            background: white;
            padding: 2rem;
            border-radius: 12px;
            max-width: 400px;
            width: 90%;
            text-align: center;
        }

        /* Responsive */
        @media (max-width: 768px) {
            .student-grid { grid-template-columns: 1fr; }
            .controls-bar { flex-direction: column; align-items: stretch; }
            .bulk-actions { padding: 0.5rem; }
        }
    </style>
</head>
<body>

<header>
    <h1>נקודות טובות ⭐</h1>
    <p>מעקב התקדמות יומית - כיתה ה'2</p>
</header>

<div class="container">
    <!-- Main Controls -->
    <div class="controls-bar">
        <div class="date-picker-wrapper">
            <label for="date-select">תאריך:</label>
            <input type="date" id="date-select">
        </div>
        
        <div style="display: flex; gap: 10px;">
            <button class="btn btn-primary" onclick="createNewDay()">
                ✨ יום חדש
            </button>
            <button class="btn btn-teal" onclick="toggleView('grid')">
                📋 רשימה
            </button>
            <button class="btn btn-teal" onclick="toggleView('reports')">
                📊 דוחות
            </button>
        </div>
    </div>

    <!-- Bulk Action Bar -->
    <div id="bulk-bar" class="bulk-actions">
        <span style="font-weight: bold; margin-left: 10px;">סמן לכולם:</span>
        <button class="bulk-btn" onclick="bulkAction('att')">תלבושת</button>
        <button class="bulk-btn" onclick="bulkAction('ontime')">הגעה בזמן</button>
        <button class="bulk-btn" onclick="bulkAction('beh1')">שיעור 1</button>
        <button class="bulk-btn" onclick="bulkAction('beh2')">שיעור 2</button>
        <button class="bulk-btn" onclick="bulkClear()">נקה הכל</button>
    </div>

    <!-- Main Student Grid -->
    <div id="grid-view" class="student-grid">
        <!-- JS injects students here -->
    </div>

    <!-- Reports Section -->
    <div id="reports-view" class="reports-section">
        <h2 style="margin-bottom: 1.5rem;">סיכום התקדמות כיתתי</h2>
        <div class="chart-container">
            <canvas id="progressChart"></canvas>
        </div>
        <div style="margin-top: 2rem;">
            <h3>סטטיסטיקה השבוע:</h3>
            <p id="stats-summary">טוען נתונים...</p>
        </div>
    </div>
</div>

<!-- Simple Confirmation Modal -->
<div id="modal" class="modal">
    <div class="modal-content">
        <h3 id="modal-title">הודעה</h3>
        <p id="modal-body" style="margin: 1rem 0;"></p>
        <div style="display: flex; gap: 10px; justify-content: center;">
            <button class="btn btn-teal" onclick="closeModal()">אישור</button>
        </div>
    </div>
</div>

<script>
    // --- Configuration (List Updated) ---
    const STUDENTS = [
        "ליאושר", "אור", "טוהר", "מיכאל", "אביה", 
        "נתנאל מלכה", "קרן", "אלין", "אילאי", "איתמר", 
        "תהל", "עדי", "שירה", "מיכל", "נתנאל טגניה", 
        "שי-לי", "אושרת"
    ];

    const CRITERIA = [
        { id: 'att', label: 'תלבושת' },
        { id: 'ontime', label: 'הגעה בזמן' },
        { id: 'beh1', label: 'התנהגות בשיעור 1' },
        { id: 'work1', label: 'עבודה בכיתה 1' },
        { id: 'beh2', label: 'התנהגות בשיעור 2' },
        { id: 'work2', label: 'עבודה בכיתה 2' }
    ];

    // --- State Management ---
    let currentDate = new Date().toISOString().split('T')[0];
    let classData = JSON.parse(localStorage.getItem('nekudot_tovot_data')) || {};
    let chartInstance = null;

    // --- Initialization ---
    window.onload = () => {
        const dateInput = document.getElementById('date-select');
        dateInput.value = currentDate;
        
        dateInput.addEventListener('change', (e) => {
            currentDate = e.target.value;
            renderStudents();
            updateBulkVisibility();
        });

        renderStudents();
        updateBulkVisibility();
        initAutoSave();
    };

    function updateBulkVisibility() {
        const isPastDate = new Date(currentDate) < new Date(new Date().toISOString().split('T')[0]);
        document.getElementById('bulk-bar').style.display = isPastDate ? 'none' : 'flex';
    }

    function renderStudents() {
        const grid = document.getElementById('grid-view');
        grid.innerHTML = '';
        
        const isPastDate = new Date(currentDate) < new Date(new Date().toISOString().split('T')[0]);
        const dayData = classData[currentDate] || {};

        STUDENTS.forEach(name => {
            const studentScore = dayData[name] || {};
            const scoreCount = Object.values(studentScore).filter(Boolean).length;
            const isPerfect = scoreCount === CRITERIA.length;

            const card = document.createElement('div');
            card.className = `student-card ${isPerfect ? 'perfect-score' : ''} ${isPastDate ? 'readonly' : ''}`;
            
            let criteriaHtml = '';
            CRITERIA.forEach(c => {
                const checked = studentScore[c.id] ? 'checked' : '';
                criteriaHtml += `
                    <li class="criteria-item" onclick="handleCheck('${name}', '${c.id}', this)">
                        <input type="checkbox" ${checked} ${isPastDate ? 'disabled' : ''}>
                        <span class="criteria-label">${c.label}</span>
                    </li>
                `;
            });

            let starsHtml = '';
            for(let i=1; i<=6; i++) {
                starsHtml += `<span class="star ${i <= scoreCount ? 'active' : ''}">★</span>`;
            }

            card.innerHTML = `
                ${isPastDate ? '<div class="readonly-overlay"></div>' : ''}
                <div class="student-name">
                    ${name}
                    <span class="score-badge">${scoreCount}/6</span>
                </div>
                <ul class="criteria-list">
                    ${criteriaHtml}
                </ul>
                <div class="stars-container">
                    ${starsHtml}
                </div>
            `;
            grid.appendChild(card);
        });
    }

    // --- Actions ---
    function handleCheck(studentName, criteriaId, element) {
        // Prevent action on past dates
        if (new Date(currentDate) < new Date(new Date().toISOString().split('T')[0])) return;

        const checkbox = element.querySelector('input');
        const newState = !checkbox.checked;
        checkbox.checked = newState;

        if (!classData[currentDate]) classData[currentDate] = {};
        if (!classData[currentDate][studentName]) classData[currentDate][studentName] = {};

        classData[currentDate][studentName][criteriaId] = newState;
        
        updateCardUI(studentName, element.closest('.student-card'));
        saveToLocalStorage();
    }

    function updateCardUI(name, cardElement) {
        const dayData = classData[currentDate][name] || {};
        const scoreCount = Object.values(dayData).filter(Boolean).length;
        
        // Update score badge
        cardElement.querySelector('.score-badge').innerText = `${scoreCount}/6`;
        
        // Update Stars
        const stars = cardElement.querySelectorAll('.star');
        stars.forEach((star, index) => {
            star.classList.toggle('active', index < scoreCount);
        });

        // Perfect score celebration
        if (scoreCount === 6) {
            cardElement.classList.add('perfect-score', 'animate-celebrate');
            setTimeout(() => cardElement.classList.remove('animate-celebrate'), 500);
        } else {
            cardElement.classList.remove('perfect-score');
        }
    }

    // --- Bulk Operations ---
    function bulkAction(criteriaId) {
        if (!classData[currentDate]) classData[currentDate] = {};
        
        STUDENTS.forEach(name => {
            if (!classData[currentDate][name]) classData[currentDate][name] = {};
            classData[currentDate][name][criteriaId] = true;
        });
        
        saveToLocalStorage();
        renderStudents();
    }

    function bulkClear() {
        classData[currentDate] = {};
        saveToLocalStorage();
        renderStudents();
    }

    function createNewDay() {
        const today = new Date().toISOString().split('T')[0];
        document.getElementById('date-select').value = today;
        currentDate = today;
        
        if (!classData[today]) {
            classData[today] = {};
            saveToLocalStorage();
            showModal("יום חדש", "התחלת יום חדש בהצלחה! כל הנתונים יאופסו להיום.");
        }
        renderStudents();
        updateBulkVisibility();
    }

    // --- Views & Reports ---
    function toggleView(view) {
        const gridView = document.getElementById('grid-view');
        const reportsView = document.getElementById('reports-view');
        const bulkBar = document.getElementById('bulk-bar');
        
        if (view === 'grid') {
            gridView.style.display = 'grid';
            reportsView.style.display = 'none';
            updateBulkVisibility();
        } else {
            gridView.style.display = 'none';
            reportsView.style.display = 'block';
            bulkBar.style.display = 'none';
            renderReports();
        }
    }

    function renderReports() {
        const ctx = document.getElementById('progressChart').getContext('2d');
        const last7Days = [];
        for (let i = 6; i >= 0; i--) {
            const d = new Date();
            d.setDate(d.getDate() - i);
            last7Days.push(d.toISOString().split('T')[0]);
        }

        const averages = last7Days.map(date => {
            const dayData = classData[date];
            if (!dayData) return 0;
            let totalPoints = 0;
            let studentCount = 0;
            Object.values(dayData).forEach(studentScore => {
                totalPoints += Object.values(studentScore).filter(Boolean).length;
                studentCount++;
            });
            return studentCount ? (totalPoints / studentCount).toFixed(1) : 0;
        });

        if (chartInstance) chartInstance.destroy();
        chartInstance = new Chart(ctx, {
            type: 'line',
            data: {
                labels: last7Days.map(d => d.split('-').reverse().slice(0,2).join('/')),
                datasets: [{
                    label: 'ממוצע כיתתי (מתוך 6)',
                    data: averages,
                    borderColor: '#4DB6AC',
                    backgroundColor: 'rgba(77, 182, 172, 0.2)',
                    fill: true,
                    tension: 0.4,
                    pointRadius: 6,
                    pointBackgroundColor: '#FFD54F'
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                scales: { y: { beginAtZero: true, max: 6 } },
                plugins: { legend: { labels: { font: { family: 'Heebo' } } } }
            }
        });

        const currentAvg = averages[averages.length - 1];
        const prevAvg = averages[averages.length - 2] || 0;
        const trend = currentAvg >= prevAvg ? 'במגמת עלייה 📈' : 'במגמת ירידה 📉';
        document.getElementById('stats-summary').innerHTML = `ממוצע היום: <strong>${currentAvg}</strong> נקודות לתלמיד. <br>הכיתה נמצאת ${trend} בהשוואה לאתמול.`;
    }

    function saveToLocalStorage() {
        try {
            localStorage.setItem('nekudot_tovot_data', JSON.stringify(classData));
        } catch (e) {
            console.error("Storage error", e);
        }
    }

    function initAutoSave() { setInterval(saveToLocalStorage, 30000); }
    function showModal(title, body) {
        document.getElementById('modal-title').innerText = title;
        document.getElementById('modal-body').innerText = body;
        document.getElementById('modal').style.display = 'flex';
    }
    function closeModal() { document.getElementById('modal').style.display = 'none'; }
</script>
</body>
</html>
