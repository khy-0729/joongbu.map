
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="theme-color" content="#f7f8f5">
  <title>캠퍼스 시설 안내</title>

  <style>
    :root {
      --green: #28765b;
      --green-light: #e5f2e9;
      --bg: #f7f8f5;
      --ink: #25342d;
      --muted: #7c8981;
      --line: #e4e9e4;
      --white: #fff;
    }

    * { box-sizing: border-box; }

    body {
      margin: 0;
      font-family: -apple-system, BlinkMacSystemFont,
        "Noto Sans KR", sans-serif;
      background: var(--bg);
      color: var(--ink);
    }

    button { font: inherit; cursor: pointer; }

    .app {
      width: 100%;
      max-width: 520px;
      min-height: 100dvh;
      margin: auto;
      background: var(--bg);
      position: relative;
      padding-bottom: 92px;
    }

    header {
      padding: 24px 20px 16px;
      background: var(--white);
    }

    .eyebrow {
      font-size: 12px;
      color: var(--green);
      font-weight: 700;
      letter-spacing: 1px;
    }

    h1 {
      font-size: 25px;
      margin: 8px 0;
      letter-spacing: -1px;
    }

    .subtitle {
      font-size: 13px;
      color: var(--muted);
      margin: 0;
    }

    .top-controls {
      display: flex;
      gap: 8px;
      padding: 16px 16px 8px;
    }

    .tab {
      flex: 1;
      padding: 12px 6px;
      border: 1px solid var(--line);
      border-radius: 13px;
      background: white;
      color: #68766e;
      font-weight: 700;
    }

    .tab.active {
      background: var(--green);
      border-color: var(--green);
      color: white;
    }

    .section-heading {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 16px 18px 10px;
    }

    .section-heading h2 {
      font-size: 16px;
      margin: 0;
    }

    .section-heading span {
      color: var(--muted);
      font-size: 12px;
    }

    .map-card {
      position: relative;
      margin: 0 12px;
      background: #edf2e8;
      border: 1px solid #dfe8dc;
      border-radius: 20px;
      overflow: hidden;
    }

    .map-canvas {
      position: relative;
      width: 100%;
      aspect-ratio: 0.88;
      overflow: hidden;
      background: #eaf0e3;
    }

    .map-canvas svg {
      position: absolute;
      inset: 0;
      width: 100%;
      height: 100%;
    }

    .map-label {
      position: absolute;
      z-index: 2;
      font-size: 11px;
      color: #667669;
      pointer-events: none;
    }

    .place {
      position: absolute;
      z-index: 3;
      transform: translate(-50%, -50%);
      border: 1px solid #d6e0d5;
      background: white;
      color: var(--ink);
      border-radius: 13px;
      padding: 9px 10px;
      box-shadow: 0 3px 10px #304b3510;
      display: flex;
      align-items: center;
      gap: 6px;
      white-space: nowrap;
      font-size: 12px;
      font-weight: 700;
    }

    .place strong { font-size: 13px; }

    .place.building {
      background: var(--green);
      border-color: var(--green);
      color: white;
      padding: 13px 15px;
      border-radius: 15px;
      box-shadow: 0 5px 15px #245d4530;
    }

    .map-legend {
      padding: 12px 14px;
      display: flex;
      flex-wrap: wrap;
      gap: 12px;
      background: white;
      font-size: 11px;
      color: #627168;
    }

    .dot {
      display: inline-block;
      width: 8px;
      height: 8px;
      border-radius: 50%;
      background: var(--green);
      margin-right: 5px;
    }

    .filters {
      display: flex;
      gap: 7px;
      overflow-x: auto;
      padding: 0 16px 12px;
      scrollbar-width: none;
    }

    .filter {
      flex-shrink: 0;
      padding: 9px 13px;
      background: white;
      border: 1px solid var(--line);
      border-radius: 22px;
      font-size: 12px;
      color: #66736a;
    }

    .filter.active {
      color: var(--green);
      border-color: var(--green);
      background: var(--green-light);
      font-weight: 700;
    }

    .floor-panel {
      padding: 12px 16px;
      background: white;
      border-bottom: 1px solid var(--line);
    }

    .building-select {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 10px;
      margin-bottom: 13px;
    }

    .building-select h2 {
      font-size: 20px;
      margin: 0 0 4px;
    }

    .building-select p {
      margin: 0;
      color: var(--muted);
      font-size: 12px;
    }

    .back-btn {
      border: 1px solid var(--line);
      background: white;
      border-radius: 12px;
      padding: 10px 12px;
      font-size: 12px;
    }

    .floors {
      display: flex;
      gap: 8px;
      overflow-x: auto;
      scrollbar-width: none;
    }

    .floor-btn {
      min-width: 52px;
      border: 1px solid var(--line);
      border-radius: 12px;
      background: #fafbf9;
      color: #738077;
      padding: 10px 8px;
      font-weight: 700;
    }

    .floor-btn.active {
      color: white;
      background: var(--green);
      border-color: var(--green);
    }

    .floor-plan {
      position: relative;
      margin: 12px;
      min-height: 365px;
      border: 2px solid #cbd7cd;
      border-radius: 8px;
      background: white;
      overflow: hidden;
    }

    .room {
      position: absolute;
      border: 1px solid #cbd7cd;
      background: #f2f5ef;
    }

    .room span {
      display: block;
      padding: 7px 4px;
      font-size: 10px;
      color: #738077;
      text-align: center;
    }

    .hall {
      position: absolute;
      background: #f9f8ef;
      border: 1px dashed #e3dfc9;
    }

    .floor-title {
      position: absolute;
      top: 12px;
      left: 12px;
      font-size: 11px;
      font-weight: 700;
      color: #7d8c80;
    }

    .facility-pin {
      position: absolute;
      z-index: 2;
      transform: translate(-50%, -50%);
      width: 65px;
      min-height: 57px;
      padding: 5px 2px;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      gap: 3px;
      border: 1px solid #dce7dc;
      border-radius: 13px;
      background: white;
      color: #34463a;
      box-shadow: 0 3px 10px #263c2910;
      font-size: 10px;
      font-weight: 700;
    }

    .facility-pin .emoji { font-size: 21px; }

    .facility-pin.selected {
      border: 2px solid var(--green);
      background: var(--green-light);
    }

    .facility-pin.hidden { display: none; }

    .plan-note {
      margin: 0 16px 12px;
      font-size: 11px;
      color: var(--muted);
      line-height: 1.6;
    }

    .info-card {
      margin: 12px;
      padding: 18px;
      background: white;
      border: 1px solid var(--line);
      border-radius: 18px;
    }

    .info-top {
      display: flex;
      align-items: flex-start;
      gap: 12px;
    }

    .info-icon {
      width: 48px;
      height: 48px;
      display: grid;
      place-items: center;
      border-radius: 15px;
      background: var(--green-light);
      font-size: 25px;
      flex-shrink: 0;
    }

    .info-card h3 {
      margin: 2px 0 5px;
      font-size: 17px;
    }

    .info-card p {
      margin: 0;
      color: var(--muted);
      font-size: 12px;
      line-height: 1.65;
    }

    .info-details {
      border-top: 1px solid var(--line);
      margin-top: 15px;
      padding-top: 13px;
      display: grid;
      gap: 11px;
    }

    .detail-row {
      display: grid;
      grid-template-columns: 76px 1fr;
      gap: 8px;
      font-size: 12px;
      line-height: 1.6;
    }

    .detail-row b { color: #7c8981; }
    .detail-row span { overflow-wrap: anywhere; }

    .empty {
      margin: 12px;
      padding: 25px;
      background: white;
      border-radius: 15px;
      text-align: center;
      color: var(--muted);
      font-size: 13px;
    }

    .bottom-nav {
      position: fixed;
      z-index: 10;
      bottom: 0;
      left: 50%;
      transform: translateX(-50%);
      width: 100%;
      max-width: 520px;
      padding: 10px 20px calc(10px + env(safe-area-inset-bottom));
      display: flex;
      gap: 12px;
      background: #ffffffed;
      border-top: 1px solid var(--line);
      backdrop-filter: blur(12px);
    }

    .nav-btn {
      flex: 1;
      border: 0;
      border-radius: 13px;
      padding: 12px 5px;
      color: #728076;
      background: transparent;
      font-size: 12px;
      font-weight: 700;
    }

    .nav-btn.active {
      color: var(--green);
      background: var(--green-light);
    }

    [hidden] { display: none !important; }

    @media (min-width: 600px) {
      body { padding: 20px 0; }
      .app {
        min-height: calc(100dvh - 40px);
        border-radius: 24px;
        overflow: hidden;
        box-shadow: 0 8px 40px #1c342015;
      }
      .bottom-nav {
        bottom: 20px;
        border-radius: 0 0 24px 24px;
      }
    }
  </style>
</head>

<body>
<div class="app">
  <header>
    <div class="eyebrow">CAMPUS GUIDE</div>
    <h1>캠퍼스 시설 안내</h1>
    <p class="subtitle">필요한 장소를 쉽고 빠르게 찾아보세요.</p>
  </header>

  <div class="top-controls">
    <button class="tab active" data-view="campus">🌳 캠퍼스</button>
    <button class="tab" data-view="building" data-building="C6">🏢 C6 건물</button>
    <button class="tab" data-view="building" data-building="C7">🏢 C7 건물</button>
  </div>

  <!-- 캠퍼스 외부 지도 -->
  <section id="campusView">
    <div class="section-heading">
      <h2>캠퍼스 지도</h2>
      <span>장소를 선택하세요</span>
    </div>

    <div class="map-card">
      <div class="map-canvas">
        <svg viewBox="0 0 400 455" preserveAspectRatio="none"
             aria-label="캠퍼스의 길과 녹지 지도">
          <path d="M-20 100 L420 350 M130 -20 L250 480"
                stroke="#fff" stroke-width="30" fill="none"/>
          <path d="M-20 100 L420 350 M130 -20 L250 480"
                stroke="#d5dfcc" stroke-width="2"
                stroke-dasharray="5 6" fill="none"/>
          <path d="M0 310 Q80 260 140 330 T400 400"
                stroke="#d6e9cf" stroke-width="45" fill="none"/>
          <rect x="18" y="25" width="88" height="54" rx="8"
                fill="#d9e9d0"/>
          <rect x="270" y="20" width="100" height="65" rx="8"
                fill="#d9e9d0"/>
          <rect x="24" y="365" width="100" height="55" rx="8"
                fill="#d9e9d0"/>
        </svg>

        <span class="map-label" style="top:9%;left:9%">녹지 공간</span>
        <span class="map-label" style="top:78%;left:66%">산책로</span>

        <button class="place" data-facility="field"
          style="top:19%;left:28%">🏃 운동장</button>

        <button class="place" data-facility="basketball"
          style="top:36%;left:76%">🏀 농구장</button>

        <button class="place" data-facility="parking"
          style="top:76%;left:24%">🅿️ 주차장</button>

        <button class="place building" data-building="C6"
          style="top:46%;left:31%">
          <span>🏢</span><strong>C6</strong>
        </button>

        <button class="place building" data-building="C7"
          style="top:59%;left:65%">
          <span>🏢</span><strong>C7</strong>
        </button>
      </div>
      <div class="map-legend">
        <span><i class="dot"></i>건물</span>
        <span>🏃 야외 운동시설</span>
        <span>🅿️ 주차시설</span>
      </div>
    </div>

    <div class="section-heading">
      <h2>야외 시설</h2>
      <span>3개 시설</span>
    </div>
    <div id="outdoorList"></div>
  </section>

  <!-- 건물 내부 지도 -->
  <section id="buildingView" hidden>
    <div class="floor-panel">
      <div class="building-select">
        <div>
          <h2 id="buildingTitle">C6 건물</h2>
          <p>층을 선택해 시설을 확인하세요.</p>
        </div>
        <button class="back-btn" id="backCampus">← 캠퍼스</button>
      </div>
      <div class="floors" id="floorButtons"></div>
    </div>

    <div class="section-heading">
      <h2 id="floorHeading">1층 안내도</h2>
      <span>아이콘을 눌러보세요</span>
    </div>

    <div class="floor-plan" id="floorPlan">
      <div class="floor-title">FLOOR PLAN · 개념도</div>
    </div>
    <p class="plan-note">
      ※ 내부 평면도는 시설 배치 예시입니다. 실제 도면과 위치를 확인한 뒤 수정해야 합니다.
    </p>

    <div class="section-heading">
      <h2>현재 층의 시설</h2>
      <span id="facilityCount"></span>
    </div>
    <div class="filters" id="filters"></div>
    <div id="facilityList"></div>

    <div id="infoCard" class="info-card" hidden>
      <div class="info-top">
        <div class="info-icon" id="infoIcon"></div>
        <div>
          <h3 id="infoName"></h3>
          <p id="infoLocation"></p>
        </div>
      </div>
      <div class="info-details">
        <div class="detail-row">
          <b>이용 안내</b><span id="infoGuide"></span>
        </div>
        <div class="detail-row">
          <b>운영시간</b><span id="infoHours"></span>
        </div>
        <div class="detail-row">
          <b>이용 방법</b><span id="infoMethod"></span>
        </div>
      </div>
    </div>
  </section>

  <nav class="bottom-nav">
    <button class="nav-btn active" data-view="campus">🌳 캠퍼스 지도</button>
    <button class="nav-btn" data-view="building" data-building="C6">🏢 C6</button>
    <button class="nav-btn" data-view="building" data-building="C7">🏢 C7</button>
  </nav>
</div>

<script>
  // 실제 건물 정보에 맞게 이 데이터를 수정하세요.
  const buildings = {
    C6: { floors: [-1, 1, 2, 3, 4] },
    C7: { floors: [1, 2, 3, 4] }
  };

  const facilities = [
    {
      id: "field", name: "운동장", icon: "🏃",
      category: "outdoor", building: "캠퍼스",
      floor: "야외", x: 28, y: 19,
      guide: "학생들의 체육활동과 야외 행사에 이용하는 공간입니다.",
      hours: "학교 공식 운영시간 확인 필요",
      method: "학교의 시설 이용 규정과 행사 일정을 확인하세요."
    },
    {
      id: "basketball", name: "농구장", icon: "🏀",
      category: "outdoor", building: "캠퍼스",
      floor: "야외", x: 76, y: 36,
      guide: "농구 등 야외 체육활동을 위한 공간입니다.",
      hours: "학교 공식 운영시간 확인 필요",
      method: "시설 이용 규정과 예약 필요 여부를 확인하세요."
    },
    {
      id: "parking", name: "주차장", icon: "🅿️",
      category: "outdoor", building: "캠퍼스",
      floor: "야외", x: 24, y: 76,
      guide: "차량을 주차하는 공간입니다.",
      hours: "학교 주차 운영정책 확인 필요",
      method: "교내 차량 등록 및 주차요금 규정을 확인하세요."
    }
  ];

  // 건물별·층별 시설을 추가하는 예시 데이터
  const sampleFacilities = [
    {
      id: "stairs", name: "계단", icon: "🪜",
      category: "move", x: 17, y: 31,
      guide: "다른 층으로 이동할 수 있는 계단입니다.",
      hours: "건물 개방시간에 따름",
      method: "계단을 이용해 원하는 층으로 이동하세요."
    },
    {
      id: "elevator", name: "엘리베이터", icon: "🛗",
      category: "move", x: 17, y: 57,
      guide: "층간 이동과 휠체어 이용자의 이동을 돕는 시설입니다.",
      hours: "건물 개방시간에 따름",
      method: "버튼을 눌러 목적 층을 선택하세요."
    },
    {
      id: "toilet", name: "화장실", icon: "🚻",
      category: "convenience", x: 82, y: 31,
      guide: "학생과 방문객이 이용할 수 있는 화장실입니다.",
      hours: "건물 개방시간에 따름",
      method: "남녀 화장실 및 장애인 화장실 위치를 확인하세요."
    },
    {
      id: "convenience", name: "편의시설", icon: "☕",
      category: "convenience", x: 82, y: 57,
      guide: "휴식이나 간단한 용무에 이용할 수 있는 시설입니다.",
      hours: "시설별 운영시간 확인 필요",
      method: "매장별 운영시간과 이용 규정을 확인하세요."
    },
    {
      id: "club", name: "과방", icon: "👥",
      category: "student", x: 35, y: 79,
      guide: "학과 학생들의 모임과 학과 활동을 위한 공간입니다.",
      hours: "학과별 이용 규정 확인 필요",
      method: "학과 사무실 또는 학생회에 이용 방법을 문의하세요."
    },
    {
      id: "admin", name: "행정시설", icon: "🏢",
      category: "admin", x: 65, y: 79,
      guide: "학사 및 행정 관련 업무를 처리하는 공간입니다.",
      hours: "담당 부서 운영시간 확인 필요",
      method: "방문 전 담당 부서와 업무시간을 확인하세요."
    }
  ];

  // 예시로 C6 1층에 시설을 표시합니다.
  // 실제 위치를 확인한 후 각 시설의 건물과 층을 변경하세요.
  sampleFacilities.forEach(f => {
    facilities.push({
      ...f,
      building: "C6",
      floor: 1
    });
  });

  // C7의 예시 시설도 생성합니다.
  sampleFacilities.forEach(f => {
    facilities.push({
      ...f,
      id: "c7-" + f.id,
      building: "C7",
      floor: 1
    });
  });

  const categories = [
    ["all", "전체"],
    ["move", "이동시설"],
    ["convenience", "편의시설"],
    ["student", "학생시설"],
    ["admin", "행정시설"]
  ];

  let currentView = "campus";
  let currentBuilding = "C6";
  let currentFloor = 1;
  let currentCategory = "all";
  let selectedId = null;

  const $ = id => document.getElementById(id);

  function showView(view, building = currentBuilding) {
    currentView = view;
    if (view === "building") currentBuilding = building;

    $("campusView").hidden = view !== "campus";
    $("buildingView").hidden = view !== "building";

    document.querySelectorAll("[data-view]").forEach(btn => {
      const active = btn.dataset.view === view &&
        (view === "campus" ||
         !btn.dataset.building ||
         btn.dataset.building === currentBuilding);
      btn.classList.toggle("active", active);
    });

    if (view === "building") {
      if (!buildings[currentBuilding].floors.includes(currentFloor)) {
        currentFloor = 1;
      }
      renderBuilding();
    }
  }

  function renderOutdoor() {
    const items = facilities.filter(f => f.building === "캠퍼스");

    $("outdoorList").innerHTML = items.map(f => `
      <div class="info-card">
        <div class="info-top">
          <div class="info-icon">${f.icon}</div>
          <div>
            <h3>${f.name}</h3>
            <p>${f.guide}</p>
          </div>
        </div>
        <div class="info-details">
          <div class="detail-row">
            <b>운영시간</b><span>${f.hours}</span>
          </div>
          <div class="detail-row">
            <b>이용 방법</b><span>${f.method}</span>
          </div>
        </div>
      </div>
    `).join("");
  }

  function renderBuilding() {
    $("buildingTitle").textContent = currentBuilding + " 건물";
    $("floorHeading").textContent =
      currentFloor === -1 ? "지하 1층 안내도" : currentFloor + "층 안내도";

    $("floorButtons").innerHTML = buildings[currentBuilding].floors
      .map(f => `
        <button class="floor-btn ${f === currentFloor ? "active" : ""}"
          data-floor="${f}">
          ${f < 0 ? "B" + Math.abs(f) : f + "F"}
        </button>
      `).join("");

    $("floorButtons").querySelectorAll("[data-floor]").forEach(btn => {
      btn.addEventListener("click", () => {
        currentFloor = Number(btn.dataset.floor);
        selectedId = null;
        renderBuilding();
      });
    });

    renderFloorPlan();
    renderFilters();
    renderFacilityList();
    renderInfoCard();
  }

  function getCurrentFacilities() {
    return facilities.filter(f =>
      f.building === currentBuilding &&
      f.floor === currentFloor
    );
  }

  function renderFloorPlan() {
    const plan = $("floorPlan");
    const items = getCurrentFacilities();

    plan.innerHTML = `
      <div class="floor-title">
        ${currentBuilding} · ${currentFloor < 0
          ? "지하 " + Math.abs(currentFloor) + "층"
          : currentFloor + "층"}
      </div>
      <div class="hall" style="left:29%;top:17%;width:42%;height:67%">
      </div>
      <div class="room" style="left:3%;top:17%;width:25%;height:67%">
        <span>공간 A</span>
      </div>
      <div class="room" style="right:3%;top:17%;width:25%;height:67%">
        <span>공간 B</span>
      </div>
      <div class="room" style="left:29%;top:86%;width:42%;height:10%">
        <span>복도</span>
      </div>
    `;

    items.forEach(f => {
      const pin = document.createElement("button");
      pin.className = "facility-pin";
      pin.dataset.id = f.id;
      pin.style.left = f.x + "%";
      pin.style.top = f.y + "%";
      pin.innerHTML = `
        <span class="emoji">${f.icon}</span>
        <span>${f.name}</span>
      `;
      pin.classList.toggle("selected", f.id === selectedId);
      pin.addEventListener("click", () => {
        selectedId = f.id;
        renderFloorPlan();
        renderFacilityList();
        renderInfoCard();
        $("infoCard").scrollIntoView({
          behavior: "smooth",
          block: "nearest"
        });
      });
      plan.appendChild(pin);
    });
  }

  function renderFilters() {
    $("filters").innerHTML = categories.map(([id, label]) => `
      <button class="filter ${currentCategory === id ? "active" : ""}"
        data-category="${id}">${label}</button>
    `).join("");

    $("filters").querySelectorAll("[data-category]").forEach(btn => {
      btn.addEventListener("click", () => {
        currentCategory = btn.dataset.category;
        renderFilters();
        renderFacilityList();
        renderFloorPlan();
      });
    });
  }

  function renderFacilityList() {
    const all = getCurrentFacilities();
    const filtered = all.filter(f =>
      currentCategory === "all" || f.category === currentCategory
    );

    $("facilityCount").textContent = filtered.length + "개";
    $("facilityList").innerHTML = filtered.length
      ? filtered.map(f => `
        <button class="info-card" data-select="${f.id}"
          style="display:flex;width:calc(100% - 24px);text-align:left;
          align-items:center;gap:12px;cursor:pointer">
          <span class="info-icon">${f.icon}</span>
          <span style="flex:1">
            <strong style="display:block;margin-bottom:5px">
              ${f.name}
            </strong>
            <span style="font-size:12px;color:var(--muted)">
              ${currentBuilding} · ${currentFloor < 0
                ? "지하 " + Math.abs(currentFloor) + "층"
                : currentFloor + "층"}
            </span>
          </span>
          <span style="color:var(--green)">›</span>
        </button>
      `).join("")
      : `<div class="empty">이 층에는 해당 시설이 없습니다.</div>`;

    $("facilityList").querySelectorAll("[data-select]").forEach(btn => {
      btn.addEventListener("click", () => {
        selectedId = btn.dataset.select;
        renderFloorPlan();
        renderFacilityList();
        renderInfoCard();
        $("infoCard").scrollIntoView({
          behavior: "smooth",
          block: "nearest"
        });
      });
    });
  }

  function renderInfoCard() {
    const f = facilities.find(item =>
      item.id === selectedId &&
      item.building === currentBuilding &&
      item.floor === currentFloor
    );

    $("infoCard").hidden = !f;
    if (!f) return;

    $("infoIcon").textContent = f.icon;
    $("infoName").textContent = f.name;
    $("infoLocation").textContent =
      `${currentBuilding} · ${currentFloor < 0
        ? "지하 " + Math.abs(currentFloor) + "층"
        : currentFloor + "층"}`;
    $("infoGuide").textContent = f.guide;
    $("infoHours").textContent = f.hours;
    $("infoMethod").textContent = f.method;
  }

  document.querySelectorAll("[data-view]").forEach(btn => {
    btn.addEventListener("click", () => {
      showView(btn.dataset.view, btn.dataset.building || currentBuilding);
    });
  });

  document.querySelectorAll("[data-building]").forEach(btn => {
    btn.addEventListener("click", () => {
      showView("building", btn.dataset.building);
    });
  });

  document.querySelectorAll(".place[data-facility]").forEach(btn => {
    btn.addEventListener("click", () => {
      const f = facilities.find(item =>
        item.id === btn.dataset.facility
      );
      if (!f) return;

      alert(
        `${f.icon} ${f.name}\n\n` +
        `${f.guide}\n\n운영시간: ${f.hours}\n\n` +
        `이용 방법: ${f.method}`
      );
    });
  });

  $("backCampus").addEventListener("click", () => showView("campus"));

  renderOutdoor();
  showView("campus");
</script>
</body>
</html>
