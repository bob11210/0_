<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>0_my music - Your Music Streaming Platform</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            background-color: #121212;
            color: white;
        }

        header {
            background-color: #000;
            padding: 1rem;
        }

        nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
            max-width: 1200px;
            margin: 0 auto;
        }

        .logo {
            font-size: 1.5rem;
            font-weight: bold;
            color: #1DB954;
        }

        nav ul {
            display: flex;
            list-style: none;
        }

        nav ul li a {
            color: white;
            text-decoration: none;
            padding: 0.5rem 1rem;
        }

        #plans {
            max-width: 1200px;
            margin: 2rem auto;
            padding: 2rem;
            text-align: center;
        }

        .plan-container {
            display: flex;
            justify-content: center;
            gap: 2rem;
            margin-top: 2rem;
        }

        .plan {
            background-color: #282828;
            padding: 2rem;
            border-radius: 10px;
            width: 300px;
        }

        .plan.premium {
            background-color: #1DB954;
            transform: scale(1.05);
        }

        .price {
            font-size: 2rem;
            margin: 1rem 0;
        }

        .plan ul {
            list-style: none;
            margin: 1rem 0;
        }

        .plan ul li {
            margin: 0.5rem 0;
        }

        button {
            background-color: #1DB954;
            color: white;
            border: none;
            padding: 1rem 2rem;
            border-radius: 25px;
            font-weight: bold;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        .premium button {
            background-color: white;
            color: #1DB954;
        }

        button:hover {
            background-color: #1ed760;
        }

        .premium button:hover {
            background-color: #f0f0f0;
        }

        /* Payment Modal Styles */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.8);
        }

        .payment-container {
            max-width: 500px;
            margin: 2rem auto;
            padding: 2rem;
            background-color: #282828;
            border-radius: 15px;
            text-align: center;
        }

        .cashapp-payment {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 1rem;
        }

        .amount {
            font-size: 2.5rem;
            font-weight: bold;
            color: #00D632;
        }

        .cashtag {
            font-size: 1.2rem;
            color: #ffffff;
        }

        .qr-code {
            background-color: white;
            padding: 1rem;
            border-radius: 10px;
            margin: 1rem 0;
        }

        .cashapp-button {
            background-color: #00D632;
            color: black;
            text-decoration: none;
            padding: 1rem 2rem;
            border-radius: 25px;
            font-weight: bold;
            margin-top: 1rem;
            display: inline-block;
        }

        .close-modal {
            position: absolute;
            right: 20px;
            top: 20px;
            color: white;
            font-size: 30px;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <header>
        <nav>
            <div class="logo">0_my music</div>
            <ul>
                <li><a href="#home">Home</a></li>
                <li><a href="#discover">Discover</a></li>
                <li><a href="#library">Library</a></li>
                <li><a href="#plans">Plans</a></li>
            </ul>
        </nav>
    </header>

    <section id="plans">
        <h2>Choose Your Plan</h2>
        <div class="plan-container">
            <div class="plan">
                <h3>Box Plan</h3>
                <p class="price">Free</p>
                <ul>
                    <li>Ad-supported streaming</li>
                    <li>Basic audio quality</li>
                    <li>Shuffle play</li>
                    <li>Mobile access</li>
                </ul>
                <button onclick="startFreePlan()">Start Free</button>
            </div>
            <div class="plan premium">
                <h3>Premium Plan</h3>
                <p class="price">$10/month</p>
                <ul>
                    <li>Ad-free streaming</li>
                    <li>High-quality audio</li>
                    <li>On-demand playback</li>
                    <li>Offline downloads</li>
                    <li>Mobile & desktop access</li>
                </ul>
                <button onclick="showPaymentModal()">Get Premium</button>
            </div>
        </div>
    </section>

    <!-- Payment Modal -->
    <div id="paymentModal" class="modal">
        <div class="payment-container">
            <span class="close-modal" onclick="closePaymentModal()">&times;</span>
            <h2>Premium Plan Payment</h2>
            <div class="cashapp-payment">
                <p class="amount">$10.00</p>
                <p class="cashtag">Send to: $0mymusic</p>
                <div class="qr-code" id="qrCode"></div>
                <button onclick="copyCashtag()">Copy $Cashtag</button>
                <a href="cashapp://pay/0mymusic" class="cashapp-button">Open in Cash App</a>
            </div>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/qrcode.js"></script>
    <script>
        // Show payment modal
        function showPaymentModal() {
            document.getElementById('paymentModal').style.display = 'block';
            generateQRCode();
        }

        // Close payment modal
        function closePaymentModal() {
            document.getElementById('paymentModal').style.display = 'none';
        }

        // Generate QR code
        function generateQRCode() {
            if (!document.getElementById('qrCode').innerHTML) {
                new QRCode(document.getElementById('qrCode'), {
                    text: 'https://cash.app/$0mymusic/10',
                    width: 180,
                    height: 180
                });
            }
        }

        // Copy Cashtag
        function copyCashtag() {
            navigator.clipboard.writeText('$0mymusic')
                .then(() => {
                    const button = document.querySelector('.cashapp-payment button');
                    button.textContent = 'Copied!';
                    setTimeout(() => {
                        button.textContent = 'Copy $Cashtag';
                    }, 2000);
                });
        }

        // Start free plan
        function startFreePlan() {
            alert('Welcome to the Box Plan! Enjoy your free music streaming.');
        }

        // Close modal when clicking outside
        window.onclick = function(event) {
            if (event.target == document.getElementById('paymentModal')) {
                closePaymentModal();
            }
        }
    </script>
</body>
</html>
