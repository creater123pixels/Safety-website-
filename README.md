<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Send GPS Location</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            padding: 20px;
        }
        button {
            padding: 15px;
            font-size: 18px;
            background-color: #28a745;
            color: white;
            border: none;
            cursor: pointer;
            margin-top: 20px;
            border-radius: 5px;
        }
        button:hover {
            background-color: #218838;
        }
    </style>
</head>
<body>

    <h2>GPS Location Sender</h2>
    <button onclick="confirmSend()">Send My Location</button>

    <script>
        const phoneNumber = "9626083889";  // Replace with the required phone number

        function confirmSend() {
            if (confirm("Do you want to send your location?")) {
                sendLocation();
            }
        }

        function sendLocation() {
            if (navigator.geolocation) {
                navigator.geolocation.getCurrentPosition(position => {
                    let lat = position.coords.latitude;
                    let lon = position.coords.longitude;
                    let locationLink = `https://www.google.com/maps?q=${lat},${lon}`;
                    let message = `My current location: ${locationLink}`;
                    
                    // Send via WhatsApp
                    let whatsappURL = `https://api.whatsapp.com/send?phone=${phoneNumber}&text=${encodeURIComponent(message)}`;
                    window.open(whatsappURL, "_blank");

                    // Send via SMS (uncomment below if needed)
                    // let smsURL = `sms:${phoneNumber}?body=${encodeURIComponent(message)}`;
                    // window.location.href = smsURL;

                }, error => {
                    alert("Error getting location. Make sure GPS is enabled.");
                });
            } else {
                alert("Geolocation is not supported by this browser.");
            }
        }
    </script>

</body>
</html>
