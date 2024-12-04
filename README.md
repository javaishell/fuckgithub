<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>App Recommendation System</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
      background-color: #f5f5f5;
    }
    h1 {
      color: #333;
    }
    label, select, button {
      display: block;
      margin: 10px 0;
    }
    .results {
      margin-top: 20px;
    }
    .app {
      background-color: #fff;
      padding: 10px;
      margin-bottom: 10px;
      border-radius: 5px;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }
  </style>
</head>
<body>
  <h1>App Recommendation System</h1>

  <label for="category">카테고리 선택:</label>
  <select id="category">
    <option value="">전체</option>
    <option value="Wellness">웰니스</option>
    <option value="Education">교육</option>
    <option value="Entertainment">엔터테인먼트</option>
    <option value="Business">비즈니스</option>
    <option value="Games">게임</option>
    <option value="Productivity">생산성</option>
  </select>

  <label for="ageGroup">연령대 선택:</label>
  <select id="ageGroup">
    <option value="">전체</option>
    <option value="Teen">청소년</option>
    <option value="Adult">성인</option>
  </select>

  <button onclick="recommendApps()">추천 받기</button>

  <div class="results">
    <h2>추천 앱:</h2>
    <div id="resultsContainer"></div>
  </div>

  <script>
    // 앱 데이터베이스
    const apps = [
      { name: "Calm", category: "Wellness", ageGroup: "All", rating: 4.8 },
      { name: "Duolingo", category: "Education", ageGroup: "All", rating: 4.7 },
      { name: "TikTok", category: "Entertainment", ageGroup: "Teen", rating: 4.5 },
      { name: "LinkedIn", category: "Business", ageGroup: "Adult", rating: 4.3 },
      { name: "Candy Crush", category: "Games", ageGroup: "All", rating: 4.4 },
      { name: "Zoom", category: "Productivity", ageGroup: "Adult", rating: 4.6 }
    ];

    // 앱 추천 함수
    function recommendApps() {
      const category = document.getElementById("category").value;
      const ageGroup = document.getElementById("ageGroup").value;
      const resultsContainer = document.getElementById("resultsContainer");

      // 추천된 앱 필터링
      const recommendedApps = apps.filter(app => {
        const matchesCategory = category ? app.category === category : true;
        const matchesAgeGroup = ageGroup ? app.ageGroup === ageGroup || app.ageGroup === "All" : true;
        return matchesCategory && matchesAgeGroup;
      });

      // 추천 결과 표시
      resultsContainer.innerHTML = "";

      if (recommendedApps.length === 0) {
        resultsContainer.innerHTML = "<p>추천할 앱이 없습니다.</p>";
        return;
      }

      recommendedApps.forEach(app => {
        const appElement = document.createElement("div");
        appElement.className = "app";
        appElement.innerHTML = `<strong>${app.name}</strong><br>카테고리: ${app.category}<br>평점: ${app.rating}`;
        resultsContainer.appendChild(appElement);
      });
    }
  </script>
</body>
</html>
