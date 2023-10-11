# hospitalmanagement
Testing page
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Patient Details</title>
    <style>
        /* ... (your existing styles) ... */
        body {
            font-family: Arial, sans-serif;
            background-color: #b5b1b0;
            padding: 20px;
        }

        .navbar {
            background-color: #5d5e5d;
            color: #fff;
            padding: 10px;
            border-radius: 5px;
            margin-top: 2%;
        }

        .navbar ul {
            list-style-type: none;
            text-align: left;
            margin: 0;
            padding: 0;
            overflow: hidden;
        }

        .navbar li {
            display: inline;
            margin-right: 10px;
        }

        .navbar li a {
            text-decoration: none; /* Fixed: solid -> none */
            color: #fff;
            padding: 10px 10px;
            margin-top: 5%;
        }

        .navbar li a:hover {
            background-color: #555;
            transition: 0.5s;
        }

        .logout {
            background-color: #4a90e2;
            color: #fff;
            padding: 10px;
            border-radius: 5px;
            width: 5%;
            margin-left: 90%;
            margin-top: -39px;
        }

        .logout ul {
            list-style-type: none;
            margin: 0;
            padding: 0;
            overflow: hidden;
        }

        .logout li a {
            text-decoration: none; /* Fixed: solid -> none */
            color: #fff;
            padding: 10px 10px;
            margin-top: 5%;
            text-align: center;
        }

        .logout:hover {
            background-color: #1037ab;
            transition: 0.5s;
        }

        .input-form {
            margin-bottom: 20px;
            margin-top: 10%;
            margin-left: 20%;
        }

        .input-form label {
            display: block;
            font-weight: bold;
            margin-bottom: 5px;
            text-align: justify; /* Fixed: text-align:justify; */
            margin-left: 20%;
        }

        .input-form input[type="number"] {
            width: 200px;
            padding: 5px;
            width: 60%;
        }

        .input-form button {
            padding: 5px 10px;
            background-color: #4a90e2;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        #details-table {
            border-collapse: collapse;
            width: 100%;
            margin-top: 20px;
            background-color: #fff;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        }

        #details-table th,
        #details-table td {
            padding: 8px;
            text-align: left;
            border-bottom: 1px solid #ddd;
        }

        #details-table th {
            background-color: #f2f2f2;
        }

        #patient-photo {
            max-width: 200px;
            max-height: 200px;
            margin-bottom: 10px;
            margin-left: 40%;
        }

        #appointment-form label {
            display: block;
            font-size: 16px;
            font-weight: bold;
            margin-bottom: 8px;
        }

        #appointment-form .select {
            width: 100%;
            padding: 10px;
            border-radius: 5px;
            border: 1px solid #ccc;
            margin-bottom: 10px;
            font-size: 16px;
            transition: 0.5s;
        }

        #appointment-form .button {
            padding: 5px 10px;
            background-color: #4a90e2;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
    </style>
</head>
<body>

<div class="image">
    <img src="file:///C:/Users/rajar/Desktop/hospital%20management/download.jpg" width="100" height="100" alt="Local Image">
</div>

<div class="navbar">
    <ul>
        <li><a href="#">Home</a></li>
        <li><a href="#">About Us</a></li>
        <li><a href="#">Contact Us</a></li>
    </ul>
</div>

<div class="logout">
    <ul>
        <li><a href="logout.html" target="_blank">Logout</a></li>
    </ul>
</div>

<div class="input-form">
    <label for="patient-number">Enter Patient Number (6 digits):</label>
    <input type="number" id="patient-number" placeholder="Patient Number" min="100000" max="999999">
    <button onclick="fetchPatientDetails()">Get Patient Details</button>
</div>

<div id="patient-info">
    <p id="patient-number-display"></p>
    <p id="patient-name"></p>
    <p id="patient-age"></p>
    <p id="patient-place"></p>
    <p id="patient-blood-group"></p>
    <img id="patient-photo" alt="Patient Photo" />
</div>

<table id="details-table" style="display: none;">
    <thead>
    <tr>
        <th>Patient Number</th>
        <th>Name</th>
        <th>Age</th>
        <th>Gender</th>
    </tr>
    </thead>
    <tbody id="details-table-body">
    </tbody>
</table>

<div id="appointment-form" style="display: none;">
    <h2>Book Appointment</h2>
    <label for="doctor-name">OP</label>
    <select name="OP" id="op" style="width: 90%;">
        <option value=""></option>
        <option value="E&T">E&T</option>
        <option value="Dental">Dental</option>
        <option value="Eye Specialist">Eye Specialist</option>
        <option value="Dermatologist">Dermatologist</option>
        <option value="Pediatrician">Pediatrician</option>
    </select>
    <button onclick="bookAppointment()" style="appearance: initial; padding: 5px 10px; background-color: #4a90e2; color: #fff; border: none; border-radius: 5px; cursor: pointer;">Book</button>
</div>

<script>
    // ... (your existing JavaScript code) ...
    var patientData = [
        {
            patientNumber: '123456',
            name: 'John Doe',
            age: 35,
            place: 'New York',
            bloodGroup: 'A+'
        },
        {
            patientNumber: '234567',
            name: 'Alice Smith',
            age: 28,
            place: 'Los Angeles',
            bloodGroup: 'B+'
        },
        {
            patientNumber: '345678',
            name: 'Michael Johnson',
            age: 42,
            place: 'Chicago',
            bloodGroup: 'O+'
        },
        {
            patientNumber: '456789',
            name: 'Emily Davis',
            age: 51,
            place: 'San Francisco',
            bloodGroup: 'AB+'
        },
        {
            patientNumber: '567890',
            name: 'William Brown',
            age: 29,
            place: 'Houston',
            bloodGroup: 'O-'
        }
    ];

    function fetchPatientDetails() {
        var patientNumber = document.getElementById('patient-number').value;
        var patientInfo = patientData.find(patient => patient.patientNumber === patientNumber);

        if (patientInfo) {
            document.getElementById('patient-number-display').innerText = `Patient Number: ${patientInfo.patientNumber}`;
            document.getElementById('patient-name').innerText = `Name: ${patientInfo.name}`;
            document.getElementById('patient-age').innerText = `Age: ${patientInfo.age}`;
            document.getElementById('patient-place').innerText = `Place: ${patientInfo.place}`;
            document.getElementById('patient-blood-group').innerText = `Blood Group: ${patientInfo.bloodGroup}`;
            document.getElementById('patient-photo').src = `file:///C:/Users/rajar/Desktop/hospital%20management/download.jpg`;
        } else {
            alert('Patient not found!');
        }
    }

    function bookAppointment() {
        var doctorName = document.getElementById('op').value;
        var selectedPatientNumber = document.getElementById('patient-number').value;
        alert('Appointment booked successfully!');
    }
</script>

</body>
</html>
