<!DOCTYPE html>    
<html lang="ar" dir="rtl">    
<head>    
  <meta charset="UTF-8">    
  <meta name="viewport" content="width=device-width, initial-scale=1">    
  <title>saha</title>    
  <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&display=swap" rel="stylesheet">    
  <style>    
    * { font-family: 'Cairo', sans-serif !important; box-sizing: border-box; }    
    body { background-color: #ffffff; margin: 0; padding: 0; }    
    .header { background-color: #f6fefe; display: flex; justify-content: space-between; align-items: center; padding: 15px 20px; }    
    .menu-icon { font-size: 26px; color: #0e639c; cursor: pointer; }    
    .logo { height: 30px; }    
    h1 { color: #2e6fa2; text-align: center; font-weight: 700; font-size: 38px; margin-top: 40px; text-shadow: 2px 2px 5px rgba(0, 0, 0, 0.1); }    
    p { color: #6d7781; text-align: center; font-size: 16px; margin: 10px 20px 30px; text-shadow: 1px 1px 3px rgba(0, 0, 0, 0.05); }    

    .input-field { 
      width: calc(100% - 40px); 
      display: block; 
      padding: 4px 12px;
      font-size: 16px; 
      margin: 10px auto; 
      border: 1px solid #ccc; 
      border-radius: 8px; 
      background-color: white; 
      text-align: right;
      transition: border-color 0.3s ease;
    }

    #leaveCode {
      margin-bottom: 0.8em; /* تباعد بمقدار 80% */
    }

    .input-field:focus {
      border-color: #67b3f5;
      outline: none;
    }

    .center-btn, .back-btn, .new-btn, .back-list-btn { 
      display: block; 
      margin: 15px auto; 
      padding: 6px 10px; 
      background-color: #2e6fa2; 
      color: white; 
      border: none; 
      border-radius: 8px; 
      font-size: 12px; 
      width: 120px; 
      cursor: pointer; 
    }

    .error-tab { background-color: #ffe5e5; color: red; text-align: center; padding: 10px; margin: 10px auto; border-radius: 5px; width: calc(100% - 40px); }    
    .result-box { background-color: #f0f0f0; padding: 20px; margin: 40px auto 20px; border-radius: 8px; width: calc(100% - 40px); text-align: center; }    
    .info-label { font-weight: bold; margin-top: 10px; }    
    .info-data { margin-bottom: 15px; }    
    .footer { background-color: #2e6fa2; color: white; padding: 30px 15px; text-align: center; font-size: 13px; }    
    .footer img { height: 35px; margin: 10px 8px; vertical-align: middle; }    
    .footer-links { margin-top: 15px; }    
    .footer-links span { margin: 0 8px; display: inline-block; }    
    .footer-contact { margin-top: 10px; font-size: 14px; }    
    .footer-contact a { color: white; text-decoration: none; }    
    .footer-icons img { height: 20px; margin: 0 6px; vertical-align: middle; }    
    .popup-menu { position: fixed; top: 40px; left: 0; width: 100%; height: 50vh; background-color: #f8fcff; display: none; flex-direction: column; justify-content: flex-start; align-items: center; padding-top: 30px; z-index: 999; box-shadow: 0 5px 20px rgba(0,0,0,0.1); }  
    .popup-menu .menu-item { font-size: 15px; color: #226699; margin: 15px 0; }  
    .popup-menu .menu-login { background-color: #3c8dc4; color: white; padding: 8px 20px; border-radius: 12px; margin-top: 12px; font-size: 15px; }  
    .popup-menu .menu-login span { margin-right: 8px; }  
    .popup-menu .close-btn { position: absolute; top: 10px; right: 15px; font-size: 24px; color: #333; cursor: pointer; }  
    .new-btn, .back-list-btn { display: none; }  
    .bold { font-weight: bold; color: black; }    
    .normal { font-weight: normal; color: black; }    
    .info-label.bold { margin-bottom: 5px; }    
    .info-label.normal { margin-top: 10px; }    
  </style>    
</head>    
<body>    
    
  <div class="header">    
    <img src="seha_logo.jpg" alt="شعار صحة" class="logo">    
    <div class="menu-icon" id="menuIcon" onclick="toggleMenu()">&#9776;</div>    
  </div>    

  <div class="popup-menu" id="popupMenu">  
    <div class="close-btn" onclick="toggleMenu()">X</div>  
    <div class="menu-item">الخدمات</div>  
    <div class="menu-item">الاستعلامات</div>  
    <div class="menu-item">إنشاء حساب</div>  
    <div class="menu-login"><span>👨‍💼</span>تسجيل الدخول</div>  
  </div>  
    
  <h1>الإجازات المرضية</h1>    
  <p>خدمة الاستعلام عن الإجازات المرضية تتيح لك الاستعلام عن حالة طلبك للإجازة ويمكنك طباعتها عن طريق تطبيق صحتي</p>    

  <input id="leaveCode" type="text" class="input-field" placeholder="رمز الخدمة" maxlength="12">    
  <input id="idNumber" type="text" class="input-field" placeholder="رقم الهوية / الإقامة" maxlength="10" inputmode="numeric">    

  <div id="errorTab" class="error-tab" style="display:none;">خطأ في البيانات</div>    
    
  <button class="center-btn" id="searchBtn" onclick="checkData()">استعلام</button>    
  <button class="back-btn" id="backBtn" onclick="resetForm()">رجوع للاستعلامات</button>    

  <div id="resultBox" class="result-box" style="display:none;">    
    <div class="info-label bold">الاسم</div>    
    <div class="info-data normal">نائف ياسين عبدالعزيز عقلان</div>    
    <div class="info-label bold">تاريخ إصدار تقرير الاجازة</div>    
    <div class="info-data normal">2025-03-12</div>    
    <div class="info-label bold">تبدأ من</div>    
    <div class="info-data normal">2025-03-14</div>    
    <div class="info-label bold">وحتى</div>    
    <div class="info-data normal">2025-06-23</div>    
    <div class="info-label bold">المدة بالأيام</div>    
    <div class="info-data normal">1</div>    
    <div class="info-label bold">اسم الطبيب</div>    
    <div class="info-data normal">امين المساعد</div>    
    <div class="info-label bold">المسمى الوظيفي</div>    
    <div class="info-data normal">طبيب عام</div>    
  </div>    

  <button class="new-btn" id="newSearchBtn" onclick="newSearch()">استعلام جديد</button>    
  <button class="back-list-btn" id="backListBtn" onclick="resetForm()">رجوع للاستعلامات</button>    

  <br><br><br><br><br><br>

  <div class="footer">    
    <img src="https://www.moh.gov.sa/_layouts/15/MOH/Portal/images/logo.png" alt="شعار وزارة الصحة">    
    <img src="https://cdn.sehhty.com/assets/lean-logo-white.png" alt="شعار لين">    
    <div>منصة صحة معتمدة من قبل وزارة الصحة © 2025</div>    
    <div class="footer-links">    
      <span>سياسة الخصوصية وشروط الإستخدام</span> |    
      <span>دليل الإستخدام</span>    
    </div>    
    <div class="footer-contact">    
      <span>920002005</span> |    
      <a href="mailto:support@seha.sa">support@seha.sa</a>    
    </div>    
    <div class="footer-icons">    
      <img src="https://cdn-icons-png.flaticon.com/512/733/733585.png" alt="whatsapp">    
      <img src="https://cdn-icons-png.flaticon.com/512/2111/2111646.png" alt="telegram">    
      <img src="https://cdn-icons-png.flaticon.com/512/1384/1384060.png" alt="youtube">    
    </div>    
  </div>    

  <script>    
    function checkData() {    
      const idNumber = document.getElementById("idNumber").value.trim();    
      const leaveCode = document.getElementById("leaveCode").value.trim();    
      const errorTab = document.getElementById("errorTab");    
      const resultBox = document.getElementById("resultBox");    
      const searchBtn = document.getElementById("searchBtn");    
      const backBtn = document.getElementById("backBtn");    
      const newSearchBtn = document.getElementById("newSearchBtn");    
      const backListBtn = document.getElementById("backListBtn");    

      const idValid = /^[0-9]{10}$/.test(idNumber);    
      const codeValid = /^[A-Za-z]{2}[0-9]{10}$/.test(leaveCode);    

      if (idValid && codeValid) {    
        errorTab.style.display = "none";    
        resultBox.style.display = "block";    
        searchBtn.style.display = "none";    
        backBtn.style.display = "none";    
        newSearchBtn.style.display = "block";    
        backListBtn.style.display = "block";    
      } else {    
        errorTab.style.display = "block";    
        resultBox.style.display = "none";    
      }    
    }    

    function resetForm() {    
      document.getElementById("idNumber").value = "";    
      document.getElementById("leaveCode").value = "";    
      document.getElementById("resultBox").style.display = "none";    
      document.getElementById("errorTab").style.display = "none";    
      document.getElementById("searchBtn").style.display = "block";    
      document.getElementById("backBtn").style.display = "block";    
      document.getElementById("newSearchBtn").style.display = "none";    
      document.getElementById("backListBtn").style.display = "none";    
    }    

    function newSearch() {    
      resetForm();    
    }    

    function toggleMenu() {    
      const menu = document.getElementById("popupMenu");    
      const icon = document.getElementById("menuIcon");    
      if (menu.style.display === "flex") {    
        menu.style.display = "none";    
        icon.innerHTML = "&#9776;";    
      } else {    
        menu.style.display = "flex";    
        icon.innerHTML = "";    
      }    
    }    
  </script>    

</body>    
</html
