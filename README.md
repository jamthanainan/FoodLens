
<html lang="en">
 <head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>FoodLens – Daily Health Scanner</title>
  <script src="/_sdk/element_sdk.js"></script>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&amp;display=swap" rel="stylesheet">
  <style>
    body {
      box-sizing: border-box;
    }

    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    html, body {
      width: 100%;
      height: 100%;
    }

    body {
      font-family: 'Inter', sans-serif;
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      color: #2d3748;
      overflow-x: hidden;
    }

    .app-container {
      width: 100%;
      min-height: 100%;
      padding: 2rem;
      display: flex;
      flex-direction: column;
      gap: 2rem;
    }

    .header {
      text-align: center;
      color: white;
      margin-bottom: 1rem;
    }

    .header h1 {
      font-size: 3rem;
      font-weight: 700;
      margin-bottom: 0.5rem;
      text-shadow: 0 2px 10px rgba(0,0,0,0.2);
    }

    .header p {
      font-size: 1.2rem;
      font-weight: 300;
      opacity: 0.95;
    }

    .main-content {
      display: grid;
      grid-template-columns: 1fr 2fr;
      gap: 2rem;
      max-width: 1400px;
      margin: 0 auto;
      width: 100%;
    }

    .input-panel {
      background: white;
      border-radius: 20px;
      padding: 2rem;
      box-shadow: 0 10px 40px rgba(0,0,0,0.15);
      height: fit-content;
    }

    .input-panel h2 {
      font-size: 1.5rem;
      margin-bottom: 1.5rem;
      color: #667eea;
    }

    .input-group {
      margin-bottom: 1.5rem;
    }

    .input-group label {
      display: block;
      margin-bottom: 0.5rem;
      font-weight: 500;
      color: #4a5568;
    }

    .food-input {
      width: 100%;
      min-height: 150px;
      padding: 1rem;
      border: 2px solid #e2e8f0;
      border-radius: 12px;
      font-family: 'Inter', sans-serif;
      font-size: 1rem;
      resize: vertical;
      transition: border-color 0.3s;
    }

    .food-input:focus {
      outline: none;
      border-color: #667eea;
    }

    .activity-select {
      width: 100%;
      padding: 0.875rem 1rem;
      border: 2px solid #e2e8f0;
      border-radius: 12px;
      font-family: 'Inter', sans-serif;
      font-size: 1rem;
      cursor: pointer;
      transition: border-color 0.3s;
      background: white;
    }

    .activity-select:focus {
      outline: none;
      border-color: #667eea;
    }

    .analyze-btn {
      width: 100%;
      padding: 1rem;
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      color: white;
      border: none;
      border-radius: 12px;
      font-size: 1.1rem;
      font-weight: 600;
      cursor: pointer;
      transition: transform 0.2s, box-shadow 0.2s;
      box-shadow: 0 4px 15px rgba(102, 126, 234, 0.4);
    }

    .analyze-btn:hover {
      transform: translateY(-2px);
      box-shadow: 0 6px 20px rgba(102, 126, 234, 0.5);
    }

    .analyze-btn:active {
      transform: translateY(0);
    }

    .dashboard-panel {
      display: flex;
      flex-direction: column;
      gap: 1.5rem;
    }

    .score-card {
      background: white;
      border-radius: 20px;
      padding: 2.5rem;
      box-shadow: 0 10px 40px rgba(0,0,0,0.15);
      text-align: center;
    }

    .score-card h2 {
      font-size: 1.3rem;
      margin-bottom: 2rem;
      color: #667eea;
    }

    .gauge-container {
      position: relative;
      width: 200px;
      height: 200px;
      margin: 0 auto 1.5rem;
    }

    .gauge-bg {
      width: 100%;
      height: 100%;
      border-radius: 50%;
      background: #f7fafc;
      position: relative;
      box-shadow: inset 0 2px 10px rgba(0,0,0,0.1);
    }

    .gauge-fill {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      border-radius: 50%;
      background: conic-gradient(from 0deg, #48bb78 0%, #48bb78 0%, #f7fafc 0%);
      transition: background 0.8s ease;
    }

    .gauge-center {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 160px;
      height: 160px;
      background: white;
      border-radius: 50%;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      box-shadow: 0 4px 15px rgba(0,0,0,0.1);
    }

    .score-value {
      font-size: 3rem;
      font-weight: 700;
      color: #48bb78;
      line-height: 1;
    }

    .score-label {
      font-size: 0.875rem;
      color: #718096;
      margin-top: 0.5rem;
    }

    .personality-badge {
      display: inline-block;
      padding: 0.75rem 1.5rem;
      background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
      color: white;
      border-radius: 50px;
      font-size: 1.1rem;
      font-weight: 600;
      margin-bottom: 1rem;
    }

    .personality-message {
      color: #4a5568;
      font-size: 1rem;
    }

    .avatar-display {
      font-size: 3rem;
      margin: 1rem 0;
    }

    .nutrients-grid {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 1rem;
    }

    .nutrient-card {
      background: white;
      border-radius: 16px;
      padding: 1.5rem;
      box-shadow: 0 4px 15px rgba(0,0,0,0.1);
    }

    .nutrient-card h3 {
      font-size: 1rem;
      color: #4a5568;
      margin-bottom: 1rem;
      font-weight: 600;
    }

    .nutrient-bar {
      width: 100%;
      height: 8px;
      background: #f7fafc;
      border-radius: 10px;
      overflow: hidden;
      margin-bottom: 0.5rem;
    }

    .nutrient-fill {
      height: 100%;
      border-radius: 10px;
      transition: width 0.6s ease;
    }

    .nutrient-label {
      font-size: 0.875rem;
      color: #718096;
      font-weight: 500;
    }

    .tips-card {
      background: white;
      border-radius: 20px;
      padding: 2rem;
      box-shadow: 0 10px 40px rgba(0,0,0,0.15);
    }

    .tips-card h2 {
      font-size: 1.3rem;
      margin-bottom: 1.5rem;
      color: #667eea;
    }

    .tip-item {
      display: flex;
      align-items: flex-start;
      margin-bottom: 1rem;
      padding: 1rem;
      background: #f7fafc;
      border-radius: 12px;
      border-left: 4px solid #667eea;
    }

    .tip-icon {
      font-size: 1.5rem;
      margin-right: 1rem;
      flex-shrink: 0;
    }

    .tip-text {
      color: #4a5568;
      line-height: 1.6;
    }

    .trend-card {
      background: white;
      border-radius: 20px;
      padding: 2rem;
      box-shadow: 0 10px 40px rgba(0,0,0,0.15);
    }

    .trend-card h2 {
      font-size: 1.3rem;
      margin-bottom: 1.5rem;
      color: #667eea;
    }

    .trend-disclaimer {
      font-size: 0.875rem;
      color: #718096;
      margin-bottom: 1.5rem;
      font-style: italic;
    }

    .chart-container {
      display: flex;
      align-items: flex-end;
      justify-content: space-around;
      height: 150px;
      padding: 1rem;
      background: #f7fafc;
      border-radius: 12px;
      gap: 0.5rem;
    }

    .chart-bar {
      flex: 1;
      background: linear-gradient(to top, #667eea, #764ba2);
      border-radius: 8px 8px 0 0;
      position: relative;
      transition: height 0.6s ease;
      min-width: 30px;
    }

    .chart-label {
      position: absolute;
      bottom: -25px;
      left: 50%;
      transform: translateX(-50%);
      font-size: 0.75rem;
      color: #718096;
      white-space: nowrap;
    }

    .hidden {
      display: none;
    }

    @media (max-width: 1024px) {
      .main-content {
        grid-template-columns: 1fr;
      }

      .header h1 {
        font-size: 2.5rem;
      }

      .nutrients-grid {
        grid-template-columns: 1fr;
      }
    }

    @media (max-width: 640px) {
      .app-container {
        padding: 1rem;
      }

      .header h1 {
        font-size: 2rem;
      }

      .header p {
        font-size: 1rem;
      }

      .input-panel, .score-card, .tips-card, .trend-card {
        padding: 1.5rem;
      }
    }
  </style>
  <style>@view-transition { navigation: auto; }</style>
  <script src="/_sdk/data_sdk.js" type="text/javascript"></script>
  <script src="https://cdn.tailwindcss.com" type="text/javascript"></script>
 </head>
 <body>
  <div class="app-container">
   <header class="header">
    <h1 id="app-title">FoodLens</h1>
    <p id="app-tagline">Your Daily Health Scanner</p>
   </header>
   <div class="main-content"><!-- Input Panel -->
    <div class="input-panel">
     <h2 id="input-label">What did you eat today?</h2>
     <div class="input-group"><label for="food-input">List your meals and snacks:</label> <textarea id="food-input" class="food-input" placeholder="Example: breakfast - oatmeal with berries, lunch - grilled chicken salad, snack - apple, dinner - salmon with vegetables"></textarea>
     </div>
     <div class="input-group"><label for="activity-level" id="activity-label">Activity Level:</label> <select id="activity-level" class="activity-select"> <option value="low">Low (Mostly sitting)</option> <option value="medium" selected>Medium (Some walking)</option> <option value="high">High (Very active)</option> </select>
     </div><button class="analyze-btn" id="analyze-button">Analyze my day</button>
    </div><!-- Dashboard Panel -->
    <div class="dashboard-panel"><!-- Score Card -->
     <div class="score-card" id="score-card">
      <h2 id="score-title">Daily Health Score</h2>
      <div class="gauge-container">
       <div class="gauge-bg"></div>
       <div class="gauge-fill" id="gauge-fill"></div>
       <div class="gauge-center">
        <div class="score-value" id="score-value">
         --
        </div>
        <div class="score-label">
         out of 100
        </div>
       </div>
      </div>
      <div id="personality-display"></div>
      <div class="avatar-display" id="avatar-display"></div>
     </div><!-- Nutrients Grid -->
     <div class="nutrients-grid" id="nutrients-grid">
      <div class="nutrient-card">
       <h3 id="nutrients-title-calories">Calories</h3>
       <div class="nutrient-bar">
        <div class="nutrient-fill" id="calories-fill" style="width: 0%; background: #f6ad55;"></div>
       </div>
       <div class="nutrient-label" id="calories-label">
        --
       </div>
      </div>
      <div class="nutrient-card">
       <h3 id="nutrients-title-sugar">Sugar</h3>
       <div class="nutrient-bar">
        <div class="nutrient-fill" id="sugar-fill" style="width: 0%; background: #fc8181;"></div>
       </div>
       <div class="nutrient-label" id="sugar-label">
        --
       </div>
      </div>
      <div class="nutrient-card">
       <h3 id="nutrients-title-fat">Fat</h3>
       <div class="nutrient-bar">
        <div class="nutrient-fill" id="fat-fill" style="width: 0%; background: #f6ad55;"></div>
       </div>
       <div class="nutrient-label" id="fat-label">
        --
       </div>
      </div>
      <div class="nutrient-card">
       <h3 id="nutrients-title-fiber">Fiber</h3>
       <div class="nutrient-bar">
        <div class="nutrient-fill" id="fiber-fill" style="width: 0%; background: #48bb78;"></div>
       </div>
       <div class="nutrient-label" id="fiber-label">
        --
       </div>
      </div>
     </div><!-- Tips Card -->
     <div class="tips-card" id="tips-card">
      <h2 id="tips-title">Your Health Tips</h2>
      <div id="tips-container"></div>
     </div><!-- Trend Card -->
     <div class="trend-card">
      <h2 id="trend-title">7-Day Health Trend</h2>
      <div class="trend-disclaimer">
       Sample data for visualization
      </div>
      <div class="chart-container" id="chart-container"></div>
     </div>
    </div>
   </div>
  </div>
  <script>
    // Default configuration
    const defaultConfig = {
      app_title: "FoodLens",
      app_tagline: "Your Daily Health Scanner",
      input_label: "What did you eat today?",
      activity_label: "Activity Level:",
      analyze_button: "Analyze my day",
      score_title: "Daily Health Score",
      nutrients_title: "Nutrients",
      tips_title: "Your Health Tips",
      trend_title: "7-Day Health Trend",
      primary_color: "#667eea",
      secondary_color: "#764ba2",
      success_color: "#48bb78",
      warning_color: "#f6ad55",
      danger_color: "#fc8181",
      font_family: "Inter",
      font_size: 16
    };

    // Initialize Element SDK
    if (window.elementSdk) {
      window.elementSdk.init({
        defaultConfig: defaultConfig,
        onConfigChange: async (config) => {
          const baseSize = config.font_size || defaultConfig.font_size;
          const customFont = config.font_family || defaultConfig.font_family;
          const baseFontStack = 'sans-serif';
          const fontFamily = `${customFont}, ${baseFontStack}`;

          // Update text content
          document.getElementById('app-title').textContent = config.app_title || defaultConfig.app_title;
          document.getElementById('app-tagline').textContent = config.app_tagline || defaultConfig.app_tagline;
          document.getElementById('input-label').textContent = config.input_label || defaultConfig.input_label;
          document.getElementById('activity-label').textContent = config.activity_label || defaultConfig.activity_label;
          document.getElementById('analyze-button').textContent = config.analyze_button || defaultConfig.analyze_button;
          document.getElementById('score-title').textContent = config.score_title || defaultConfig.score_title;
          document.getElementById('tips-title').textContent = config.tips_title || defaultConfig.tips_title;
          document.getElementById('trend-title').textContent = config.trend_title || defaultConfig.trend_title;

          // Apply colors
          const primaryColor = config.primary_color || defaultConfig.primary_color;
          const secondaryColor = config.secondary_color || defaultConfig.secondary_color;
          const successColor = config.success_color || defaultConfig.success_color;
          const warningColor = config.warning_color || defaultConfig.warning_color;
          const dangerColor = config.danger_color || defaultConfig.danger_color;

          document.body.style.background = `linear-gradient(135deg, ${primaryColor} 0%, ${secondaryColor} 100%)`;

          const analyzeBtn = document.querySelector('.analyze-btn');
          analyzeBtn.style.background = `linear-gradient(135deg, ${primaryColor} 0%, ${secondaryColor} 100%)`;

          document.querySelectorAll('.input-panel h2, .score-card h2, .tips-card h2, .trend-card h2').forEach(h2 => {
            h2.style.color = primaryColor;
          });

          const chartBars = document.querySelectorAll('.chart-bar');
          chartBars.forEach(bar => {
            bar.style.background = `linear-gradient(to top, ${primaryColor}, ${secondaryColor})`;
          });

          // Apply font
          document.body.style.fontFamily = fontFamily;

          // Apply font sizes
          document.querySelector('.header h1').style.fontSize = `${baseSize * 1.875}px`;
          document.querySelector('.header p').style.fontSize = `${baseSize * 1.125}px`;
          document.querySelectorAll('.input-panel h2, .score-card h2, .tips-card h2, .trend-card h2').forEach(h2 => {
            h2.style.fontSize = `${baseSize * 1.3}px`;
          });
          document.querySelectorAll('.food-input, .activity-select, .analyze-btn').forEach(el => {
            el.style.fontSize = `${baseSize}px`;
          });
        },
        mapToCapabilities: (config) => ({
          recolorables: [
            {
              get: () => config.primary_color || defaultConfig.primary_color,
              set: (value) => {
                if (window.elementSdk && window.elementSdk.config) {
                  window.elementSdk.config.primary_color = value;
                  window.elementSdk.setConfig({ primary_color: value });
                }
              }
            },
            {
              get: () => config.secondary_color || defaultConfig.secondary_color,
              set: (value) => {
                if (window.elementSdk && window.elementSdk.config) {
                  window.elementSdk.config.secondary_color = value;
                  window.elementSdk.setConfig({ secondary_color: value });
                }
              }
            },
            {
              get: () => config.success_color || defaultConfig.success_color,
              set: (value) => {
                if (window.elementSdk && window.elementSdk.config) {
                  window.elementSdk.config.success_color = value;
                  window.elementSdk.setConfig({ success_color: value });
                }
              }
            },
            {
              get: () => config.warning_color || defaultConfig.warning_color,
              set: (value) => {
                if (window.elementSdk && window.elementSdk.config) {
                  window.elementSdk.config.warning_color = value;
                  window.elementSdk.setConfig({ warning_color: value });
                }
              }
            },
            {
              get: () => config.danger_color || defaultConfig.danger_color,
              set: (value) => {
                if (window.elementSdk && window.elementSdk.config) {
                  window.elementSdk.config.danger_color = value;
                  window.elementSdk.setConfig({ danger_color: value });
                }
              }
            }
          ],
          borderables: [],
          fontEditable: {
            get: () => config.font_family || defaultConfig.font_family,
            set: (value) => {
              if (window.elementSdk && window.elementSdk.config) {
                window.elementSdk.config.font_family = value;
                window.elementSdk.setConfig({ font_family: value });
              }
            }
          },
          fontSizeable: {
            get: () => config.font_size || defaultConfig.font_size,
            set: (value) => {
              if (window.elementSdk && window.elementSdk.config) {
                window.elementSdk.config.font_size = value;
                window.elementSdk.setConfig({ font_size: value });
              }
            }
          }
        }),
        mapToEditPanelValues: (config) => new Map([
          ["app_title", config.app_title || defaultConfig.app_title],
          ["app_tagline", config.app_tagline || defaultConfig.app_tagline],
          ["input_label", config.input_label || defaultConfig.input_label],
          ["activity_label", config.activity_label || defaultConfig.activity_label],
          ["analyze_button", config.analyze_button || defaultConfig.analyze_button],
          ["score_title", config.score_title || defaultConfig.score_title],
          ["nutrients_title", config.nutrients_title || defaultConfig.nutrients_title],
          ["tips_title", config.tips_title || defaultConfig.tips_title],
          ["trend_title", config.trend_title || defaultConfig.trend_title]
        ])
      });
    }

    // Keyword mapping for food analysis
    const unhealthyKeywords = [
      'fried', 'soda', 'dessert', 'sweet', 'butter', 'cake', 'cookie', 
      'candy', 'chocolate', 'ice cream', 'pizza', 'burger', 'fries',
      'milk tea', 'bubble tea', 'soft drink', 'donut', 'pastry', 'chips'
    ];

    const healthyKeywords = [
      'salad', 'grilled', 'boiled', 'vegetable', 'fruit', 'water',
      'steamed', 'baked', 'quinoa', 'spinach', 'broccoli', 'apple',
      'orange', 'berries', 'oatmeal', 'salmon', 'chicken breast', 'tofu'
    ];

    const highSugarKeywords = [
      'milk tea', 'bubble tea', 'soft drink', 'soda', 'dessert', 'sweet',
      'candy', 'cake', 'cookie', 'ice cream', 'donut', 'pastry'
    ];

    const highFatKeywords = [
      'fried', 'butter', 'pizza', 'burger', 'fries', 'cheese', 
      'bacon', 'sausage', 'cream'
    ];

    const fiberKeywords = [
      'salad', 'vegetable', 'fruit', 'oatmeal', 'quinoa', 'beans',
      'lentils', 'broccoli', 'spinach', 'apple', 'berries', 'whole grain'
    ];

    /**
     * Main analysis function
     * Processes user input and calculates health metrics
     */
    function analyzeFoodInput() {
      const foodInput = document.getElementById('food-input').value.toLowerCase();
      const activityLevel = document.getElementById('activity-level').value;

      if (!foodInput.trim()) {
        showInlineMessage('Please enter what you ate today!');
        return;
      }

      // Count keyword occurrences
      const unhealthyCount = countKeywords(foodInput, unhealthyKeywords);
      const healthyCount = countKeywords(foodInput, healthyKeywords);
      const sugarCount = countKeywords(foodInput, highSugarKeywords);
      const fatCount = countKeywords(foodInput, highFatKeywords);
      const fiberCount = countKeywords(foodInput, fiberKeywords);

      // Calculate nutrient levels (0-100)
      const caloriesLevel = Math.min(100, (unhealthyCount * 15 + 40));
      const sugarLevel = Math.min(100, (sugarCount * 20 + 20));
      const fatLevel = Math.min(100, (fatCount * 18 + 25));
      const fiberLevel = Math.min(100, (fiberCount * 25 + 10));

      // Calculate overall health score
      const score = calculateScore(healthyCount, unhealthyCount, sugarLevel, fatLevel, fiberLevel, activityLevel);

      // Update dashboard
      updateDashboard(score, caloriesLevel, sugarLevel, fatLevel, fiberLevel);
    }

    /**
     * Count how many keywords appear in the text
     */
    function countKeywords(text, keywords) {
      let count = 0;
      keywords.forEach(keyword => {
        if (text.includes(keyword)) {
          count++;
        }
      });
      return count;
    }

    /**
     * Calculate health score using nutrient levels
     * Formula: Higher healthy items and fiber boost score, high sugar/fat reduce it
     */
    function calculateScore(healthyCount, unhealthyCount, sugar, fat, fiber, activity) {
      let baseScore = 50;

      // Add points for healthy choices
      baseScore += healthyCount * 8;
      baseScore += fiber * 0.3;

      // Subtract points for unhealthy choices
      baseScore -= unhealthyCount * 10;
      baseScore -= sugar * 0.4;
      baseScore -= fat * 0.35;

      // Activity level bonus
      if (activity === 'high') baseScore += 10;
      if (activity === 'low') baseScore -= 5;

      // Clamp between 0-100
      return Math.max(0, Math.min(100, Math.round(baseScore)));
    }

    /**
     * Update the dashboard with calculated values
     */
    function updateDashboard(score, calories, sugar, fat, fiber) {
      // Update score gauge
      updateScoreGauge(score);

      // Update nutrient bars
      updateNutrientBar('calories', calories, '#f6ad55');
      updateNutrientBar('sugar', sugar, '#fc8181');
      updateNutrientBar('fat', fat, '#f6ad55');
      updateNutrientBar('fiber', fiber, '#48bb78');

      // Update personality
      updatePersonality(score, sugar, fat, fiber);

      // Update tips
      updateTips(score, sugar, fat, fiber);

      // Show cards
      document.getElementById('tips-card').classList.remove('hidden');
    }

    /**
     * Update the circular score gauge
     */
    function updateScoreGauge(score) {
      const scoreValue = document.getElementById('score-value');
      const gaugeFill = document.getElementById('gauge-fill');

      scoreValue.textContent = score;

      // Color based on score
      let color = '#48bb78'; // Green
      if (score < 50) {
        color = '#fc8181'; // Red
        scoreValue.style.color = '#fc8181';
      } else if (score < 75) {
        color = '#f6ad55'; // Orange
        scoreValue.style.color = '#f6ad55';
      } else {
        scoreValue.style.color = '#48bb78';
      }

      // Update gauge fill (conic gradient)
      const percentage = score;
      gaugeFill.style.background = `conic-gradient(from 0deg, ${color} 0%, ${color} ${percentage}%, #f7fafc ${percentage}%)`;
    }

    /**
     * Update individual nutrient bar
     */
    function updateNutrientBar(nutrientId, level, color) {
      const fill = document.getElementById(`${nutrientId}-fill`);
      const label = document.getElementById(`${nutrientId}-label`);

      fill.style.width = `${level}%`;
      fill.style.background = color;

      // Determine label text
      let labelText = 'Low';
      if (level > 66) labelText = 'High';
      else if (level > 33) labelText = 'Medium';

      label.textContent = labelText;
    }

    /**
     * Determine and display health personality
     */
    function updatePersonality(score, sugar, fat, fiber) {
      const personalityDisplay = document.getElementById('personality-display');
      const avatarDisplay = document.getElementById('avatar-display');

      let personality = '';
      let message = '';
      let avatar = '';

      if (sugar > 70) {
        personality = 'Sugar Overload 😵';
        message = 'Too much sugar detected. Your energy might spike and crash!';
        avatar = '🥀';
      } else if (fiber > 60) {
        personality = 'Fiber Hero 🥦';
        message = 'Great job! Your digestive system is happy!';
        avatar = '🌳';
      } else if (score >= 75) {
        personality = 'Balanced Explorer 😌';
        message = 'Excellent balance! You\'re on the right track!';
        avatar = '🌳';
      } else if (fat > 70) {
        personality = 'Heavy Fuel Day 🍔';
        message = 'High fat detected. Consider lighter options tomorrow!';
        avatar = '🥀';
      } else if (score < 50) {
        personality = 'Needs Attention 😟';
        message = 'Your body needs more nutrients. Let\'s improve!';
        avatar = '🥀';
      } else {
        personality = 'Getting There 🌱';
        message = 'You\'re making progress. Keep it up!';
        avatar = '🌱';
      }

      personalityDisplay.innerHTML = `
        <div class="personality-badge">${personality}</div>
        <p class="personality-message">${message}</p>
      `;

      avatarDisplay.textContent = avatar;

      // Update avatar message
      if (score < 50) {
        avatarDisplay.title = 'Your health plant needs care';
      } else if (score < 75) {
        avatarDisplay.title = 'Your health plant is growing';
      } else {
        avatarDisplay.title = 'Your health plant is thriving';
      }
    }

    /**
     * Generate actionable tips based on analysis
     */
    function updateTips(score, sugar, fat, fiber) {
      const tipsContainer = document.getElementById('tips-container');
      const tips = [];

      if (sugar > 60) {
        tips.push({ icon: '🍬', text: 'Reduce sugary drinks and desserts. Try herbal tea or infused water instead.' });
      }

      if (fat > 60) {
        tips.push({ icon: '🥑', text: 'Choose grilled or baked options instead of fried. Use healthier fats like olive oil.' });
      }

      if (fiber < 40) {
        tips.push({ icon: '🥗', text: 'Add more vegetables, fruits, and whole grains to boost your fiber intake.' });
      }

      if (score < 50) {
        tips.push({ icon: '💧', text: 'Stay hydrated! Drink at least 8 glasses of water throughout the day.' });
      }

      if (score >= 75) {
        tips.push({ icon: '✨', text: 'Excellent work! Maintain this balance and stay consistent.' });
      } else {
        tips.push({ icon: '🎯', text: 'Plan your meals ahead to make healthier choices easier.' });
      }

      // Always show portion control tip
      tips.push({ icon: '🍽️', text: 'Watch your portion sizes. Even healthy foods should be eaten in moderation.' });

      // Render tips
      tipsContainer.innerHTML = tips.map(tip => `
        <div class="tip-item">
          <div class="tip-icon">${tip.icon}</div>
          <div class="tip-text">${tip.text}</div>
        </div>
      `).join('');
    }

    /**
     * Show inline message instead of alert
     */
    function showInlineMessage(message) {
      const foodInput = document.getElementById('food-input');
      foodInput.placeholder = message;
      foodInput.style.borderColor = '#fc8181';
      setTimeout(() => {
        foodInput.placeholder = 'Example: breakfast - oatmeal with berries, lunch - grilled chicken salad, snack - apple, dinner - salmon with vegetables';
        foodInput.style.borderColor = '#e2e8f0';
      }, 2000);
    }

    /**
     * Initialize 7-day trend chart with sample data
     */
    function initTrendChart() {
      const chartContainer = document.getElementById('chart-container');
      const trendData = [65, 72, 80, 60, 78, 85, 70];
      const days = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'];

      chartContainer.innerHTML = trendData.map((value, index) => {
        const height = (value / 100) * 100; // Convert to percentage
        return `
          <div class="chart-bar" style="height: ${height}%">
            <div class="chart-label">${days[index]}</div>
          </div>
        `;
      }).join('');
    }

    // Event listener for analyze button
    document.getElementById('analyze-button').addEventListener('click', analyzeFoodInput);

    // Initialize trend chart on load
    initTrendChart();
  </script>
 <script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'9a6079ed267fce7a',t:'MTc2NDQwMjIyOS4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
