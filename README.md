<?php
session_start();

// Khởi tạo mảng sách nếu chưa tồn tại
if (!isset($_SESSION['books'])) {
    $_SESSION['books'] = [];
}

// Xử lý khi form được gửi
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $title = $_POST['title'];
    $authors = $_POST['authors'];
    $year = $_POST['year'];

    // Thêm sách vào mảng
    $book = [
        'title' => $title,
        'authors' => $authors,
        'year' => $year
    ];
    $_SESSION['books'][] = $book;
}
?>

<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Thêm sách</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 20px; }
        label { display: block; margin: 10px 0 5px; }
        input { width: 100%; max-width: 300px; padding: 5px; }
        input[type="submit"] { width: auto; margin-top: 10px; background-color: #4CAF50; color: white; border: none; padding: 10px; cursor: pointer; }
        h1 { color: #333; }
        h6 { font-size: 12px; color: #666; }
    </style>
</head>
<body>
    <h1>Thêm sách</h1>
    <form method="POST">
        <label for="title">Tên sách:</label>
        <input type="text" id="title" name="title" required>
        <label for="authors">Tác giả:</label>
        <input type="text" id="authors" name="authors" required>
        <label for="year">Năm xuất bản:</label>
        <input type="number" id="year" name="year" required>
        <input type="submit" value="Thêm sách">
    </form>

    <h2>Danh sách sách</h2>
    <?php
    if (!empty($_SESSION['books'])) {
        echo "<ul>";
        foreach ($_SESSION['books'] as $index => $book) {
            echo "<li>" . htmlspecialchars($book['title']) . " (" . htmlspecialchars($book['year']) . "). " . htmlspecialchars($book['authors']) . "</li>";
        }
        echo "</ul>";
    } else {
        echo "<p>Chưa có sách nào được thêm.</p>";
    }
    ?>
    <h6>Thực hiện bởi: Họ tên sinh viên - MSSV</h6>
</body>
</html>
