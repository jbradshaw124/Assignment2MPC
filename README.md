<html>
    <head>
        <title>GCSE Music Quiz</title>
        
        <style>
           /*answer button class (. = class, # = id) */
            Body {
                background-color: #fdf;
                height: 100%;
                width: 100%;
                
            }
            #questionBox {
                position: absolute;
                font-family: 'Century Gothic', futura, 'URW Gothic L', Verdana, sans-serif;
                margin: 20px;
                font-size: 35px;
            }
            #musicPlayer {
                position: absolute;
                bottom: 210px;  
                height: 60px;
                width: 10%;
            }
            .answerButtons {
                background-color: beige;
                position: absolute;
                height: 50px;
                width: 100%;
                font-family:'Century Gothic', futura, 'URW Gothic L', Verdana, sans-serif;
                font-size: 20px;
            }
            #answerA {
                bottom: 160px; 
            }
            #answerB {
                bottom: 110px; 
            }
            #answerC {
                bottom: 60px; 
            }
            #answerD {
                bottom: 10px; 
            }
        </style>
        
        <script src="AudioBufferManager.js"></script>
        
    </head>
    <body width="100%" height="100%">
        <!--Slide Body-->

        <div id= "slideBody">
        
            <div id= "questionBox">
                question
            </div>
            <div id= "musicPlayer">
                <audio controls id="audioPlayer"></audio>
            </div>
            <!--<div id= "answerCheck">
                
            </div>-->
            <div id="answerBox">
                    <button id="answerA" class="answerButtons" onclick="checkResult(0)"></button>
                    <br />
                    <button id="answerB" class="answerButtons" onclick="checkResult(1)"></button>
                    <br />
                    <button id="answerC" class="answerButtons" onclick="checkResult(2)"></button>
                    <br />
                    <button id="answerD" class="answerButtons" onclick="checkResult(3)"></button>
                
            </div>
        
        </div>



        <script>
            //this is where script goes

        // we need an audio context to use the web audio API
        var audioContext = new (window.AudioContext || window.webkitAudioContext)();
    
        // this audioBufferManager makes it convenient to load audio files
        var audioBufferManager = new AudioBufferManager(audioContext);

        //TODO: need to add a variable for number of slides

        var correctButton = 0;
        var slideNumber = 0;
        var correctAnswerCount = 0;

        window.onload = function() {
        //first slide
        loadSlide(0);
        };

 
        // load slides depending on slide number
        function loadSlide(slideNumber)
        {
            var musicPlayer = document.getElementById("musicPlayer");
            //answerCheck.innerHTML = "";
            var songFile;
            
            
                if(slideNumber == 0)
            {
                correctAnswerCount = 0;
                setupSlide("What woodwind instrument can be heard here?","Flute", "Clarinet", "Bassoon", "Oboe", "audio1.wav");
                correctButton = 3;
            }
            else if(slideNumber == 1)
            {
                setupSlide("Identify the time signature of this piece","4/4", "3/4", "6/8", "12/8", "audio2.mp3");
                correctButton = 1;
            }
            else if(slideNumber == 2)
            {
                setupSlide("What era was this piece written in?","Romantic", "20th Century", "Classical", "Baroque", "audio3.wav");
                correctButton = 0;
            }
            else if(slideNumber == 3)
            {
                setupSlide("Name the composer of this piece","Ludwig Van Beethoven", "Wolfgang Amadeus Mozart", "Johann Sebastian Bach", "George Frideric Handel", "audio4.wav");
                correctButton = 2;
            }
            else if(slideNumber == 4)
            {
                setupSlide("Name the music interval heard here","major 3rd", "Perfect 4th", "Perfect 5th", "Augmented 5th", "audio5.wav");
                correctButton = 1;
            }
            else if(slideNumber == 5)
            {
                setupSlide("What type of music is this?","Disco", "Tango", "Waltz", "Country and Western", "audio6.wav");
                correctButton = 1;
            }
            else if(slideNumber == 6)
            {
                setupSlide("Which term best describes the tempo of the piece?", "Andante", "Allegro", "Presto", "Lento", "audio7.wav");
                correctButton = 2;
            }
            else if(slideNumber == 7)
            {
                setupSlide("Which percussion instrument can be heard here?","Marimba", "Timpani", "Xylophone", "Glockenspeil", "audio8.wav");
                correctButton = 0;
            }
            else if(slideNumber == 8)
            {
                setupSlide("Which of these timbres best describes the music?","Metallic", "Harsh", "Boomy", "Warm", "audio9.wav");
                correctButton = 3;
            }
            else if(slideNumber == 9)
            {
                setupSlide("Name the vocal effect used in the performance?", "Tremolo", "Harmony", "Vibrato", "Whispering", "audio10.mp3");
                correctButton = 2;
            }

            else
            {
                songFile = "audioFile.mp3";
                if (correctAnswerCount == 10){
                    alert("Your score was: " + correctAnswerCount + "/10, congratulations!\nClick close to retry");
                    slideNumber = 10;
                    
                }
                else {
                    alert("Your score was: " + correctAnswerCount + "/10. Keep playing until you get full marks.\nClick close to retry");
                    slideNumber = 0;
                }
            }
            
            
            
            
        }

        function checkResult(buttonID)
        {
            if(buttonID == correctButton)
            {
                /*audio should play here but it doesnt work
                playFromBufferNumber("correct.mp3");*/
                alert("Correct!");
                //go to next slide and increment correct answer
                slideNumber ++;
                correctAnswerCount ++;
            }
            else if(buttonID != correctButton)

            {
                //var answerCheck = document.getElementById("answerCheck");
                //answerCheck.innerHTML = "Incorrect!";
                
                //playFromBufferNumber(incorrect.mp3);
                alert("Incorrect!");
                //goto next slide
                slideNumber ++;
        
            }
            loadSlide(slideNumber);
        }

        function playFromBufferNumber(song)
        {
            var currentBuffer = 1;
            audioBufferManager.createBufferFor(song);
            audioBufferManager.buffers[0];
    
            var audioSource = audioContext.createBufferSource();
            audioSource.buffer = audioBufferManager.buffers[currentBuffer];
            audioSource.connect(audioContext.destination);
            audioSource.start(0);
    
        }

        function setupSlide(question,answerA,answerB,answerC,answerD, songFile)
        {
            // initialising buttons for answers
            var answers = [];
             answers[0] = document.getElementById("answerA");
             answers[1] = document.getElementById("answerB");
             answers[2] = document.getElementById("answerC");
             answers[3] = document.getElementById("answerD");
             // initialising audio player for file
             var Track = document.getElementById("audioPlayer");
            
            //initialising question box
            var questionBox = document.getElementById("questionBox");
            
            //setting text in question/answer box
            questionBox.innerHTML = question;
            answers[0].innerHTML = answerA;
            answers[1].innerHTML = answerB;
            answers[2].innerHTML = answerC;
            answers[3].innerHTML = answerD;
            //adding file to source parameter of audio player
            Track.src = songFile;
        }
        
        </script>

    </body>
</html>
