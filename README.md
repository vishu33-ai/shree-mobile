<!DOCTYPE html>
<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SHREE MOBILE - Admin Panel</title>
<style>
  * { box-sizing: border-box; margin: 0; padding: 0; font-family: Arial, sans-serif; }
  body { background: #0f172a; color: white; display: flex; justify-content: center; align-items: center; min-height: 100vh; }

  /* Mobile Container */
  .app {
    width: 100%;
    max-width: 400px;
    height: 100vh;
    max-height: 800px;
    background: #f8fafc;
    border-radius: 20px;
    overflow: hidden;
    position: relative;
    box-shadow: 0 10px 30px rgba(0,0,0,0.5);
  }

  /* Common Header */
  .header {
    background: #0f172a;
    color: #fbbf24;
    padding: 15px;
    text-align: center;
    font-size: 18px;
    font-weight: bold;
    letter-spacing: 1px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .header span { color: white; font-size: 14px; cursor: pointer; }

  /* LOGIN SCREEN */
  #loginScreen {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100%;
    padding: 20px;
    background: #f8fafc;
    color: #0f172a;
  }
  #loginScreen h2 { color: #0f172a; margin-bottom: 5px; font-size: 24px; }
  #loginScreen p { color: #64748b; font-size: 13px; margin-bottom: 30px; }
  .input-group { width: 100%; margin-bottom: 15px; }
  .input-group label { font-size: 12px; color: #0f172a; font-weight: bold; display: block; margin-bottom: 5px; }
  .input-group input {
    width: 100%; padding: 12px; border: 1px solid #cbd5e1; border-radius: 8px; font-size: 14px; outline: none;
  }
  .input-group input:focus { border-color: #fbbf24; }
  .btn-login {
    width: 100%; padding: 12px; background: #0f172a; color: #fbbf24; border: none; border-radius: 8px;
    font-size: 16px; font-weight: bold; margin-top: 10px; cursor: pointer;
  }
  .error { color: red; font-size: 12px; margin-top: 5px; display: none; }

  /* DASHBOARD SCREEN */
  #dashboardScreen {
    display: none;
    height: 100%;
    background: #f8fafc;
    color: #0f172a;
    overflow-y: auto;
  }
  .dash-header {
    background: #0f172a; color: white; padding: 15px; text-align: center;
  }
  .dash-header h2 { color: #fbbf24; font-size: 18px; }
  .dash-header p { font-size: 11px; color: #cbd5e1; }
  .dash-menu { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; padding: 15px; }
  .dash-card {
    background: white; padding: 15px; border-radius: 10px; text-align: center;
    box-shadow: 0 2px 5px rgba(0,0,0,0.05); cursor: pointer;
  }
  .dash-card span { font-size: 24px; display: block; margin-bottom: 5px; }
  .dash-card h3 { font-size: 12px; color: #0f172a; }
  .dash-card p { font-size: 10px; color: #64748b; margin-top: 3px; }
  .logout-btn {
    display: block; width: 90%; margin: 10px auto; padding: 10px;
    background: #ef4444; color: white; border: none; border-radius: 8px; font-weight: bold; cursor: pointer;
  }

  /* WEBSITE SCREEN (App UI) */
  #websiteScreen {
    display: none;
    height: 100%;
    background: #f8fafc;
    overflow-y: auto;
  }
  .hero {
    background: linear-gradient(135deg, #0f172a, #1e293b); color: white; padding: 25px 15px; text-align: center;
  }
  .hero .logo { font-size: 40px; }
  .hero h1 { color: #fbbf24; font-size: 22px; margin: 5px 0; }
  .hero p { font-size: 11px; color: #cbd5e1; }
  .grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; padding: 15px; background: white; }
  .box {
    background: #f1f5f9; border-radius: 12px; padding: 12px 8px; text-align: center;
    text-decoration: none; color: #0f172a; display: flex; flex-direction: column; align-items: center; justify-content: center;
  }
  .box .icon {
    width: 45px; height: 45px; border-radius: 50%; display: flex; align-items: center;
    justify-content: center; font-size: 20px; margin-bottom: 8px; color: white;
  }
  .blue .icon { background: #3b82f6; }
  .orange .icon { background: #f97316; }
  .green .icon { background: #22c55e; }
  .purple .icon { background: #a855f7; }
  .sky .icon { background: #0ea5e9; }
  .pink .icon { background: #ec4899; }
  .box h3 { font-size: 12px; margin-bottom: 2px; }
  .box p { font-size: 9px; color: #64748b; }
  .footer { background: #0f172a; color: white; text-align: center; padding: 12px; font-size: 11px; }
  
  /* Bottom Nav */
  .bottom-nav { display: flex; background: white; border-top: 1px solid #e2e8f0; position: absolute; bottom: 0; width: 100%; justify-content: space-around; padding: 10px 0; }
  .nav-item { text-align: center; color: #64748b; font-size: 10px; cursor: pointer; }
  .nav-item span { display: block; font-size: 18px; margin-bottom: 2px; }
  .nav-item.active { color: #0f172a; font-weight: bold; }

</style>
</head>
<body>

<div class="app">
  
  <!-- ================= LOGIN SCREEN ================= -->
  <div id="loginScreen">
    <h2>Admin Login</h2>
    <p>SHREE MOBILE Dashboard</p>
    
    <div class="input-group">
      <label>User ID</label>
      <input type="text" id="username" placeholder="Enter your ID">
    </div>
    <div class="input-group">
      <label>Password</label>
      <input type="password" id="password" placeholder="Enter Password">
    </div>
    <button class="btn-login" onclick="login()">Login</button>
    <div class="error" id="errorMsg">Galat ID ya Password! (Hint: admin / 1234)</div>
  </div>

  <!-- ================= DASHBOARD SCREEN ================= -->
  <div id="dashboardScreen">
    <div class="dash-header">
      <h2>Welcome, Admin!</h2>
      <p>SHREE MOBILE - Control Panel</p>
    </div>
    
    <div class="dash-menu">
      <div class="dash-card" onclick="showWebsite()">
        <span>🌐</span>
        <h3>View Website</h3>
        <p>Customer View</p>
      </div>
      <div class="dash-card">
        <span>📦</span>
        <h3>Add Product</h3>
        <p>Mobiles & Accessories</p>
      </div>
      <div class="dash-card">
        <span>🔧</span>
        <h3>Repair Orders</h3>
        <p>Pending: 3</p>
      </div>
      <div class="dash-card">
        <span>⚙️</span>
        <h3>Settings</h3>
        <p>Change Details</p>
      </div>
    </div>
    
    <button class="logout-btn" onclick="logout()">Logout</button>
    <div class="bottom-nav">
      <div class="nav-item active" onclick="showDashboard()"><span>🏠</span>Dashboard</div>
      <div class="nav-item"><span>📞</span>Contact</div>
    </div>
  </div>

  <!-- ================= WEBSITE SCREEN (Customer View) ================= -->
  <div id="websiteScreen">
    <div class="hero">
      <div class="logo">📱</div>
      <h1>SHREE MOBILE</h1>
      <p>Mobile All Services | Best Price | Best Service</p>
    </div>

    <div class="grid">
      <a href="tel:6268757970" class="box blue">
        <div class="icon">📱</div>
        <h3>Mobile Phones</h3>
        <p>All Brands & Models</p>
      </a>
      <a href="https://wa.me/916268757970?text=Repair%20karwana%20hai" class="box orange">
        <div class="icon">🔧</div>
        <h3>Repair Services</h3>
        <p>Display • Battery • Software</p>
      </a>
      <a href="https://wa.me/916268757970" class="box purple">
        <div class="icon">📞</div>
        <h3>Contact Us</h3>
        <p>Call / WhatsApp</p>
      </a>
      <a href="https://maps.google.com/?q=Medpar+Bazar+Bilaspur" target="_blank" class="box sky">
        <div class="icon">📍</div>
        <h3>Shop Location</h3>
        <p>Medpar Bazar, Bilaspur</p>
      </a>
      <a href="#" class="box green">
        <div class="icon">🎧</div>
        <h3>Accessories</h3>
        <p>Original & Quality</p>
      </a>
      <a href="#" class="box pink">
        <div class="icon">🛡️</div>
        <h3>Why Choose Us</h3>
        <p>Trusted by Everyone</p>
      </a>
    </div>

    <div class="footer">
      Thank you for choosing SHREE MOBILE 💛<br>
      📞 6268757970 | 📷 vishnukarmakar232
    </div>
    
    <div class="bottom-nav">
      <div class="nav-item" onclick="showDashboard()"><span>🏠</span>Admin</div>
      <div class="nav-item active"><span>🌐</span>Website</div>
    </div>
  </div>

</div>

<script>
  // Demo ID aur Password
  const ADMIN_ID = "admin";
  const ADMIN_PASS = "1234";

  function login() {
    var user = document.getElementById("username").value;
    var pass = document.getElementById("password").value;
    
    if (user === ADMIN_ID && pass === ADMIN_PASS) {
      document.getElementById("loginScreen").style.display = "none";
      document.getElementById("dashboardScreen").style.display = "block";
      document.getElementById("errorMsg").style.display = "none";
    } else {
      document.getElementById("errorMsg").style.display = "block";
    }
  }

  function logout() {
    document.getElementById("dashboardScreen").style.display = "none";
    document.getElementById("websiteScreen").style.display = "none";
    document.getElementById("loginScreen").style.display = "flex";
    document.getElementById("username").value = "";
    document.getElementById("password").value = "";
  }

  function showWebsite() {
    document.getElementById("dashboardScreen").style.display = "none";
    document.getElementById("websiteScreen").style.display = "block";
  }

  function showDashboard() {
    document.getElementById("websiteScreen").style.display = "none";
    document.getElementById("dashboardScreen").style.display = "block";
  }
</script>

</body>
</html>
