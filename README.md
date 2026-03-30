<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ระบบออมเงินอัจฉริยะ | Smart Savings</title>
    <meta name="description" content="ระบบออมเงินอัจฉริยะ ช่วยวางแผนการออม ติดตามเป้าหมาย และวิเคราะห์แนวโน้มการออมเงินของคุณ">
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Prompt:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.1/dist/chart.umd.min.js"></script>
    <link rel="stylesheet" href="style.css">
</head>
<body>

    <!-- ========== HEADER ========== -->
    <header class="site-header">
        <div class="container header-inner">
            <a href="#" class="logo">
                <div class="logo-icon-box">
                    <svg width="28" height="28" viewBox="0 0 28 28" fill="none">
                        <circle cx="14" cy="14" r="12" stroke="#FBBC05" stroke-width="2"/>
                        <path d="M14 7v14M9 12h10M9 16h10" stroke="#FBBC05" stroke-width="1.8" stroke-linecap="round"/>
                    </svg>
                </div>
                <span class="logo-text">ออมเงินอัจฉริยะ</span>
            </a>
            <div class="header-stats-bar">
                <div class="header-chip">
                    <span class="chip-label">ออมแล้ว</span>
                    <span class="chip-value" id="headerTotal">฿0</span>
                </div>
                <div class="header-chip streak">
                    <span class="chip-label">ต่อเนื่อง</span>
                    <span class="chip-value" id="headerStreak">0 วัน 🔥</span>
                </div>
            </div>
        </div>
    </header>

    <!-- ========== HERO BANNER ========== -->
    <section class="hero-banner">
        <div class="container hero-content">
            <nav class="breadcrumb">หน้าหลัก &gt; <span>ระบบออมเงินอัจฉริยะ</span></nav>
            <h1>ระบบออมเงินอัจฉริยะ</h1>
            <p>เครื่องมือช่วยวางแผนการออม ติดตามเป้าหมาย และวิเคราะห์แนวโน้มอย่างง่าย</p>
        </div>
    </section>

    <!-- ========== MAIN ========== -->
    <main class="main-area">
        <div class="container">

            <!-- ===== Section: เพิ่มเงินออม & สรุป ===== -->
            <section class="tool-section" id="sectionSave">
                <h2 class="section-title">บันทึกการออม</h2>
                <p class="section-subtitle">บันทึกเงินออมประจำวัน ดูสรุป และจัดการรายการ</p>

                <div class="card-grid cols-2">
                    <!-- Card: เพิ่มเงินออม -->
                    <div class="tool-card" id="cardAddSaving">
                        <div class="card-icon-wrap">
                            <svg class="card-icon" viewBox="0 0 80 80" fill="none">
                                <rect x="10" y="18" width="60" height="44" rx="6" stroke="#FBBC05" stroke-width="2.5"/>
                                <circle cx="40" cy="40" r="12" stroke="#FBBC05" stroke-width="2"/>
                                <path d="M40 34v12M34 40h12" stroke="#FBBC05" stroke-width="2" stroke-linecap="round"/>
                                <rect x="16" y="24" width="12" height="8" rx="2" stroke="#555" stroke-width="1.5"/>
                            </svg>
                        </div>
                        <h3 class="card-title">เพิ่มเงินออม</h3>
                        <p class="card-desc">บันทึกเงินออมของคุณแต่ละวัน วันละนิดหน่อย สะสมไปเรื่อยๆ เพื่ออนาคตที่ดี</p>
                        <button class="btn-pill" onclick="openModal('modalAdd')">เริ่มบันทึก</button>
                    </div>

                    <!-- Card: สรุปรายงาน -->
                    <div class="tool-card" id="cardSummary">
                        <div class="card-icon-wrap">
                            <svg class="card-icon" viewBox="0 0 80 80" fill="none">
                                <rect x="14" y="10" width="52" height="60" rx="5" stroke="#FBBC05" stroke-width="2.5"/>
                                <line x1="24" y1="28" x2="56" y2="28" stroke="#555" stroke-width="1.5" stroke-linecap="round"/>
                                <line x1="24" y1="38" x2="50" y2="38" stroke="#555" stroke-width="1.5" stroke-linecap="round"/>
                                <line x1="24" y1="48" x2="44" y2="48" stroke="#555" stroke-width="1.5" stroke-linecap="round"/>
                                <line x1="24" y1="58" x2="40" y2="58" stroke="#555" stroke-width="1.5" stroke-linecap="round"/>
                                <path d="M18 18h8" stroke="#FBBC05" stroke-width="2" stroke-linecap="round"/>
                            </svg>
                        </div>
                        <h3 class="card-title">สรุปรายงาน</h3>
                        <p class="card-desc">ดูสรุปการออมรายวัน สัปดาห์ เดือน และปี พร้อมตารางรายละเอียดทุกรายการ</p>
                        <button class="btn-pill" onclick="openModal('modalSummary')">ดูสรุป</button>
                    </div>
                </div>
            </section>

            <hr class="section-divider">

            <!-- ===== Section: วิเคราะห์แนวโน้ม ===== -->
            <section class="tool-section" id="sectionAnalysis">
                <h2 class="section-title">วิเคราะห์แนวโน้ม</h2>
                <p class="section-subtitle">กราฟแสดงแนวโน้มการออมเงินของคุณ ช่วยให้เห็นภาพรวมชัดเจน</p>

                <div class="card-grid cols-2">
                    <div class="tool-card" id="cardChart">
                        <div class="card-icon-wrap">
                            <svg class="card-icon" viewBox="0 0 80 80" fill="none">
                                <polyline points="12,60 28,40 42,50 56,25 68,35" stroke="#FBBC05" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round" fill="none"/>
                                <line x1="12" y1="68" x2="68" y2="68" stroke="#555" stroke-width="1.5"/>
                                <line x1="12" y1="18" x2="12" y2="68" stroke="#555" stroke-width="1.5"/>
                                <circle cx="28" cy="40" r="3" fill="#FBBC05"/>
                                <circle cx="42" cy="50" r="3" fill="#FBBC05"/>
                                <circle cx="56" cy="25" r="3" fill="#FBBC05"/>
                            </svg>
                        </div>
                        <h3 class="card-title">กราฟแนวโน้ม</h3>
                        <p class="card-desc">ดูแนวโน้มการออมแบบเส้น แท่ง หรือสะสม เลือกช่วงเวลาได้ตามต้องการ</p>
                        <button class="btn-pill" onclick="openModal('modalChart')">ดูกราฟ</button>
                    </div>

                    <div class="tool-card" id="cardHistory">
                        <div class="card-icon-wrap">
                            <svg class="card-icon" viewBox="0 0 80 80" fill="none">
                                <circle cx="40" cy="40" r="24" stroke="#FBBC05" stroke-width="2.5"/>
                                <path d="M40 24v16l10 6" stroke="#555" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                                <path d="M20 40a20 20 0 0 1 6-14" stroke="#FBBC05" stroke-width="2" stroke-linecap="round" stroke-dasharray="4 3"/>
                            </svg>
                        </div>
                        <h3 class="card-title">ประวัติการออม</h3>
                        <p class="card-desc">ดูรายการบันทึกย้อนหลังทั้งหมด ค้นหาและจัดการได้ง่ายๆ</p>
                        <button class="btn-pill" onclick="openModal('modalHistory')">ดูประวัติ</button>
                    </div>
                </div>
            </section>

            <hr class="section-divider">

            <!-- ===== Section: วางแผนการออม ===== -->
            <section class="tool-section" id="sectionPlan">
                <h2 class="section-title">วางแผนการออม</h2>
                <p class="section-subtitle">เครื่องมือช่วยวางแผนการออมเงิน ช่วยให้เราวางแผนจัดการเงินได้ง่ายขึ้น</p>

                <div class="card-grid cols-3">
                    <div class="tool-card" id="cardGoals">
                        <div class="card-icon-wrap">
                            <svg class="card-icon" viewBox="0 0 80 80" fill="none">
                                <circle cx="40" cy="40" r="24" stroke="#FBBC05" stroke-width="2.5"/>
                                <circle cx="40" cy="40" r="15" stroke="#FBBC05" stroke-width="2"/>
                                <circle cx="40" cy="40" r="6" fill="#FBBC05"/>
                                <line x1="56" y1="24" x2="68" y2="12" stroke="#555" stroke-width="1.5"/>
                                <polygon points="68,12 62,14 66,18" fill="#555"/>
                            </svg>
                        </div>
                        <h3 class="card-title">ตั้งเป้าหมาย</h3>
                        <p class="card-desc">ตั้งเป้าหมายการออม พร้อมติดตามความคืบหน้าแบบ real-time</p>
                        <button class="btn-pill" onclick="openModal('modalGoals')">ตั้งเป้าหมาย</button>
                    </div>

                    <div class="tool-card" id="cardPlanner">
                        <div class="card-icon-wrap">
                            <svg class="card-icon" viewBox="0 0 80 80" fill="none">
                                <rect x="18" y="14" width="44" height="52" rx="4" stroke="#FBBC05" stroke-width="2.5"/>
                                <rect x="26" y="8" width="6" height="12" rx="2" stroke="#555" stroke-width="1.5"/>
                                <rect x="48" y="8" width="6" height="12" rx="2" stroke="#555" stroke-width="1.5"/>
                                <line x1="18" y1="28" x2="62" y2="28" stroke="#FBBC05" stroke-width="1.5"/>
                                <rect x="26" y="34" width="8" height="8" rx="1.5" fill="#FBBC05" opacity="0.3"/>
                                <rect x="36" y="34" width="8" height="8" rx="1.5" fill="#FBBC05" opacity="0.3"/>
                                <rect x="46" y="34" width="8" height="8" rx="1.5" fill="#FBBC05"/>
                                <rect x="26" y="46" width="8" height="8" rx="1.5" fill="#FBBC05" opacity="0.3"/>
                            </svg>
                        </div>
                        <h3 class="card-title">วางแผนออมเงิน</h3>
                        <p class="card-desc">อยากมี 10,000 ใน 3 เดือน? คำนวณว่าต้องออมวันละเท่าไหร่</p>
                        <button class="btn-pill" onclick="openModal('modalPlanner')">คำนวณ</button>
                    </div>

                    <div class="tool-card" id="cardTips">
                        <div class="card-icon-wrap">
                            <svg class="card-icon" viewBox="0 0 80 80" fill="none">
                                <path d="M40 14c-12 0-20 9-20 20 0 8 5 14 10 18v8h20v-8c5-4 10-10 10-18 0-11-8-20-20-20z" stroke="#FBBC05" stroke-width="2.5" stroke-linejoin="round"/>
                                <line x1="34" y1="66" x2="46" y2="66" stroke="#555" stroke-width="1.5" stroke-linecap="round"/>
                                <line x1="36" y1="70" x2="44" y2="70" stroke="#555" stroke-width="1.5" stroke-linecap="round"/>
                                <line x1="40" y1="30" x2="40" y2="44" stroke="#FBBC05" stroke-width="2" stroke-linecap="round"/>
                                <circle cx="40" cy="26" r="2" fill="#FBBC05"/>
                            </svg>
                        </div>
                        <h3 class="card-title">เคล็ดลับออมเงิน</h3>
                        <p class="card-desc">เทคนิคและคำแนะนำดีๆ ที่จะช่วยให้คุณออมเงินได้สำเร็จ</p>
                        <button class="btn-pill" onclick="openModal('modalTips')">อ่านเคล็ดลับ</button>
                    </div>
                </div>
            </section>

        </div>
    </main>

    <!-- ========== FOOTER ========== -->
    <footer class="site-footer">
        <div class="container footer-inner">
            <p>&copy; 2026 ระบบออมเงินอัจฉริยะ — Smart Savings Tracker</p>
        </div>
    </footer>

    <!-- ========== BACK TO TOP ========== -->
    <button class="back-to-top" id="btnTop" onclick="window.scrollTo({top:0,behavior:'smooth'})">TOP</button>

    <!-- ============================================================ -->
    <!-- MODALS                                                        -->
    <!-- ============================================================ -->

    <!-- Modal: เพิ่มเงินออม -->
    <div class="modal-overlay" id="modalAdd">
        <div class="modal">
            <div class="modal-header">
                <h2>เพิ่มเงินออม</h2>
                <button class="modal-close" onclick="closeModal('modalAdd')">&times;</button>
            </div>
            <div class="modal-body">
                <div class="form-group">
                    <label for="savingsDate">วันที่</label>
                    <input type="date" id="savingsDate" class="form-input">
                </div>
                <div class="form-group">
                    <label for="savingsAmount">จำนวนเงิน (บาท)</label>
                    <div class="input-with-icon">
                        <span class="input-icon">฿</span>
                        <input type="number" id="savingsAmount" class="form-input input-lg" placeholder="0.00" min="0" step="0.01">
                    </div>
                </div>
                <div class="quick-btns">
                    <button class="quick-amount" data-amount="10">฿10</button>
                    <button class="quick-amount" data-amount="20">฿20</button>
                    <button class="quick-amount" data-amount="50">฿50</button>
                    <button class="quick-amount" data-amount="100">฿100</button>
                    <button class="quick-amount" data-amount="200">฿200</button>
                    <button class="quick-amount" data-amount="500">฿500</button>
                </div>
                <div class="form-group">
                    <label for="savingsNote">บันทึกช่วยจำ (ไม่บังคับ)</label>
                    <input type="text" id="savingsNote" class="form-input" placeholder="เช่น ไม่ซื้อชานมไข่มุกวันนี้ 🧋">
                </div>
                <button class="btn-primary" onclick="addSavings()">💰 บันทึกการออม</button>

                <div class="recent-entries" id="recentEntries">
                    <!-- Dynamic -->
                </div>
            </div>
        </div>
    </div>

    <!-- Modal: สรุปรายงาน -->
    <div class="modal-overlay" id="modalSummary">
        <div class="modal modal-lg">
            <div class="modal-header">
                <h2>สรุปรายงาน</h2>
                <button class="modal-close" onclick="closeModal('modalSummary')">&times;</button>
            </div>
            <div class="modal-body">
                <div class="period-tabs">
                    <button class="period-tab active" data-period="day">รายวัน</button>
                    <button class="period-tab" data-period="week">สัปดาห์</button>
                    <button class="period-tab" data-period="month">เดือน</button>
                    <button class="period-tab" data-period="year">ปี</button>
                </div>

                <div class="stat-cards">
                    <div class="stat-card gold">
                        <div class="stat-emoji">💰</div>
                        <div class="stat-info">
                            <span class="stat-label">ยอดรวม</span>
                            <span class="stat-number" id="summaryTotal">฿0</span>
                        </div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-emoji">📊</div>
                        <div class="stat-info">
                            <span class="stat-label">ค่าเฉลี่ย/วัน</span>
                            <span class="stat-number" id="summaryAvg">฿0</span>
                        </div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-emoji">🔥</div>
                        <div class="stat-info">
                            <span class="stat-label">ออมมากสุด</span>
                            <span class="stat-number" id="summaryMax">฿0</span>
                        </div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-emoji">📅</div>
                        <div class="stat-info">
                            <span class="stat-label">วันที่ออม</span>
                            <span class="stat-number" id="summaryDays">0 วัน</span>
                        </div>
                    </div>
                </div>

                <div class="table-wrap">
                    <table class="data-table">
                        <thead>
                            <tr><th>วันที่</th><th>จำนวนเงิน</th><th>บันทึก</th><th></th></tr>
                        </thead>
                        <tbody id="summaryTableBody"></tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>

    <!-- Modal: กราฟแนวโน้ม -->
    <div class="modal-overlay" id="modalChart">
        <div class="modal modal-lg">
            <div class="modal-header">
                <h2>กราฟแนวโน้ม</h2>
                <button class="modal-close" onclick="closeModal('modalChart')">&times;</button>
            </div>
            <div class="modal-body">
                <div class="chart-toolbar">
                    <div class="toolbar-group">
                        <button class="toolbar-btn active" data-chart="line">เส้น</button>
                        <button class="toolbar-btn" data-chart="bar">แท่ง</button>
                        <button class="toolbar-btn" data-chart="cumulative">สะสม</button>
                    </div>
                    <div class="toolbar-group">
                        <button class="range-btn active" data-range="7">7 วัน</button>
                        <button class="range-btn" data-range="30">30 วัน</button>
                        <button class="range-btn" data-range="90">3 เดือน</button>
                        <button class="range-btn" data-range="365">1 ปี</button>
                        <button class="range-btn" data-range="0">ทั้งหมด</button>
                    </div>
                </div>
                <div class="chart-box">
                    <canvas id="savingsChart"></canvas>
                </div>
                <div class="insights-row" id="chartInsights"></div>
            </div>
        </div>
    </div>

    <!-- Modal: ประวัติการออม -->
    <div class="modal-overlay" id="modalHistory">
        <div class="modal modal-lg">
            <div class="modal-header">
                <h2>ประวัติการออมทั้งหมด</h2>
                <button class="modal-close" onclick="closeModal('modalHistory')">&times;</button>
            </div>
            <div class="modal-body">
                <div class="table-wrap">
                    <table class="data-table">
                        <thead>
                            <tr><th>วันที่</th><th>จำนวนเงิน</th><th>บันทึก</th><th></th></tr>
                        </thead>
                        <tbody id="historyTableBody"></tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>

    <!-- Modal: เป้าหมาย -->
    <div class="modal-overlay" id="modalGoals">
        <div class="modal modal-lg">
            <div class="modal-header">
                <h2>เป้าหมายการออม</h2>
                <button class="modal-close" onclick="closeModal('modalGoals')">&times;</button>
            </div>
            <div class="modal-body">
                <div class="goal-form-section">
                    <h3>ตั้งเป้าหมายใหม่</h3>
                    <div class="inline-form">
                        <div class="form-group">
                            <label for="goalName">ชื่อเป้าหมาย</label>
                            <input type="text" id="goalName" class="form-input" placeholder="เช่น ท่องเที่ยวญี่ปุ่น 🗾">
                        </div>
                        <div class="form-group">
                            <label for="goalAmount">เป้าหมาย (฿)</label>
                            <div class="input-with-icon">
                                <span class="input-icon">฿</span>
                                <input type="number" id="goalAmount" class="form-input" placeholder="10000" min="0">
                            </div>
                        </div>
                        <div class="form-group">
                            <label for="goalDeadline">กำหนดวัน</label>
                            <input type="date" id="goalDeadline" class="form-input">
                        </div>
                    </div>
                    <div class="form-group">
                        <label>ไอคอน</label>
                        <div class="emoji-row">
                            <button class="emoji-pick active" data-emoji="🎯">🎯</button>
                            <button class="emoji-pick" data-emoji="✈️">✈️</button>
                            <button class="emoji-pick" data-emoji="🏠">🏠</button>
                            <button class="emoji-pick" data-emoji="🚗">🚗</button>
                            <button class="emoji-pick" data-emoji="📱">📱</button>
                            <button class="emoji-pick" data-emoji="💎">💎</button>
                            <button class="emoji-pick" data-emoji="🎓">🎓</button>
                            <button class="emoji-pick" data-emoji="💊">💊</button>
                        </div>
                    </div>
                    <button class="btn-primary" onclick="addGoal()">🎯 เพิ่มเป้าหมาย</button>
                </div>

                <div class="goals-list" id="goalsList"></div>
            </div>
        </div>
    </div>

    <!-- Modal: วางแผนออมเงิน -->
    <div class="modal-overlay" id="modalPlanner">
        <div class="modal modal-lg">
            <div class="modal-header">
                <h2>วางแผนออมเงิน</h2>
                <button class="modal-close" onclick="closeModal('modalPlanner')">&times;</button>
            </div>
            <div class="modal-body">
                <div class="planner-form">
                    <div class="inline-form">
                        <div class="form-group">
                            <label for="planTarget">จำนวนเงินที่ต้องการ (฿)</label>
                            <div class="input-with-icon">
                                <span class="input-icon">฿</span>
                                <input type="number" id="planTarget" class="form-input" placeholder="10000" min="0">
                            </div>
                        </div>
                        <div class="form-group">
                            <label>ระยะเวลา</label>
                            <div class="duration-row">
                                <input type="number" id="planMonths" class="form-input" placeholder="3" min="0" max="120">
                                <span>เดือน</span>
                                <input type="number" id="planDays" class="form-input" placeholder="0" min="0" max="31">
                                <span>วัน</span>
                            </div>
                        </div>
                        <div class="form-group">
                            <label for="planCurrent">เงินออมปัจจุบัน (฿)</label>
                            <div class="input-with-icon">
                                <span class="input-icon">฿</span>
                                <input type="number" id="planCurrent" class="form-input" placeholder="0" min="0">
                            </div>
                        </div>
                    </div>
                    <button class="btn-primary" onclick="calculatePlan()">🧮 คำนวณแผนการออม</button>
                </div>

                <div class="plan-results hidden" id="planResults">
                    <div class="big-result">
                        <span class="big-result-label">ต้องออมวันละ</span>
                        <span class="big-result-value" id="resDailyAmount">฿0</span>
                    </div>
                    <div class="stat-cards">
                        <div class="stat-card"><div class="stat-emoji">📅</div><div class="stat-info"><span class="stat-label">ต่อสัปดาห์</span><span class="stat-number" id="resWeekly">฿0</span></div></div>
                        <div class="stat-card"><div class="stat-emoji">📆</div><div class="stat-info"><span class="stat-label">ต่อเดือน</span><span class="stat-number" id="resMonthly">฿0</span></div></div>
                        <div class="stat-card"><div class="stat-emoji">⏰</div><div class="stat-info"><span class="stat-label">จำนวนวัน</span><span class="stat-number" id="resTotalDays">0</span></div></div>
                        <div class="stat-card"><div class="stat-emoji">🎯</div><div class="stat-info"><span class="stat-label">วันที่ถึงเป้า</span><span class="stat-number" id="resTargetDate">-</span></div></div>
                    </div>

                    <div class="timeline-section" id="planTimeline"></div>
                    <div class="tips-section" id="planTips"></div>
                </div>
            </div>
        </div>
    </div>

    <!-- Modal: เคล็ดลับ -->
    <div class="modal-overlay" id="modalTips">
        <div class="modal">
            <div class="modal-header">
                <h2>💡 เคล็ดลับออมเงิน</h2>
                <button class="modal-close" onclick="closeModal('modalTips')">&times;</button>
            </div>
            <div class="modal-body">
                <div class="tips-list">
                    <div class="tip-item"><span class="tip-icon">☕</span><div><strong>กฎ Latte Factor</strong><p>ลดรายจ่ายเล็กๆ น้อยๆ ในแต่ละวัน เช่น กาแฟ ชานม ขนม สะสมไปเรื่อยๆ จะเห็นผลลัพธ์ที่น่าตกใจ</p></div></div>
                    <div class="tip-item"><span class="tip-icon">🏦</span><div><strong>กฎ 50/30/20</strong><p>แบ่งรายได้ 50% สำหรับค่าใช้จ่ายจำเป็น, 30% สำหรับความต้องการ, 20% สำหรับออม/ลงทุน</p></div></div>
                    <div class="tip-item"><span class="tip-icon">📱</span><div><strong>ออมก่อนใช้</strong><p>พอได้เงินเดือน หักออมทันที! อย่ารอให้เหลือค่อยออม เพราะมักจะไม่เหลือ</p></div></div>
                    <div class="tip-item"><span class="tip-icon">🎮</span><div><strong>ท้าทาย 365 วัน</strong><p>วันที่ 1 ออม 1 บาท, วันที่ 2 ออม 2 บาท... วันที่ 365 ออม 365 บาท รวมทั้งปี = 66,795 บาท!</p></div></div>
                    <div class="tip-item"><span class="tip-icon">🛒</span><div><strong>รอ 24 ชม.</strong><p>ก่อนซื้อของที่ไม่จำเป็น ลองรอ 24 ชม. ถ้ายังอยากได้ค่อยซื้อ ส่วนใหญ่จะเปลี่ยนใจ</p></div></div>
                    <div class="tip-item"><span class="tip-icon">🎯</span><div><strong>ตั้งเป้าหมาย</strong><p>การมีเป้าหมายที่ชัดเจนจะทำให้เรามีแรงจูงใจในการออมมากขึ้น ตั้งเป้าและติดตามผลเสมอ</p></div></div>
                </div>
            </div>
        </div>
    </div>

    <!-- Toast container -->
    <div class="toast-container" id="toastContainer"></div>

    <!-- Confetti -->
    <canvas id="confettiCanvas" class="confetti-canvas"></canvas>

    <script src="app.js"></script>
</body>
</html>
