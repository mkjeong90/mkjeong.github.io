<!DOCTYPE html>
<html>
<head>
    <title>노래 리스트와 검색</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            margin: 20px;
            background-color: #f1f1f1;
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
            background-color: #fff;
            padding: 20px;
            box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
            border-radius: 8px;
        }

        h1 {
            text-align: center;
            margin-bottom: 30px;
            color: #007bff;
        }

        h2 {
            margin-bottom: 10px;
            color: #007bff;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            margin-bottom: 30px;
        }

        th, td {
            border: 1px solid #ccc;
            padding: 10px;
            text-align: center;
        }

        th {
            background-color: #f2f2f2;
        }

        #search-input {
            padding: 10px;
        }

        #search-button, #add-button {
            padding: 10px 20px;
            background-color: #007bff;
            color: #fff;
            border: none;
            cursor: pointer;
        }

        #search-button:hover, #add-button:hover {
            background-color: #0056b3;
        }

        #search-result {
            display: none;
        }

        .highlight {
            background-color: #ffff99;
        }

        #search-result-message {
            text-align: center;
            display: none;
            color: #ff0000;
            font-weight: bold;
            font-size: 18px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>신져리 노래 리스트</h1>

        <h2></h2>
        <input type="text" id="search-input" placeholder="노래 제목을 입력하세요">
        <button id="search-button" onclick="searchSongs()">검색</button>

        <h2>곡 추가</h2>
        <input type="text" id="title-input" placeholder="노래 제목">
        <input type="text" id="artist-input" placeholder="가수">
        <button id="add-button" onclick="addSong()">추가</button>

        <table id="song-table">
            <tr>
                <th>제목</th>
                <th>가수</th>
           
            </tr>
            <tr>
                <td>들리나요</td>
                <td>신지현</td>
          
            </tr>
            <tr>
                <td>하루</td>
                <td>신지현</td>
            </tr>
            <!-- 추가적인 노래 리스트를 원하는 만큼 추가할 수 있습니다 -->
        </table>

        <table id="search-result">
            <!-- 검색 결과가 여기에 표시될 것입니다 -->
        </table>

        <!-- 검색 결과 메시지 -->
        <div id="search-result-message">검색 결과가 없습니다.</div>
    </div>

    <script>
  // 노래 리스트를 로컬 스토리지에서 불러와서 테이블에 표시하는 함수
        function loadSongsFromLocalStorage() {
            const songTable = document.getElementById("song-table");
            const songs = JSON.parse(localStorage.getItem("songs") || "[]");

            songs.forEach(song => {
                const newRow = songTable.insertRow();
                const newTitleCell = newRow.insertCell(0);
                const newArtistCell = newRow.insertCell(1);

                newTitleCell.innerHTML = song.title;
                newArtistCell.innerHTML = song.artist;
            });
        }

        // 초기 페이지 로드시 노래 리스트를 불러옵니다.
        window.onload = loadSongsFromLocalStorage();

        function searchSongs() {
            // ... 검색 기능과 관련된 자바스크립트 코드 ...
        }

        function addSong() {
            const title = document.getElementById("title-input").value;
            const artist = document.getElementById("artist-input").value;
            const songTable = document.getElementById("song-table");

            if (!title || !artist) {
                alert("노래 제목과 가수를 모두 입력하세요.");
                return;
            }

            const newRow = songTable.insertRow();
            const newTitleCell = newRow.insertCell(0);
            const newArtistCell = newRow.insertCell(1);

            newTitleCell.innerHTML = title;
            newArtistCell.innerHTML = artist;

            // 입력한 노래를 로컬 스토리지에 저장합니다.
            const songs = JSON.parse(localStorage.getItem("songs") || "[]");
            songs.push({ title: title, artist: artist });
            localStorage.setItem("songs", JSON.stringify(songs));

            // 입력 필드 초기화
            document.getElementById("title-input").value = "";
            document.getElementById("artist-input").value = "";
        }
    </script>
</body>
</html>
