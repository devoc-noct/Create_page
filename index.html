<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <title>テトリス</title>
    <style>
        body { 
            background: #111; 
            color: #fff; 
            text-align: center; 
            font-family: 'Courier New', Courier, monospace; 
            margin: 0;
            padding: 20px;
        }
        h1 { color: #ff0; text-shadow: 0 0 10px #ff0; margin-bottom: 5px; }
        .controls { color: #aaa; font-size: 14px; margin-bottom: 15px; }
        
        .game-container {
            display: flex;
            justify-content: center;
            align-items: flex-start;
            gap: 20px;
            max-width: 500px;
            margin: 0 auto;
        }
        
        canvas { 
            background: #000; 
            border: 4px solid #fff; 
            box-shadow: 0 0 20px rgba(255,255,255,0.2);
        }
        
        .side-panel {
            background: #222;
            border: 2px solid #555;
            padding: 15px;
            width: 140px;
            text-align: left;
            box-sizing: border-box;
        }
        
        .info-label { font-size: 12px; color: #888; margin-top: 10px; }
        .info-value { font-size: 20px; font-weight: bold; color: #0f0; margin-bottom: 10px; }
        #next-canvas { background: #000; border: 1px solid #555; margin-top: 5px; }
    </style>
</head>
<body>

    <h1>ARCADE TETRIS</h1>
    <div class="controls">【←】【→】:移動 / 【↓】:加速 / 【↑】:一発落下 / 【スペース】:回転</div>

    <div class="game-container">
        
        <canvas id="game" width="300" height="600"></canvas>
        
        <div class="side-panel">
                        <div class="info-label">HOLD</div>
            <canvas id="hold-canvas" width="100" height="100"></canvas>

            <div class="info-label">NEXT</div>
            <canvas id="next-canvas" width="100" height="100"></canvas>
            
            <div class="info-label">SCORE</div>
            <div id="score" class="info-value">0</div>
            
            <div class="info-label">LINES</div>
            <div id="lines" class="info-value">0</div>
            
            <div class="info-label">LEVEL</div>
            <div id="level" class="info-value">1</div>
        </div>
    </div>

    <script>
        const canvas = document.getElementById("game");
        const ctx = canvas.getContext("2d");
        const nextCanvas = document.getElementById("next-canvas");
        const nextCtx = nextCanvas.getContext("2d");
        const holdCanvas = document.getElementById("hold-canvas");
        const holdCtx = holdCanvas.getContext("2d");
        let holdType = 0; // 最初は何もキープしていないので0
        let hasHeld = false; // 1つのブロックにつき1回だけホールドできるようにするフラグ

        
        const BLOCK_SIZE = 30;
        const ROWS = 20;
        const COLS = 10;

        let score = 0;
        let linesCleared = 0;
        let level = 1;
        let gameInterval;
        let currentSpeed = 500;

        let board = Array.from({ length: ROWS }, () => Array(COLS).fill(0));

        // すべての形状のマス目を1マスずつ数字で完全に記述
        const SHAPES = [
            [],
            [[0,0,0,0],[1,1,1,1],[0,0,0,0],[0,0,0,0]], // I型
            [[2,2],[2,2]],                             // O型
            [[0,3,3],[3,3,0],[0,0,0]],                 // S型
            [[4,4,0],[0,4,4],[0,0,0]],                 // Z型
            [[5,0,0],[5,5,5],[0,0,0]],                 // J型
            [[0,0,6],[6,6,6],[0,0,0]],                 // L型
            [[0,7,0],[7,7,7],[0,0,0]]                  // T型
        ];

        const COLORS = ["", "#00f0f0", "#f0f000", "#00f000", "#f00000", "#0000f0", "#f0a500", "#a000f0"];

        // --- 【完全修正版】7種1巡（7-Bag）システム ---
        let tetrisBag = []; // ブロックを貯めておく「袋」

        // 袋からランダムに1つブロックを取り出す関数
        function getNextFromBag() {
            // 袋が空になったら、新しく1〜7の数字（全種類）を補充してシャッフル
            if (tetrisBag.length === 0) {
                // 自動消去バグ対策：1から7の数値をループ処理で確実に袋に入れます
                for (let n = 1; n <= 7; n++) {
                    tetrisBag.push(n);
                }
                
                // フィッシャー・イェーツのシャッフルアルゴリズムで袋の中身をバラバラにする
                for (let i = tetrisBag.length - 1; i > 0; i--) {
                    const j = Math.floor(Math.random() * (i + 1));
                    [tetrisBag[i], tetrisBag[j]] = [tetrisBag[j], tetrisBag[i]];
                }
            }
            // 袋の先頭から1つ取り出して返す
            return tetrisBag.shift();
        }

        // 初期ブロックの設定
        let currentType = getNextFromBag();
        let currentPiece = SHAPES[currentType];
        let nextType = getNextFromBag();
        let nextPiece = SHAPES[nextType];
        
        let blockX = 3;
        let blockY = 0;
        // --- ここまで ---




        function spawnPiece() {
            currentType = nextType;
            currentPiece = SHAPES[currentType];
            blockX = Math.floor((COLS - currentPiece.length) / 2);
            blockY = 0;
            rotationState = 0;

    // 【書き換え前】 nextType = Math.floor(Math.random() * 7) + 1;
    nextType = getNextFromBag(); // 【書き換え後】袋から次のブロックを取得する

            nextPiece = SHAPES[nextType];

            if (checkCollision(blockX, blockY, currentPiece)) {
                alert("GAME OVER!\nスコア: " + score + "\n消したライン: " + linesCleared);
                resetGame();
            }
            drawNext();
            hasHeld = false;
        }
                // 【新機能】ブロックを入れ替える（ホールド）
        function holdPiece() {
            if (hasHeld) return; // すでにそのターンでホールドを使っていたら何もしない
            
            let temp = currentType;
            if (holdType === 0) {
                // 初めてホールドを使う場合：今のブロックを保存し、次のブロックを出す
                holdType = currentType;
                spawnPiece();
            } else {
                // すでに保存されている場合：中身を入れ替えて、位置を上に戻す
                currentType = holdType;
                currentPiece = SHAPES[currentType];
                holdType = temp;
                blockX = Math.floor((COLS - currentPiece.length) / 2);
                blockY = 0;
            }
            hasHeld = true; // このターンはもう使えないようにする
            drawHold();
            draw();
        }

        // 【新機能】HOLD画面を描画する
        function drawHold() {
            holdCtx.fillStyle = "#000";
            holdCtx.fillRect(0, 0, holdCanvas.width, holdCanvas.height);
            if (holdType === 0) return;
            
            let p = SHAPES[holdType];
            let offsetX = (holdCanvas.width - p.length * BLOCK_SIZE) / 2;
            let offsetY = (holdCanvas.height - p.length * BLOCK_SIZE) / 2;

            for (let r = 0; r < p.length; r++) {
                for (let c = 0; c < p[r].length; c++) {
                    if (p[r][c]) {
                        holdCtx.fillStyle = COLORS[holdType];
                        holdCtx.fillRect(offsetX + c * BLOCK_SIZE, offsetY + r * BLOCK_SIZE, BLOCK_SIZE - 1, BLOCK_SIZE - 1);
                    }
                }
            }
        }


        function resetGame() {
            board = Array.from({ length: ROWS }, () => Array(COLS).fill(0));
            score = 0;
            linesCleared = 0;
            level = 1;
            currentSpeed = 500;
            updatePointsDisplay();
            spawnPiece();
            updateTimer();
        }

        function checkCollision(x, y, piece) {
            for (let r = 0; r < piece.length; r++) {
                for (let c = 0; c < piece[r].length; c++) {
                    if (piece[r][c]) {
                        let newX = x + c;
                        let newY = y + r;
                        if (newX < 0 || newX >= COLS || newY >= ROWS) return true;
                        if (newY >= 0 && board[newY][newX]) return true;
                    }
                }
            }
            return false;
        }

        function lockPiece() {
            for (let r = 0; r < currentPiece.length; r++) {
                for (let c = 0; c < currentPiece[r].length; c++) {
                    if (currentPiece[r][c]) {
                        if (blockY + r >= 0) {
                            board[blockY + r][blockX + c] = currentType;
                        }
                    }
                }
            }
        }

        function clearLines() {
            let count = 0;
            for (let r = ROWS - 1; r >= 0; r--) {
                if (board[r].every(val => val > 0)) {
                    board.splice(r, 1);
                    board.unshift(Array(COLS).fill(0));
                    count++;
                    r++; 
                }
            }
            if (count > 0) {
                linesCleared += count;
                // 消去数に応じたスコア配列（インデックス0から4まで完全に記述）
                const comboPoints =[0, 100, 300, 500, 800];
                score += comboPoints[count] * level;

                let nextLevel = Math.floor(linesCleared / 10) + 1;
                if (nextLevel > level && level < 10) {
                    level = nextLevel;
                    currentSpeed = Math.max(100, 500 - (level - 1) * 45);
                    updateTimer();
                }
                updatePointsDisplay();
            }
        }

        function updatePointsDisplay() {
            document.getElementById("score").innerText = score;
            document.getElementById("lines").innerText = linesCleared;
            document.getElementById("level").innerText = level;
        }

        // --- ここから Tスピン（DT砲など）に完全対応したSRS壁蹴りシステム ---
        
        // 現在の回転状態を記録する変数（0:初期, 1:右90度, 2:180度, 3:左90度）
        let rotationState = 0;

                // --- ここから【完全修正版】SRS壁蹴りシステム ---

        // 状態の変化 [oldState->newState] に応じた5つのずらし候補を計算する関数
        function getSRSOffsetX(oldState, newState, index) {
            const key = oldState + "->" + newState;
            // indexは 0 から 4 までの候補番号
            if (index === 0) return 0; // 候補1：ずらしなし

            // 候補2〜5のX方向のずらし量を数字で直接指定（バグ防止）
            if (key === "0->1") { if(index===1) return -1; if(index===2) return -1; if(index===3) return 0; if(index===4) return -1; }
            if (key === "1->0") { if(index===1) return 1;  if(index===2) return 1;  if(index===3) return 0; if(index===4) return 1;  }
            if (key === "1->2") { if(index===1) return 1;  if(index===2) return 1;  if(index===3) return 0; if(index===4) return 1;  }
            if (key === "2->1") { if(index===1) return -1; if(index===2) return -1; if(index===3) return 0; if(index===4) return -1; }
            if (key === "2->3") { if(index===1) return 1;  if(index===2) return 1;  if(index===3) return 0; if(index===4) return 1;  }
            if (key === "3->2") { if(index===1) return -1; if(index===2) return -1; if(index===3) return 0; if(index===4) return -1; }
            if (key === "3->0") { if(index===1) return -1; if(index===2) return -1; if(index===3) return 0; if(index===4) return -1; }
            if (key === "0->3") { if(index===1) return 1;  if(index===2) return 1;  if(index===3) return 0; if(index===4) return 1;  }
            return 0;
        }

        function getSRSOffsetY(oldState, newState, index) {
            const key = oldState + "->" + newState;
            if (index === 0) return 0; // 候補1：ずらしなし

            // 候補2〜5のY方向のずらし量を数字で直接指定（バグ防止）
            if (key === "0->1") { if(index===1) return 0; if(index===2) return -1; if(index===3) return 2; if(index===4) return 2; }
            if (key === "1->0") { if(index===1) return 0; if(index===2) return 1;  if(index===3) return -2; if(index===4) return -2; }
            if (key === "1->2") { if(index===1) return 0; if(index===2) return 1;  if(index===3) return -2; if(index===4) return -2; }
            if (key === "2->1") { if(index===1) return 0; if(index===2) return -1; if(index===3) return 2; if(index===4) return 2; }
            if (key === "2->3") { if(index===1) return 0; if(index===2) return -1; if(index===3) return 2; if(index===4) return 2; }
            if (key === "3->2") { if(index===1) return 0; if(index===2) return 1;  if(index===3) return -2; if(index===4) return -2; }
            if (key === "3->0") { if(index===1) return 0; if(index===2) return 1;  if(index===3) return -2; if(index===4) return -2; }
            if (key === "0->3") { if(index===1) return 0; if(index===2) return 1;  if(index===3) return -2; if(index===4) return -2; }
            return 0;
        }

        // SRS基準でねじり込み回転を試す関数
        function attemptRotationSRS(nextP, oldState, newState) {
            // 5つの候補（0から4）を順番にテストする
            for (let i = 0; i < 5; i++) {
                let moveX = getSRSOffsetX(oldState, newState, i);
                let moveY = getSRSOffsetY(oldState, newState, i);

                let testX = blockX + moveX;
                let testY = blockY - moveY; // SRS規格の上下を補正

                // 衝突しなければ回転確定（狭い穴への滑り込み成功）
                if (!checkCollision(testX, testY, nextP)) {
                    blockX = testX;
                    blockY = testY;
                    currentPiece = nextP;
                    rotationState = newState; // 回転状態を更新
                    return;
                }
            }
        }
        // --- ここまで ---

        function rotatePiece() {
            let nextP = currentPiece.map((_, c) => currentPiece.map(r => r[c]).reverse());
            const oldState = rotationState;
            const newState = (rotationState + 1) % 4;
            attemptRotationSRS(nextP, oldState, newState);
        }

        function rotatePieceCCW() {
            let nextP = currentPiece.map((_, c) => currentPiece.map(r => r[c])).reverse();
            const oldState = rotationState;
            const newState = (rotationState + 3) % 4;
            attemptRotationSRS(nextP, oldState, newState);
        }

        // 世界基準(SRS)の壁蹴りデータ（Tミノ、J, L, S, Z型用）
        // 状態の変化 [oldState->newState] に応じた5つのずらし候補(X, Y)
        function getSRSOffsets(oldState, newState) {
            // [oldState][newState] の組み合わせごとのOffsetデータ
            const key = `${oldState}->${newState}`;
            const srsTable = {
                "0->1": [[0,0], [-1,0], [-1,-1], [0,2], [-1,2]],
                "1->0": [[0,0], [1,0], [1,1], [0,-2], [1,-2]],
                "1->2": [[0,0], [1,0], [1,1], [0,-2], [1,-2]],
                "2->1": [[0,0], [-1,0], [-1,-1], [0,2], [-1,2]],
                "2->3": [[0,0], [1,0], [1,-1], [0,2], [1,2]],
                "3->2": [[0,0], [-1,0], [-1,1], [0,-2], [-1,-2]],
                "3->0": [[0,0], [-1,0], [-1,1], [0,-2], [-1,-2]],
                "0->3": [[0,0], [1,0], [1,-1], [0,2], [1,2]]
            };
            // 該当するパターンがない場合は通常の簡易Offsetを返す
            return srsTable[key] || [[0,0], [1,0], [-1,0], [0,-1]];
        }

        // SRS基準でねじり込み回転を試す関数
        function attemptRotationSRS(nextP, oldState, newState) {
            // 1型以外のブロックは世界基準のSRSテーブルを使用
            const offsets = getSRSOffsets(oldState, newState);

            for (let i = 0; i < offsets.length; i++) {
                // offsets[i][1] はY軸の移動。テトリスは下方向が+なので符号に注意
                let testX = blockX + offsets[i][0];
                let testY = blockY + offsets[i][1]; // SRS規格のY反転を補正

                // 衝突しなければ回転確定（潜り込み成功）
                if (!checkCollision(testX, testY, nextP)) {
                    blockX = testX;
                    blockY = testY;
                    currentPiece = nextP;
                    rotationState = newState; // 回転状態を更新
                    return;
                }
            }
        }
        // --- ここまで ---



        function updateTimer() {
            clearInterval(gameInterval);
            gameInterval = setInterval(() => {
                if (!checkCollision(blockX, blockY + 1, currentPiece)) {
                    blockY++;
                } else {
                    lockPiece();
                    clearLines();
                    spawnPiece();
                }
                draw();
            }, currentSpeed);
        }

        function draw() {
            ctx.fillStyle = "#000";
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            for (let r = 0; r < ROWS; r++) {
                for (let c = 0; c < COLS; c++) {
                    if (board[r][c]) {
                        drawBlock(ctx, c, r, board[r][c]);
                    }
                }
            }
            for (let r = 0; r < currentPiece.length; r++) {
                for (let c = 0; c < currentPiece[r].length; c++) {
                    if (currentPiece[r][c]) {
                        drawBlock(ctx, blockX + c, blockY + r, currentType);
                    }
                }
            }
        }

        function drawNext() {
            nextCtx.fillStyle = "#000";
            nextCtx.fillRect(0, 0, nextCanvas.width, nextCanvas.height);
            
            let p = nextPiece;
            let offsetX = (nextCanvas.width - p.length * BLOCK_SIZE) / 2;
            let offsetY = (nextCanvas.height - p.length * BLOCK_SIZE) / 2;

            for (let r = 0; r < p.length; r++) {
                for (let c = 0; c < p[r].length; c++) {
                    if (p[r][c]) {
                        nextCtx.fillStyle = COLORS[nextType];
                        nextCtx.fillRect(offsetX + c * BLOCK_SIZE, offsetY + r * BLOCK_SIZE, BLOCK_SIZE - 1, BLOCK_SIZE - 1);
                    }
                }
            }
        }

        function drawBlock(context, x, y, type) {
            context.fillStyle = COLORS[type];
            context.fillRect(x * BLOCK_SIZE, y * BLOCK_SIZE, BLOCK_SIZE - 1, BLOCK_SIZE - 1);
        }

        window.addEventListener("keydown", (e) => {
            if (e.key === "ArrowLeft" && !checkCollision(blockX - 1, blockY, currentPiece)) blockX--;
            if (e.key === "ArrowRight" && !checkCollision(blockX + 1, blockY, currentPiece)) blockX++;
            if (e.key === "ArrowDown" && !checkCollision(blockX, blockY + 1, currentPiece)) blockY++;
            
            if (e.key === "ArrowUp") {
                while (!checkCollision(blockX, blockY + 1, currentPiece)) {
                    blockY++;
                }
                lockPiece();
                clearLines();
                spawnPiece();
            }
            
            if (e.key === " " || e.key === "Spacebar") rotatePiece();
            if (e.key === "z" || e.key === "Z") rotatePieceCCW(); 
            if (e.key === "c" || e.key === "C" || e.key === "Shift") holdPiece();

            draw();
        });


        drawNext();
        updateTimer();
        draw();
    </script>
</body>
</html>


