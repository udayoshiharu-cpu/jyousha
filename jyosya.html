<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>救急隊 乗車割スケジュール</title>
<style>
    :root {
        --bg-color: #F5F3F0;
        --card-bg: #FFFFFF;
        --text-main: #3A3A3A;
        --text-sub: #7A7A7A;
        --color-ride: #738678; 
        --color-off: #E0DCD3;  
        --color-reset: #B5A496;
        --border-color: #E8E5DF;
        --accent-color: #D98C72;
    }
    
    body {
        font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
        background-color: var(--bg-color);
        color: var(--text-main);
        margin: 0;
        padding-bottom: 50px;
        scroll-behavior: smooth;
    }

    header {
        background-color: var(--card-bg);
        border-bottom: 1px solid var(--border-color);
        position: sticky;
        top: 0;
        z-index: 100;
        padding: 10px 15px;
        box-shadow: 0 2px 10px rgba(0,0,0,0.03);
    }

    h1 { font-size: 1rem; margin: 5px 0; text-align: center; }

    .stats-section {
        display: grid;
        grid-template-columns: 1fr 1fr;
        gap: 10px;
        margin-top: 10px;
    }

    .stat-box {
        background-color: #FDFDFD;
        border: 1px solid var(--border-color);
        border-radius: 8px;
        padding: 8px;
    }

    .stat-title {
        font-size: 0.7rem;
        color: var(--text-sub);
        text-align: center;
        margin-bottom: 5px;
        font-weight: bold;
    }

    .totals-container {
        display: flex;
        justify-content: space-around;
    }

    .total-item {
        text-align: center;
        font-size: 0.85rem;
        font-weight: bold;
    }

    .total-item span {
        display: block;
        font-size: 0.65rem;
        color: var(--text-sub);
        font-weight: normal;
    }

    .current-stat { color: var(--accent-color); }

    #schedule-list { padding: 15px; max-width: 600px; margin: 0 auto; }

    .day-card {
        background-color: var(--card-bg);
        border-radius: 12px;
        padding: 15px;
        margin-bottom: 15px;
        box-shadow: 0 2px 6px rgba(0,0,0,0.02);
        border: 1px solid var(--border-color);
        scroll-margin-top: 160px;
    }

    .past-day { opacity: 0.8; background-color: #FAFAFA; }
    .today-day { border: 2px solid var(--color-ride); background-color: #F0F4F1; }

    .day-header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 12px;
        border-bottom: 1px dashed var(--border-color);
        padding-bottom: 8px;
    }

    .date-text { font-size: 1.1rem; font-weight: bold; }
    
    .lock-icon {
        font-size: 1rem;
        margin-right: 5px;
        vertical-align: middle;
    }

    .status-badge {
        font-size: 0.7rem;
        padding: 3px 6px;
        border-radius: 4px;
        background-color: var(--bg-color);
        color: var(--text-sub);
    }

    .status-badge.manual { background-color: #FFF3CD; color: #856404; }

    .reset-btn {
        font-size: 0.7rem;
        background-color: var(--color-reset);
        color: white;
        border: none;
        padding: 3px 8px;
        border-radius: 4px;
        cursor: pointer;
        margin-left: 5px;
    }

    .buttons-container { display: grid; grid-template-columns: repeat(4, 1fr); gap: 8px; }

    .member-btn {
        padding: 10px 0;
        border: none;
        border-radius: 8px;
        font-size: 0.9rem;
        font-weight: bold;
        cursor: pointer;
        text-align: center;
    }

    .member-btn.ride { background-color: var(--color-ride); color: white; }
    .member-btn.off { background-color: var(--color-off); color: var(--text-sub); }

    /* ロック状態のボタンはカーソルを変える */
    .locked-btn { cursor: default; }

    .system-controls { text-align: center; margin-top: 30px; }
    .clear-data-btn {
        background-color: transparent;
        color: var(--text-sub);
        border: 1px solid var(--border-color);
        padding: 8px 16px;
        border-radius: 20px;
        font-size: 0.8rem;
        cursor: pointer;
    }
</style>
</head>
<body>

<header>
    <h1>🚑 救急乗車割状況</h1>
    <div class="stats-section">
        <div class="stat-box">
            <div class="stat-title">今日までの累計 (進捗)</div>
            <div class="totals-container" id="current-totals"></div>
        </div>
        <div class="stat-box">
            <div class="stat-title">年度末の着地予測</div>
            <div class="totals-container" id="final-totals"></div>
        </div>
    </div>
</header>

<div id="schedule-list"></div>

<div class="system-controls">
    <button class="clear-data-btn" onclick="clearAllData()">データを全リセット</button>
</div>

<script>
    const MEMBERS = [
        { id: 'fujimori', name: '藤森', tieBreaker: 2 },
        { id: 'nakazaki', name: '中崎', tieBreaker: 1 },
        { id: 'uda', name: '宇田', tieBreaker: 4 },
        { id: 'niwa', name: '丹羽', tieBreaker: 3 }
    ];

    const START_DATE = new Date(2026, 2, 31);
    const END_DATE = new Date(2027, 2, 29);
    const DAYS_STR = ['日', '月', '火', '水', '木', '金', '土'];
    const STORAGE_KEY = 'rescue_app_data_v2'; // 以前のデータを引き継ぐため変更なし
    const EDIT_PASSWORD = "7973";

    let scheduleData = [];
    let isFirstLoad = true; 
    let isUnlocked = false; // パスワードロック解除状態

    function init() {
        loadData();
        if (scheduleData.length === 0) {
            generateBaseDates();
            setInitialManualDays();
        }
        recalculateAndRender();
        
        if (isFirstLoad) {
            scrollToToday();
            isFirstLoad = false;
        }
    }

    function loadData() {
        const saved = localStorage.getItem(STORAGE_KEY);
        if (saved) scheduleData = JSON.parse(saved);
    }

    function saveData() {
        localStorage.setItem(STORAGE_KEY, JSON.stringify(scheduleData));
    }

    function generateBaseDates() {
        let current = new Date(START_DATE);
        while (current <= END_DATE) {
            scheduleData.push({
                dateTimestamp: current.getTime(),
                dateStr: `${current.getMonth() + 1}/${current.getDate()}(${DAYS_STR[current.getDay()]})`,
                isManual: false,
                riders: { fujimori: true, nakazaki: true, uda: true, niwa: true }
            });
            current.setDate(current.getDate() + 3);
        }
    }

    function setInitialManualDays() {
        if (scheduleData.length > 0) {
            scheduleData[0].isManual = true;
            scheduleData[0].riders = { fujimori: true, nakazaki: false, uda: true, niwa: true };
        }
        if (scheduleData.length > 1) {
            scheduleData[1].isManual = true;
            scheduleData[1].riders = { fujimori: false, nakazaki: true, uda: true, niwa: true };
        }
    }

    function recalculateAndRender() {
        let finalCounts = { fujimori: 0, nakazaki: 0, uda: 0, niwa: 0 };
        let currentCounts = { fujimori: 0, nakazaki: 0, uda: 0, niwa: 0 };
        const now = new Date();
        now.setHours(23, 59, 59, 999);

        scheduleData.forEach((day) => {
            if (!day.isManual) {
                let candidates = [...MEMBERS].sort((a, b) => {
                    if (finalCounts[b.id] !== finalCounts[a.id]) {
                        return finalCounts[b.id] - finalCounts[a.id];
                    }
                    return a.tieBreaker - b.tieBreaker;
                });
                let memberToOff = candidates[0].id;
                MEMBERS.forEach(m => { day.riders[m.id] = (m.id !== memberToOff); });
            }

            MEMBERS.forEach(m => {
                if (day.riders[m.id]) {
                    finalCounts[m.id]++;
                    if (day.dateTimestamp <= now.getTime()) {
                        currentCounts[m.id]++;
                    }
                }
            });
        });

        saveData();
        renderUI(currentCounts, finalCounts);
    }

    function renderUI(currentCounts, finalCounts) {
        document.getElementById('current-totals').innerHTML = MEMBERS.map(m => `
            <div class="total-item current-stat"><span>${m.name}</span>${currentCounts[m.id]}</div>
        `).join('');

        document.getElementById('final-totals').innerHTML = MEMBERS.map(m => `
            <div class="total-item"><span>${m.name}</span>${finalCounts[m.id]}</div>
        `).join('');

        const listDiv = document.getElementById('schedule-list');
        const now = new Date();
        now.setHours(0,0,0,0);
        const todayTime = now.getTime();

        let foundNext = false;

        listDiv.innerHTML = scheduleData.map((day, index) => {
            const dayDate = new Date(day.dateTimestamp);
            let dayClass = "day-card";
            let idAttr = "";
            let isPast = false;
            let lockHtml = "";

            if (dayDate.getTime() < todayTime) {
                dayClass += " past-day";
                isPast = true;
                lockHtml = `<span class="lock-icon">${isUnlocked ? '🔓' : '🔒'}</span>`;
            } else if (dayDate.getTime() === todayTime) {
                dayClass += " today-day";
                idAttr = 'id="target-day"';
                foundNext = true;
            } else if (!foundNext && dayDate.getTime() > todayTime) {
                idAttr = 'id="target-day"';
                foundNext = true;
            }

            const buttonsHtml = MEMBERS.map(m => `
                <button class="member-btn ${day.riders[m.id] ? 'ride' : 'off'} ${isPast && !isUnlocked ? 'locked-btn' : ''}" 
                        onclick="toggleRider(${index}, '${m.id}')">
                    ${m.name}<br><small>${day.riders[m.id] ? '乗車' : '休'}</small>
                </button>
            `).join('');

            return `
                <div class="${dayClass}" ${idAttr}>
                    <div class="day-header">
                        <div class="date-text">${lockHtml}${day.dateStr} ${dayDate.getTime() === todayTime ? '✨今日' : ''}</div>
                        <div>
                            <span class="status-badge ${day.isManual ? 'manual' : ''}">
                                ${day.isManual ? '手動変更' : '自動調整'}
                            </span>
                            ${day.isManual ? `<button class="reset-btn" onclick="resetDay(${index})">戻す</button>` : ''}
                        </div>
                    </div>
                    <div class="buttons-container">${buttonsHtml}</div>
                </div>
            `;
        }).join('');
    }

    function scrollToToday() {
        setTimeout(() => {
            const target = document.getElementById('target-day');
            if (target) {
                target.scrollIntoView({ behavior: 'smooth', block: 'start' });
            }
        }, 100);
    }

    // 過去日付の編集時にパスワードを確認する関数
    function checkPermission(dayTimestamp) {
        const now = new Date();
        now.setHours(0,0,0,0);
        
        // もし今日以降の当務日なら無条件で編集可能
        if (dayTimestamp >= now.getTime()) {
            return true;
        }

        // 過去の当務日の場合、ロックが解除されているかチェック
        if (isUnlocked) {
            return true;
        }

        // ロックされている場合はパスワード入力
        const input = prompt("過去の記録を編集・変更するためのパスワードを入力してください:");
        if (input === EDIT_PASSWORD) {
            isUnlocked = true;
            alert("ロックを解除しました。ページを閉じるまで過去の記録を編集できます。");
            recalculateAndRender(); // 鍵マークを更新
            return true;
        } else if (input !== null) {
            alert("パスワードが違います。");
        }
        return false;
    }

    function toggleRider(dayIndex, memberId) {
        if (!checkPermission(scheduleData[dayIndex].dateTimestamp)) return;

        scheduleData[dayIndex].riders[memberId] = !scheduleData[dayIndex].riders[memberId];
        scheduleData[dayIndex].isManual = true;
        recalculateAndRender();
    }

    function resetDay(dayIndex) {
        if (!checkPermission(scheduleData[dayIndex].dateTimestamp)) return;

        scheduleData[dayIndex].isManual = false;
        recalculateAndRender();
    }

    function clearAllData() {
        if(confirm("全データを消去します。この操作は取り消せません。よろしいですか？")) {
            localStorage.removeItem(STORAGE_KEY);
            scheduleData = [];
            init();
        }
    }

    window.onload = init;
</script>
</body>
</html>
