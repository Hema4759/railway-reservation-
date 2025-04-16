# railway-reservation-
<!DOCTYPE html>
<html>
<head>
    <title>Insert and Display Data</title>
</head>
<body>
    <!-- Form for input -->
    <form action="" method="POST">
        <label for="name">Name:</label>
        <input type="text" name="name" required><br><br>

        <label for="email">Email:</label>
        <input type="email" name="email" required><br><br>

        <label for="age">Age:</label>
        <input type="number" name="age" required><br><br>

        <button type="submit">Submit</button>
    </form>

    <?php
    $servername = "localhost";
    $username = "root";
    $password = "";
    $dbname = "my_admin";

    $conn = new mysqli($servername, $username, $password, $dbname);

    if ($conn->connect_error) {
        die("Connection failed: " . $conn->connect_error);
    }

    if ($_SERVER["REQUEST_METHOD"] == "POST") {
        $name = $_POST["name"];
        $email = $_POST["email"];
        $age = $_POST["age"];

        $sql = "INSERT INTO emp (name, email, age) VALUES ('$name', '$email', $age)";

        if ($conn->query($sql) === TRUE) {
            echo "New record created successfully<br>";
        } else {
            echo "Error: " . $sql . "<br>" . $conn->error;
        }
    }

    $sql = "SELECT name, email, age FROM emp";
    $result = $conn->query($sql);

    if ($result->num_rows > 0) {
        echo "<h3>Users Table</h3>";
        echo "<table border='1'>
                <tr>
                  
                    <th>Name</th>
                    <th>Email</th>
                    <th>Age</th>
                </tr>";
        while($row = $result->fetch_assoc()) {
            echo "<tr>
                  
                    <td>" . $row["name"] . "</td>
                    <td>" . $row["email"] . "</td>
                    <td>" . $row["age"] . "</td>
                  </tr>";
        }
        echo "</table>";
    } else {
        echo "No records found.";
    }
    $conn->close();
    ?>
</body>
</html>
