# prism-test
一种新型性格测试
---

```html
<!DOCTYPE html>
<html lang="zh">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=yes, viewport-fit=cover">
  <title>PRISM · 棱镜人格测试</title>
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
    }

    body {
      font-family: system-ui, -apple-system, 'Helvetica Neue', 'PingFang SC', 'Microsoft YaHei', sans-serif;
      background: #f5f7fb;
      color: #1e293b;
      padding: 0 0 24px;
      line-height: 1.5;
    }

    .container {
      max-width: 680px;
      margin: 0 auto;
      padding: 20px 16px;
    }

    /* 卡片 */
    .card {
      background: rgba(255,255,255,0.9);
      backdrop-filter: blur(8px);
      -webkit-backdrop-filter: blur(8px);
      border-radius: 32px;
      padding: 28px 20px;
      box-shadow: 0 15px 35px -10px rgba(0,0,0,0.08), 0 2px 8px rgba(0,0,0,0.02);
      border: 1px solid rgba(255,255,255,0.6);
      margin-bottom: 20px;
    }

    h1 {
      font-size: 2.4rem;
      font-weight: 700;
      letter-spacing: -0.02em;
      background: linear-gradient(135deg, #1e293b 0%, #3b5e8b 100%);
      -webkit-background-clip: text;
      background-clip: text;
      color: transparent;
      margin-bottom: 8px;
      line-height: 1.2;
    }

    .sub {
      color: #64748b;
      font-size: 1rem;
      border-left: 4px solid #94a3b8;
      padding-left: 16px;
      margin: 16px 0 8px;
    }

    .badge {
      display: inline-block;
      background: #e9eef4;
      color: #334155;
      padding: 6px 14px;
      border-radius: 40px;
      font-size: 0.9rem;
      font-weight: 500;
      margin-bottom: 16px;
    }

    /* 题目区域 */
    .question-item {
      margin-bottom: 28px;
      border-bottom: 1px solid #eef2f6;
      padding-bottom: 20px;
    }

    .q-title {
      font-weight: 600;
      margin-bottom: 14px;
      font-size: 1.2rem;
      display: flex;
      align-items: baseline;
    }

    .q-num {
      color: #6b7b8f;
      font-weight: 400;
      font-size: 0.9rem;
      margin-right: 10px;
    }

    .options {
      display: flex;
      flex-direction: column;
      gap: 10px;
    }

    .option {
      display: flex;
      align-items: flex-start;
      background: #fafcff;
      padding: 12px 16px;
      border-radius: 24px;
      border: 1.5px solid #e2e8f0;
      transition: all 0.15s;
      cursor: pointer;
    }

    .option.selected {
      border-color: #3b5e8b;
      background: #f0f5ff;
      box-shadow: 0 4px 10px -6px #1e3a5f1a;
    }

    .option input {
      margin-right: 14px;
      accent-color: #3b5e8b;
      width: 18px;
      height: 18px;
      margin-top: 2px;
      flex-shrink: 0;
      cursor: pointer;
    }

    .option label {
      flex: 1;
      cursor: pointer;
      font-size: 1rem;
      color: #1e293b;
    }

    .btn {
      background: #1e293b;
      color: white;
      border: none;
      border-radius: 60px;
      padding: 16px 28px;
      font-size: 1.2rem;
      font-weight: 600;
      width: 100%;
      cursor: pointer;
      box-shadow: 0 8px 20px -8px #1e293b80;
      transition: 0.15s;
      border: 1px solid #ffffff20;
      margin-top: 16px;
    }

    .btn:hover {
      background: #2d3b4f;
      transform: scale(0.98);
    }

    .btn-outline {
      background: transparent;
      color: #1e293b;
      box-shadow: none;
      border: 1.5px solid #cbd5e1;
      margin-top: 12px;
    }

    .result-header {
      text-align: center;
      margin-bottom: 24px;
    }

    .prism-code {
      font-size: 3.8rem;
      font-weight: 800;
      letter-spacing: 6px;
      background: linear-gradient(145deg, #1e2b3c, #3a5f7a);
      -webkit-background-clip: text;
      background-clip: text;
      color: transparent;
      margin: 10px 0 4px;
    }

    .type-name {
      font-size: 1.8rem;
      font-weight: 600;
      color: #0f172a;
    }

    .section-title {
      font-weight: 700;
      font-size: 1.3rem;
      margin: 28px 0 12px;
      border-bottom: 3px solid #dce5ec;
      padding-bottom: 6px;
    }

    .report-text {
      color: #2c3e50;
      margin-bottom: 16px;
    }

    .highlight {
      background: #eef6ff;
      padding: 18px 18px;
      border-radius: 24px;
      font-style: normal;
      border-left: 6px solid #3b5e8b;
      margin: 20px 0;
    }

    .footnote {
      color: #62748c;
      font-size: 0.9rem;
      margin-top: 30px;
      text-align: center;
    }

    .hidden {
      display: none !important;
    }

    .progress {
      font-size: 0.9rem;
      color: #5e7188;
      margin-bottom: 20px;
      background: #e6edf5;
      padding: 6px 16px;
      border-radius: 40px;
      display: inline-block;
    }

    .flex-row {
      display: flex;
      gap: 12px;
    }

    .flex-row .btn {
      width: auto;
      flex: 1;
    }
  </style>
</head>
<body>
<div class="container" id="app">
  <!-- 起始页 / 说明页 -->
  <div id="intro-section">
    <div class="card">
      <h1>PRISM</h1>
      <div style="font-size: 1.2rem; font-weight: 400; margin-bottom: 16px;">棱镜人格测试</div>
      <div class="badge">全新四维 · 32型深度解读</div>
      <p style="margin-bottom: 20px; color: #334155;">基于动机、节奏、认知、能量四维构建。不贴标签，只折射你的独特切面。<br>共30题，约4分钟。</p>
      <p style="background: #f0f5fa; border-radius: 20px; padding: 16px; font-size: 0.95rem;">✅ 非MBTI · 全新字母体系<br>✅ 后缀 -A / -T 精准定位<br>✅ 每型皆有超千字内省报告</p>
      <button class="btn" id="start-btn">开始测试</button>
    </div>
  </div>

  <!-- 测试区 -->
  <div id="test-section" class="hidden">
    <div class="progress" id="progress-indicator">第1-5题 / 共30题</div>
    <div id="questions-container"></div>
    <div class="flex-row">
      <button class="btn btn-outline" id="prev-btn" disabled>← 上一部分</button>
      <button class="btn" id="next-btn">下一部分 →</button>
    </div>
    <button class="btn btn-outline" id="submit-btn" style="display:none;">✨ 查看我的棱镜报告</button>
  </div>

  <!-- 结果区 -->
  <div id="result-section" class="hidden">
    <div class="card">
      <div class="result-header">
        <div style="font-weight: 500; color:#617b9b;">你的PRISM代码</div>
        <div class="prism-code" id="result-code">----</div>
        <div class="type-name" id="result-type-name"></div>
        <div style="margin-top: 6px; color:#54708f;" id="result-sub"></div>
      </div>
      <div id="report-content" class="report-text"></div>
      <button class="btn" id="retake-btn">重新测试</button>
      <div class="footnote">PRISM · 像棱镜一样，看见内在光谱</div>
    </div>
  </div>
</div>

<script>
  (function(){
    "use strict";

    // ---------- 题库定义 ----------
    const questions = [
      // 动力来源 P/F (1-5)
      { text: "开始新的一天时，你更关注：", options: ["今天要完成什么具体任务 (P)", "今天会有什么新鲜体验 (F)", "看情况，都差不多"] },
      { text: "旅行时，你更倾向于：", options: ["提前规划好主要行程和目的地 (P)", "走到哪算哪，享受意外发现 (F)", "有个大概方向，其他随意"] },
      { text: "你更欣赏哪种人：", options: ["目标明确、执行力强的人 (P)", "随遇而安、享受当下的人 (F)", "两者各有各的好"] },
      { text: "面对一项任务，你的动力更多来自：", options: ["完成它、搞定它的成就感 (P)", "做这件事过程中的乐趣 (F)", "两者都有"] },
      { text: "你认为人生的意义更在于：", options: ["达成某些重要的目标或成就 (P)", "经历丰富、感受充分 (F)", "无法简单二选一"] },
      // 反应速度 R/C (6-10)
      { text: "开会讨论时，你通常：", options: ["很快就想发言，边想边说 (R)", "先听大家说完，最后再整理观点 (C)", "看话题而定"] },
      { text: "别人突然问你一个意料之外的问题，你：", options: ["能迅速给出一个还不错的回应 (R)", "会停顿一下，组织好再回答 (C)", "有时快有时慢"] },
      { text: "遇到突发状况时，你：", options: ["先采取行动，边做边调整 (R)", "先停下来想清楚最佳方案 (C)", "看状况的紧急程度"] },
      { text: "你说话的风格更接近：", options: ["语速偏快，想到什么说什么 (R)", "语速平缓，斟酌过再说 (C)", "不太确定"] },
      { text: "学习新东西时，你倾向于：", options: ["先上手试试，在试错中学习 (R)", "先理解原理和框架，再动手 (C)", "看学的是什么"] },
      // 信息偏好 I/D (11-15)
      { text: "读一本书或看一部电影后，你更容易记住：", options: ["整体的感觉、主题和隐喻 (I)", "具体的桥段、细节和台词 (D)", "都差不多"] },
      { text: "听别人讲一件事，你更关注：", options: ["这件事意味着什么、背后是什么 (I)", "这件事具体是怎么发生的、顺序如何 (D)", "两者都关注"] },
      { text: "描述一个朋友时，你更可能说：", options: ["他是一个很有想法/很有温度的人 (I)", "他做了一件什么事/他说了什么话 (D)", "都会说"] },
      { text: "做决策时，你更依赖：", options: ["一种整体的感觉或直觉 (I)", "具体的事实和数据 (D)", "两者结合"] },
      { text: "你更擅长：", options: ["看到事情之间的联系和大局 (I)", "注意到别人忽略的具体细节 (D)", "都还行"] },
      // 决策依据 S/H (16-20)
      { text: "做一个重要决定时，你更看重：", options: ["这样做是否合理、是否符合逻辑 (S)", "这样做是否让我内心舒服、是否符合我的价值观 (H)", "两者都重要"] },
      { text: "当逻辑和人情发生冲突时，你内心更倾向于：", options: ["坚持原则和逻辑 (S)", "照顾到人的感受 (H)", "真的很纠结"] },
      { text: "评价一个方案好坏，你首先看：", options: ["它的效率和可行性 (S)", "它对相关人员的影响 (H)", "都看"] },
      { text: "朋友找你倾诉一个困境，你的第一反应是：", options: ["帮他分析问题、找解决方案 (S)", "先接纳他的情绪、让他感觉被理解 (H)", "都会做"] },
      { text: "你认为自己是：", options: ["偏理性的人 (S)", "偏感性的人 (H)", "理性和感性比较平衡"] },
      // 能量模式 M/S (21-25)
      { text: "连续参加几天社交活动后，你通常感觉：", options: ["虽然累但挺充实的，能量有进有出 (M)", "被掏空了，急需独处回血 (S)", "看活动本身是否喜欢"] },
      { text: "面对一个需要解决的问题，你的本能是：", options: ["找人讨论，在交流中理清思路 (M)", "自己先想清楚，再和别人说 (S)", "看问题类型"] },
      { text: "你更享受：", options: ["在人群中一起完成某件事 (M)", "独自沉浸在自己的世界里完成某件事 (S)", "都喜欢"] },
      { text: "在一个新环境里，你更倾向于：", options: ["主动认识人、建立联系 (M)", "先观察，等别人来认识你或被环境接纳 (S)", "看心情"] },
      { text: "你的能量更接近于：", options: ["一个广播站，向外发射信号 (M)", "一个接收器，向内收集信号 (S)", "不太确定"] },
      // 身份后缀 -A/-T (26-30)
      { text: "对于自己的性格和状态，你通常：", options: ["挺接纳的，我就是我 (-A)", "经常反思，觉得自己还可以更好 (-T)", "有时候接纳，有时候反思"] },
      { text: "做决定后，你：", options: ["很少后悔，选了就走了 (-A)", "常常会想「另一个选项会不会更好」 (-T)", "看事情大小"] },
      { text: "面对别人的评价或批评，你：", options: ["比较稳，不会太影响自我判断 (-A)", "会反复琢磨，即使表面平静 (-T)", "看是谁说的、怎么说的"] },
      { text: "你的情绪状态更像：", options: ["一条比较平稳的河流 (-A)", "有起有伏的波浪 (-T)", "时稳时浪"] },
      { text: "回顾过去，你更可能：", options: ["觉得大部分选择在当时都是合理的 (-A)", "有很多「如果当时……就好了」的瞬间 (-T)", "两者都有"] }
    ];

    // 维度分组
    const dimensions = [
      { name: 'P/F', letterA: 'P', letterB: 'F', start: 0, end: 4 },
      { name: 'R/C', letterA: 'R', letterB: 'C', start: 5, end: 9 },
      { name: 'I/D', letterA: 'I', letterB: 'D', start: 10, end: 14 },
      { name: 'S/H', letterA: 'S', letterB: 'H', start: 15, end: 19 },
      { name: 'M/S', letterA: 'M', letterB: 'S', start: 20, end: 24 }
    ];

    // 后缀维度
    const suffixDim = { name: 'A/T', letterA: 'A', letterB: 'T', start: 25, end: 29 };

    // 状态存储
    let currentAnswers = new Array(30).fill(null); // 0,1,2 对应选项
    let currentPage = 0; // 0: 1-5, 1:6-10, ... 5:26-30
    const questionsPerPage = 5;

    // DOM 元素
    const intro = document.getElementById('intro-section');
    const testSection = document.getElementById('test-section');
    const resultSection = document.getElementById('result-section');
    const questionsDiv = document.getElementById('questions-container');
    const prevBtn = document.getElementById('prev-btn');
    const nextBtn = document.getElementById('next-btn');
    const submitBtn = document.getElementById('submit-btn');
    const progressSpan = document.getElementById('progress-indicator');
    const startBtn = document.getElementById('start-btn');
    const retakeBtn = document.getElementById('retake-btn');

    // 渲染当前页题目
    function renderPage(page) {
      const startIdx = page * questionsPerPage;
      const endIdx = Math.min(startIdx + questionsPerPage, questions.length);
      let html = '';
      for (let i = startIdx; i < endIdx; i++) {
        const q = questions[i];
        const selected = currentAnswers[i];
        html += `<div class="question-item">`;
        html += `<div class="q-title"><span class="q-num">${i+1}/30</span> ${q.text}</div>`;
        html += `<div class="options">`;
        q.options.forEach((opt, optIdx) => {
          const checked = (selected === optIdx) ? 'checked' : '';
          html += `<div class="option ${selected === optIdx ? 'selected' : ''}" data-q="${i}" data-opt="${optIdx}">`;
          html += `<input type="radio" name="q${i}" value="${optIdx}" ${checked} id="q${i}_${optIdx}">`;
          html += `<label for="q${i}_${optIdx}">${opt}</label>`;
          html += `</div>`;
        });
        html += `</div></div>`;
      }
      questionsDiv.innerHTML = html;

      // 绑定点击事件
      document.querySelectorAll('.option').forEach(optDiv => {
        optDiv.addEventListener('click', (e) => {
          const radio = optDiv.querySelector('input[type="radio"]');
          if (radio) {
            radio.checked = true;
            const qIdx = parseInt(optDiv.dataset.q);
            const optIdx = parseInt(optDiv.dataset.opt);
            currentAnswers[qIdx] = optIdx;
            renderPage(currentPage); // 刷新样式
            updateButtons();
          }
        });
      });

      // 更新进度文字
      const s = startIdx+1;
      const e = endIdx;
      progressSpan.innerText = `第${s}-${e}题 / 共30题`;
      updateButtons();
    }

    function updateButtons() {
      const startIdx = currentPage * questionsPerPage;
      const endIdx = Math.min(startIdx + questionsPerPage, questions.length);
      const allAnswered = currentAnswers.slice(startIdx, endIdx).every(a => a !== null);
      
      prevBtn.disabled = (currentPage === 0);
      
      if (currentPage === 5) { // 最后一页
        nextBtn.style.display = 'none';
        submitBtn.style.display = 'block';
        // 检查是否所有题都答了才启用提交
        const allThirty = currentAnswers.every(a => a !== null);
        submitBtn.disabled = !allThirty;
      } else {
        nextBtn.style.display = 'block';
        submitBtn.style.display = 'none';
        nextBtn.disabled = !allAnswered;
      }
    }

    // 计分 & 生成结果
    function calculateResult() {
      const dimResults = [];
      dimensions.forEach(dim => {
        let scoreA = 0, scoreB = 0;
        for (let i = dim.start; i <= dim.end; i++) {
          const ans = currentAnswers[i];
          if (ans === 0) scoreA++;
          else if (ans === 1) scoreB++;
        }
        dimResults.push(scoreA >= scoreB ? dim.letterA : dim.letterB);
      });
      
      // 后缀
      let scoreA = 0, scoreB = 0;
      for (let i = suffixDim.start; i <= suffixDim.end; i++) {
        const ans = currentAnswers[i];
        if (ans === 0) scoreA++;
        else if (ans === 1) scoreB++;
      }
      const suffix = scoreA >= scoreB ? 'A' : 'T';
      
      const code = dimResults.join('-') + '-' + suffix;
      const baseCode = dimResults.join('-');
      return { code, baseCode, suffix, dims: dimResults };
    }

    // ---------- 动态报告生成器 (精准长文) ----------
    function generateReport(result) {
      const dims = result.dims;
      const suffix = result.suffix;
      
      // 维度解读短词
      const dimMap = {
        'P': { name: '目标驱动', desc: '你为清晰的目标和结果而行动，达成里程碑给你注入强能量。' },
        'F': { name: '过程导向', desc: '你更在意体验本身的意义，过程的丰富度比终点更吸引你。' },
        'R': { name: '快速响应', desc: '你的思维敏捷，倾向先行动再修正，在动态中寻找最优解。' },
        'C': { name: '沉稳反应', desc: '你习惯深度处理信息，谋定而后动，沉稳是你的保护色。' },
        'I': { name: '抽象框架', desc: '你天然捕捉本质、隐喻和可能性，对细节容易忽略但大局观极强。' },
        'D': { name: '具体细节', desc: '你关注事实与细节，脚踏实地，相信魔鬼在细节里。' },
        'S': { name: '逻辑系统', desc: '决策时你优先调用原则与合理性，追求前后一致。' },
        'H': { name: '内心感受', desc: '你的选择必须过心里那杆秤，人情与价值观是重要的指南针。' },
        'M': { name: '向外推动', desc: '能量向外流动，喜欢影响环境，在人群中获得滋养。' },
        'S': { name: '向内守护', desc: '能量内敛，需要独处回血，你的内心世界深邃而丰饶。' }
      };
      
      const typeNameMap = {
        'P-R-I-S-M': '推进者', 'P-R-I-H-M': '领航者', 'P-R-D-S-M': '执行者', 'P-R-D-H-M': '督导者',
        'P-C-I-S-M': '架构者', 'P-C-I-H-M': '协调官', 'P-C-D-S-M': '工匠', 'P-C-D-H-M': '守护者',
        'F-R-I-S-M': '灵感者', 'F-R-I-H-M': '氛围组', 'F-R-D-S-M': '体验派', 'F-R-D-H-M': '陪伴者',
        'F-C-I-S-M': '哲思者', 'F-C-I-H-M': '调停者', 'F-C-D-S-M': '收集者', 'F-C-D-H-M': '治愈者',
        // M换成S的内向版
        'P-R-I-S-S': '策划者', 'P-R-I-H-S': '守望者', 'P-R-D-S-S': '匠人', 'P-R-D-H-S': '养护者',
        'P-C-I-S-S': '隐士战略家', 'P-C-I-H-S': '静水流深', 'P-C-D-S-S': '精密匠魂', 'P-C-D-H-S': '暖愈后盾',
        'F-R-I-S-S': '白日梦想家', 'F-R-I-H-S': '温柔观察员', 'F-R-D-S-S': '自在体验官', 'F-R-D-H-S': '情绪树洞',
        'F-C-I-S-S': '内省者', 'F-C-I-H-S': '宁静港湾', 'F-C-D-S-S': '雅致藏家', 'F-C-D-H-S': '疗愈师'
      };
      
      const base = dims.join('-');
      let typeName = typeNameMap[base] || '棱镜旅人';
      if (suffix === 'A') typeName += '·自洽';
      else typeName += '·敏感';
      
      // 拼凑细腻长报告 (根据维度组合动态生成，足够有细节)
      const pDesc = dimMap[dims[0]].desc;
      const rDesc = dimMap[dims[1]].desc;
      const iDesc = dimMap[dims[2]].desc;
      const hDesc = dimMap[dims[3]].desc;
      const mDesc = dimMap[dims[4]].desc;
      const suffixDesc = suffix === 'A' ? '你对自己的状态较为笃定，接纳度高，很少后悔。' : '你常常自我审视，情绪丰富，对内在波动极为敏锐。';
      
      const core = `你是一个${dims[0]==='P'?'目标感清晰':'随遇而安'}、反应${dims[1]==='R'?'敏捷':'沉稳'}、认知偏${dims[2]==='I'?'抽象本质':'具体细节'}、决策时更看重${dims[3]==='S'?'逻辑自洽':'内心和谐'}、能量流向${dims[4]==='M'?'外界人群':'内在世界'}的人。${suffixDesc}`;
      
      // 长文报告 (嵌入具体组合)
      return `
        <div class="section-title">🔮 核心气质</div>
        <p>${core} ${pDesc} ${rDesc} ${iDesc} ${hDesc} ${mDesc}</p>
        <p>你的PRISM代码折射出一种独特的${dims.includes('I')?'深度':'务实'}气质。你习惯${dims[1]==='R'?'在动态中捕捉灵感':'先沉淀再发声'}，${
          dims[4]==='M'?'在人群中你能汲取能量，但你也需要高浓度的精神共鸣。':'独处是你最重要的恢复仪式，外界喧嚣容易让你过载。'
        }</p>
        <div class="highlight">✨ 你的核心天赋：${dims[2]==='I'?'穿透表象的直觉力':'对现实精准的把握'} · ${dims[3]==='H'?'温暖而坚定的共情':'冷静缜密的判断'} · ${dims[0]==='F'?'对过程的沉浸与享受':'强烈的目标达成力'}</div>
        
        <div class="section-title">⚠️ 你大概会遇到的问题</div>
        <ul style="padding-left:20px;">
          <li>${dims[1]==='R'?'容易因为反应过快而忽略细节，事后需要修补。':'可能因为思考过久错过时机，被误解为犹豫不决。'}</li>
          <li>${dims[3]==='H'?'在需要强硬立场时内心拉扯，不忍伤害关系。':'有时显得过于理性，被人误解为缺乏温度。'}</li>
          <li>${dims[4]==='S'?'社交消耗后需要较长的独处恢复期，可能被催促。':'外向能量有时会忽略深度内省，导致浮躁感。'}</li>
          <li>${suffix==='T'?'你容易陷入自我怀疑的循环，对反馈过度敏感。':'你偶尔会因过于自洽而忽略改进信号。'}</li>
          <li>${dims[0]==='P'?'对目标的执着可能带来焦虑，忽略了沿途风景。':'过程导向有时让截止日期变成压力源。'}</li>
        </ul>
        
        <div class="section-title">🧭 你通常是怎么做的</div>
        <p>面对冲突：${dims[1]==='C'?'你会先沉默观察，内心反复推演后再温和表达。' : '你倾向于即时沟通，用语言梳理思路，哪怕有些混乱。'} 在工作中，你擅长${dims[2]==='I'?'搭建框架、提炼方向':'执行细节、优化流程'}，${dims[3]==='H'?'你希望团队氛围和谐，会主动调和。':'你重视效率和原则，对事不对人。'} 关系中，你是${dims[4]==='M'?'主动联结者，乐于分享能量':'慢热但长情，一旦信任便会展露深邃'}。</p>
        
        <div class="section-title">🌱 优势与需要管理的部分</div>
        <p><strong>✨ 天赋：</strong> ${dims[2]==='I'?'洞察本质、联想丰富':'务实可靠、观察入微'}；${dims[3]==='H'?'共情力强、善解人意':'逻辑清晰、公正客观'}；${dims[0]==='F'?'享受过程、灵活开放':'目标专注、坚韧不拔'}。</p>
        <p><strong>🛡️ 需要留意的：</strong> ${dims[1]==='R'?'冲动与虎头蛇尾':'过度思虑与行动迟缓'}；${dims[4]==='S'?'回避人群导致孤独感':'忽视内在需求导致耗竭'}；${suffix==='T'?'精神内耗与完美主义':'偶尔的盲目自信'}</p>
        <p style="margin-top:20px;"><em>“你是独一无二的棱镜，世界的光经过你，便有了更丰富的色彩。”</em></p>
      `;
    }

    function showResult() {
      const result = calculateResult();
      document.getElementById('result-code').innerText = result.code;
      const typeNameSpan = document.getElementById('result-type-name');
      const base = result.dims.join('-');
      const typeNameMap = {
        'P-R-I-S-M': '推进者', 'P-R-I-H-M': '领航者', 'P-R-D-S-M': '执行者', 'P-R-D-H-M': '督导者',
        'F-R-I-S-M': '灵感者', 'F-R-I-H-M': '氛围组', 'F-R-D-S-M': '体验派', 'F-R-D-H-M': '陪伴者',
        'P-C-I-S-M': '架构者', 'P-C-I-H-M': '协调官', 'P-C-D-S-M': '工匠', 'P-C-D-H-M': '守护者',
        'F-C-I-S-M': '哲思者', 'F-C-I-H-M': '调停者', 'F-C-D-S-M': '收集者', 'F-C-D-H-M': '治愈者',
        'P-R-I-S-S': '策划者', 'P-R-I-H-S': '守望者', 'P-R-D-S-S': '匠人', 'P-R-D-H-S': '养护者',
        'P-C-I-S-S': '隐士战略家', 'P-C-I-H-S': '静水流深', 'P-C-D-S-S': '精密匠魂', 'P-C-D-H-S': '暖愈后盾',
        'F-R-I-S-S': '白日梦想家', 'F-R-I-H-S': '温柔观察员', 'F-R-D-S-S': '自在体验官', 'F-R-D-H-S': '情绪树洞',
        'F-C-I-S-S': '内省者', 'F-C-I-H-S': '宁静港湾', 'F-C-D-S-S': '雅致藏家', 'F-C-D-H-S': '疗愈师'
      };
      let tn = typeNameMap[base] || '棱镜旅人';
      tn += (result.suffix === 'A' ? '·自洽' : '·敏感');
      typeNameSpan.innerText = tn;
      document.getElementById('result-sub').innerText = `后缀 ${result.suffix} 型`;
      
      const reportHtml = generateReport(result);
      document.getElementById('report-content').innerHTML = reportHtml;
      
      intro.classList.add('hidden');
      testSection.classList.add('hidden');
      resultSection.classList.remove('hidden');
      window.scrollTo(0,0);
    }

    // 事件绑定
    startBtn.addEventListener('click', ()=>{
      intro.classList.add('hidden');
      testSection.classList.remove('hidden');
      currentPage = 0;
      renderPage(0);
    });

    prevBtn.addEventListener('click', ()=>{
      if (currentPage > 0) {
        currentPage--;
        renderPage(currentPage);
      }
    });

    nextBtn.addEventListener('click', ()=>{
      if (currentPage < 5) {
        currentPage++;
        renderPage(currentPage);
      }
    });

    submitBtn.addEventListener('click', showResult);

    retakeBtn.addEventListener('click', ()=>{
      currentAnswers = new Array(30).fill(null);
      currentPage = 0;
      resultSection.classList.add('hidden');
      intro.classList.remove('hidden');
    });

    // 初始化
  })();
</script>
</body>
</html>
```
