<html>
    <head>
        <title>GCSE Music Quiz</title>
        
        <style>
            /*answer button class (. = class, # = id) */
            Body {
                background-color: seashell;
                height: 100%;
                width: 100%;
                
            }
        #questionBox {
            position: absolute;
            font-family: 'Century Gothic', futura, 'URW Gothic L', Verdana, sans-serif;
            margin: 20px;
            font-size: 35px;
            text-align: centre;
        }
        #musicPlayer {
            position: absolute;
            bottom: 210px;
            width: 100%;
        }
        .answerButtons {
            background-color: beige;
            position: absolute;
            height: 50px;
            width: 100%;
            font-family:'Century Gothic', futura, 'URW Gothic L', Verdana, sans-serif;
            font-size: 20px;
            font-weight: 900;
            letter-spacing: 0.5px;
            
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
        
        <script src="Tone.js"></script>
        
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
                setupSlide("Which of these timbres best describes the music?","Metallic", "Harsh", "Boomy", "Mellow", "audio9.wav");
                correctButton = 3;
            }
            else if(slideNumber == 9)
            {
                setupSlide("Name the vocal effect used in the performance?", "Tremolo", "Harmony", "Vibrato", "Whispering", "audio10.mp3");
                correctButton = 2;
            }
            else
            {
                if (correctAnswerCount == 10){
                    setupSlide("Your score was: " + correctAnswerCount + "/10, congratulations!","","","","","");
                    
                }
                else {
                   setupSlide("Your score was: " + correctAnswerCount + "/10.\n\n Keep playing until you get full marks.\nRefresh the page and retry","","","","","");
                   
                }
            }
            
            
            
            
        }
        
        
        function checkResult(buttonID)
        {
            if(buttonID == correctButton)
            {
                
                audioPlayer.pause();
                playFromBufferNumber("correct.mp3");
                //go to next slide and increment correct answer
                slideNumber ++;
                correctAnswerCount ++;
                
                //alert("Correct!");
            }
            else
            {
                audioPlayer.pause();
                playFromBufferNumber("incorrect.wav");
               
                //goto next slide
                slideNumber ++;
                //alert("Incorrect!");
                
            }
            loadSlide(slideNumber);
        }
        
        function playFromBufferNumber(song)
        {
            var song = song;
            var player = new Tone.Player({
                                         "url" : song,
                                         "autostart" : true
                                         }).toMaster();
            player.autostart = true;
            
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
            if (slideNumber == 10){
                answers[0].style.visibility = "hidden";
                answers[1].style.visibility = "hidden";
                answers[2].style.visibility = "hidden";
                answers[3].style.visibility = "hidden";
                Track.style.visibility = "hidden";
            }
        }
        
            </script>
        
    </body>
