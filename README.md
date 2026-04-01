<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Physio Booking</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            margin: 20px;
        }
        .container {
            max-width: 800px;
            margin: auto;
            padding: 20px;
            border: 1px solid #ddd;
            border-radius: 8px;
        }
        .form-group {
            margin-bottom: 15px;
        }
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }
        input[type="text"],
        input[type="date"],
        select,
        textarea {
            width: 100%;
            padding: 8px;
            border: 1px solid #ccc;
            border-radius: 4px;
            box-sizing: border-box;
        }
        .radio-group label {
            display: inline-block;
            margin-right: 15px;
            font-weight: normal;
        }
        .radio-group input[type="radio"] {
            margin-right: 5px;
        }
        button {
            background-color: #4CAF50;
            color: white;
            padding: 10px 15px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
        }
        button:hover {
            background-color: #45a049;
        }
        .error-message {
            color: red;
            font-weight: bold;
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Physiotherapy Appointment Booking</h1>
        <p>Please fill in your details below to book your appointment. Available days are Tuesdays, Wednesdays, and Thursdays.</p>

        <form id="bookingForm" action="/submit-booking" method="post">
            <div class="form-group">
                <label for="fullName">Full Name *</label>
                <input type="text" id="fullName" name="fullName" required>
            </div>

            <div class="form-group">
                <label for="sport">Sport *</label>
                <select id="sport" name="sport" required>
                    <option value="">-- Select Sport --</option>
                    <option value="swimming">Swimming</option>
                    <option value="diving">Diving</option>
                    <option value="weightlifting">Weightlifting</option>
                    <option value="badminton">Badminton</option>
                    <option value="cycling">Cycling</option>
                    <option value="gymnastics">Gymnastics</option>
                    <option value="golf">Golf</option>
                    <option value="fencing">Fencing</option>
                    <option value="archery">Archery</option>
                    <option value="shooting">Shooting</option>
                    <option value="athletics">Athletics</option>
                    <option value="sailing">Sailing</option>
                    <option value="hockey">Hockey</option>
                    <option value="judo">Judo</option>
                    <option value="table-tennis">Ping Pong</option>
                    <option value="taekwondo">Taekwondo</option>
                    <option value="karate">Karate</option>
                    <option value="lawn-bowls">Lawn Bowls</option>
                    <option value="pencak-silat">Pencak Silat</option>
                    <option value="sepak-takraw">Sepak Takraw</option>
                    <option value="squash">Squash</option>
                    <option value="tenpin-bowling">Tenpin Bowling</option>
                    <option value="wushu">Wushu</option>
                    <option value="football">Football</option>
                    <option value="netball">Netball</option>
                    <option value="basketball">Basketball</option>
                    <option value="rugby">Rugby</option>
                    <option value="tennis">Tennis</option>
                    <option value="boxing">Boxing</option>
                    <option value="softball">Softball</option>
                    <option value="other">Other</option>
                </select>
            </div>

            <div class="form-group">
                <label>Gender *</label>
                <div class="radio-group">
                    <input type="radio" id="male" name="gender" value="male" required>
                    <label for="male">Male</label>
                    <input type="radio" id="female" name="gender" value="female" required>
                    <label for="female">Female</label>
                </div>
            </div>

            <div class="form-group">
                <label for="bookingDate">Preferred Date *</label>
                <input type="date" id="bookingDate" name="bookingDate" required>
                <!-- JavaScript will be needed to restrict selectable dates -->
            </div>

            <div class="form-group">
                <label for="timeSlot">Preferred Time Slot *</label>
                <select id="timeSlot" name="timeSlot" required>
                    <option value="">-- Select Time Slot --</option>
                    <option value="14:30">02:30 PM</option>
                    <option value="15:15">03:15 PM</option>
                    <option value="16:00">04:00 PM</option>
                </select>
            </div>

            <button type="submit">Book Appointment</button>
        </form>
        <div id="bookingMessage" class="error-message"></div>
    </div>

    <script>
        // --- JavaScript for Date Restriction and Form Validation ---

        const bookingForm = document.getElementById('bookingForm');
        const bookingDateInput = document.getElementById('bookingDate');
        const timeSlotInput = document.getElementById('timeSlot');
        const bookingMessageDiv = document.getElementById('bookingMessage');

        // Function to check if a date is a Tuesday, Wednesday, or Thursday
        function isAllowedDay(date) {
            const dayOfWeek = date.getDay(); // 0 = Sunday, 1 = Monday, 2 = Tuesday, ..., 6 = Saturday
            return dayOfWeek === 2 || dayOfWeek === 3 || dayOfWeek === 4; // Tuesday, Wednesday, Thursday
        }

        // Set event listener for date input changes
        bookingDateInput.addEventListener('change', function() {
            const selectedDate = new Date(this.value);
            if (!isAllowedDay(selectedDate)) {
                bookingMessageDiv.textContent = "Booking is only available on Tuesdays, Wednesdays, and Thursdays. Please select an available date.";
                this.value = ''; // Clear the invalid date
            } else {
                bookingMessageDiv.textContent = ''; // Clear any previous message
                // You might want to dynamically update available time slots here based on the selected date
            }
        });

        // --- Backend Logic Simulation (for demonstration) ---
        // In a real application, this logic would be on the server-side.

        // Example data structure to simulate booking status
        // This would typically be stored in a database
        let bookings = {}; // { 'YYYY-MM-DD_HH:MM': { male: count, female: count } }

        bookingForm.addEventListener('submit', function(event) {
            event.preventDefault(); // Prevent default form submission

            const formData = new FormData(bookingForm);
            const fullName = formData.get('fullName');
            const sport = formData.get('sport');
            const gender = formData.get('gender');
            const bookingDate = formData.get('bookingDate');
            const timeSlot = formData.get('timeSlot');

            const selectedDateTimeKey = `${bookingDate}_${timeSlot}`;

            // --- Date and Time Slot Validation ---
            const selectedDateObj = new Date(bookingDate);
            if (!isAllowedDay(selectedDateObj)) {
                bookingMessageDiv.textContent = "Booking failed: Selected date is not available. Please choose a Tuesday, Wednesday, or Thursday.";
                return;
            }

            if (!timeSlot) {
                bookingMessageDiv.textContent = "Booking failed: Please select a time slot.";
                return;
            }

            // --- Slot Capacity Check (Simulated Backend Logic) ---
            const currentBookings = bookings[selectedDateTimeKey] || { male: 0, female: 0 };

            if (gender === 'male') {
                if (currentBookings.male >= 2) {
                    bookingMessageDiv.textContent = `Booking failed: Slot ${timeSlot} on ${bookingDate} is full for male participants (max 2).`;
                    return;
                }
                currentBookings.male++;
            } else if (gender === 'female') {
                if (currentBookings.female >= 1) {
                    bookingMessageDiv.textContent = `Booking failed: Slot ${timeSlot} on ${bookingDate} is full for female participants (max 1).`;
                    return;
                }
                currentBookings.female++;
            }

            // If all checks pass, update bookings and show success message
            bookings[selectedDateTimeKey] = currentBookings;
            bookingMessageDiv.textContent = `Booking successful for ${fullName}! Your appointment is on ${bookingDate} at ${timeSlot}.`;
            bookingForm.reset(); // Clear the form after successful booking

            // In a real application, you would send this data to your server here
            // using fetch() or XMLHttpRequest.
            console.log("Booking submitted:", { fullName, sport, gender, bookingDate, timeSlot });
        });

        // --- Initial Date Restriction Setup ---
        // This ensures that if the page loads with a date pre-filled, it's validated.
        const initialDate = bookingDateInput.value;
        if (initialDate) {
            const selectedDate = new Date(initialDate);
            if (!isAllowedDay(selectedDate)) {
                bookingMessageDiv.textContent = "Booking is only available on Tuesdays, Wednesdays, and Thursdays. Please select an available date.";
                bookingDateInput.value = ''; // Clear the invalid date
            }
        }

    </script>
</body>
</html>
