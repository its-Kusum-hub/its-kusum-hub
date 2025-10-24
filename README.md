## Hi there 👋
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Typing Effect Profile</title>
    <!-- Load Tailwind CSS for styling -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Load Google Font 'Inter' -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700;900&display=swap" rel="stylesheet">

    <style>
        /* Base font for the page */
        body {
            font-family: 'Inter', sans-serif;
        }

        /* The blinking cursor */
        .cursor {
            display: inline-block;
            width: 3px;
            /* Height will be based on the font size of its parent */
            height: 1.1em; 
            /* A blue color matching the text */
            background-color: #2563eb; 
            /* Aligns the cursor with the text baseline */
            vertical-align: text-bottom;
            /* The blink animation */
            animation: blink 0.7s infinite;
        }

        /* The container for the typing text needs a minimum height
           so the layout doesn't jump as text appears/disappears */
        #typing-container {
            min-height: 1.2em; /* 1.2 * font-size */
        }

        /* Animation keyframes */
        @keyframes blink {
            0%, 100% {
                opacity: 1;
            }
            50% {
                opacity: 0;
            }
        }
    </style>
</head>
<body class="bg-gray-100 text-gray-900 min-h-screen flex items-center justify-center p-4">

    <!-- Main content card -->
    <div class="w-full max-w-2xl p-8">
        
        <!-- Line 1: B.Tech (This will type once) -->
        <h3 id="line-1" class="text-3xl md:text-4xl font-semibold text-blue-600 mb-2"></h3>
        
        <!-- Line 2: The looping typewriter effect -->
        <!-- We use a container to set a min-height, preventing layout shift -->
        <div id="typing-container" class="text-4xl md:text-6xl font-black text-gray-900 mb-12">
            <!-- The JavaScript will target this span -->
            <span id="typing-text"></span>
            <!-- The initial cursor -->
            <span class="cursor"></span>
        </div>

        <!-- The "About Me" section, styled to look like the image -->
        <h2 class="text-2xl font-bold mb-4">About Me:</h2>
        
        <ul class="space-y-2 text-base md:text-lg text-gray-700">
            <li class="flex items-center">
                <span class="mr-2">🎓</span>
                <span>B.Tech CSE Student | Full-Stack Developer</span>
            </li>
            <li class="flex items-center">
                <span class="mr-2">💻</span>
                <span>Passionate about Frontend with React.js</span>
            </li>
            <li class="flex items-center">
                <span class="mr-2">🐍</span>
                <span>Python Enthusiast</span>
            </li>
            <li class="flex items-center">
                <span class="mr-2">🚀</span>
                <span>Currently Building MERN & Django Projects</span>
            </li>
             <li class="flex items-center">
                <span class="mr-2">💡</span>
                <span>Tech Explorer | Problem Solver | Lifelong Learner</span>
            </li>
             <li class="flex items-center">
                <span class="mr-2">🎯</span>
                <span>Focused on Career Growth & Real-World Projects</span>
            </li>
        </ul>

    </div>

    <script>
        // --- Configuration ---
        const line1Target = document.getElementById('line-1');
        const typingTarget = document.getElementById('typing-text');
        
        const line1Text = "B.Tech";
        // Add all the phrases you want to loop through here
        const phrases = [
            "Mohammad Waris",
            "A Full-Stack Developer",
            "A Python Enthusiast",
            "A Lifelong Learner"
        ];

        const typeSpeed = 100; // Time (in ms) between typing each letter
        const deleteSpeed = 50; // Time (in ms) between deleting each letter
        const line1Delay = 500; // Delay (in ms) after "B.Tech" finishes
        const phraseLoopDelay = 1500; // Delay (in ms) after a word is typed, before deleting

        // --- State Variables ---
        let line1Index = 0;
        let phraseIndex = 0;
        let letterIndex = 0;
        let isDeleting = false;

        // --- Function to type "B.Tech" ---
        function typeLine1() {
            if (line1Index < line1Text.length) {
                // Type one letter
                line1Target.textContent += line1Text.charAt(line1Index);
                line1Index++;
                setTimeout(typeLine1, typeSpeed);
            } else {
                // Finished typing, wait a bit, then start the main loop
                setTimeout(typeLoop, line1Delay);
            }
        }

        // --- Main Looping Typewriter Function ---
        function typeLoop() {
            const currentPhrase = phrases[phraseIndex];
            let speed = isDeleting ? deleteSpeed : typeSpeed;

            if (isDeleting) {
                // Deleting
                typingTarget.textContent = currentPhrase.substring(0, letterIndex - 1);
                letterIndex--;
            } else {
                // Typing
                typingTarget.textContent = currentPhrase.substring(0, letterIndex + 1);
                letterIndex++;
            }

            // Always show the cursor at the end
            typingTarget.innerHTML = typingTarget.textContent + '<span class="cursor"></span>';

            // --- Logic to change state (typing/deleting) ---

            // 1. If NOT deleting and word is complete
            if (!isDeleting && letterIndex === currentPhrase.length) {
                speed = phraseLoopDelay; // Pause at end of word
                isDeleting = true; // Start deleting next
            } 
            // 2. If deleting and word is fully deleted
            else if (isDeleting && letterIndex === 0) {
                isDeleting = false; // Start typing next
                phraseIndex = (phraseIndex + 1) % phrases.length; // Move to next phrase
            }

            // Schedule the next "keystroke"
            setTimeout(typeLoop, speed);
        }

        // --- Start the animation when the page loads ---
        document.addEventListener('DOMContentLoaded', () => {
            // Start by typing "B.Tech"
            typeLine1();
        });
    </script>

</body>
</html>
