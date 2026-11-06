# tin-học
<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chinh Phục HTML - Game Học Bài</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background: linear-gradient(135deg, #4f46e5 0%, #7c3aed 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .game-card {
            background: #ffffff;
            width: 100%;
            max-width: 650px;
            border-radius: 24px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.25);
            padding: 30px;
            position: relative;
            overflow: hidden;
        }

        .screen {
            display: none;
            animation: fadeIn 0.3s ease-in-out;
        }

        .screen.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* ------------------- 1. MÀN HÌNH CHÍNH ------------------- */
        .home-title {
            text-align: center;
            font-size: 28px;
            color: #3730a3;
            margin-bottom: 10px;
        }

        .home-subtitle {
            text-align: center;
            color: #6b7280;
            font-size: 15px;
            margin-bottom: 30px;
        }

        .banner-img {
            text-align: center;
            font-size: 80px;
            margin-bottom: 30px;
        }

        .btn-main {
            display: block;
            width: 100%;
            padding: 16px;
            background: #4f46e5;
            color: white;
            border: none;
            border-radius: 14px;
            font-size: 18px;
            font-weight: bold;
            cursor: pointer;
            text-align: center;
            transition: all 0.2s;
            margin-bottom: 12px;
            box-shadow: 0 4px 12px rgba(79, 70, 229, 0.3);
        }

        .btn-main:hover {
            background: #4338ca;
            transform: translateY(-2px);
        }

        /* ------------------- 2. MÀN HÌNH CHỌN NHÂN VẬT ------------------- */
        .char-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 15px;
            margin: 25px 0;
        }

        .char-card {
            border: 3px solid #e5e7eb;
            border-radius: 16px;
            padding: 15px 10px;
            text-align: center;
            cursor: pointer;
            transition: all 0.2s;
        }

        .char-card:hover {
            border-color: #a5b4fc;
        }

        .char-card.selected {
            border-color: #4f46e5;
background: #eeeffe;
            transform: scale(1.03);
        }

        .char-avatar {
            font-size: 50px;
            margin-bottom: 8px;
        }

        .char-name {
            font-weight: bold;
            color: #1f2937;
            font-size: 15px;
        }

        .char-skill {
            font-size: 12px;
            color: #6b7280;
            margin-top: 4px;
        }

        /* ------------------- 3. MÀN HÌNH QUIZ ------------------- */
        .top-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 12px;
            border-bottom: 2px solid #f3f4f6;
        }

        .player-info {
            display: flex;
            align-items: center;
            gap: 8px;
            font-weight: bold;
            color: #3730a3;
        }

        .question-box {
            font-size: 19px;
            font-weight: 600;
            color: #1f2937;
            margin-bottom: 25px;
            line-height: 1.5;
            min-height: 60px;
        }

        .options-list {
            display: flex;
            flex-direction: column;
            gap: 12px;
        }

        .option-btn {
            background: #f9fafb;
            border: 2px solid #e5e7eb;
            border-radius: 14px;
            padding: 14px 20px;
            font-size: 16px;
            color: #374151;
            text-align: left;
            cursor: pointer;
            font-weight: 500;
            transition: all 0.2s;
        }

        .option-btn:hover:not([disabled]) {
            background: #f3f4f6;
            border-color: #d1d5db;
        }

        /* Đáp án đúng - sai */
        .option-btn.correct {
            background-color: #10b981 !important;
            color: white !important;
            border-color: #059669 !important;
        }

        .option-btn.incorrect {
            background-color: #ef4444 !important;
            color: white !important;
            border-color: #dc2626 !important;
        }

        .next-btn {
            margin-top: 20px;
            background: #10b981;
            display: none;
        }

        .next-btn:hover {
            background: #059669;
        }

        /* ------------------- 4. MÀN HÌNH TỔNG KẾT ------------------- */
        .result-box {
            text-align: center;
            padding: 10px 0;
        }

        .result-stars {
            font-size: 50px;
            margin: 15px 0;
        }

        .score-big {
            font-size: 36px;
            font-weight: bold;
            color: #4f46e5;
            margin-bottom: 10px;
        }

        .result-text {
            color: #4b5563;
            font-size: 16px;
            margin-bottom: 25px;
        }
    </style>
</head>
<body>

<div class="game-card">

    <!-- 1. MÀN HÌNH CHÍNH -->
    <div id="screen-home" class="screen active">
