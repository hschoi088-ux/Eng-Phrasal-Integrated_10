<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>스피드 영어 퀴즈 (Week 9~12)</title>
    <style>
        body {
            font-family: 'Pretendard', -apple-system, BlinkMacSystemFont, system-ui, Roboto, sans-serif;
            background-color: #f0f4f8;
            color: #333;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            padding: 20px;
            box-sizing: border-box;
        }
        .container {
            background: white;
            padding: 30px;
            border-radius: 16px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.08);
            max-width: 650px;
            width: 100%;
        }
        h1 { text-align: center; margin-bottom: 20px; color: #1e293b; font-size: 26px; }
        
        /* Week 탭 스타일 */
        .week-tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 25px;
            border-bottom: 2px solid #e2e8f0;
            padding-bottom: 10px;
            justify-content: center;
            flex-wrap: wrap;
        }
        .week-tab {
            padding: 10px 16px;
            border: none;
            background: none;
            font-size: 15px;
            font-weight: bold;
            color: #94a3b8;
            cursor: pointer;
            border-radius: 8px;
            transition: all 0.2s;
        }
        .week-tab.active {
            background-color: #e0f2fe;
            color: #0284c7;
        }
        .week-tab:hover:not(.active):not(:disabled) { background-color: #f1f5f9; }
        .week-tab:disabled { cursor: not-allowed; opacity: 0.5; }

        /* 카테고리 영역 */
        .category-section {
            margin-bottom: 25px;
            background: #f8fafc;
            padding: 20px;
            border-radius: 12px;
            border: 1px solid #e2e8f0;
        }
        .category-title {
            font-size: 18px; font-weight: bold; color: #334155;
            margin-top: 0; margin-bottom: 15px; display: flex; align-items: center; gap: 8px;
        }
        
        /* 순한맛 / 매운맛 버튼 */
        .flavor-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 15px; }
        @media (max-width: 480px) { .flavor-grid { grid-template-columns: 1fr; } }
        .flavor-btn {
            background: white; border: 2px solid #cbd5e1; border-radius: 10px;
            padding: 15px; text-align: left; cursor: pointer; transition: all 0.2s ease;
        }
        .flavor-btn:hover { border-color: #3b82f6; box-shadow: 0 4px 12px rgba(59, 130, 246, 0.15); transform: translateY(-2px); }
        .flavor-title { font-size: 16px; font-weight: bold; display: block; margin-bottom: 6px; }
        .flavor-desc { font-size: 13px; color: #64748b; line-height: 1.4; word-break: keep-all; }
        .t-easy { color: #10b981; } .t-hard { color: #ef4444; }
        .hidden { display: none !important; }
        
        /* 퀴즈 영역 스타일 */
        #quiz-area { display: flex; flex-direction: column; gap: 20px; }
        #question-counter { font-size: 15px; color: #64748b; font-weight: bold; text-align: center;}
        
        .question-box { 
            font-size: 22px; font-weight: bold; word-break: keep-all; line-height: 1.5; 
            background: #f8fafc; padding: 30px 20px; border-radius: 12px;
            border: 2px dashed #cbd5e1; cursor: pointer; transition: background 0.2s; text-align: center;
        }
        .question-box:hover { background: #e2e8f0; }
        .question-box::after { content: "(클릭하여 정답 확인)"; font-size: 13px; color: #94a3b8; display: block; margin-top: 10px; font-weight: normal; }

        .answer-box { 
            background: #ecfdf5; padding: 25px 20px; border-radius: 12px; border: 1px solid #a7f3d0; text-align: left;
        }
        .en-text { font-size: 22px; color: #059669; font-weight: bold; margin-bottom: 15px; line-height: 1.4; word-break: keep-all;}
        .meta-info { font-size: 14px; color: #475569; margin-bottom: 5px; background: #fff; display: inline-block; padding: 4px 10px; border-radius: 20px; border: 1px solid #e2e8f0; }
        .meaning-info { font-size: 15px; color: #b45309; margin-bottom: 15px; background: #fef3c7; padding: 8px 12px; border-radius: 8px; font-weight: 500;}
        
        .controls { display: flex; justify-content: space-between; align-items: center; margin-top: 10px; flex-wrap: wrap; gap: 10px;}
        .left-controls { display: flex; gap: 10px; }
        
        /* 버튼 스타일 */
        .btn { padding: 10px 20px; border: none; border-radius: 8px; cursor: pointer; font-weight: bold; font-size: 15px; transition: 0.2s;}
        .btn-tts { background-color: #8b5cf6; color: white; display: flex; align-items: center; gap: 5px; }
        .btn-tts:hover { background-color: #7c3aed; }
        .btn-star { background-color: #e2e8f0; color: #475569; }
        .btn-star.active { background-color: #fef08a; color: #ca8a04; border: 1px solid #fde047; }
        .btn-next { background-color: #10b981; color: white; }
        .btn-next:hover { background-color: #059669; }
        .btn-finish { background-color: #3b82f6; color: white; width: 100%; padding: 15px; font-size: 16px; margin-top: 10px; }
        .btn-finish:hover { background-color: #2563eb; }
        .btn-home { background-color: #64748b; color: white; width: 100%; padding: 15px; font-size: 16px; margin-top: 20px;}
        .btn-home:hover { background-color: #475569; }

        /* 복습(결과) 영역 스타일 */
        #review-area { display: flex; flex-direction: column; gap: 15px; }
        .review-card { background: #fff; border: 1px solid #e2e8f0; border-radius: 10px; padding: 15px; box-shadow: 0 2px 5px rgba(0,0,0,0.05); text-align: left;}
        .review-ko { font-size: 16px; font-weight: bold; color: #334155; margin-bottom: 8px; }
        .review-en { font-size: 18px; font-weight: bold; color: #059669; margin-bottom: 8px; }
        .review-empty { text-align: center; padding: 40px 20px; font-size: 18px; color: #10b981; font-weight: bold; background: #ecfdf5; border-radius: 12px;}
    </style>
</head>
<body>

<div class="container">
    <h1 id="main-title">🚀 스피드 영어 퀴즈</h1>
    
    <div id="mode-selection">
        <div class="week-tabs">
            <button class="week-tab active" onclick="setWeek(9, this)">Week 9</button>
            <button class="week-tab" onclick="setWeek(10, this)">Week 10</button>
            <button class="week-tab" disabled>Week 11 (준비중)</button>
            <button class="week-tab" disabled>Week 12 (준비중)</button>
            <button class="week-tab" onclick="setWeek('all', this)">Week 9~10 누적</button>
        </div>

        <div class="category-section">
            <h3 class="category-title">🧩 구동사 (Phrasal Verbs)</h3>
            <div class="flavor-grid">
                <button class="flavor-btn" onclick="startQuiz('phrasal-easy')">
                    <span class="flavor-title t-easy">🟢 순한맛</span>
                    <span class="flavor-desc">구동사 의미별로 짧고 쉬운 문장들이 선별해서 담겨있음</span>
                </button>
                <button class="flavor-btn" onclick="startQuiz('phrasal-hard')">
                    <span class="flavor-title t-hard">🔴 매운맛</span>
                    <span class="flavor-desc">전체 예문에서 선별됨</span>
                </button>
            </div>
        </div>

        <div class="category-section">
            <h3 class="category-title">🗣️ 영어회화 (Conversation)</h3>
            <div class="flavor-grid">
                <button class="flavor-btn" onclick="startQuiz('conv-easy')">
                    <span class="flavor-title t-easy">💬 순한맛</span>
                    <span class="flavor-desc">'대표문장'과 '교재1'만 담고 있음</span>
                </button>
                <button class="flavor-btn" onclick="startQuiz('conv-hard')">
                    <span class="flavor-title t-hard">🔥 매운맛</span>
                    <span class="flavor-desc">전체 예문에서 선별됨</span>
                </button>
            </div>
        </div>
    </div>

    <div id="quiz-area" class="hidden">
        <div id="question-counter">문제 1 / 7</div>
        
        <div class="question-box" id="ko-box" onclick="showAnswer()">
            <span id="ko-text">한국어 문장이 여기에 표시됩니다.</span>
        </div>

        <div class="answer-box hidden" id="answer-section">
            <div class="meta-info" id="source-info">출처: Day001 교재1</div>
            <div class="en-text" id="en-text">English Answer</div>
            <div class="meaning-info hidden" id="meaning-info">의미: </div>
            
            <div class="controls">
                <div class="left-controls">
                    <button class="btn btn-tts" onclick="playTTS()">🔊 듣기</button>
                    <button class="btn btn-star" id="btn-star" onclick="toggleStar()">⭐ 어려워요</button>
                </div>
                <button class="btn btn-next" id="btn-next" onclick="nextQuestion()">다음 문제 ➡</button>
            </div>
        </div>

        <button class="btn btn-finish hidden" id="btn-finish" onclick="showReview()">결과 보기 (오답 노트) 📝</button>
    </div>

    <div id="review-area" class="hidden">
        <h2 style="text-align: center; color: #1e293b; margin-top:0;">⭐ 나의 오답 노트</h2>
        <p style="text-align: center; color: #64748b; font-size: 14px; margin-top:-10px;">어려웠던 문장들을 다시 확인해 보세요!</p>
        
        <div id="review-list"></div>

        <button class="btn btn-home" onclick="resetToHome()">🏠 처음으로 돌아가기</button>
    </div>
</div>

<script>
    let currentWeekFilter = 9;

    function setWeek(week, btn) {
        if (week === 'all') currentWeekFilter = 'all';
        else currentWeekFilter = parseInt(week);
        
        document.querySelectorAll('.week-tab').forEach(el => el.classList.remove('active'));
        btn.classList.add('active');
    }

    // 📌 구동사 Week 9~10 의미 매핑
    const meanings = {
        "go over_1": "go over: (내용이나 설명이 상대에게) 받아들여지다, 반응을 얻다",
        "go over_2": "go over: (실수가 없는지 서류 등을) 꼼꼼하게 검토하다",
        "go over_3": "go over: (방법 등을 차근차근) 설명하다, 짚어주다",
        "go over_4": "go over: (내용이 너무 어려워) 전혀 이해가 안 되다 (머리 위로 지나가다)",
        "go through_1": "go through: (터널이나 산을 물리적으로) 통과하다, 지나가다",
        "go through_2": "go through: (물건을 찾으려고 서랍이나 파일을) 샅샅이 뒤지다",
        "go through_3": "go through: (거래 시 중간에 전문가를) 거쳐 가다, 중개를 끼다",
        "go through_4": "go through: (인생의 힘든 고난이나 상황을) 몸소 겪다, 경험하다",
        "go through_5": "go through: (목록이나 단계를 처음부터 끝까지) 하나하나 살펴보다",
        "go through_6": "go through: (짧은 시간 내에 많은 양을) 소비하다, 써버리다",
        "go through_7": "go through: (부정문에서) 메시지가 전송되지 않거나 결제가 승인되지 않다",
        "hang out_1": "hang out: (사람들과 특별한 목적 없이) 시간을 보내며 놀다, 어울리다",
        "meet up_1": "meet up: (특정 장소와 목적을 강조하여) 만나다 (만나는 '행위' 자체를 강조)",
        "mingle with_1": "mingle with: (파티 등에서 낯선 이와 친해지려고 대화하며) 어울리다, 섞이다",
        "hold back_1": "hold back: (군중이나 물결 등을) 물리적으로 막아내다",
        "hold back_2": "hold back: (성장이나 발전을) 뒤처지게 가로막다, 발목을 잡다",
        "hold back_3": "hold back: (하고 싶은 말을 꾹) 참다, 내뱉지 않다",
        "hold back_4": "hold back: (웃음, 눈물, 생리 현상 등을) 억지로 참다",
        "hold back_5": "hold back: (정보 등을 다 말하지 않고) 일부러 숨기다",
        
        "hold off_1": "hold off: (적절한 때를 기다리며 결정을) 보류하다, 미루다",
        "hold off_2": "hold off: (다가오는 적이나 공격을) 물리적으로 막다, 저지하다",
        "hold up_1": "hold up: (시각적으로 잘 보이게 사물을) 높이 들다, 갖다 대다",
        "hold up_2": "hold up: (무거운 것이 떨어지지 않게 밑에서) 지탱하다, 받치다",
        "hold up_3": "hold up: (교통 정체 등으로 진행을) 지연시키다, 가로막다",
        "hold up_4": "hold up: (힘든 상황 속에서도 정신적으로) 잘 견디다, 버티다",
        "hold up_5": "hold up: (건물이나 다리 등 사물이 무게/압력을) 잘 견뎌내다",
        "keep up_1": "keep up: (앞서가는 상대를) 뒤처지지 않고 보조를 맞추어 따르다",
        "keep up_2": "keep up: (좋은 상태나 습관을 중단 없이) 계속 유지하다",
        "keep up_3": "keep up: (빠르게 변하는 트렌드나 정보를) 놓치지 않고 접하다",
        "leave out_1": "leave out: (목록이나 재료에서) 포함하지 않고 빼놓다",
        "leave out_2": "leave out: (이야기를 할 때 특정 사실을) 빼고 말하다, 생략하다",
        "leave out_3": "leave out: (주변 사람들에게서) 따돌림을 당하거나 소외감을 느끼다"
    };

    // 1. 구동사 순한맛 (Week 9~10)
    const phrasalEasy = [
        // Week 9
        { week: 9, ko: "그녀에게 자초지종을 설명했지만, 잘 못 받아들이더라고.", en: "I told her what happened, and it didn’t go over well.", source: "Day 041 순한맛", meaning: meanings["go over_1"] },
        { week: 9, ko: "계약서에 서명하기 전에 반드시 작은 글씨를 검토해 보세요.", en: "Please make sure to go over the fine print before signing the contract.", source: "Day 041 순한맛", meaning: meanings["go over_2"] },
        { week: 9, ko: "곱셈 법칙을 설명해 줄게.", en: "Let me go over the rules for multiplication.", source: "Day 041 순한맛", meaning: meanings["go over_3"] },
        { week: 9, ko: "백신의 원리 설명이 전혀 이해가 안 된다.", en: "The explanation of how the vaccine works goes over my head.", source: "Day 041 순한맛", meaning: meanings["go over_4"] },
        { week: 9, ko: "이 고속도로는 산을 몇 개나 지나간다.", en: "The highway goes through several mountains.", source: "Day 042 순한맛", meaning: meanings["go through_1"] },
        { week: 9, ko: "한 시간 동안 컴퓨터를 뒤져 봐도 없었다.", en: "I went through my computer for like an hour and couldn’t find it.", source: "Day 042 순한맛", meaning: meanings["go through_2"] },
        { week: 9, ko: "주식 투자를 할 때는 재무 상담가를 거치는 것이 현명하다.", en: "When investing in stocks, it’s wise to go through a financial advisor.", source: "Day 042 순한맛", meaning: meanings["go through_3"] },
        { week: 9, ko: "너 최근에 여러 가지로 힘들었다는 것 알아.", en: "I know you have gone through a lot lately.", source: "Day 042 순한맛", meaning: meanings["go through_4"] },
        { week: 9, ko: "1장을 자세히 살펴보고 익숙하지 않은 어휘가 있는지 봅시다.", en: "Let’s go through chapter 1 and find any vocabulary you are not familiar with.", source: "Day 043 순한맛", meaning: meanings["go through_5"] },
        { week: 9, ko: "우리 벌써 우유를 다 먹었네!", en: "I can’t believe we’ve already gone through all of our milk!", source: "Day 043 순한맛", meaning: meanings["go through_6"] },
        { week: 9, ko: "결제가 이루어지지 않았습니다.", en: "Your payment didn’t go through.", source: "Day 043 순한맛", meaning: meanings["go through_7"] },
        { week: 9, ko: "조만간 얼굴 한번 보자.", en: "We should hang out soon.", source: "Day 044 순한맛", meaning: meanings["hang out_1"] },
        { week: 9, ko: "7번 출구에서 4시쯤 만나서 저녁 먹을 때까지 놀자고.", en: "Let’s meet up at exit 7 around 4 p.m.", source: "Day 044 순한맛", meaning: meanings["meet up_1"] },
        { week: 9, ko: "워크숍은 다른 학생들과 어울릴 수 있는 기회를 줄 것입니다.", en: "The workshop will give you a chance to mingle with other students.", source: "Day 044 순한맛", meaning: meanings["mingle with_1"] },
        { week: 9, ko: "보안 요원들이 군중을 막아야만 했다.", en: "The security guards had to hold back the crowd.", source: "Day 045 순한맛", meaning: meanings["hold back_1"] },
        { week: 9, ko: "우리 대부분은 두려움에 발목이 잡힌다.", en: "Most of us are often held back by fear.", source: "Day 045 순한맛", meaning: meanings["hold back_2"] },
        { week: 9, ko: "내가 그를 어떻게 생각하는지 말할 뻔했지만, 참았다.", en: "I nearly told him what I thought of him, but I held back.", source: "Day 045 순한맛", meaning: meanings["hold back_3"] },
        { week: 9, ko: "굳이 방귀를 참아야 하나 생각했다.", en: "I thought I didn’t have to hold back my fart.", source: "Day 045 순한맛", meaning: meanings["hold back_4"] },
        { week: 9, ko: "그 사람은 틀림없이 뭔가 숨기고 있어.", en: "He is obviously holding something back.", source: "Day 045 순한맛", meaning: meanings["hold back_5"] },
        
        // Week 10
        { week: 10, ko: "우선은 크리스마스 선물 사는 거 보류하자.", en: "Let’s hold off on buying Christmas presents for now.", source: "Day 046 순한맛", meaning: meanings["hold off_1"] },
        { week: 10, ko: "어느 선량한 시민이 공격하려는 사람을 제지했다.", en: "A good Samaritan held off an attacker.", source: "Day 046 순한맛", meaning: meanings["hold off_2"] },
        { week: 10, ko: "전화기를 단말기에 갖다 대세요.", en: "Hold your phone up to the card reader.", source: "Day 047 순한맛", meaning: meanings["hold up_1"] },
        { week: 10, ko: "어떻게 저렇게 작은 테이블이 이렇게 무거운 유리를 지탱하는 걸까?", en: "How does that little table hold up such a heavy piece of glass?", source: "Day 047 순한맛", meaning: meanings["hold up_2"] },
        { week: 10, ko: "왜 이렇게 늦어?", en: "What’s the hold-up?", source: "Day 047 순한맛", meaning: meanings["hold up_3"] },
        { week: 10, ko: "잘 견디고 계시나요?", en: "How is she holding up?", source: "Day 048 순한맛", meaning: meanings["hold up_4"] },
        { week: 10, ko: "이 교각은 많은 교통량의 무게에도 잘 견뎌 왔다.", en: "This bridge has held up under the weight of the heavy traffic.", source: "Day 048 순한맛", meaning: meanings["hold up_5"] },
        { week: 10, ko: "따라갈 수가 없어.", en: "I can’t keep up.", source: "Day 049 순한맛", meaning: meanings["keep up_1"] },
        { week: 10, ko: "그동안 근력 운동을 꾸준히 했습니다. 근육량이 유지되고 있는 기분입니다.", en: "I’ve kept up with weightlifting. I feel like I’m maintaining muscle mass.", source: "Day 049 순한맛", meaning: meanings["keep up_2"] },
        { week: 10, ko: "요즘은 신규 앱이 너무 많이 출시되어서 따라갈 수가 없다.", en: "I just can’t keep up with all these new apps coming out.", source: "Day 049 순한맛", meaning: meanings["keep up_3"] },
        { week: 10, ko: "아몬드는 넣지 말아 주시겠어요?", en: "Can you leave them out?", source: "Day 050 순한맛", meaning: meanings["leave out_1"] },
        { week: 10, ko: "클럽에서 춤추다가 만났다는 건 이야기 안 합니다.", en: "I leave out the part where we met dancing at a club.", source: "Day 050 순한맛", meaning: meanings["leave out_2"] },
        { week: 10, ko: "파티에서 따돌림을 당한 기분이 들더라고.", en: "I felt left out at the party.", source: "Day 050 순한맛", meaning: meanings["leave out_3"] }
    ];

    // 2. 구동사 매운맛 (Week 9~10)
    const phrasalHard = [
        // Week 9
        { week: 9, ko: "너 방금 Tom을 때리고 도망간 거니? Tom에게 (다시) 가서 사과하렴.", en: "Did you just punch Tom and run away? Go (back) over to him and apologize.", source: "Day 041 교재1", meaning: null },
        { week: 9, ko: "그녀에게 자초지종을 설명했지만, 잘 못 받아들이더라고(= 여전히 화가 나 있어).", en: "I told her what happened, and it didn’t go over well.", source: "Day 041 교재1", meaning: meanings["go over_1"] },
        { week: 9, ko: "A: 내가 일어날까?", en: "A: Do you need me to get up?", source: "Day 041 교재1", meaning: null },
        { week: 9, ko: "B: 아, 아니. 내가 너를 타넘고 가면 돼.", en: "B: Oh, no. I can just go over you.", source: "Day 041 교재1", meaning: null },
        { week: 9, ko: "시험 시작 전에 선생님은 노트를 마지막으로 한 번 더 살펴보라고 했다.", en: "Before the exam, the teacher asked us to go over our notes one last time.", source: "Day 041 교재1", meaning: meanings["go over_2"] },
        { week: 9, ko: "계약서에 서명하기 전에 반드시 작은 글씨를 검토해 보세요.", en: "Please make sure to go over the fine print before signing the contract.", source: "Day 041 교재1", meaning: meanings["go over_2"] },
        { week: 9, ko: "다시 한번 설명해 주실 수 있을까요? 무슨 말을 하시려는 건지 잘 이해가 안 돼서요.", en: "Could you go over it again? I can’t quite understand what you were getting at.", source: "Day 041 교재1", meaning: meanings["go over_3"] },
        { week: 9, ko: "누군가가 백신의 원리를 설명해 줄 때마다 전혀 이해가 안 된다(= 감이 안 잡힌다).", en: "Every time someone tries to explain how the vaccine works, it goes over my head.", source: "Day 041 교재1", meaning: meanings["go over_4"] },
        { week: 9, ko: "Sam이 나한테 공구 빌려주기로 해서 (공구) 가지러 Sam 집 쪽으로 가야 해.", en: "I need to go over to Sam’s place to pick up the tool he’s lending me.", source: "Day 041 교재1", meaning: null },
        { week: 9, ko: "그 언덕을 넘어가면 주유소가 있을 거야. 그 안에 현금 인출기가 있어.", en: "If you go over that hill, you’ll find a gas station and they have an ATM inside.", source: "Day 041 교재1", meaning: null },
        { week: 9, ko: "어젯밤 데이트 때 여자 친구를 늦게 데리러 갔다. 이유를 설명하려 했지만 여자 친구가 잘 받아들이지 않았다. 아직도 나랑 말을 안 하려 한다.", en: "I was late to pick up my girlfriend for our date last night, and it didn’t go over well when I tried to explain why. She still won’t talk to me.", source: "Day 041 교재1", meaning: meanings["go over_1"] },
        { week: 9, ko: "새로 발표된 교육 정책이 어린 자녀를 둔 시민들 사이에서 반응이 좋지 않다.", en: "The new education policy is not going over well with citizens who have young children.", source: "Day 041 교재1", meaning: meanings["go over_1"] },
        { week: 9, ko: "쪽지 시험 보기 전에 어휘를 한 번 더 살펴봅시다.", en: "Let’s go over the vocabulary one more time before the quiz.", source: "Day 041 교재1", meaning: meanings["go over_2"] },
        { week: 9, ko: "로펌에서의 내 업무는 재판 전에 고객 문서를 반복적으로 검토해서 사실을 정확히 파악하는 것이다.", en: "My job at the law firm is to go over my client’s documents again and again before the trial to ensure we get the facts right.", source: "Day 041 교재1", meaning: meanings["go over_2"] },
        { week: 9, ko: "의류 관리기를 새로 구매했다. 문제는 설치 기사님이 사용법을 설명해주는 동안 딴생각을 한 것이다. 그래서 어제 고객센터에 전화해서 유선상으로 다시 설명을 부탁해야 했다.", en: "I bought a new steam closet for my wardrobe, but I wasn’t paying enough attention when the installation guy went over how to use it. I had to call customer service yesterday so he could go over it with me again over the phone.", source: "Day 041 교재1", meaning: meanings["go over_3"] },
        { week: 9, ko: "A: 나 지금 이 대수학 문제를 30분 동안이나 못 풀고 있어.", en: "A: I’ve been stuck on this one algebra problem for, like, 30 minutes.", source: "Day 041 교재1", meaning: null },
        { week: 9, ko: "B: 아, 문제가 뭔지 알겠다. 곱셈 법칙을 설명해 줄게.", en: "B: Oh, I think I see the problem. Let me go over the rules for multiplication.", source: "Day 041 교재1", meaning: meanings["go over_3"] },
        { week: 9, ko: "A: 야구에 재미를 붙여 보고 싶지만, (누군가) 야구 규칙을 설명해 주려고 할 때마다 이해가 안 돼.", en: "A: I want to get into baseball, but every time someone tries to explain the rules, they go right over my head.", source: "Day 041 교재1", meaning: meanings["go over_4"] },
        { week: 9, ko: "B: 응, 무슨 말인지 알아. (야구 규칙이) 보기보다 복잡하거든.", en: "B: Yeah, I know what you mean. It’s not as simple as it looks.", source: "Day 041 교재1", meaning: null },
        { week: 9, ko: "내일 데리러 오실 때 제가 용산역 쪽으로 가는 게 편할까요? 저희 집이 오기가 좀 까다로워서요.", en: "Would it be easier if I went over to Yongsan Station tomorrow when you pick me up? My place is a little tricky to get to.", source: "Day 041 교재2", meaning: null },
        { week: 9, ko: "아니요, 괜찮을 것 같아요. 그 동네 잘 알거든요. 아침 8시에 집 앞에서 뵐게요.", en: "No, I think it’ll be fine. I know your area pretty well. I’ll see you in front of your place at 8 a.m.", source: "Day 041 교재2", meaning: null },
        { week: 9, ko: "대부분 미국인들은 엔진오일 교환 방법을 안다고 들었어요. 진짜예요?", en: "I’ve heard that most Americans know how to do oil changes themselves. Is that true?", source: "Day 041 교재2", meaning: null },
        { week: 9, ko: "네! 거의 대부분은 십 대 때 기본적인 차량 관리를 배워요. 제가 교환하는 법을 설명해 줄까요? 오래 안 걸리고, 돈도 아낄 수 있을 거예요.", en: "Yeah! I think pretty much everybody learns basic maintenance as a teenager. Do you maybe want me to go over how to do it? It doesn’t take long and you can save some money.", source: "Day 041 교재2", meaning: meanings["go over_3"] },
        { week: 9, ko: "전공 바꾸는 거 왜 아직 부모님한테 말씀 안 드린 거야?", en: "Why haven’t you told your parents about switching your major yet?", source: "Day 041 교재2", meaning: null },
        { week: 9, ko: "우리 부모님이 잘 못 받아들이실 것 같아서 그냥 말 안 하는 거야. 부모님은 무조건 내가 치과의사가 되기만을 원하시거든.", en: "It wouldn’t go over well with my parents, so I just don’t tell them. They’re really set on me becoming a dentist.", source: "Day 041 교재2", meaning: meanings["go over_1"] },
        { week: 9, ko: "어젯밤에 친구들과 저녁을 먹으러 나갔다.", en: "I went out to dinner with my friends last night.", source: "Day 041 교재3", meaning: null },
        { week: 9, ko: "다들 즐거운 시간을 보내고 있었는데, 대학교 친구 중 한 명이 중동 문제 이야기를 계속 꺼냈다. 나만 빼고 다들 그 주제를 재미있어 했다.", en: "We were all having a good time, but one of my old college friends kept bringing up the problems in the Middle East, and everyone but me really got into the topic.", source: "Day 041 교재3", meaning: null },
        { week: 9, ko: "나는 무슨 말인지 도무지 이해가 안 되었다. 내가 (시사) 뉴스를 잘 안 봐서 그런지도 모른다.", en: "It all went over my head, maybe because I don’t follow the news at all.", source: "Day 041 교재3", meaning: meanings["go over_4"] },
        { week: 9, ko: "소외된 기분도 들고 멍청이가 된 기분이었다.", en: "It made me feel left out and dumb.", source: "Day 041 교재3", meaning: null },
        { week: 9, ko: "버라이어티 쇼나 비디오 게임과 같은 다른 이야기를 하려고 시도해 봤지만, 아무도 관심이 없어 하는 눈치였다.", en: "I tried to start talking about other things, like variety shows or video games, but no one seemed interested.", source: "Day 041 교재3", meaning: null },
        { week: 9, ko: "차를 가지고 가면 분당까지 가는 데 너무 오래 걸릴 거야. 강남을 거쳐야 하니까. 차라리 지하철을 타는 게 나을 거야.", en: "If you’re driving, it would take too long to reach Bundang because you have to go through Gangnam. You’d better take the subway, instead.", source: "Day 042 교재1", meaning: meanings["go through_1"] },
        { week: 9, ko: "경의선 숲길은 홍대와 마포 동쪽을 관통해서 용산역까지 이어져 있다.", en: "The Gyeongui Line Forest Park goes through Hongdae and eastern Mapo, almost all the way to Yongsan Station.", source: "Day 042 교재1", meaning: meanings["go through_1"] },
        { week: 9, ko: "방에 들어가지 못하고 있습니다. 가방을 다 뒤져 봤는데도 카드키를 못 찾겠어요.", en: "I’m having trouble getting into my room. I went through my bag and I couldn’t find my key card.", source: "Day 042 교재1", meaning: meanings["go through_2"] },
        { week: 9, ko: "너 최근에 여러 가지로 힘들었다는 것 알아.", en: "I know you have gone through a lot lately.", source: "Day 042 교재1", meaning: meanings["go through_4"] },
        { week: 9, ko: "이 고속도로는 산을 몇 개나 지나간다.", en: "The highway goes through several mountains.", source: "Day 042 교재1", meaning: meanings["go through_1"] },
        { week: 9, ko: "분명히 가족 관계 등록부를 어딘가에 저장해 뒀는데, 한 시간 동안 컴퓨터를 뒤져 봐도 없었다.", en: "I was sure that I had my family register saved somewhere, but I went through my computer for like an hour and couldn’t find it.", source: "Day 042 교재1", meaning: meanings["go through_2"] },
        { week: 9, ko: "주식 투자를 할 때는 재무 상담가를 거치는 것이 현명하다.", en: "When investing in stocks, it’s wise to go through a financial advisor.", source: "Day 042 교재1", meaning: meanings["go through_3"] },
        { week: 9, ko: "깔창을 하면 편하지가 않아. 이제서야 하이힐 신을 때 여성들이 겪는 고충을 알겠어.", en: "It doesn’t feel very comfy when I wear inserts. Now I know what women go through when they wear heels.", source: "Day 042 교재1", meaning: meanings["go through_4"] },
        { week: 9, ko: "보니까 고속도로에서 늘 요금소로 통과하더라. 하이패스 카드 만드는 건 생각 안 해 본 거니?", en: "I noticed you always go through the manual toll booths on the highway. Haven’t you considered getting a Hi-Pass card?", source: "Day 042 교재2", meaning: meanings["go through_1"] },
        { week: 9, ko: "아, 맞아. 만들어야지. 근데 맨날 깜박해.", en: "Oh, yeah. I know I should get one, but it always slips my mind.", source: "Day 042 교재2", meaning: null },
        { week: 9, ko: "이런! 옷장을 다 뒤져 봤는데도 결혼식에 입고 갈 옷이 없네.", en: "I can’t believe this! I went through my entire closet, but I can’t find anything to wear for the wedding.", source: "Day 042 교재2", meaning: meanings["go through_2"] },
        { week: 9, ko: "진짜? (다른 사람은 몰라도) 네가 결혼식에 입고 갈 만한 옷이 없다는 게 말이 돼? 너 맨날 옷만 사던데.", en: "Seriously? How can you not have any decent clothes for a wedding? All I ever see you buying is clothes.", source: "Day 042 교재2", meaning: null },
        { week: 9, ko: "James가 최근에 말썽을 많이 부리네요. (이 친구) 집에 무슨 일 있는지 아세요?", en: "James has been acting out a lot lately. Do you know how things are at home?", source: "Day 042 교재2", meaning: null },
        { week: 9, ko: "요즘 집 분위기가 안 좋고 부모님이 헤어질 수도 있다고 들었어요. 애가 요새 진짜 힘들어합니다. 우리가 최선을 다해 잘 돌봐 주자고요.", en: "I heard it’s been tough at home and his parents might separate. He’s really going through a lot. Let’s do our best to take care of him.", source: "Day 042 교재2", meaning: meanings["go through_4"] },
        { week: 9, ko: "비행기 출발 한참 전에 공항에 도착했다. 그래서 탑승 전에 잠시 짬을 내서 아시아나 비즈니스 라운지에서 커피랑 샌드위치를 좀 먹으려고 했다.", en: "I arrived at the airport with plenty of time before the flight, so I was going to take a little break to grab some coffee and a sandwich in the Asiana business lounge before I got on the plane.", source: "Day 042 교재3", meaning: null },
        { week: 9, ko: "그런데 놀랍게도 여권이 없었다. 그건 탑승 수속을 할 수 없다는 말이었다.", en: "To my shock, I couldn’t find my passport, which meant I couldn’t check in.", source: "Day 042 교재3", meaning: null },
        { week: 9, ko: "나는 가방과 수하물을 다 뒤져 봤다. 그러고 나서 그 전까지 내가 다녀왔던 장소에 다시 다 가 봤다.", en: "I went through my bag and luggage, and then I backtracked to all the places I had gone before that moment.", source: "Day 042 교재3", meaning: meanings["go through_2"] },
        { week: 9, ko: "알고 보니 화장을 확인하러 갔을 때 화장실 카운터에 놔두고 온 것이었다.", en: "It turned out I forgot it on the bathroom counter when I went to check my makeup.", source: "Day 042 교재3", meaning: null },
        { week: 9, ko: "비행기를 놓치지 않게 되어서 천만다행이었다.", en: "I was so relieved that I wouldn’t have to miss my flight.", source: "Day 042 교재3", meaning: null },
        { week: 9, ko: "계좌 거래 내역을 꼼꼼하게 살펴보고 있었는데, (제가) 모르는 출금 내역이 있었습니다.", en: "I was going through my bank transactions, and I found a charge that I didn’t recognize.", source: "Day 043 교재1", meaning: meanings["go through_5"] },
        { week: 9, ko: "우리 벌써 우유를 다 먹었네!", en: "I can’t believe we’ve already gone through all of our milk!", source: "Day 043 교재1", meaning: meanings["go through_6"] },
        { week: 9, ko: "밖에 나가서 문자 보내야겠어. 지하라서 신호가 약해서 메시지가 안 보내지네.", en: "I need to go outside to text somebody. My message didn’t go through because there is no reception down here.", source: "Day 043 교재1", meaning: meanings["go through_7"] },
        { week: 9, ko: "1장을 자세히 살펴보고 익숙하지 않은 어휘가 있는지 봅시다.", en: "Let’s go through chapter 1 and find any vocabulary you are not familiar with.", source: "Day 043 교재1", meaning: meanings["go through_5"] },
        { week: 9, ko: "긴 머리 관리하기가 힘들다. 한 달에 스프레이를 3통 이상 쓴다.", en: "It’s hard to maintain my long hair. I go through three or more bottles of hair spray a month.", source: "Day 043 교재1", meaning: meanings["go through_6"] },
        { week: 9, ko: "여기 인터넷이 안 되는 거야? 카카오톡 메시지가 안 보내져.", en: "Are we having Internet issues? My Kakao messages aren’t going through.", source: "Day 043 교재1", meaning: meanings["go through_7"] },
        { week: 9, ko: "결제가 이루어지지 않았습니다.", en: "Your payment didn’t go through.", source: "Day 043 교재1", meaning: meanings["go through_7"] },
        { week: 9, ko: "이력서를 자세히 검토해 보니 LG에서 2년 근무하셨더군요. 그 자리를 그만둔 이유가 뭔가요?", en: "I was going through your résumé and I saw that you worked at LG for two years. What was it that made you leave that position?", source: "Day 043 교재2", meaning: meanings["go through_5"] },
        { week: 9, ko: "그곳에서의 업무도 전반적으로 만족스러웠습니다. 그런데 저는 좀 더 다국적 기업인 곳에서 일해 보고 싶었습니다.", en: "I was satisfied with my job there, overall. The thing is, I was really hoping to work for a more multinational company.", source: "Day 043 교재2", meaning: null },
        { week: 9, ko: "만점 받은 소식이 언론과 SNS에 쫙 퍼졌습니다. 소감 한마디 부탁드릴게요.", en: "Your perfect score is all over the news sites and social media. Tell us, how did that make you feel?", source: "Day 043 교재2", meaning: null },
        { week: 9, ko: "얼마나 기쁜지 말로 표현이 안 됩니다. 시험지를 자세히 살펴봤을 때는 긴가민가하는 문제가 몇 개 있었습니다. 그래서 만점은 힘들다고 생각했어요.", en: "Words can’t describe how thrilled I am. When I went through my exam papers, there were several problems I wasn’t sure if I got right. I didn’t even think a perfect score was possible.", source: "Day 043 교재2", meaning: meanings["go through_5"] },
        { week: 9, ko: "친구들이랑 오늘 밤에 한잔하러 가거든. 신촌에 있는 이 삼겹살 집 위치를 인스타로 보내려고 했는데, 메시지 전송이 안 되더라고. 계속 ‘보낼 수 없습니다’만 떴어.", en: "Some friends and I are going out for drinks tonight. I was trying to send them the location of the pork belly place in Shinchon through Instagram, but the message wouldn’t go through. It kept saying, ‘unable to send’.", source: "Day 043 교재2", meaning: meanings["go through_7"] },
        { week: 9, ko: "몰랐어? 오늘 낮에 인스타그램 2시간 동안 먹통이었잖아. 그러니까 당연히 안 보내진 거지.", en: "You didn’t know? Instagram crashed for like two hours this afternoon. No wonder you couldn’t send it.", source: "Day 043 교재2", meaning: null },
        { week: 9, ko: "너 벌써 커피 두 잔째 마신 거 알아? 왜 또 한 잔 더 마시는 건데? 아직 점심 전이잖아.", en: "You already had two cups of coffee, didn’t you? Why are you having another one? It’s not even lunchtime yet.", source: "Day 043 교재3", meaning: null },
        { week: 9, ko: "알아, 안다고. 사실 전에는 하루에 여섯 잔 마셨어.", en: "I know, I know. I actually used to go through six cups a day.", source: "Day 043 교재3", meaning: meanings["go through_6"] },
        { week: 9, ko: "너무 많다. 줄여야 해. 아님 카페인이 없는 걸로 마셔 보든지.", en: "That’s way too much. You should definitely cut down. Or you could try decaf.", source: "Day 043 교재3", meaning: null },
        { week: 9, ko: "이미 마셔 봤지. 근데 카페인이 없는 건 별로더라고.", en: "I’ve already tried it, but decaf wasn’t really for me.", source: "Day 043 교재3", meaning: null },
        { week: 9, ko: "위가 불편하다고 그러지 않았어? 커피 마시면 더 안 좋아질 텐데.", en: "Didn’t you say that your stomach was bothering you? Coffee is only going to make it worse.", source: "Day 043 교재3", meaning: null },
        { week: 9, ko: "알지. 줄이려고 하고는 있는데, 커피 없이는 하루를 버틸 수가 없어.", en: "I know and I’ve been trying to drink less, but I just can’t seem to get through my day without it.", source: "Day 043 교재3", meaning: null },
        { week: 9, ko: "조만간 얼굴 한번 보자(= 만나서 놀자, 모이자).", en: "We should hang out soon.", source: "Day 044 교재1", meaning: meanings["hang out_1"] },
        { week: 9, ko: "심심하면 언제든 우리 집에 와서 (나랑 같이) 놀아도 돼.", en: "If you are ever bored, you can always come hang out at my place.", source: "Day 044 교재1", meaning: meanings["hang out_1"] },
        { week: 9, ko: "7번 출구에서 4시쯤 만나서 저녁 먹을 때까지 놀자고.", en: "Let’s meet up at exit 7 around 4 p.m., and then we’ll hang out until dinner time.", source: "Day 044 교재1", meaning: null },
        { week: 9, ko: "A: 당근마켓의 그 여성분은 만난 거야?", en: "A: Did you meet up with that lady from Daangn Market?", source: "Day 044 교재1", meaning: meanings["meet up_1"] },
        { week: 9, ko: "B: 응, 현금으로 결제했는데, 내가 잔돈이 없으니까, 그분이 (거스름돈은) 그냥 놔두라고 하더라고.", en: "B: Yeah, and she paid in cash, but I didn’t have change, so she said I could keep it.", source: "Day 044 교재1", meaning: null },
        { week: 9, ko: "저녁 내내 Nick과 이야기를 하는구나. 다른 손님들하고도 좀 어울려야지.", en: "You’ve been talking to Nick all evening – you really ought to be mingling with the other guests.", source: "Day 044 교재1", meaning: meanings["mingle with_1"] },
        { week: 9, ko: "영업하는 사람은 성공하려면 잠재 고객들과 어울리는 걸 즐길 수 있어야 한다.", en: "Any salesperson has to enjoy mingling with potential clients in order to get ahead.", source: "Day 044 교재1", meaning: meanings["mingle with_1"] },
        { week: 9, ko: "이 회사에 입사하고는 친구들과 전혀 못 어울렸습니다.", en: "I haven’t been able to hang out with any of my friends since I joined this company.", source: "Day 044 교재1", meaning: meanings["hang out_1"] },
        { week: 9, ko: "우리들 몇 명이서 퇴근하고 와인 바에서 만날 건데, 생각 있으면 편하게 오세요.", en: "A few of us are meeting up at the wine bar after work. You’re free to join us if you’d like.", source: "Day 044 교재1", meaning: meanings["meet up_1"] },
        { week: 9, ko: "곧 있을 워크숍은 다른 학생들과 어울릴 수 있는 기회를 줄 것입니다.", en: "The upcoming workshop will give you a chance to mingle with other students.", source: "Day 044 교재1", meaning: meanings["mingle with_1"] },
        { week: 9, ko: "대학교 때 주로 놀았던 곳이 여기란 말이지? 꽤나 고급스러워 보인다.", en: "So this is where you used to hang out in college? It looks pretty fancy.", source: "Day 044 교재2", meaning: meanings["hang out_1"] },
        { week: 9, ko: "응, 대학교 때는 이런 모습이 아니었어. 그때 당시에는 사람들이 그렇게 많이 가는 곳은 아니었지.", en: "Yeah, it didn’t look like this when I was in college. It wasn’t a popular area to hang out back then.", source: "Day 044 교재2", meaning: meanings["hang out_1"] },
        { week: 9, ko: "음, 이제 친구 만나러 가야 하는데, 언제 한번 만날 생각 있으시면 여기 제 전화번호 드릴게요.", en: "Well, I have to go meet my friend now, but here’s my number if you’d like to meet up some other time.", source: "Day 044 교재2", meaning: meanings["meet up_1"] },
        { week: 9, ko: "당연하죠. 곧 전화드릴게요.", en: "Absolutely. I will call you soon.", source: "Day 044 교재2", meaning: null },
        { week: 9, ko: "이봐, 여기 새로운 사람들 만나려고 온 거잖아. 그냥 앉아 있지 말고, 나가서 사람들과 좀 어울려.", en: "Hey, we’re here to meet new people. Don’t just sit around. Get out there and mingle with people.", source: "Day 044 교재2", meaning: meanings["mingle with_1"] },
        { week: 9, ko: "(모르는) 사람들이랑 담소를 나누는 게 익숙하지가 않아. 꼭 그래야 되는 거야?", en: "I’m really not good at small talk. Do I have to?", source: "Day 044 교재2", meaning: null },
        { week: 9, ko: "친구 결혼식이 끝난 후 고급 호텔 연회장에서 피로연이 열렸다.", en: "After my friend’s wedding, the reception took place at a fancy hotel ballroom.", source: "Day 044 교재3", meaning: null },
        { week: 9, ko: "다들 잘 차려입고 와인을 마시고 있었다.", en: "People there were all dressed up and sipping wine.", source: "Day 044 교재3", meaning: null },
        { week: 9, ko: "내가 있을 곳이 아니라는 기분이 들었고 허세를 부리는 듯한 모르는 이들과 어울리고 싶지도 않았다.", en: "I felt so out of place and I didn’t want to mingle with these pretentious strangers.", source: "Day 044 교재3", meaning: meanings["mingle with_1"] },
        { week: 9, ko: "내 친구들은 춤을 추느라 정신이 없었기 때문에, 당장 그 자리를 뜰 수도 없었다.", en: "My friends were busy dancing, so I couldn’t leave right away.", source: "Day 044 교재3", meaning: null },
        { week: 9, ko: "그래서 혼자 서서 창문 밖을 보고 있었다.", en: "I was, instead, standing alone just looking out the window.", source: "Day 044 교재3", meaning: null },
        { week: 9, ko: "그때 신랑 친구가 내게 다가와서는 와인을 권했다. 하지만 (술) 생각이 없었기 때문에 단칼에 거절했다.", en: "That’s when the groom’s friend came up to me and offered me a glass of wine, which I flatly declined because I wasn’t in the mood.", source: "Day 044 교재3", meaning: null },
        { week: 9, ko: "정말 불편하기 짝이 없는 날이었다.", en: "What an uncomfortable day that was!", source: "Day 044 교재3", meaning: null },
        { week: 9, ko: "제 강아지가 다른 개를 공격하려고 해서 그러지 못하게 붙잡아야만 했어요.", en: "I had to hold my dog back because he was going to attack another dog.", source: "Day 045 교재1", meaning: meanings["hold back_1"] },
        { week: 9, ko: "자네는 좋은 매니저가 될 수 있어. 하지만 위험을 감수하는 걸 두려워하는 태도가 발목을 잡고 있어.", en: "You could be a good manager, but your fear of taking risks is holding you back.", source: "Day 045 교재1", meaning: meanings["hold back_2"] },
        { week: 9, ko: "A: 나도 할 말 많지만 참으려고 노력하고 있는데, 참을 만큼 참았어. 이제 더 이상 은 못 참겠어.", en: "You know, I’ve been trying to hold back, but now I have had enough. I won’t tolerate this anymore.", source: "Day 045 교재1", meaning: meanings["hold back_3"] },
        { week: 9, ko: "B: 참는다고? 장난해? (당신은) 나를 들들 볶기만 하는데!", en: "Holding back? Are you joking? All you ever do is nag me!", source: "Day 045 교재1", meaning: meanings["hold back_3"] },
        { week: 9, ko: "내 화를 억누르기 위해 노력해야 하는 건 알아. 하지만 늘 내가 지지(= 화를 참지 못 하지). 그러고는 상처 주는 말을 하게 돼.", en: "I know I should work on holding back my anger. It always gets the best of me and I say hurtful things.", source: "Day 045 교재1", meaning: meanings["hold back_3"] },
        { week: 9, ko: "그 사람은 틀림없이 뭔가 숨기고 (말하지 않는 게) 있어.", en: "He is obviously holding something back.", source: "Day 045 교재1", meaning: meanings["hold back_5"] },
        { week: 9, ko: "보안 요원들이 Ohtani의 안전을 위해 군중을 막아야만 했다.", en: "The security guards had to hold back the crowd for Ohtani’s safety.", source: "Day 045 교재1", meaning: meanings["hold back_1"] },
        { week: 9, ko: "우리 대부분은 실패와 조롱의 두려움에 발목이 잡힌다.", en: "Most of us are often held back by fear of failure or ridicule.", source: "Day 045 교재1", meaning: meanings["hold back_2"] },
        { week: 9, ko: "내가 그를 어떻게 생각하는지 말할 뻔했지만, 참았다.", en: "I nearly told him what I thought of him, but I held back.", source: "Day 045 교재1", meaning: meanings["hold back_3"] },
        { week: 9, ko: "하루는 엘리베이터에 혼자 있어서 굳이 방귀를 참아야 하나 생각했다. 방귀를 뀐 후 5초도 안 되어 한 나이든 여성분이 엘리베이터에 탔다. 그러고는 나를 째려봤다.", en: "One day, I was in an elevator by myself, so I thought I didn’t have to hold back my fart. Not even five seconds after I let it rip, an old lady came into the elevator, and she gave me such a dirty look.", source: "Day 045 교재1", meaning: meanings["hold back_4"] },
        { week: 9, ko: "그는 정말 좋은 사람처럼 보이지만, 저와 사생활에 대해 이야기하지 않으려 해요. 뭔가 숨기는 게 있는 것 같아요.", en: "He seems like such a great guy, but he won’t get into his personal life with me. It seems like he’s holding something back.", source: "Day 045 교재1", meaning: meanings["hold back_5"] },
        { week: 9, ko: "우리 대표님이 신년 파티에서 연설했는데, 다들 깜짝 놀랐잖아! 대표님에게 그런 재미있는 면이 있는 줄을 미처 몰랐거든. 다들 웃겨서 눈물을 참느라고 고생을 한 듯 보였어.", en: "Our boss gave a speech at the New Year’s Party, and he blew everyone away! I never knew he had such a funny side. It seemed like everyone was holding back tears from laughing so hard.", source: "Day 045 교재2", meaning: meanings["hold back_4"] },
        { week: 9, ko: "난 파티에 못 갔지만 영상은 봤어! 영상이 지금 퍼지고 있어. 영상 대박 나면 사장님 코미디언이 될지도!", en: "I couldn’t make it to the party, but I saw the video! It’s actually going viral. Maybe he’ll become a comedian if it really takes off!", source: "Day 045 교재2", meaning: null },
        { week: 9, ko: "‘유리 천장’이라는 게 옛말이 되고 있다고 하는 사람들이 있어. 기사를 읽었는데, 주요 IT 기업에서조차 고위직 직원의 거의 절반이 여성이라고 해.", en: "Some people say that the term “glass ceiling” is becoming a thing of the past. I read an article that said something like ‒ even at major tech companies, almost half of senior-level positions are now held by women.", source: "Day 045 교재2", meaning: null },
        { week: 9, ko: "그래도 아직 여성들의 경력 발전을 가로막는 작은 것들이 많아. 유리 천장이 무너지 고 있다는 말이 없어졌다는 말은 아니거든.", en: "I think there are still a lot of small things holding women back from career advancement. Just because the ceiling is harder to see doesn’t mean it’s not there.", source: "Day 045 교재2", meaning: meanings["hold back_2"] },
        { week: 9, ko: "어제 몸이 너무 안 좋았는데 남자 친구가 (내가) 늦었다고 계속 뭐라고 하는 거 있지. 보통은 참는데, 이번에는 못 참겠더라고. 대판 싸우고 말았어.", en: "I was feeling terrible yesterday and my boyfriend kept getting on me about being late. Usually I can hold back, but not this time. We ended up getting in a huge fight.", source: "Day 045 교재2", meaning: meanings["hold back_3"] },
        { week: 9, ko: "그래서 어제 일 관련해서 오늘 얘기 좀 해 본 거야? 남자 친구가 좀 가라앉으면 어제 네가 몸이 안 좋았다는 걸 이해해 줄지도 모르잖아.", en: "Have you talked to him today about it? If he’s cooled down, he might understand that you just weren’t feeling well.", source: "Day 045 교재2", meaning: null },
        { week: 9, ko: "사람들이 더 이상 영어 공부를 진지하게 생각하지 않는 듯합니다.", en: "It seems like people don’t take studying English seriously anymore.", source: "Day 045 교재3", meaning: null },
        { week: 9, ko: "영어를 배우는 유튜브 채널을 보거나 스피킹 앱을 이용하면 언젠가는 유창해질 거라고 생각하는 것 같습니다.", en: "They just seem to believe watching some English-learning YouTube channels or using speaking apps would help them to become fluent at some point.", source: "Day 045 교재3", meaning: null },
        { week: 9, ko: "\"챗GPT 같은 걸 쓰면 되는 데 굳이 영어 배우는 데 많은 시간과 돈을 들여야 하나?”라는 태도입니다.", en: "They are just like, “What’s the point of spending all this time and money learning English when I could just use ChatGPT and stuff like that?”", source: "Day 045 교재3", meaning: null },
        { week: 9, ko: "왜 그렇게 생각하는지는 알겠습니다만, 제 생각은 다릅니다.", en: "I see where they are coming from, but I had a different point of view.", source: "Day 045 교재3", meaning: null },
        { week: 9, ko: "챗GPT와 무료 유튜브 채널은 한계가 있습니다.", en: "ChatGPT and free YouTube channels only go so far.", source: "Day 045 교재3", meaning: null },
        { week: 9, ko: "전력을 다하고 시간과 돈을 투자하지 않는 한 영어를 잘하는 것을 기대하기는 힘듭니다.", en: "You can never expect to have a good command of English unless you fully commit and invest time and money.", source: "Day 045 교재3", meaning: null },
        { week: 9, ko: "구글에서 근무하는 것이 제 목표라서 영어를 유창하게 하는 건 필수입니다.", en: "My goal is to work at Google, so the need to speak English fluently is not an option for me.", source: "Day 045 교재3", meaning: null },
        { week: 9, ko: "영어에 발목을 잡힐 수는 없습니다.", en: "I can’t let English hold me back.", source: "Day 045 교재3", meaning: meanings["hold back_2"] },

        // Week 10
        { week: 10, ko: "애한테 병원 가는 이야기는 지금 하지 않는 게 좋을지도 모르겠어. 괜히 더 걱정하게 만들 테니까. 그냥 차에 타서 드라이브 가자고 하자.", en: "Maybe we should hold off on telling her we are going to the doctor’s for now. It will just make her more worried. Let’s just tell her to get in the car for a ride.", source: "Day 046 교재1", meaning: meanings["hold off_1"] },
        { week: 10, ko: "우선은 크리스마스 선물 사는 거 보류하자. 먼저 그분들께 뭘 원하는지 여쭤봐야 해.", en: "Let’s hold off on buying Christmas presents for now. We should ask them what they want, first.", source: "Day 046 교재1", meaning: meanings["hold off_1"] },
        { week: 10, ko: "갤럭시 새 모델 사는 거 좀 미루려고 해.", en: "I am going to hold off on buying the new Galaxy.", source: "Day 046 교재1", meaning: meanings["hold off_1"] },
        { week: 10, ko: "헬스장 등록 좀 미뤄야겠다.", en: "I’m holding off signing up for the gym.", source: "Day 046 교재1", meaning: meanings["hold off_1"] },
        { week: 10, ko: "A: 술을 좀 시켜야 하나?", en: "A: Should I order us some drinks?", source: "Day 046 교재1", meaning: null },
        { week: 10, ko: "B: 좀 있다 하자. 다들 도착할 때까지 기다리자고. 거의 다 왔대.", en: "B: Let’s hold off on that and wait till everyone arrives; they’re almost here.", source: "Day 046 교재1", meaning: meanings["hold off_1"] },
        { week: 10, ko: "내가 새로운 직장을 구할 때까지 은행에서 대출금 (상환)을 좀 유예해 줬으면 했지만, 바로 갚기를 원한다.", en: "I was hoping the bank could hold off my payments until I get a new job, but they want their money now.", source: "Day 046 교재1", meaning: meanings["hold off_1"] },
        { week: 10, ko: "어느 선량한 시민이 지하철에서 (다른 승객을) 공격하려는 사람을 제지했고 그러는 동안 다른 승객들은 탈출했다.", en: "A good Samaritan held off an attacker in the subway while others escaped.", source: "Day 046 교재1", meaning: meanings["hold off_2"] },
        { week: 10, ko: "드디어 내가 연애를 하고 있다. 이제 가족들이 더 이상 소개팅 나가라는 잔소리를 못하게 될 것이다.", en: "I’m finally dating someone, so that will hold off the constant nagging from my family to go on so many blind dates.", source: "Day 046 교재1", meaning: meanings["hold off_2"] },
        { week: 10, ko: "온라인에서 후기를 좀 볼 때까지는 신규 모델 구매를 보류해야 할 것 같아.", en: "I think I should hold off on buying the new model until I can see some reviews online.", source: "Day 046 교재1", meaning: meanings["hold off_1"] },
        { week: 10, ko: "손님들이 도착하기 시작할 때까지는 케이크 굽는 걸 미뤄야겠다.", en: "I am going to hold off on baking the cake until they start arriving.", source: "Day 046 교재1", meaning: meanings["hold off_1"] },
        { week: 10, ko: "남편 줄 떡을 남겨 두려고 했지만, 아들을 말릴 수가 없었어요.", en: "I wanted to save that rice cake for my husband, but I couldn’t hold my son off.", source: "Day 046 교재1", meaning: meanings["hold off_2"] },
        { week: 10, ko: "그 나라에서는 가이드를 대동하는 것이 필수야. (호객 행위를 하는) 몹시 적극적인 노점상들이 너무 많아서 (그들의) 접근을 막을 누군가가 필요하거든.", en: "It’s essential to have a guide in that country. You need someone to hold off all the aggressive street vendors.", source: "Day 046 교재1", meaning: meanings["hold off_2"] },
        { week: 10, ko: "드디어 애플 신형 스마트 워치가 이번 주말에 판매되기 시작하는군. 이번엔 절대 놓치지 않을 거야.", en: "Finally, Apple’s new smartwatch goes on sale this weekend. I am definitely not gonna miss out on this.", source: "Day 046 교재2", meaning: null },
        { week: 10, ko: "정말 신난 듯한데, 그게 정말 그렇게 대단해? 새 모델이 이전 모델이랑 많이 다를지 잘 모르겠던데. 나는 온라인 후기를 좀 볼 때까지 (새 모델 사는 것을) 미루려고 해.", en: "Sounds like you are thrilled, but is it really such a big deal? I am not really sure if the new model will be all that different from the previous one. I think I’ll hold off (on buying the new model) until I can see some reviews online.", source: "Day 046 교재2", meaning: meanings["hold off_1"] },
        { week: 10, ko: "아우, 나는 조금 취기가 오르기 시작한다. 술 한잔하면서 이야기하는 건 너무 좋지만, 나는 (술 자체보다는) 분위기를 즐기는 타입이야. 이 정도로 빨리 마시는 건 감당하기 어려워.", en: "Wow, I’m starting to feel a bit tipsy. Catching up over drinks is great, but I’m more of a social drinker. This pace is more than I can really handle.", source: "Day 046 교재2", meaning: null },
        { week: 10, ko: "정말? 난 네가 나보다 술을 더 잘 마시는 줄 알았어. 너 잠깐 동안 마시지 말아야겠다.어차피 (술을 먹는 게 목적이 아니라) 서로 친해지자고 마시는 건데. 네가 정신이 혼미하면 무슨 재미야.", en: "Really? I thought you were better at holding your liquor. Maybe you should hold off on the drinks for a bit. It’s more about bonding, anyway. No fun if you’re not able to think straight.", source: "Day 046 교재2", meaning: meanings["hold off_1"] },
        { week: 10, ko: "엄마, 생일 케이크 먹고 싶지만, 아빠가 집에 오실 때까지 참을래요. 아빠 언제 오시나요?", en: "Mom, I want to eat my birthday cake, but I’m holding off until Dad gets home. When is he going to get here?", source: "Day 046 교재2", meaning: meanings["hold off_1"] },
        { week: 10, ko: "아빠부터 생각하고 우리 아들 참 착하네! 근데 걱정 마. 아빠 안 계실 때 먹어도 아빠는 개의치 않으실 거니까.", en: "It’s so sweet of you to put your dad first! Please don’t worry about it, though. I’m sure he won’t mind if you eat without him.", source: "Day 046 교재2", meaning: null },
        { week: 10, ko: "나는 피아노 연주가 즐겁다. 하지만 엄마는 늘 나에게 더 연습하라고 강요한다.", en: "I love playing piano, but my mom is always pushing me to practice more.", source: "Day 046 교재3", meaning: null },
        { week: 10, ko: "지난주 금요일에 엄마는 내가 연습 시간을 더 가지게 하려고 Steve의 생일 파티에 빠졌으면 했다.", en: "Last Friday, my mom wanted me to skip my friend Steve’s birthday party to get in more practice time.", source: "Day 046 교재3", meaning: null },
        { week: 10, ko: "그래서 엄마를 설득할 방법을 찾아야만 했다. 그래서 일요일에 연습을 좀 더 하겠다고 약속했다.", en: "I knew I had to find a way to hold Mom off, so I promised to practice extra on Sunday.", source: "Day 046 교재3", meaning: meanings["hold off_2"] },
        { week: 10, ko: "엄마도 동의했고, 금요일에 피아노 연습을 쉴 수 있었다.", en: "She agreed, and I could take Friday off.", source: "Day 046 교재3", meaning: null },
        { week: 10, ko: "좋은 절충안이었다. 나는 나대로 즐기면서 엄마도 기쁘게 해 드릴 수 있었다.", en: "It was a good compromise ‒ I got to have fun and still keep my mom happy.", source: "Day 046 교재3", meaning: null },
        { week: 10, ko: "나는 얼마 전에 코스트코 회원에 가입했다.", en: "I recently signed up for a Costco membership.", source: "Day 046 교재3", meaning: null },
        { week: 10, ko: "그동안 가입을 미뤄 온 이유는 다른 마트에서 쇼핑을 하면 되는데 굳이 연회비를 내야 할 이유를 몰랐기 때문이었다.", en: "The reason I held off on joining was that I didn’t see the point of paying an annual membership fee when I could just shop at other grocery stores.", source: "Day 046 교재3", meaning: meanings["hold off_1"] },
        { week: 10, ko: "게다가 코스트코는 현대카드와 현금만 받는데, 정말 불편하다.", en: "Besides, Costco only takes Hyundai cards and cash, which is really inconvenient.", source: "Day 046 교재3", meaning: null },
        { week: 10, ko: "아마도 현대카드와 사업적인 제휴 같은 걸 맺었나 보다.", en: "I guess they have a certain business partnership with Hyundai Card or something.", source: "Day 046 교재3", meaning: null },
        { week: 10, ko: "이런 이유로 코스트코에 갈 때마다 쇼핑객들이 현금을 인출하기 위해 정문 근처에 있는 인출기에 줄을 서 있는 걸 보게 된다.", en: "Because of that, every time you go, you can see shoppers waiting in line at ATMs near the front door to withdraw the money they need.", source: "Day 046 교재3", meaning: null },
        { week: 10, ko: "계속 손을 들고 있었지만 선생님은 나를 호명하지 않았다.", en: "I was holding my hand up, but the teacher didn’t call on me.", source: "Day 047 교재1", meaning: meanings["hold up_1"] },
        { week: 10, ko: "전화기를 단말기에 갖다 대세요.", en: "Hold your phone up to the card reader.", source: "Day 047 교재1", meaning: meanings["hold up_1"] },
        { week: 10, ko: "어떻게 저렇게 작은 테이블이 이렇게 무거운 유리를 지탱하는 걸까? 디자인이 정말 놀랍군.", en: "How does that little table hold up such a heavy piece of glass? The design is amazing.", source: "Day 047 교재1", meaning: meanings["hold up_2"] },
        { week: 10, ko: "기차가 5분 전에 도착했어야 하는데. 왜 지연이 되는지 모르겠네.", en: "The train was supposed to arrive five minutes ago. I wonder what’s holding it up.", source: "Day 047 교재1", meaning: meanings["hold up_3"] },
        { week: 10, ko: "A: 어디야? 커피 사러 30분 전에 갔잖아. 왜 이렇게 늦어?", en: "A: Hey, where are you? You went to get coffee 30 minutes ago. What’s the hold-up?", source: "Day 047 교재1", meaning: meanings["hold up_3"] },
        { week: 10, ko: "B: 그러게 말이야. 공사를 하고 있어서 (카페에서) 여섯 블록 떨어진 곳에 주차를 해야만 했어.", en: "B: I know. There was construction going on and I had to park six blocks away.", source: "Day 047 교재1", meaning: null },
        { week: 10, ko: "A: 이 바보 같은 휴대폰은 맨날 안 돼. 왜 그냥 현금을 쓸 수 없는 거야?", en: "A: These silly phones never work. Why can’t I just use cash?", source: "Day 047 교재1", meaning: null },
        { week: 10, ko: "B: 엄마, 휴대폰을 들고 단말기에 가까이 대야 해요.", en: "B: Mom, you need to hold your phone up closer to the card reader.", source: "Day 047 교재1", meaning: meanings["hold up_1"] },
        { week: 10, ko: "본격적인 선거철이다. 선거 운동원들이 지하철역과 거의 모든 교차로에서 (선거 관련) 표지판을 들고 있었다.", en: "Campaign season is in full swing. I saw campaigners holding up signs in the subway station and at pretty much every intersection.", source: "Day 047 교재1", meaning: meanings["hold up_1"] },
        { week: 10, ko: "A: 화상회의 시 노트북을 쓸 때면 편안한 자세를 찾는 게 쉽지가 않아.", en: "A: I’m really struggling to find a comfortable position when I use my laptop for video calls.", source: "Day 047 교재1", meaning: null },
        { week: 10, ko: "B: 좋은 컴퓨터 거치대를 하나 마련하는 걸 생각해 봐. 내 거치대는 눈높이에 맞게 노트북을 유지해 주거든. 자세에도 도움이 되고 좀 더 전문적으로 보이더라고.", en: "B: You should consider getting a good computer stand. Mine holds my laptop up at eye level. It’s helped my posture and made my setup look more professional.", source: "Day 047 교재1", meaning: meanings["hold up_1"] },
        { week: 10, ko: "교차로에 사고가 나서 차가 막히고 있어.", en: "There is an accident holding up traffic at the intersection.", source: "Day 047 교재1", meaning: meanings["hold up_3"] },
        { week: 10, ko: "차가 막혀서 옴짝달싹을 못 했어.", en: "I was held up in traffic.", source: "Day 047 교재1", meaning: meanings["hold up_3"] },
        { week: 10, ko: "지엽적인 세부 내용에 얽매이지 맙시다.", en: "Let’s not get held up on small details.", source: "Day 047 교재1", meaning: meanings["hold up_3"] },
        { week: 10, ko: "이 크리스마스 화환을 어디다 걸면 좋으려나. 여기 창문 옆은 어때?", en: "I wonder where a good place would be to hang this Christmas wreath. Maybe here, by the window?", source: "Day 047 교재2", meaning: null },
        { week: 10, ko: "음, 한번 보자. 내가 들고 있어 볼게. 뒤로 몇 걸음 가서 어떤지 말해 줘.", en: "Well, let’s see. I’ll hold it up. Try taking a few steps back and tell me how it looks.", source: "Day 047 교재2", meaning: meanings["hold up_1"] },
        { week: 10, ko: "텐트 폴을 찾을 수가 없네. 그런데 이 막대면 오늘 밤 동안 텐트가 잘 버틸 수 있을 거야.", en: "I can’t find the tent pole, but this stick should hold the tent up for the night.", source: "Day 047 교재2", meaning: meanings["hold up_2"] },
        { week: 10, ko: "그 막대는 너무 약해 보여. 텐트 폴을 트렁크에 두고 온 거 같아. 다시 가서 한번 보고 올게.", en: "That stick looks too weak. I think you left it in the truck. I’ll go look again.", source: "Day 047 교재2", meaning: null },
        { week: 10, ko: "그러니까 (트레이너님 말은) 2-3시간에 한 번씩 먹되 단백질을 섭취하기 전에는 탄수화물을 먹으면 안 되고, 지방은 100칼로리 이상 섭취하면 안 된다는 말이군요... 이번 다이어트는 너무 복잡하네요.", en: "So, I need to eat every 2-3 hours, but I can’t eat carbohydrates before protein, and I should eat no more than 100 calories worth of fat… this diet is getting confusing.", source: "Day 047 교재2", meaning: null },
        { week: 10, ko: "지금은 너무 세부적인 것에 얽매이지 마세요. 그냥 단백질 섭취량을 늘리시고 더 많이 걷도록 하세요.", en: "I don’t want you to get held up on small details right now. Just try to eat more protein and walk more.", source: "Day 047 교재2", meaning: meanings["hold up_3"] },
        { week: 10, ko: "시내에서 시위가 있어 저녁 내내 차가 막혔다.", en: "The protest downtown held up traffic most of the evening.", source: "Day 047 교재3", meaning: meanings["hold up_3"] },
        { week: 10, ko: "금요일 밤에는 집에 갈 때 버스를 타면 안 된다는 걸 알고는 있었다.", en: "I knew I shouldn’t have taken the bus home on a Friday night.", source: "Day 047 교재3", meaning: null },
        { week: 10, ko: "하지만 너무 힘든 한 주를 보냈던 터라 창가 쪽 자리에 앉아서 좀 쉬고 싶었다.", en: "I just wanted a seat by the window where I could relax after a grueling week at work.", source: "Day 047 교재3", meaning: null },
        { week: 10, ko: "지하철로 갈아타지 않고 버스로 한 번에 가려고 말이다.", en: "One bus, no underground subway transfers.", source: "Day 047 교재3", meaning: null },
        { week: 10, ko: "하지만 버스는 30분이나 움직이지 않았다. 올 들어 최대 규모의 시위가 오늘 밤에 있었기 때문에… 난 참 운도 없다.", en: "The bus didn’t move for thirty minutes, though, because the biggest protest of the year was tonight… just my luck.", source: "Day 047 교재3", meaning: null },
        { week: 10, ko: "2시간 동안 버스에서 옴짝달싹하지 못했다. 이렇게 한 주를 마무리하다니!", en: "I was held up on the bus for two hours. What a way to end the week!", source: "Day 047 교재3", meaning: meanings["hold up_3"] },
        { week: 10, ko: "어머니께서 편찮으신 거 알고 있어요. 잘 견디고 계시나요?", en: "I know your mother is sick. How is she holding up?", source: "Day 048 교재1", meaning: meanings["hold up_4"] },
        { week: 10, ko: "안녕하세요, Diana. Sarkisian 박사입니다. 안부 확인차 연락드렸습니다. 임시 치아는 안 떨어지고 잘 붙어 있나요?", en: "Hello? Diana, it’s Dr. Sarkisian. I’m just checking in on you. How is that temp holding up?", source: "Day 048 교재1", meaning: meanings["hold up_5"] },
        { week: 10, ko: "Rowley에게 먼저 벤치프레스를 써 보게 했다. 빗자루가 (안 부러지고) 잘 견디는지 보고 싶어서였다.", en: "I made Rowley use the bench press first, because I wanted to see if the broomstick was going to hold up.", source: "Day 048 교재1", meaning: meanings["hold up_5"] },
        { week: 10, ko: "최근에 신규 제품을 출시하지 않았음에도 매출이 의외로 줄지 않고 잘 버티고 있다.", en: "Even though we haven’t introduced any new products recently, sales have surprisingly held up.", source: "Day 048 교재1", meaning: meanings["hold up_4"] },
        { week: 10, ko: "내 남동생이 이혼한 후에 잘 지내지 못하고 있다. 걱정된다. 일주일 넘게 집에만 있는 것 같다.", en: "My brother hasn’t been holding up very well after the divorce. I’m worried; I don’t think he’s left the house in over a week.", source: "Day 048 교재1", meaning: meanings["hold up_4"] },
        { week: 10, ko: "제품 리콜 이후에 사업이 좀 어떤가요?(= 잘 버티고 있나요?)", en: "How has your business been holding up since, you know, the product recall?", source: "Day 048 교재1", meaning: meanings["hold up_4"] },
        { week: 10, ko: "이 교각은 많은 교통량의 무게에도 잘 견뎌 왔다.", en: "This bridge has held up under the weight of the heavy traffic.", source: "Day 048 교재1", meaning: meanings["hold up_5"] },
        { week: 10, ko: "잘 버티고 있는지 궁금해서 연락했어. 이번이 첫 대장 내시경 검사였잖아.", en: "I just wanted to check on how you are holding up. This was your first colonoscopy, after all.", source: "Day 048 교재2", meaning: meanings["hold up_4"] },
        { week: 10, ko: "괜찮아. 사실 생각보다는 별것 아니더라고. 다만 검사를 담당한 의사분과 간호사분들을 길거리에서 안 마주쳤으면 해. 너무 창피할 것 같거든.", en: "I’m feeling fine. It was no big deal, actually. I just hope I never have to face the doctors and nurses who did it in public. The shame would be too much to bear.", source: "Day 048 교재2", meaning: null },
        { week: 10, ko: "이제 저희 집 냉장고가 한동안은 고장 안 나고 잘 쓸 수 있을 거라는 말씀이죠?", en: "Now do you think our refrigerator will hold up for a while longer?", source: "Day 048 교재2", meaning: meanings["hold up_5"] },
        { week: 10, ko: "맞습니다. 한동안은 아무 문제 없이 쓰실 수 있을 겁니다.", en: "Absolutely. It should be good to go for quite some time now.", source: "Day 048 교재2", meaning: null },
        { week: 10, ko: "경기가 안 좋은데 장사는 잘 되고 있는 거예요? 저희 가게 마진은 매달 줄고 있어요.", en: "How is your business holding up in this current economic downturn? My margins are getting squeezed more and more every month.", source: "Day 048 교재2", meaning: meanings["hold up_4"] },
        { week: 10, ko: "누가 아니래요. 겨우 버티고 있어요. 아르바이트생 급여도 주기 힘든 상황이라, 제가 직접 매일 가게 문을 열고 닫고 그럽니다. 그런데 경기 탓만은 아니에요. 이 동네에 카페가 너무 많아요.", en: "You’re telling me. I can barely stay afloat. I can’t afford to pay my part-timer, so I’m opening and closing up every day myself. It’s not just the slumping economy, though. There are simply too many cafés in this neighborhood.", source: "Day 048 교재2", meaning: null },
        { week: 10, ko: "올해는 US 오픈에 출전하지 않기로 했습니다.", en: "I’ve decided not to play in the US Open this year.", source: "Day 048 교재3", meaning: null },
        { week: 10, ko: "(출전을 강행할 경우) 제 무릎이 버티지 못할 것 같습니다.", en: "I am afraid my knee wouldn’t hold up.", source: "Day 048 교재3", meaning: meanings["hold up_5"] },
        { week: 10, ko: "아시다시피 제가 무릎 수술을 몇 차례 받았습니다.", en: "You know, I’ve had several surgeries on my knee.", source: "Day 048 교재3", meaning: null },
        { week: 10, ko: "눈치 채셨겠지만, 제가 코트에서 평상시의 모습이 아니었습니다.", en: "As you probably noticed, I wasn’t my usual self out on the grass courts.", source: "Day 048 교재3", meaning: null },
        { week: 10, ko: "이번 대회에 출전을 강행하더라도 성치 않은 무릎으로는 최선의 모습을 보여 드릴 수 없을 겁니다.", en: "Even if I went ahead and entered the upcoming tournament, I wouldn’t be able to play at my best with the injured knee.", source: "Day 048 교재3", meaning: null },
        { week: 10, ko: "출전 대신에 회복에 집중하기로 했습니다. 그래서 다음 시즌에 더 강한 모습으로 돌아오겠습니다.", en: "Instead, I’ve chosen to focus on my recovery to make sure that I come back stronger for the next season.", source: "Day 048 교재3", meaning: null },
        { week: 10, ko: "힘든 결정이었지만 저의 건강과 커리어를 위해서는 옳은 결정이었다고 생각합니다.", en: "It’s a tough decision, but I believe it’s the right one for my health and career.", source: "Day 048 교재3", meaning: null },
        { week: 10, ko: "넌 너무 빨리 걸어. 따라갈 수가 없어.", en: "You walk too fast. I can’t keep up.", source: "Day 049 교재1", meaning: meanings["keep up_1"] },
        { week: 10, ko: "A: Sally. 오늘 컨디션 괜찮은 거예요?", en: "A: Hey, Sally. Are you feeling okay today?", source: "Day 049 교재1", meaning: null },
        { week: 10, ko: "B: 아침부터 감기 기운이 있어요. 그래서 업무를 제때 처리하는 게 어렵네요.", en: "B: I’ve been feeling a cold coming on since this morning. I’m having a hard time keeping up.", source: "Day 049 교재1", meaning: meanings["keep up_1"] },
        { week: 10, ko: "그동안 근력 운동을 꾸준히 했습니다. 근육량이 유지되고 있는 기분입니다.", en: "I’ve kept up with weightlifting. I feel like I’m maintaining muscle mass.", source: "Day 049 교재1", meaning: meanings["keep up_2"] },
        { week: 10, ko: "A: 그거 스마트 링이야? 스마트 링 가지고 있는 사람은 처음 본다.", en: "A: Is that a smart ring? You’re the first person I know who’s actually gotten one.", source: "Day 049 교재1", meaning: null },
        { week: 10, ko: "B: 응! 내가 IT 트렌드에 민감한 편은 아닌데, 스마트 링은 하나 갖고 싶더라고. 스마트 워치는 너무 크고 성가셔서.", en: "B: Yeah! I’m not normally the kind of person who keeps up with tech trends, but I wanted to get a smart ring because smart watches always looked so bulky and annoying.", source: "Day 049 교재1", meaning: meanings["keep up_3"] },
        { week: 10, ko: "등산로에서 (너무 빠른) 남편의 속도에 겨우 보조를 맞췄어요.", en: "I could barely keep up with my husband on the hiking trail.", source: "Day 049 교재1", meaning: meanings["keep up_1"] },
        { week: 10, ko: "고등학교 때 3년간 일본어 수업을 들었지만 졸업 후에는 (일본어) 공부를 하지 못했다. 그래서 이력서에 ‘일본어 유창’이라고 적으려면 다시 연습해야 한다.", en: "I took Japanese for three years in high school, but I haven’t kept up with it since graduating. I need to work on it again if I want to claim that I’m fluent on job applications.", source: "Day 049 교재1", meaning: meanings["keep up_2"] },
        { week: 10, ko: "요즘은 신규 앱이 너무 많이 출시되어서 따라갈 수가 없다.", en: "I just can’t keep up with all these new apps coming out.", source: "Day 049 교재1", meaning: meanings["keep up_3"] },
        { week: 10, ko: "A: 요즘 통 연락을 못해서 미안해. 너무 정신이 없었어.", en: "A: Hey, sorry I haven’t been keeping up with you these days. Life has been crazy.", source: "Day 049 교재1", meaning: meanings["keep up_3"] },
        { week: 10, ko: "B: 괜찮아, 걱정 마! 나도 나름 정신이 없었어.", en: "B: It’s okay; don’t worry! I’ve had my own stuff going on, too.", source: "Day 049 교재1", meaning: null },
        { week: 10, ko: "지난주, 망원 시장에서 영국 사람을 만났어! 너무 멋진 경험이었는데, 말이 너무 빨라서 못 따라가겠더라고.", en: "Last week, I met someone from England at Mangwon Market! It was fascinating, but he spoke so fast it was hard to keep up with him.", source: "Day 049 교재2", meaning: meanings["keep up_1"] },
        { week: 10, ko: "멋지다! 악센트 때문에도 힘들었겠네. 내 친구 남편도 영국 출신인데 말을 따라가기 힘들더라고.", en: "That’s so cool! It must have been hard with the accent, too. My friend’s husband is from England and I always have a hard time keeping up.", source: "Day 049 교재2", meaning: meanings["keep up_1"] },
        { week: 10, ko: "몇 달 뒤에 파리 여행 계획하고 있는 거지? 가기 전에 프랑스어 공부할 거야?", en: "You’re planning a trip to Paris in a few months, right? Are you going to study French before you go?", source: "Day 049 교재2", meaning: null },
        { week: 10, ko: "음, 실은 대학교 때 프랑스어를 했어. 그런데 그 뒤로는 못 해서 지금은 프랑스어 실력이 녹슬었어. 복습을 좀 하면 문제없겠지 뭐.", en: "Well, I actually studied French in college. But I didn’t keep up with it, so I’m pretty rusty. I’ll have to brush up on it, and then I should be fine.", source: "Day 049 교재2", meaning: meanings["keep up_2"] },
        { week: 10, ko: "최근에 연봉이 인상됐어. 그런데도 여전히 빠듯하네.", en: "I just got a raise, but money is still tight.", source: "Day 049 교재2", meaning: null },
        { week: 10, ko: "누가 아니래. 연봉 인상률이 물가 인상률을 못 따라가는 듯해.", en: "I hear you. Annual raises can’t seem to keep up with inflation.", source: "Day 049 교재2", meaning: meanings["keep up_1"] },
        { week: 10, ko: "나는 늘 패션에 관심이 무척 많았다.", en: "I’ve always been a big fan of fashion.", source: "Day 049 교재3", meaning: null },
        { week: 10, ko: "요즘은 SNS 덕분에 새로운 스타일과 트렌드를 따라가는 게 어렵지 않다.", en: "And these days, with social media, it’s easy to keep up with new styles and trends.", source: "Day 049 교재3", meaning: meanings["keep up_3"] },
        { week: 10, ko: "하지만 재미로 시작한 것이 시간을 너무 많이 빼앗는 취미가 되었다.", en: "But you know, what started out as fun has turned into a big waste of time.", source: "Day 049 교재3", meaning: null },
        { week: 10, ko: "새로운 스타일의 패션이나 시계를 보면 이를 착용한 나를 상상해 본다.", en: "When I look at new styles or watches, I always picture them on myself.", source: "Day 049 교재3", meaning: null },
        { week: 10, ko: "내가 착용하면 어떤 모습일까, 내가 소화를 할 수 있을까를 상상한다.", en: "I imagine what they would look like on me, and whether I could pull them off or not.", source: "Day 049 교재3", meaning: null },
        { week: 10, ko: "이런 생각을 하는 것만으로도 시간을 너무 많이 소비한다.", en: "Just thinking about it takes up so much time.", source: "Day 049 교재3", meaning: null },
        { week: 10, ko: "일할 때는 정말 집중을 방해하는 요소다! 내가 좋아하는 것을 놓치지 않으면서도 제때 업무를 처리할 방법을 찾아야 한다.", en: "It’s such a distraction at work! I have to find a way to get my work done on time, while still keeping up with what I love.", source: "Day 049 교재3", meaning: meanings["keep up_3"] },
        { week: 10, ko: "처음부터 설탕을 안 넣었으면 더 맛날 텐데요.", en: "This would taste better if you left out the sugar.", source: "Day 050 교재1", meaning: meanings["leave out_1"] },
        { week: 10, ko: "아몬드 알레르기가 있어서요. 아몬드는 (음식에) 넣지 말아 주시겠어요?", en: "I am allergic to almonds. Can you leave them out?", source: "Day 050 교재1", meaning: meanings["leave out_1"] },
        { week: 10, ko: "남자 친구를 어떻게 만났냐고 물으면 그냥 서로가 아는 친구가 소개해 줬다고 말해요. 클럽에서 춤추다가 만났다는 건 이야기 안 합니다. 사람들이 저희를 그렇게 기억하는 건 싫거든요.", en: "Whenever someone asks me how I met my boyfriend, I just say we were introduced by a mutual friend. I leave out the part where we met dancing at a club. That’s not the kind of thing I want people to remember.", source: "Day 050 교재1", meaning: meanings["leave out_2"] },
        { week: 10, ko: "파티에서 따돌림을 당한 기분이 들더라고.", en: "I felt left out at the party.", source: "Day 050 교재1", meaning: meanings["leave out_3"] },
        { week: 10, ko: "토마토 파스타 주세요. 그런데 고추는 빼 주실 수 있을까요?", en: "I’d like the tomato pasta, but could you leave out the chili peppers, please?", source: "Day 050 교재1", meaning: meanings["leave out_1"] },
        { week: 10, ko: "민수에게 여자 친구와 헤어진 이유를 물었더니 여자 친구의 습관이 거슬린다는 등 주저리주저리 늘어놓았다. 당연히 자신이 바람을 피운 부분은 말하지 않았다.", en: "When I asked Minsu about why he broke up with his girlfriend, he said all kinds of things about her annoying habits. Of course, he left out the part about him cheating.", source: "Day 050 교재1", meaning: meanings["leave out_2"] },
        { week: 10, ko: "동료들에게 왕따를 당하고 있는 기분이다. 한 번이라도 술 자리에 나를 불러 주면 좋으련만.", en: "I’m feeling left out by my co-workers. I wish they’d invite me out drinking at least once.", source: "Day 050 교재1", meaning: meanings["leave out_3"] },
        { week: 10, ko: "비프카레가 좀 더 당기는군요. 혹시 청고추는 넣지 말아 주실 수 있을까요? 너무 매운 건 힘들어서요.", en: "I’m leaning towards the beef curry, but could you leave out the green peppers? I can’t really handle lots of spice.", source: "Day 050 교재2", meaning: meanings["leave out_1"] },
        { week: 10, ko: "물론입니다. 주방장님에게 청고추를 빼고 준비해 달라고 할게요. 채소를 추가하거나 치즈를 넣는 것 같은 다른 변경 사항 있을까요?", en: "Of course. I’ll have the chef prepare it without the peppers. Any other changes, like extra vegetables or cheese?", source: "Day 050 교재2", meaning: null },
        { week: 10, ko: "브리즈번 여행 갔다 온 것 다 이야기해 줘. 하나도 빠짐없이!", en: "Tell me all about your trip to Brisbane. Don’t leave out any details!", source: "Day 050 교재2", meaning: meanings["leave out_2"] },
        { week: 10, ko: "아시다시피 영어에서는 대부분의 경우 주어를 생략하지 않잖아요.", en: "You know, in English, we usually shouldn’t leave out the subject.", source: "Day 050 교재2", meaning: meanings["leave out_2"] },
        { week: 10, ko: "저도 영어 교사로서 그 점 잘 알고 있어요. 하지만 한국어는 그렇지 않거든요. 바로 이런 차이점 때문에 한국 학습자들이 영어를 배우기가 쉽지 않은 것 같아요.", en: "I am well aware of that as an English teacher myself, but that’s not the case in Korean. I would say that’s a difference that makes learning English tricky for most Korean learners.", source: "Day 050 교재2", meaning: null },
        { week: 10, ko: "지난달에 남영동 복지관에서 요가 수업을 듣기 시작했다.", en: "I started a yoga class at Namyeong-dong Community Center last month.", source: "Day 050 교재3", meaning: null },
        { week: 10, ko: "석 달 전 이 동네로 이사 와서 친한 친구를 만들지 못했기 때문에 요가를 하면 허리 통증도 좋아지고 새로운 사람도 만날 수 있기를 바랐다.", en: "Since I moved to this neighborhood just three months ago and didn’t have any close friends, I hoped yoga would help me ease my back pain and meet new people.", source: "Day 050 교재3", meaning: null },
        { week: 10, ko: "하지만 계획대로는 되지 않았다.", en: "However, it hasn’t gone as planned.", source: "Day 050 교재3", meaning: null },
        { week: 10, ko: "수업 시간에 몇몇 주부들과 대화를 하긴 하지만, 이들은 같이 점심 먹으러 나갈 때 나를 초대하지 않는다.", en: "Although I chat with some housewives in my class, they go out for lunch without inviting me.", source: "Day 050 교재3", meaning: meanings["leave out_3"] },
        { week: 10, ko: "(부르지도 않았는데) 가서 분위기를 어색하게 하고 싶지는 않지만, 이럴 때면 정말 소외감이 든다.", en: "I don’t want to invite myself and make things awkward, but I feel really left out when this happens.", source: "Day 050 교재3", meaning: meanings["leave out_3"] }
    ];

    // 3. 영어회화 데이터 (Week 9~10)
    const rawConvData = [
        // Week 9
        { week: 9, source: "Day041 교재1", ko: "멋진 핸드크림 선물로 주셔서 감사해요! 그러지 않으셔도 되는데.", en: "Thanks for getting me such nice hand cream! You didn’t have to." },
        { week: 9, source: "Day041 교재1", ko: "학생들에게 크리스마스 선물로 스킨로션을 해 줄까 생각 중입니다.", en: "I’m thinking about getting my students some skin lotion for Christmas." },
        { week: 9, source: "Day041 교재1", ko: "아내분 생일 선물을 뭐 해 주셨어요?", en: "What did you get your wife for her birthday?" },
        { week: 9, source: "Day041 교재1", ko: "제가 계산하는 동안에 나가서 택시 좀 불러 주실 수 있을까요?", en: "Do you mind going out and getting us a taxi while I pay?" },
        { week: 9, source: "Day041 교재2", ko: "안녕하세요. 오늘은 어린이날이라서, 애들 주려고 과자를 사 왔어요. 좀 드시겠어요?", en: "Good morning. It’s Children’s Day, so I got the kids some snacks. Would you like some?" },
        { week: 9, source: "Day041 교재2", ko: "우와! 선생님 너무 친절하세요. 저는 쿠키 먹을게요, 감사합니다.", en: "Oh, wow! You’re so thoughtful. I’ll have a cookie, thanks." },
        { week: 9, source: "Day041 교재2", ko: "이곳 겨울 날씨 너무 힘드네요. 교실 안에 있어도 얼어 죽을 것 같아요!", en: "I really can’t handle the winters here. Even in the classroom, I’m always freezing!" },
        { week: 9, source: "Day041 교재2", ko: "고향은 훨씬 더 따뜻한 거예요? 잠시만요, 사무실 가서 스웨터 갖다 줄게요.", en: "Is it much warmer back home? Hold on, I’ll get you a sweater from my office." },
        { week: 9, source: "Day041 교재2", ko: "여자 친구 생일이 얼마 안 남았는데 뭘 사 줘야 할지 모르겠어. 혹시 추천할 거 있을까?", en: "My girlfriend’s birthday is coming up and I’m not sure what to get her. Do you have any suggestions?" },
        { week: 9, source: "Day041 교재2", ko: "음, 마음이 담긴 거라면, 뭘 해 줘도 좋아할 거야!", en: "Well, as long as it’s thoughtful, I’m sure she’ll love anything you get her!" },
        { week: 9, source: "Day041 교재3", ko: "그리스 가셨을 때 저에게 와인을 한 병 사다 주신 것 너무 감사해요. 제가 그리스 와인을 얼마나 좋아하는지 아실 거예요. 저도 무언가를 해 드려야 할 것 같은데요. 제가 미국 가서 뭐 사다 드릴 게 있을까요?", en: "It was so kind of you to get me a bottle of wine while you were in Greece. You know how much I enjoy Greek wine. Now I feel like I have to get you something. Is there anything you want from America?" },
        { week: 9, source: "Day041 교재4", ko: "여자 친구 생일 선물로 멋진 귀걸이를 해 줄까 합니다.", en: "I was thinking of getting my girlfriend nice earrings for her birthday." },
        { week: 9, source: "Day041 교재4", ko: "내가 CU에서 뭐 사다 줄까?", en: "Do you want me to get you anything from CU?" },
        { week: 9, source: "Day041 교재4", ko: "머리 너무 멋지다! 어떤 디자이너야?", en: "Your hair is great! Who’s your stylist?" },
        { week: 9, source: "Day041 교재4", ko: "홍대에 있는 디자이너에게 머리를 하는데, 내가 예약 잡아 줄까?", en: "I go to this guy in Hongdae. Want me to get you an appointment?" },
        { week: 9, source: "Day041 교재4", ko: "이 근처에 버스 정류장 있어요?", en: "Is there a bus stop nearby?" },
        { week: 9, source: "Day041 교재4", ko: "없는데요. 제가 택시를 불러 줄까요?", en: "No, I’m sorry. Would you like me to get you a taxi?" },
        { week: 9, source: "Day041 대표", ko: "커피 사 왔어요!", en: "I got you a coffee!" },
        { week: 9, source: "Day042 교재1", ko: "고맙지만 저는 괜찮아요.", en: "I’m good, thanks." },
        { week: 9, source: "Day042 교재1", ko: "A: 케이크 한 조각 더 드실래요? B: 아니요, 정말 괜찮아요.", en: "A: Would you like another piece of cake?\nB: No thanks, I’m totally good." },
        { week: 9, source: "Day042 교재1", ko: "A: Kelly, 더 줄까요? B: 아니요, 괜찮아요.", en: "A: You need any more, Kelly?\nB: No thanks, I’m good." },
        { week: 9, source: "Day042 교재1", ko: "(상대방이 음식이나 술을 더 시킬지 물었을 때) 지금 이것만으로도 충분해요.", en: "I’m good with what I already have." },
        { week: 9, source: "Day042 교재1", ko: "편의점에서 뭐 사다 줄까, 아님 괜찮아?", en: "Do you want anything from the convenience store, or are you good?" },
        { week: 9, source: "Day042 교재2", ko: "뭐 좀 더 드시겠어요, 손님?", en: "Would you like anything else to eat or drink, Sir?" },
        { week: 9, source: "Day042 교재2", ko: "고맙지만 괜찮아요.", en: "No thanks, I’m good." },
        { week: 9, source: "Day042 교재2", ko: "집에 가는 길에 가게 들를 건데, 뭐 필요한 거 있어?", en: "I’m stopping by the store on my way home, would you like anything?" },
        { week: 9, source: "Day042 교재2", ko: "아니, 괜찮아.", en: "Oh, no thanks, I’m good!" },
        { week: 9, source: "Day042 교재2", ko: "너 이번 주말에 이사한다며. 필요하면 남편이랑 내가 가서 도와줄게.", en: "I heard you’re moving this weekend. My husband and I could come and help if you need it." },
        { week: 9, source: "Day042 교재2", ko: "아, 제안 고마워! 남동생이 이미 와서 도와주기로 했으니 괜찮을 것 같아.", en: "Oh, thanks for the offer! My brother is already coming to help, so I think we’re good." },
        { week: 9, source: "Day042 교재3", ko: "A: 나 이제야 파티 가는 길이야. 늦어서 미안해. 필요한 거 있을까? 술, 아님 과자? 빈손으로 가면 좀 그렇잖아.", en: "A: I’m finally on my way to the party. Sorry for running late. What do you guys need? Drinks, snacks? I don’t want to come empty-handed." },
        { week: 9, source: "Day042 교재3", ko: "B: 우선은 괜찮아. 애들이 너무 많이 가지고 왔거든. 이따가 뭐 필요한 거 생기면 네가 사렴.", en: "B: I actually think we’re good for now. The guys who are already here brought more than enough. If we need something else later, it can be your treat, though." },
        { week: 9, source: "Day042 교재4", ko: "커피 더 드시겠어요?", en: "Would you like more coffee?" },
        { week: 9, source: "Day042 교재4", ko: "네 조금만 주세요. — 네. 그 정도면 됐습니다.", en: "Just a little please. — Okay. That’s good." },
        { week: 9, source: "Day042 교재4", ko: "아몬드 우유는 개봉하고도 한 달이 더 간다.", en: "Almond milk is good for a month or more after opening." },
        { week: 9, source: "Day042 교재4", ko: "이 쿠폰의 유효 기간은 딱 2주 입니다. 기회를 놓치지 마세요.", en: "The coupons are only good for two weeks. Don’t miss out." },
        { week: 9, source: "Day042 교재4", ko: "(줌 세션 진행 중 음향 문제가 해결된 상황) 이제 준비됐습니다!", en: "I’m good to go!" },
        { week: 9, source: "Day042 교재4", ko: "(발표하려는데 갑자기 컴퓨터가 작동되지 않는 상황) 금방 될 거예요", en: "It should be good to go in a minute." },
        { week: 9, source: "Day042 대표", ko: "저는 괜찮습니다.", en: "I’m good." },
        { week: 9, source: "Day043 교재1", ko: "나는 에어컨 도저히 못 고치겠다. 기술자 불러야겠어.", en: "I can’t figure out how to fix my a/c. I need to call a technician." },
        { week: 9, source: "Day043 교재1", ko: "숙제를 이리 가져와 보렴. 같이 풀어 보자.", en: "Bring your homework over here. We can figure it out together." },
        { week: 9, source: "Day043 교재1", ko: "외국인들한테는 서울 지하철이 좀 헷갈릴 수도 있을 거예요.", en: "Seoul’s subway system might be a bit hard for foreigners to figure out." },
        { week: 9, source: "Day043 교재1", ko: "지금 다섯 달째 쉬고 있습니다. 다음에 뭘 해야 할지 막막합니다.", en: "I’ve been out of work for five months now. I can’t figure out what to do next." },
        { week: 9, source: "Day043 교재1", ko: "옷장을 다 뒤져 봤는데도 뭘 입어야 할지 모르겠네.", en: "I’ve gone through my whole closet, and I still can’t figure out what to wear." },
        { week: 9, source: "Day043 교재2", ko: "음, 저기요! 죄송한데 좀 도와주실 수 있어요? 제 딸 만나러 고려대에 가는 길인데, 가는 방법을 도무지 알 수 없어서요.", en: "Um, hello! I’m sorry, can you help me? I’m on my way to see my daughter at Korea University, but I can’t figure out how to get over there." },
        { week: 9, source: "Day043 교재2", ko: "네, 당연히 도와드려야죠. 그렇게 어렵지 않습니다. 여기 지하철 앱 다운로드하시면, 가는 길 쉽게 알 수 있을 거예요!", en: "Oh! Sure, I can help. It’s not too hard. Here, if you download a subway app, you’ll be able to figure it out easily!" },
        { week: 9, source: "Day043 교재2", ko: "아직도 책상 조립하는 방법을 못 알아낸 거야? 뭐가 이렇게 지저분해.", en: "You still haven’t figured out how to put together the desk? I don’t like all this mess." },
        { week: 9, source: "Day043 교재2", ko: "아직 못했어. 아무래도 매장에 전화해서 도움을 구해야겠어.", en: "No. I might need to call the store for help." },
        { week: 9, source: "Day043 교재3", ko: "(배송 지연 상황에 대해 거래처에 설명하는 내용의 이메일)\n계속 지연되어 죄송합니다만, 저희 쪽 기계가 고장이 나서 현재 주문 건을 처리할 수 없는 상황입니다. 정확한 문제 원인을 파악 중입니다. 기계적 문제와 교체가 필요한 부품 때문인 것 같습니다. 문제가 해결되면, 주문 건을 바로 처리할 수 있습니다.", en: "I’m sorry for the continued delay, but our machines have been malfunctioning and so we are currently unable to complete orders. We’re trying to figure out what exactly went wrong. It is likely a mechanical issue and a part that needs replacing. Once this problem is resolved, we’ll be able to fulfill your order right away." },
        { week: 9, source: "Day043 교재4", ko: "카카오맵 쓰는 법을 알고 나니까, 삶이 편하네.", en: "Once I figured out how to use KakaoMap, life got easier." },
        { week: 9, source: "Day043 교재4", ko: "여자 친구를 10년 동안 만나왔는데도 아직도 그녀를 모르겠어요.", en: "I’ve been seeing my girlfriend for 10 years, and I still can’t figure her out." },
        { week: 9, source: "Day043 교재4", ko: "의사 선생님 조차도 제 두통의 원인을 모르십니다.", en: "Even my doctor can’t figure out what’s causing my migraines." },
        { week: 9, source: "Day043 교재4", ko: "뭘 먹을지는 만나서 정하자.", en: "Let’s figure out what to eat then." },
        { week: 9, source: "Day043 교재4", ko: "저는 40대가 되어서야 저의 성 정체성을 알게 되었답니다.", en: "I don’t think I really figured out my sexual orientation until I was in my 40s." },
        { week: 9, source: "Day043 대표", ko: "눈치가 빠르시네요.", en: "You figured that out right away." },
        { week: 9, source: "Day044 교재1", ko: "이 책상 옮기는 거 좀 도와줬으면 좋겠는데.", en: "I could use your help moving this desk." },
        { week: 9, source: "Day044 교재1", ko: "보니까 너 당분간 좀 쉬어야겠다.", en: "You look like you could really use some time off." },
        { week: 9, source: "Day044 교재1", ko: "지금 마케팅 전략으로는 안 됩니다.", en: "We could use a better marketing strategy." },
        { week: 9, source: "Day044 교재1", ko: "미안한데 내가 월세 낼 돈이 오십 달러 부족한데 네가 좀 도와주면 좋을 텐데.", en: "Sorry, I’m $50 short on rent and could use some help." },
        { week: 9, source: "Day044 교재1", ko: "어젯밤에 거의 못 잤어. 커피가 필요해.", en: "I hardly slept last night. I could really use a coffee." },
        { week: 9, source: "Day044 교재2", ko: "아직 공부하고 있는 거야? 몇 시간째야. 계속 안 쉬고 하는 거야?", en: "You’re still studying? It’s been hours. Have you been working this whole time?" },
        { week: 9, source: "Day044 교재2", ko: "응. 솔직히 좀 쉬긴 해야 할 듯. 커피 마실까?", en: "Yeah, I have. I could really use a break, honestly. Are you down for some coffee?" },
        { week: 9, source: "Day044 교재2", ko: "혹시 일본어 선생님 아는 분 있을까요, Daniel? 다음 달 오사카 가기 전에 제 일본어 좀 다듬어야 할 것 같아서요.", en: "Do you know any Japanese tutors, Daniel? I feel like my Japanese could use some work before I fly to Osaka next month." },
        { week: 9, source: "Day044 교재2", ko: "도움이 될 수 있으면 좋은데. 제가 아는 분은 전부 영어 선생님이라서요.", en: "I wish I could help. Everyone I know just teaches English." },
        { week: 9, source: "Day044 교재2", ko: "여기. 이 소스 살짝 맛 좀 봐 봐. 어때?", en: "Here. Try a bit of this sauce. What do you think?" },
        { week: 9, source: "Day044 교재2", ko: "응. 나쁘진 않은데. 음... 소금을 조금만 더 넣어야겠다.", en: "Yeah. Not bad. Umm... it could just use a little more salt." },
        { week: 9, source: "Day044 교재3", ko: "안녕, Nick. 나 소설 쓰는 거 알지? 진도가 안 나가. 이야기가 어느 방향으로 흘러가고 있는지 도무지 감이 안 잡혀. 정말 모르겠어. 지금 소주가 정말 필요하네. 한잔 콜? 내가 살게.", en: "Hey, Nick! You know that novel I’ve been working on? I feel like I’m stuck. I just can’t figure out where this story is going. Man, I don’t know. I could really use some soju right about now. Are you down? My treat." },
        { week: 9, source: "Day044 교재4", ko: "오늘 삼겹살이 당기네.", en: "I could really go for pork belly today." },
        { week: 9, source: "Day044 교재4", ko: "커피가 무지 당기네.", en: "I could really go for coffee." },
        { week: 9, source: "Day044 교재4", ko: "단 게 당기네.", en: "I could really go for something sweet." },
        { week: 9, source: "Day044 교재4", ko: "지금 당장 시원한 맥주가 당긴다.", en: "I could go for a cold beer right now." },
        { week: 9, source: "Day044 대표", ko: "커피 한 잔 마시면 좋겠네요.", en: "I could really use a cup of coffee." },
        { week: 9, source: "Day045 교재1", ko: "정말 그렇게 생각하세요? 말씀 너무 고맙습니다.", en: "You think so? That’s so nice of you to say." },
        { week: 9, source: "Day045 교재1", ko: "말씀 정말 고마워요!", en: "How nice of you to say so!" },
        { week: 9, source: "Day045 교재1", ko: "그렇게 말씀해 주시다니 너무 고맙네요.", en: "That’s so sweet of you to say something like that." },
        { week: 9, source: "Day045 교재1", ko: "(머리가 잘 됐다는 상대의 말에) 농담이죠? 말씀 감사한데, 저는 그렇게 만족스럽지는 않네요.", en: "You’re kidding, right? Thank you for saying so, but I’m still not quite happy with it." },
        { week: 9, source: "Day045 교재1", ko: "(이사하는 걸 도와주겠다는 친구에게) 제안은 너무 고맙지만, 지금은 더 이상의 도움은 필요 없어서 말이야.", en: "It’s nice of you to offer, but I don’t really need any more help." },
        { week: 9, source: "Day045 교재2", ko: "카페가 어쩜 이렇게 이뻐요! 이 동네에 딱 필요했던 거예요.", en: "What a beautiful cafe! It’s just what this neighborhood needed." },
        { week: 9, source: "Day045 교재2", ko: "말씀 고마워요. 예쁘게 꾸미려고 엄청 신경 썼답니다.", en: "How nice of you to say so! I put a lot of effort into making it look just right." },
        { week: 9, source: "Day045 교재2", ko: "면접 통과에 대해 너무 걱정하지 말아. 네가 안 되면 누가 되냐?", en: "Don’t worry so much about passing the interview. I can’t imagine anyone more qualified." },
        { week: 9, source: "Day045 교재2", ko: "그렇게 말해 주니 고맙지만, 잘 모르겠어.", en: "Thank you for saying so, but I’m not so sure." },
        { week: 9, source: "Day045 교재2", ko: "에세이 정말 인상적이군, James. 자네 많이 늘었어. 전문 에세이 쓰는 사람을 고용해서 쓴 것처럼 말이지.", en: "I’m so impressed with your writing, James. You’ve really improved. It’s almost like you hired a professional to write for you." },
        { week: 9, source: "Day045 교재2", ko: "하하! 말씀 감사드려요, Brown 교수님. 이건 완전 제가 쓴 거예요.", en: "Haha! That’s nice of you to say, Ms. Brown. This essay is all mine." },
        { week: 9, source: "Day045 교재3", ko: "A: 그동안 어떻게 지냈어요? 제 수업 그만두고 영어가 진짜 많이 나아진 것 같네요. 비밀이 뭔가요?", en: "A: How have you been? It sounds like your English has really improved since you stopped taking my classes. What’s your secret?" },
        { week: 9, source: "Day045 교재3", ko: "B: 말씀 너무 고마워요. 솔직히 다 선생님 덕분이에요. 선생님이 가르쳐 주신 걸 계속 연습하고 있거든요.", en: "B: That’s nice of you to say. Honestly, it’s all thanks to you. I’ve just been doing the same exercises you taught me." },
        { week: 9, source: "Day045 교재4", ko: "어제 남편이 제가 옷 입은 걸 칭찬해 줘서 온종일 기분이 좋았어요.", en: "My husband complimented me on my outfit yesterday, and that made my day." },
        { week: 9, source: "Day045 교재4", ko: "사람들이 저보고 남부 사투리 안 쓴다고 하는데, 저는 그걸 칭찬으로 받아들입니다.", en: "When people say I don’t have any Southern accent, I take it as a compliment." },
        { week: 9, source: "Day045 교재4", ko: "여기까지 먼 길 오셔서 뭐라고 감사를 드려야 할지.", en: "I can’t thank you enough for coming all the way out here." },
        { week: 9, source: "Day045 대표", ko: "그렇게 말씀해 주셔서 너무 고맙습니다.", en: "It’s nice of you to say so." },

        // Week 10
        { week: 10, source: "Day046 교재1", ko: "(요즘 좋아 보인다는 말에 대해) 나쁘지 않아요. 일이 잘 풀리고 있어요.", en: "I can’t complain. Things are going pretty well." },
        { week: 10, source: "Day046 교재1", ko: "(허리가 안 좋은 사람이) 최근에 몸이 살짝 불편하긴 한데, 그래도 나쁘지 않습니다.", en: "I’ve been feeling a little out of sorts lately, but I can’t complain." },
        { week: 10, source: "Day046 교재1", ko: "(새로운 상사와 일하는 것이 어떠냐는 질문에) 나쁘지 않아요. 같이 일하기 편해요.", en: "I can’t complain. He is easy to work with." },
        { week: 10, source: "Day046 교재1", ko: "(서울에서 파는 타코를 먹어 본 외국인이) 한국 타코가 좀 덜 맵긴 해요. 그래도 나쁘진 않아요.", en: "The tacos I’ve had in Korea are much less spicy. I can’t complain, though." },
        { week: 10, source: "Day046 교재1", ko: "(신차 시승을 마친 고객이) 나쁘지 않아요. 핸들링도 꽤 괜찮았어요.", en: "I can’t complain at all. The handling was pretty good." },
        { week: 10, source: "Day046 교재2", ko: "대학에 다니기 시작했다고 들었어. 처음 몇 주는 어땠어?", en: "I heard that you finally started college. How were the first few weeks?" },
        { week: 10, source: "Day046 교재2", ko: "음, 나쁘지 않아. 과제는 어렵지만, 그만한 가치가 있을 거야. 게다가 벌써 친구도 많이 사귀었어.", en: "Hm. I can’t complain. The assignments are really hard, but I know it will be worth it. And besides, I’ve made a lot of friends already!" },
        { week: 10, source: "Day046 교재2", ko: "이거 이번에 새로 산 차야? 좋아 보이는데 몇 년 된 거야? 20년이나 25년?", en: "Oh, is this your new car? It looks good, but how old is it? Maybe 20 or 25 years old?" },
        { week: 10, source: "Day046 교재2", ko: "응, 2000년 식이야. 근데 나쁘지 않아. 요즘은 저렴한 차를 구하기가 너무 힘들잖아.", en: "Yeah, it’s a 2000 model. I can’t complain, though. It’s hard to find any affordable car in this market." },
        { week: 10, source: "Day046 교재3", ko: "아빠, 잘 지내시죠?\n제가 시내에서 오토바이 타는 것을 많이 걱정하신다고 들었어요. 오토바이가 조금 낡긴 했지만, 나름 괜찮아요. 아주 싸게 샀고요. 너무 걱정 마세요. 안전 운전 과정도 이수하고 있고, 안전 장비도 풀세트로 구매했으니까요", en: "Hi Dad,\nI heard you were concerned about me riding in the city. I admit the motorcycle itself is a little bit old, but I can’t complain. I got a great deal on it. Anyways, please don’t worry too much! I’m taking a driving safety course, and I’ve bought a full set of safety gear." },
        { week: 10, source: "Day046 교재4", ko: "내 남자 친구는 괜찮은 옷이 없어.", en: "My boyfriend doesn’t have any decent clothes." },
        { week: 10, source: "Day046 교재4", ko: "애플하고 삼성 폰의 카메라가 멋지긴 하지만, 샤오미 폰도 쓸 만하다.", en: "Samsung and Apple phones have great cameras, but Xiaomi’s are still decent." },
        { week: 10, source: "Day046 교재4", ko: "나는 복지관에서 운동하는 것도 괜찮아. 장비가 새것은 아니지만, 나쁘지 않아.", en: "I don’t mind working out at a community center. Even though the equipment isn’t new, it’s still decent." },
        { week: 10, source: "Day046 교재4", ko: "요즘 그 속어가 꽤 흔하게 쓰이는 것 같아요.", en: "I guess that slang is decently common these days." },
        { week: 10, source: "Day046 대표", ko: "나쁘지 않아요.", en: "I can’t complain at all." },
        { week: 10, source: "Day047 교재1", ko: "너 나한테 십만 원 갚을 거 있잖아.", en: "You owe me 100,000 won." },
        { week: 10, source: "Day047 교재1", ko: "카페에서 뭐 좀 사 갈까? 나 어차피 너한테 점심 사야 돼.", en: "Want me to grab you something from the coffee shop? I owe you lunch, anyway." },
        { week: 10, source: "Day047 교재1", ko: "이사하는 거 도와주셔서 제가 신세를 졌네요.", en: "I owe you a favor for helping me move." },
        { week: 10, source: "Day047 교재1", ko: "(헬스 트레이너가 하는 말) 그럼 다음 수업에서는 오늘 못 한 팔굽혀펴기 스무 번 하셔야 합니다.", en: "You owe me 20 push-ups in our next session." },
        { week: 10, source: "Day047 교재1", ko: "상사들이 널 그렇게 대하는데도 왜 받아 주는 거야? 무슨 빚이라도 진 사람 같아.", en: "Why do you accept such poor treatment from your supervisors? You act like you owe them something." },
        { week: 10, source: "Day047 교재2", ko: "이렇게 빨리 수리해 주셔서 정말 감사합니다. 얼마 드리면 되나요?", en: "I really appreciate you getting this fixed so quickly. So how much do I owe you?" },
        { week: 10, source: "Day047 교재2", ko: "부품값만 주시면 됩니다. 뭐 크게 어려운 것도 아니었는데요.", en: "Just paying for the parts would be good enough. It wasn’t any trouble." },
        { week: 10, source: "Day047 교재2", ko: "잘 모르겠어. 이렇게 그만두니 마음이 안 좋아. 후임자 찾는 걸 도와줘야 할까? 아님 마지막 날 좋은 이별 선물이라도 해야 할까?", en: "I don’t know. I just feel bad leaving my job like this. Should I help them find my replacement? Or should I give them a nice good-bye gift on my last day?" },
        { week: 10, source: "Day047 교재2", ko: "잊어버려, Alex! 뭘 고마운 게 있다고. 뒤도 돌아보지 말라고!", en: "Forget about it, Alex! You don’t owe them anything. Leave and never look back!" },
        { week: 10, source: "Day047 교재3", ko: "안녕하세요. Bernstein 씨,\n19일에 있었던 제 딸 결혼식 식사 준비를 너무 잘해 주셔서 다시 한번 감사하다는 말씀을 드립니다. 청구서를 요청하려고 메일 드립니다. 정확한 금액 알려 주시면 월요일에 계좌로 송금하겠습니다.", en: "Good afternoon, Mr. Bernstein,\nI would like to thank you again for the terrific job you did catering my daughter’s wedding on the 19th. I’m writing to ask for an invoice. Please let me know exactly how much I owe you, and I will transfer the money to your account on Monday." },
        { week: 10, source: "Day047 교재4", ko: "얼마 드리면 되나요? (‘정가’가 얼마인지 묻는 느낌)", en: "How much does it cost?" },
        { week: 10, source: "Day047 교재4", ko: "얼마 드리면 되나요? (정해지지 않은 가격)", en: "How much do I owe you?" },
        { week: 10, source: "Day047 교재4", ko: "의사분들과 간호사분들 그리고 그밖에 현장에서 고생하시는 분들 덕분입니다.", en: "We owe it to the doctors and nurses and other front-line workers." },
        { week: 10, source: "Day047 교재4", ko: "5달러 내놔.", en: "You owe me five bucks." },
        { week: 10, source: "Day047 대표", ko: "너 나한테 5달러 줄 거 있어.", en: "You owe me five bucks." },
        { week: 10, source: "Day048 교재1", ko: "당신도 그렇게 느꼈다니 다행이군.", en: "I’m glad you felt the same way." },
        { week: 10, source: "Day048 교재1", ko: "그곳 서비스가 진짜 마음에 들었어? 난 전혀 아닌데.", en: "Were you really happy with the service there? I certainly didn’t feel the same way." },
        { week: 10, source: "Day048 교재1", ko: "그 사람이랑 일하는 게 싫고, 그 사람도 나에 대해 마찬가지일 거야.", en: "I don’t like working with him, and I think he feels the same way towards me." },
        { week: 10, source: "Day048 교재1", ko: "언젠가 같이 다시 일했으면 좋겠네요. 당신도 그렇길 바라요.", en: "I want to work with you again someday, and I hope you feel the same way." },
        { week: 10, source: "Day048 교재1", ko: "(카페 주인이 음악 소리가 너무 크지 않은지 묻자) 그 이야기를 꺼내 주셔서 다행이네요. 저도 그렇게 느꼈어요.", en: "I’m glad you brought it up. I was feeling the same way." },
        { week: 10, source: "Day048 교재2", ko: "Johnson 씨, 이 제안서 좀 서둘렀나 봐요. 오타 같은 게 보여요. 좀 더 신경 썼으면 좋았을 텐데요.", en: "Mr. Johnson, this proposal looks like it was a bit rushed. I see a few typos and such. I think you could have done better." },
        { week: 10, source: "Day048 교재2", ko: "솔직히 저도 그렇게 생각합니다. 좀 더 시간을 들였어야 했어요.", en: "Honestly, I feel the same way. I wish I had spent more time on it." },
        { week: 10, source: "Day048 교재2", ko: "Frank, 얘기 좀 해. 우리 사이가 좀 멀어진 것 같아.", en: "Frank, we need to talk. I think we’ve grown apart." },
        { week: 10, source: "Day048 교재2", ko: "응, Sally. 나도 그렇게 느낀 지 좀 됐어", en: "Yeah, Sally. I’ve felt the same way for a while now." },
        { week: 10, source: "Day048 교재2", ko: "포르쉐에 전화해서 수리 일정 잡으려 했는데, 10월까지 기다려야 된다고 하더라. 신규 고객이 아니면 별로 신경을 안 쓰는 듯.", en: "I called Porsche and tried to arrange a repair, but they said I would have to wait until October. It’s like they don’t care about you unless you’re a new customer." },
        { week: 10, source: "Day048 교재2", ko: "응, 맞아! 지난번에 엔진오일 갈 때 나도 그렇게 느꼈거든.", en: "Yeah, really! I felt the same way the last time I got my oil changed." },
        { week: 10, source: "Day048 교재3", ko: "저희 식당에 대해 좋게 말해 주셔서 고맙습니다. 저희가 편안한 분위기와 특별한 음식을 제공하고 있다고 생각은 하는데, 그렇게 느끼셨다니 너무 좋습니다. 이런 의견 덕분에 노력한 보람을 느낀답니다. 다음 방문도 기다리겠습니다.", en: "Thank you for your very kind review of our restaurant. We think that we provide a comfortable atmosphere and unique food, and we’re glad you feel the same way. Comments like yours make all of our efforts worth it. We look forward to your next visit." },
        { week: 10, source: "Day048 교재4", ko: "(회의를 마무리하면서) 우리가 모두 같은 생각인 거죠?", en: "Are we on the same page?" },
        { week: 10, source: "Day048 교재4", ko: "저는 그냥 가볍게 만나는 관계를 찾고 있었는데, 남자 쪽은 그게 아니더군요.", en: "I was just looking for a casual relationship, but he wasn’t on the same page." },
        { week: 10, source: "Day048 교재4", ko: "(줌 수업으로 착각한 선생님이 학생에게) 우리가 온라인으로 만나는 줄 알았는데 서로 다르게 알고 있었네요.", en: "I thought we were meeting online, but it turns out we weren’t on the same page about that." },
        { week: 10, source: "Day048 교재4", ko: "근로 계약에 대해 모두가 같은 생각인지 확인하고 싶습니다.", en: "I’d like to make sure we’re on the same page about our labor contract." },
        { week: 10, source: "Day048 대표", ko: "저도 같은 생각이에요.", en: "I feel the same way." },
        { week: 10, source: "Day049 교재1", ko: "그건 저한테 엄청 귀찮게 느껴져요.", en: "That feels like a big hassle to me." },
        { week: 10, source: "Day049 교재1", ko: "혼자 먹으려고 요리하는 게 엄청 귀찮게 느껴지시죠?", en: "Does cooking for one feel like too much of a hassle?" },
        { week: 10, source: "Day049 교재1", ko: "커피 원두를 쏟으면 주워 담는 게 일이지.", en: "Coffee beans are a hassle to pick up if you spill them." },
        { week: 10, source: "Day049 교재1", ko: "머리를 짧게 하면 아침에 시간도 아끼고, 번거롭지도 않아요.", en: "Keeping my hair short saves me time and hassle in the morning." },
        { week: 10, source: "Day049 교재1", ko: "Josh가 소파를 문 앞에 두고 갔어. 밖에 나갈 때마다 타 넘고 가는 게 몹시 번거로웠어.", en: "Josh left the sofa in front of the door. It was such a hassle to get over it every time I went outside." },
        { week: 10, source: "Day049 교재2", ko: "아침에 운동하면, 기분이 좋아지고 업무 집중도 더 잘 돼.", en: "When I work out in the morning, it puts me in a good mood, and it’s easier to stay focused at work, too." },
        { week: 10, source: "Day049 교재2", ko: "응, 나도 출근 전에 운동하고 싶은데 귀찮아.", en: "Yeah, I’d like to start exercising before work too, but it feels like such a hassle." },
        { week: 10, source: "Day049 교재2", ko: "저희가 직접 에어컨을 수리하려고 했는데 잘 안됐어요. 그래서 에어컨 아래쪽에 플라스틱 통을 놔뒀는데 한 시간마다 비워 줘야 해요.", en: "We tried fixing the air conditioner ourselves, but it didn’t work. We put a big plastic bowl underneath it and have to empty that every hour or so." },
        { week: 10, source: "Day049 교재2", ko: "진짜요? 엄청 번거롭겠어요. 그래도 어떻게든 되기는 하네요. 요즘 같은 날씨에 난 에어컨 없이는 못 살아요.", en: "Wow! That sounds like such a hassle. At least it’s still working. I couldn’t live without a/c in this weather." },
        { week: 10, source: "Day049 교재3", ko: "이번 여행에서는 미국에서 코로나 검사 받는 게 가장 번거로웠던 일입니다. 미국은 PCR 검사기기가 부족한 상황이었던 터라, 한국으로 돌아가는 비행 편에 맞춰서 검사 결과가 나오지를 않았지요. 그래서 어쩔 수 없이 공항에서 신속 항원 검사 키트를 사야만 했어요. 근데 너무 비싸더군요.", en: "Getting tested in America was the biggest hassle of my trip. They had a shortage of PCR tests, and I couldn’t get a result in time before my flight. I had no choice but to buy a rapid test at the airport, which cost an arm and a leg." },
        { week: 10, source: "Day049 교재4", ko: "(밖에 나가 담배를 피워야 하는 상황) 겨울이 너무 싫어요. 담배 피우고 싶을 때마다 옷을 여러 겹 입는 게 너무 귀찮아요", en: "I hate winter. It’s quite a hassle to put on layers every time I want to smoke." },
        { week: 10, source: "Day049 교재4", ko: "공항에 너 픽업 가는 게 그렇게 귀찮지는 않았어.", en: "It wasn’t too much of a hassle for me to pick you up from the airport." },
        { week: 10, source: "Day049 교재4", ko: "식료품은 온라인에서 주문하지 그래?", en: "Why don’t you just order groceries online?" },
        { week: 10, source: "Day049 교재4", ko: "나는 식료품 상점 가는 게 하나도 안 귀찮은데.", en: "Going to the store is no hassle at all for me." },
        { week: 10, source: "Day049 대표", ko: "두 번 갈아타는 게 너무 귀찮게 느껴져요.", en: "Transferring twice feels like a huge hassle." },
        { week: 10, source: "Day050 교재1", ko: "(업무 방식에 대해 하는 말) “그렇지만 여기는 원래 그래요.”라는 변명을 자주 듣게 될 겁니다.", en: "You’ll often hear excuses like, “but that’s just how things work here.”" },
        { week: 10, source: "Day050 교재1", ko: "자본주의 사회에서는 원래 그런 거죠.", en: "That’s just how things work in capitalism." },
        { week: 10, source: "Day050 교재1", ko: "처음에는 CEO의 딸이 저보다 먼저 승진해서 정말 화가 났습니다. 근데 가족 운영 기업에서는 원래 그렇다는 걸 알게 되었지요.", en: "At first, I was mad about the CEO’s daughter being promoted faster than me. But then I realized that’s just how things work at a family owned company." },
        { week: 10, source: "Day050 교재1", ko: "워라밸이 보장되면 참 좋겠지만, 대부분 한국 기업은 그렇지가 않아요.", en: "I wish I had a nice balance between work and home life, but that’s not how it works in most Korean companies." },
        { week: 10, source: "Day050 교재1", ko: "네가 요금을 내면, 팁은 내가 낼게.", en: "If you are paying the fare, then I’ve got the tip!" },
        { week: 10, source: "Day050 교재2", ko: "하하, 고맙지만, 한국에서는 그렇게 안 해. 택시 기사분들에게 팁을 안 주거든.", en: "Haha, thanks, but that’s not how things work here. We don’t tip taxi drivers." },
        { week: 10, source: "Day050 교재2", ko: "월세 낼 돈이 모자라면 사장한테 연봉 올려 달라고 하면 안 돼?", en: "If you don’t have enough money to pay your rent, can’t you just ask your boss for a raise?" },
        { week: 10, source: "Day050 교재2", ko: "앗, 대기업에서 누가 그래.", en: "Eh, that’s not really how things work at a conglomerate." },
        { week: 10, source: "Day050 교재2", ko: "혹시 예외적으로 30%의 금액만으로 주문할 수 있을까요?", en: "Could you possibly make an exception and let me place an order with only 30% down?" },
        { week: 10, source: "Day050 교재2", ko: "죄송한데, 그건 힘듭니다. 무조건 50%를 내야 합니다.", en: "I am afraid it doesn’t work that way. Everybody has to put down at least 50%." },
        { week: 10, source: "Day050 교재3", ko: "미국에서는 지나가다 누군가와 부딪히면 곧장 사과를 합니다. 그런데 여기는 그렇지 않습니다! 이곳은 빨리빨리 사회라서 개인의 공간은 무시되기 일쑤입니다.", en: "In America, if you accidentally bump into someone as you walk past them, you immediately apologize. But that’s not how it works here! This is a very fast paced country and personal space is often disregarded." },
        { week: 10, source: "Day050 교재4", ko: "너 월세 밀리면 안 되잖아.", en: "I don’t want you to get behind on your rent." },
        { week: 10, source: "Day050 교재4", ko: "우리 등록금이 오른다는 소식 들었어?", en: "Did you hear about our tuition going up?" },
        { week: 10, source: "Day050 교재4", ko: "주문하신 음식 10분 안에 준비됩니다.", en: "Your order will be ready in 10 minutes." },
        { week: 10, source: "Day050 대표", ko: "여기서는 원래 그래요.", en: "That’s just how things work here." }
    ];

    // 영어회화 난이도 분리
    const convEasy = rawConvData.filter(item => item.source.includes('대표') || item.source.includes('교재1'));
    const convHard = rawConvData.filter(item => !(item.source.includes('대표') || item.source.includes('교재1')));

    // 퀴즈 진행 상태 변수
    let currentQuestions = [];
    let currentIndex = 0;
    let isPhrasalMode = false;
    let starredQuestions = []; 

    function shuffleArray(array) {
        let shuffled = [...array];
        for (let i = shuffled.length - 1; i > 0; i--) {
            const j = Math.floor(Math.random() * (i + 1));
            [shuffled[i], shuffled[j]] = [shuffled[j], shuffled[i]];
        }
        return shuffled;
    }

    // 선택된 주차에 맞게 필터링
    function filterByWeek(dataArray) {
        if (currentWeekFilter === 'all') {
            return dataArray.filter(item => item.week >= 9 && item.week <= 10);
        }
        return dataArray.filter(item => item.week === currentWeekFilter);
    }

    function startQuiz(mode) {
        let sourceArray = [];
        let titleMode = "";

        if (mode === 'phrasal-easy') { 
            sourceArray = phrasalEasy; isPhrasalMode = true; 
            titleMode = "🟢 구동사 순한맛 퀴즈"; 
        }
        else if (mode === 'phrasal-hard') { 
            sourceArray = phrasalHard; isPhrasalMode = true; 
            titleMode = "🔴 구동사 매운맛 퀴즈"; 
        }
        else if (mode === 'conv-easy') { 
            sourceArray = convEasy; isPhrasalMode = false; 
            titleMode = "💬 영어회화 순한맛 퀴즈"; 
        }
        else if (mode === 'conv-hard') { 
            sourceArray = convHard; isPhrasalMode = false; 
            titleMode = "🔥 영어회화 매운맛 퀴즈"; 
        }

        const filteredData = filterByWeek(sourceArray);

        if (filteredData.length === 0) {
            alert(`선택하신 주차(Week ${currentWeekFilter})에 해당하는 데이터가 아직 없습니다.`);
            return;
        }

        document.getElementById('mode-selection').classList.add('hidden');
        document.getElementById('quiz-area').classList.remove('hidden');
        
        let weekText = currentWeekFilter === 'all' ? " (Week 9~10 누적)" : ` (Week ${currentWeekFilter})`;
        document.getElementById('main-title').innerText = titleMode + weekText; 
        
        starredQuestions = []; 
        // 7문제만 추출 (데이터가 7개 미만이면 전체 추출)
        const qCount = Math.min(filteredData.length, 7);
        currentQuestions = shuffleArray(filteredData).slice(0, qCount);
        currentIndex = 0;
        
        loadQuestion();
    }

    function loadQuestion() {
        document.getElementById('answer-section').classList.add('hidden');
        document.getElementById('btn-next').classList.add('hidden');
        document.getElementById('btn-finish').classList.add('hidden');
        document.getElementById('meaning-info').classList.add('hidden');
        
        const koBox = document.getElementById('ko-box');
        koBox.style.cursor = 'pointer';
        koBox.style.pointerEvents = 'auto';

        const q = currentQuestions[currentIndex];
        document.getElementById('question-counter').innerText = `문제 ${currentIndex + 1} / ${currentQuestions.length}`;
        document.getElementById('ko-text').innerText = q.ko;
        document.getElementById('en-text').innerText = q.en;
        document.getElementById('source-info').innerText = `출처: ${q.source}`;
        
        if(isPhrasalMode && q.meaning) {
            document.getElementById('meaning-info').innerText = q.meaning;
        }

        const starBtn = document.getElementById('btn-star');
        if (starredQuestions.includes(q)) {
            starBtn.classList.add('active');
            starBtn.innerText = "⭐ 어려워요 (저장됨)";
        } else {
            starBtn.classList.remove('active');
            starBtn.innerText = "⭐ 어려워요";
        }
    }

    function showAnswer() {
        const koBox = document.getElementById('ko-box');
        koBox.style.cursor = 'default';
        koBox.style.pointerEvents = 'none';

        document.getElementById('answer-section').classList.remove('hidden');
        
        if(isPhrasalMode && currentQuestions[currentIndex].meaning) {
            document.getElementById('meaning-info').classList.remove('hidden');
        }
        
        if (currentIndex < currentQuestions.length - 1) {
            document.getElementById('btn-next').classList.remove('hidden');
        } else {
            document.getElementById('btn-finish').classList.remove('hidden');
        }
    }

    function toggleStar() {
        const q = currentQuestions[currentIndex];
        const starBtn = document.getElementById('btn-star');
        const index = starredQuestions.indexOf(q);
        
        if (index > -1) {
            starredQuestions.splice(index, 1);
            starBtn.classList.remove('active');
            starBtn.innerText = "⭐ 어려워요";
        } else {
            starredQuestions.push(q);
            starBtn.classList.add('active');
            starBtn.innerText = "⭐ 어려워요 (저장됨)";
        }
    }

    function playTTS() {
        const textToSpeak = currentQuestions[currentIndex].en;
        if ('speechSynthesis' in window) {
            window.speechSynthesis.cancel();
            const utterance = new SpeechSynthesisUtterance(textToSpeak);
            utterance.lang = 'en-US';
            utterance.rate = 0.9; 
            window.speechSynthesis.speak(utterance);
        } else {
            alert('이 브라우저에서는 음성 듣기 기능을 지원하지 않습니다.');
        }
    }

    function nextQuestion() {
        currentIndex++;
        loadQuestion();
    }

    function showReview() {
        document.getElementById('quiz-area').classList.add('hidden');
        document.getElementById('review-area').classList.remove('hidden');
        document.getElementById('main-title').innerText = "결과 및 오답 노트";

        const reviewList = document.getElementById('review-list');
        reviewList.innerHTML = '';

        if (starredQuestions.length === 0) {
            reviewList.innerHTML = `<div class="review-empty">🎉 어려운 문장이 없습니다! 완벽해요! 🎉</div>`;
        } else {
            starredQuestions.forEach((q, idx) => {
                let meaningHtml = (isPhrasalMode && q.meaning) ? `<div style="font-size: 13px; color: #b45309; background: #fef3c7; padding: 4px 8px; border-radius: 4px; display: inline-block; margin-bottom: 5px;">${q.meaning}</div>` : '';
                
                reviewList.innerHTML += `
                    <div class="review-card">
                        <div style="font-size: 12px; color: #94a3b8; margin-bottom: 5px;">${idx + 1}. 출처: ${q.source}</div>
                        ${meaningHtml}
                        <div class="review-ko">${q.ko}</div>
                        <div class="review-en">${q.en}</div>
                    </div>
                `;
            });
        }
    }

    function resetToHome() {
        document.getElementById('review-area').classList.add('hidden');
        document.getElementById('mode-selection').classList.remove('hidden');
        document.getElementById('main-title').innerText = "🚀 스피드 영어 퀴즈";
    }
</script>
<script src="https://hschoi088-ux.github.io/StudianClass_BasicVerbs100/track.js"></script>
</body>
</html>
