<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Smart Savings Tracker | ระบบออมเงินอัจฉริยะ</title>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+Thai:wght@300;400;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #2563eb;
            --secondary: #10b981;
            --bg: #f1f5f9;
            --card: #ffffff;
            --text: #1e293b;
        }

        * { box-sizing: border-box; font-family: 'Noto Sans Thai', sans-serif; }
        body { background-color: var(--bg); color: var(--text); margin: 0; padding: 20px; }
        .container { max-width: 800px; margin: 0 auto; }

        header { text-align: center; margin-bottom: 30px; }
        h1 { color: var(--primary); margin-bottom: 5px; }

        /* Dashboard Grid */
        .dashboard {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 15px;
            margin-bottom: 30px;
        }
        .stat-card {
            background: var(--card);
            padding: 20px;
            border-radius: 15px;
            text-align: center;
            box-shadow: 0 4px 6px -1px rgba(0,0,0,0.1);
        }
        .stat-card h3 { margin: 0; font-size: 0.9rem; color: #64748b; }
        .stat-card p { margin: 10px 0 0; font-size: 1.4rem; font-weight: 700; color: var(--primary); }

        /* Tabs & Forms */
        .main-card {
            background: var(--card);
            padding: 25px;
            border-radius: 20px;
            box-shadow: 0 10px 15px -3px rgba(0,0,0,0.1);
        }
        .tabs { display: flex; gap: 10px; margin-bottom: 20px; border-bottom: 2px solid #e2e8f0; }
        .tab-btn {
            padding: 10px 20px; border: none; background: none; cursor: pointer;
            font-weight: 600; color: #94a3b8; transition: 0.3s;
        }
        .tab-btn.active { color: var(--primary); border-bottom: 3px solid var(--primary); }

        .form-group { margin-bottom: 15px; }
        label { display: block; margin-bottom: 5px; font-weight: 600; }
        input {
            width: 100%; padding: 12px; border: 1px solid #cbd5e1;
            border-radius: 8px; font-size: 1rem;
        }
        button.btn-main {
            width: 100%; padding: 12px; background: var(--primary);
            color: white; border: none; border-radius: 8px; font-size: 1rem;
            font-weight: 600; cursor: pointer; transition: 0.3s;
        }
        button.btn-main:hover { background: #1d4ed8; }

        .history-list { margin-top: 20px; max-height: 200px; overflow-y: auto; }
        .history-item {
            display: flex; justify-content: space-between; padding: 10px;
            border-bottom: 1px solid #f1f5f9; font-size: 0.9rem;
        }

        .planner-res {
            background: #f8fafc; padding: 15px; border-radius: 10px;
            margin-top: 15px; border-left: 4px solid var(--secondary);
        }
        .hidden { display: none; }
    </style>
</head>
<body>

<div class="container">
    <header>
        <h1>💰 ระบบออมเงินอัจฉริยะ</h1>
        <p>บันทึก ติดตาม และวางแผนการเงินของคุณ</p>
    </header>

    <div class="dashboard">
        <div class="stat-card">
            <h3>วันนี้</h3>
            <p id="sum-day">฿0</p>
        </div>
        <div class="stat-card">
            <h3>สัปดาห์นี้</h3>
            <p id="sum-week">฿0</p>
        </div>
        <div class="stat-card">
            <h3>เดือนนี้</h3>
            <p id="sum-month">฿0</p>
        </div>
        <div class="stat-card">
            <h3>ปีนี้</h3>
            <p id="sum-year">฿0</p>
        </div>
    </div>

    <div class="main-card">
        <div class="tabs">
            <button class="tab-btn active" onclick="switchTab('add')">บันทึกการออม</button>
            <button class="tab-btn" onclick="switchTab('plan')">วางแผนเป้าหมาย</button>
        </div>

        <div id="tab-add">
            <div class="form-group">
                <label>จำนวนเงินที่ออม (บาท)</label>
                <input type="number" id="amount" placeholder="ระบุจำนวนเงิน เช่น 100" min="0">
            </div>
            <button class="btn-main" onclick="saveMoney()">บันทึกข้อมูล</button>
            
            <div class="history-list" id="history">
                </div>
        </div>

        <div id="tab-plan" class="hidden">
            <div class="form-group">
                <label>เป้าหมายเงินออม (บาท)</label>
                <input type="number" id="goal-amount" placeholder="เช่น 10000">
            </div>
            <div class="form-group">
                <label>ต้องการทำให้สำเร็จภายใน (เดือน)</label>
                <input type="number" id="goal-months" placeholder="เช่น 6">
            </div>
            <button class="btn-main" style="background: var(--secondary);" onclick="calculatePlan()">คำนวณแผนการออม</button>
            
            <div id="plan-result" class="planner-res hidden">
                <p id="plan-text"></p>
            </div>
        </div>
    </div>
</div>

<script>
    // เก็บข้อมูลใน LocalStorage เพื่อให้ข้อมูลไม่หายเมื่อรีเฟรชหน้าจอ
    let savings = JSON.parse(localStorage.getItem('savingsData')) || [];

    function switchTab(type) {
        document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
        event.target.classList.add('active');
        
        if(type === 'add') {
            document.getElementById('tab-add').classList.remove('hidden');
            document.getElementById('tab-plan').classList.add('hidden');
        } else {
            document.getElementById('tab-add').classList.add('hidden');
            document.getElementById('tab-plan').classList.remove('hidden');
        }
    }

    function saveMoney() {
        const amountInput = document.getElementById('amount');
        const amount = parseFloat(amountInput.value);

        if (isNaN(amount) || amount <= 0) {
            alert("กรุณาระบุจำนวนเงินที่ถูกต้อง");
            return;
        }

        const record = {
            amount: amount,
            date: new Date().toISOString()
        };

        savings.push(record);
        localStorage.setItem('savingsData', JSON.stringify(savings));
        amountInput.value = '';
        
        updateDashboard();
        renderHistory();
    }

    function updateDashboard() {
        const now = new Date();
        const startOfDay = new Date(now.setHours(0,0,0,0));
        const startOfWeek = new Date(now.setDate(now.getDate() - now.getDay()));
        const startOfMonth = new Date(now.getFullYear(), now.getMonth(), 1);
        const startOfYear = new Date(now.getFullYear(), 0, 1);

        const calculateSum = (startDate) => {
            return savings
                .filter(item => new Date(item.date) >= startDate)
                .reduce((sum, item) => sum + item.amount, 0);
        };

        document.getElementById('sum-day').innerText = `฿${calculateSum(startOfDay).toLocaleString()}`;
        document.getElementById('sum-week').innerText = `฿${calculateSum(startOfWeek).toLocaleString()}`;
        document.getElementById('sum-month').innerText = `฿${calculateSum(startOfMonth).toLocaleString()}`;
        document.getElementById('sum-year').innerText = `฿${calculateSum(startOfYear).toLocaleString()}`;
    }

    function renderHistory() {
        const historyDiv = document.getElementById('history');
        historyDiv.innerHTML = '<strong>ประวัติล่าสุด:</strong>';
        
        [...savings].reverse().slice(0, 5).forEach(item => {
            const date = new Date(item.date).toLocaleDateString('th-TH', {
                day: '2-digit', month: 'short', hour: '2-digit', minute: '2-digit'
            });
            historyDiv.innerHTML += `
                <div class="history-item">
                    <span>${date}</span>
                    <span style="color: var(--secondary); font-weight: bold;">+ ฿${item.amount.toLocaleString()}</span>
                </div>
            `;
        });
    }

    function calculatePlan() {
        const goal = parseFloat(document.getElementById('goal-amount').value);
        const months = parseInt(document.getElementById('goal-months').value);

        if (!goal || !months) {
            alert("กรุณากรอกข้อมูลให้ครบถ้วน");
            return;
        }

        const perMonth = goal / months;
        const perDay = perMonth / 30;

        const resultDiv = document.getElementById('plan-result');
        const resultText = document.getElementById('plan-text');
        
        resultDiv.classList.remove('hidden');
        resultText.innerHTML = `
            🎯 เพื่อให้ถึงเป้าหมาย <strong>฿${goal.toLocaleString()}</strong> ใน ${months} เดือน<br><br>
            📅 คุณต้องออมเงินเดือนละ: <strong>฿${perMonth.toLocaleString(undefined, {minimumFractionDigits: 2})}</strong><br>
            ☀️ หรือคิดเป็นวันละประมาณ: <strong>฿${perDay.toLocaleString(undefined, {minimumFractionDigits: 2})}</strong>
        `;
    }

    // เรียกทำงานเมื่อเปิดหน้าเว็บ
    updateDashboard();
    renderHistory();
</script>

</body>
</html>