<div class="banner-img">📘⚡</div>
        <h1 class="home-title">Đấu Trí HTML</h1>
        <p class="home-subtitle">Chủ đề 4 - Bài 7: HTML và Cấu trúc trang web</p>
        <button class="btn-main" onclick="goToScreen('screen-char')">🎮 Bắt Đầu Học Bài</button>
    </div>

    <!-- 2. MÀN HÌNH CHỌN NHÂN VẬT -->
    <div id="screen-char" class="screen">
        <h2 style="text-align: center; color: #3730a3;">Chọn Bạn Đồng Hành</h2>
        <div class="char-grid">
            <div class="char-card selected" onclick="selectCharacter('🦉', 'Cú Tri Thức', this)">
                <div class="char-avatar">🦉</div>
                <div class="char-name">Cú Tri Thức</div>
                <div class="char-skill">Tăng sự tập trung</div>
            </div>
            <div class="char-card" onclick="selectCharacter('🤖', 'Robot Coder', this)">
                <div class="char-avatar">🤖</div>
                <div class="char-name">Robot Coder</div>
                <div class="char-skill">Lập trình siêu tốc</div>
            </div>
            <div class="char-card" onclick="selectCharacter('🐱', 'Mèo Chăm Học', this)">
                <div class="char-avatar">🐱</div>
                <div class="char-name">Mèo Chăm Học</div>
                <div class="char-skill">Cần cù may mắn</div>
            </div>
        </div>
        <button class="btn-main" onclick="startQuiz()">Vào Học Ngay ➔</button>
    </div>

    <!-- 3. MÀN HÌNH QUIZ -->
    <div id="screen-quiz" class="screen">
        <div class="top-bar">
            <div class="player-info">
                <span id="player-avatar" style="font-size: 24px;">🦉</span>
                <span id="player-name">Cú Tri Thức</span>
            </div>
            <div style="font-weight: bold; color: #6b7280;" id="quiz-progress">Câu 1/5</div>
            <div style="font-weight: bold; color: #10b981;" id="quiz-score">Điểm: 0</div>
        </div>

        <div class="question-box" id="question-text">Đang tải câu hỏi...</div>

        <div class="options-list" id="options-container">
            <!-- Nút câu trả lời tạo bằng JS -->
        </div>

        <button class="btn-main next-btn" id="btn-next" onclick="nextQuestion()">Câu Tiếp Theo ➔</button>
    </div>

    <!-- 4. MÀN HÌNH TỔNG KẾT -->
    <div id="screen-result" class="screen">
        <div class="result-box">
            <h2 style="color: #3730a3;">Bài Học Hoàn Thành!</h2>
            <div class="result-stars" id="result-stars">⭐⭐⭐</div>
            <div class="score-big" id="result-score">100 Điểm</div>
            <p class="result-text" id="result-details">Bạn đã trả lời đúng 5/5 câu hỏi.</p>
            
            <button class="btn-main" onclick="startQuiz()">🔄 Học Lại Bài Này</button>
<button class="btn-main" style="background: #e5e7eb; color: #374151;" onclick="goToScreen('screen-home')">🏠 Về Màn Hình Chính</button>
        </div>
    </div>

</div>

<script>
    // Dữ liệu nhân vật
    let selectedChar = { avatar: '🦉', name: 'Cú Tri Thức' };

    // Bộ câu hỏi trắc nghiệm dựa trên nội dung SGK trong ảnh
    const quizData = [
        {
            question: "1. Ngôn ngữ siêu văn bản dùng để thiết lập cấu trúc và hiển thị nội dung trang web là gì?",
            options: ["C++", "Java", "HTML", "Python"],
            correct: 2
        },
        {
            question: "2. Thẻ HTML nào dưới đây dùng để chứa toàn bộ các phần tử của trang web?",
            options: ["<head>", "<body>", "<html>", "<div>"],
            correct: 2
        },
        {
            question: "3. Dòng khai báo <!DOCTYPE html> nằm ở vị trí nào trong tệp văn bản HTML?",
            options: ["Dòng đầu tiên", "Dòng cuối cùng", "Nằm trong thẻ <body>", "Nằm trong thẻ <head>"],
            correct: 0
        },
        {
            question: "4. Cụm từ HTML là viết tắt của thuật ngữ tiếng Anh nào?",
            options: [
                "HyperText Markup Language",
                "HighText Machine Language",
                "Hyperlink Text Markup Language",
                "HyperText Marking Lan
