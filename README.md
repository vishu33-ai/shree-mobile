<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Shree Mobile - Home Repair Service</title>
    <style>
        /* CSS Styling */
        * { box-sizing: border-box; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; }
        body { background: #1a1a1a; color: white; margin: 0; padding: 20px; text-align: center; }
        .hidden { display: none !important; }
        .card { background: #2a2a2a; padding: 25px; border-radius: 12px; max-width: 450px; margin: auto; box-shadow: 0 4px 15px rgba(0,0,0,0.6); }
        h1 { color: #FFD700; margin-bottom: 5px; font-size: 28px; }
        h3 { margin-top: 0; color: #ddd; font-size: 16px; }
        p { color: #bbb; font-size: 14px; }
        .btn { display: inline-block; padding: 14px 20px; margin: 10px 0; border-radius: 8px; text-decoration: none; font-weight: bold; cursor: pointer; border: none; width: 100%; font-size: 16px; transition: 0.3s; }
        .btn-wa { background: #25D366; color: white; }
        .btn-wa:hover { background: #1ebe5d; }
        .btn-gold { background: #FFD700; color: black; }
        .btn-gold:hover { background: #e6c200; }
        .btn-red { background: #e74c3c; color: white; }
        .btn-outline { background: transparent; color: #888; border: 1px solid #555; font-size: 12px; width: auto; padding: 8px 15px; }
        input { width: 100%; padding: 12px; margin: 8px 0; border-radius: 6px; border: 1px solid #555; background: #333; color: white; font-size: 14px; }
        table { width: 100%; border-collapse: collapse; margin-top: 15px; font-size: 13px; }
        th, td { border: 1px solid #555; padding: 10px; text-align: left; }
        th { background: #FFD700; color: black; }
        .services { text-align: left; display: inline-block; margin: 15px auto; padding-left: 20px; color: #ccc; }
        .services li { margin-bottom: 6px; }
        .error { color: #e74c3c; font-size: 13px; margin-top: 10px; }
        .admin-link { color: #666; font-size: 11px; margin-top: 20px; display: block; cursor: pointer; text-decoration: underline; }
    </style>
</head>
<body>

    <!-- ================= CUSTOMER VIEW ================= -->
    <div id="view-customer" class="card">
        <h1>SHREE MOBILE</h1>
        <h3>Ab Mobile Kharab Ho Toh Chinta Nahi... Hum Hain Na!</h3>
        <p>Home Repairing Service Aapke Ghar Tak (25 KM Area)</p>
        <p>📍 Medpar Bazar, Bilaspur (C.G.)</p>
        
        <ul class="services">
            <li>📱 Display Change</li>
            <li>🔋 Battery Change</li>
            <li>🔌 Charging Problem</li>
            <li>📷 Camera Repair</li>
            <li>⚙️ Software Problem</li>
            <li>💧 Water Damage</li>
            <li>🔊 Speaker Repair</li>
            <li>✅ All Mobile Brands</li>
        </ul>

        <a href="https://wa.me/918982298822?text=Bhaiya,%20mujhe%20mobile%20repair%20ke%20liye%20doorstep%20service%20chahiye." class="btn btn-wa">📞 WhatsApp Par Book Karein</a>
        
        <!-- Admin Login Link -->
        <span class="admin-link" onclick="showAdminLogin()">🔒 Admin Login</span>
    </div>

    <!-- ================= ADMIN LOGIN VIEW ================= -->
    <div id="view-admin-login" class="card hidden">
        <h2 style="color: #FFD700;">Admin Login</h2>
        <p>Kripya apni ID aur Password daalein</p>
        
        <input type="text" id="adminUser" placeholder="Username (ID)">
        <input type="password" id="adminPass" placeholder="Password">
        
        <button class="btn btn-gold" onclick="checkLogin()">Login Karein</button>
        <button class="btn btn-outline" onclick="goBack()">⬅ Wapas Jayein</button>
        
        <p id="errorMsg" class="error"></p>
    </div>

    <!-- ================= ADMIN DASHBOARD VIEW ================= -->
    <div id="view-admin-dash" class="card hidden">
        <h2 style="color: #FFD700;">Welcome Admin! 👋</h2>
        <p>Yahan aapki saari bookings ki list hai:</p>
        
        <table>
            <tr>
                <th>Customer</th>
                <th>Model</th>
                <th>Problem</th>
            </tr>
            <tr>
                <td>Rahul (Demo)</td>
                <td>iPhone 13</td>
                <td>Screen Change</td>
            </tr>
            <tr>
                <td>Amit (Demo)</td>
                <td>Redmi Note 10</td>
                <td>Battery Change</td>
            </tr>
            <tr>
                <td>Vishu (Demo)</td>
                <td>Samsung S21</td>
                <td>Charging Port</td>
            </tr>
        </table>
        <br>
        <button class="btn btn-red" onclick="logout()">Logout Karein</button>
    </div>

    <!-- JavaScript Logic -->
    <script>
        // Yahan Admin ka ID aur Password set kiya gaya hai
        const ADMIN_USER = "admin";
        const ADMIN_PASS = "shree@123";

        // Admin Login form dikhane ke liye
        function showAdminLogin() {
            document.getElementById('view-customer').classList.add('hidden');
            document.getElementById('view-admin-login').classList.remove('hidden');
            document.getElementById('errorMsg').innerText = "";
        }

        // Wapas customer page par jane ke liye
        function goBack() {
            document.getElementById('view-admin-login').classList.add('hidden');
            document.getElementById('view-customer').classList.remove('hidden');
            document.getElementById('adminUser').value = "";
            document.getElementById('adminPass').value = "";
            document.getElementById('errorMsg').innerText = "";
        }

        // Login check karne ke liye
        function checkLogin() {
            let user = document.getElementById('adminUser').value;
            let pass = document.getElementById('adminPass').value;

            if (user === ADMIN_USER && pass === ADMIN_PASS) {
                document.getElementById('view-admin-login').classList.add('hidden');
                document.getElementById('view-admin-dash').classList.remove('hidden');
                document.getElementById('adminUser').value = "";
                document.getElementById('adminPass').value = "";
            } else {
                document.getElementById('errorMsg').innerText = "❌ Galat ID ya Password!";
            }
        }

        // Dashboard se logout karne ke liye
        function logout() {
            document.getElementById('view-admin-dash').classList.add('hidden');
            document.getElementById('view-customer').classList.remove('hidden');
        }
    </script>
</body>
</html>
