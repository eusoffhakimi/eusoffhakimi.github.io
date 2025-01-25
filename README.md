<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Timewatch</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            margin: 0;
            background-color: red;
        }

        h1{
            font-size: 50px;
            text-align: center;
            color: #f7e13b;
        }

        #time-display {
            font-size: 3rem;
            font-weight: bold;
            margin-bottom: 20px;
        }

        .button {
            padding: 10px 20px;
            margin: 5px;
            font-size: 1.2rem;
            cursor: pointer;
            border: none;
            border-radius: 5px;
            color: white;
        }

        .start-stop {
            background-color: #007bff;
        }

        .reset {
            background-color: #28a745;
        }

        .button:active {
            transform: scale(0.98);
        }
    </style>
</head>
<body>
    <h1>CHUCKLES CHALLENGE</h1>
    <div id="time-display" style="color: black;">00:00:00</div>
    <button id="start-stop-btn" class="button start-stop">Start</button>
    <button id="reset-btn" class="button reset">Reset</button>

    <script>
        let timerInterval = null;
        let elapsedTime = 0; // Time in milliseconds
        let running = false;
        const timeDisplay = document.getElementById('time-display');
        const startStopBtn = document.getElementById('start-stop-btn');
        const resetBtn = document.getElementById('reset-btn');

        // Speed control (1 = normal speed, 0.5 = 2x faster, etc.)
        const speed = 1; // Change this value to modify speed

        // Update time display
        function updateTimeDisplay() {
            const hours = Math.floor(elapsedTime / 3600000);
            const minutes = Math.floor((elapsedTime % 3600000) / 60000);
            const seconds = Math.floor((elapsedTime % 60000) / 1000);

            timeDisplay.textContent =
                `${hours.toString().padStart(2, '0')}:${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
        }

        // Start/Stop the stopwatch
        startStopBtn.addEventListener('click', () => {
            if (running) {
                clearInterval(timerInterval);
                running = false;
                startStopBtn.textContent = 'Start';
            } else {
                timerInterval = setInterval(() => {
                    elapsedTime += 1000 * speed; // Increment time based on speed
                    updateTimeDisplay();
                }, 0.5);
                running = true;
                startStopBtn.textContent = 'Stop';
            }
        });

        // Reset the stopwatch
        resetBtn.addEventListener('click', () => {
            clearInterval(timerInterval);
            elapsedTime = 0;
            running = false;
            startStopBtn.textContent = 'Start';
            updateTimeDisplay();
        });

        // Initial display update
        updateTimeDisplay();

        // Developer customization for font color
        // Change the color to your desired value
        timeDisplay.style.color = '#f5e9e9';
    </script>
</body>
</html>
