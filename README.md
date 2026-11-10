# my-personal-pages<!DOCTYPE html>
<html lang="zh-TW">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>我的個人 GitHub Page</title>
  <!-- 載入 jQuery CDN -->
  <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
  <style>
    body {
      font-family: "標楷體", "Times New Roman", sans-serif;
      line-height: 1.6;
      max-width: 700px;
      margin: 40px auto;
      padding: 0 20px;
      color: #333;
      background-color: #f9f9f9;
    }
    header, section {
      background: #ffffff;
      padding: 20px;
      margin-bottom: 20px;
      border-radius: 8px;
      border: 1px solid #ddd;
    }
    h1, h2 {
      margin-top: 0;
    }
    .btn {
      padding: 8px 16px;
      font-size: 14px;
      cursor: pointer;
      background-color: #0969da;
      color: white;
      border: none;
      border-radius: 4px;
    }
    .btn:hover {
      background-color: #024c96;
    }
    .toggle-box {
      display: none;
      margin-top: 10px;
      padding: 10px;
      background: #f1f3f5;
      border-left: 4px solid #0969da;
    }
    #ajax-result {
      margin-top: 10px;
      padding: 10px;
      background: #f8f9fa;
      border: 1px dashed #ccc;
    }
  </style>
</head>
<body>

  <header>
    <h1>我的個人主頁</h1>
    <p>這是透過 GitHub Pages 部署的靜態網頁作品</p>
  </header>

  <!-- jQuery 功能一：DOM 動態互動 (收合與展開) -->
  <section>
    <h2>關於我</h2>
    <p>歡迎來到我的個人頁面！本頁面使用 HTML5、CSS 與 jQuery 製作。</p>
    <button id="toggle-btn" class="btn">點擊展開 / 收合詳細介紹 (jQuery 特效)</button>
    <div id="toggle-box" class="toggle-box">
      <p>💡 這裡使用了 jQuery 的 <code>slideToggle()</code> 方法來做出平滑的動畫效果。</p>
    </div>
  </section>

  <!-- jQuery 功能二：AJAX 非同步請求 -->
  <section>
    <h2>即時資料展示 (jQuery AJAX)</h2>
    <p>點擊下方按鈕，透過 jQuery 發送非同步請求取得測試資料：</p>
    <button id="ajax-btn" class="btn">取得資料</button>
    <div id="ajax-result">等待發送請求...</div>
  </section>

  <script>
    $(document).ready(function() {
      // 1. 綁定按鈕點擊事件，切換區塊顯示與隱藏
      $("#toggle-btn").on("click", function() {
        $("#toggle-box").slideToggle("fast");
      });

      // 2. 綁定按鈕點擊事件，使用 AJAX 取得遠端測試 API 資料
      $("#ajax-btn").on("click", function() {
        const $result = $("#ajax-result");
        $result.html("資料載入中...");

        $.ajax({
          url: "https://jsonplaceholder.typicode.com/todos/1",
          type: "GET",
          dataType: "json",
          success: function(data) {
            $result.html(
              "<strong>請求成功！</strong><br>" +
              "項目標題: " + data.title + "<br>" +
              "完成狀態: " + (data.completed ? "已完成" : "未完成")
            );
          },
          error: function() {
            $result.html("<span style='color:red;'>載入失敗，請檢查網路連線。</span>");
          }
        });
      });
    });
  </script>

</body>
</html>
