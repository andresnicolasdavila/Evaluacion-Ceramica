<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Evaluación Ceramista</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f3f4f6; /* Light gray background */
        }
        /* Custom styles for better aesthetics */
        .card {
            background-color: #ffffff;
            border-radius: 1rem; /* More rounded corners */
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
            padding: 2.5rem;
        }
        .input-field, .textarea-field, .select-field {
            width: 100%;
            padding: 0.75rem;
            border: 1px solid #d1d5db; /* Light gray border */
            border-radius: 0.5rem; /* Rounded input fields */
            font-size: 1rem;
            transition: border-color 0.2s;
        }
        .input-field:focus, .textarea-field:focus, .select-field:focus {
            outline: none;
            border-color: #6366f1; /* Indigo focus color */
            box-shadow: 0 0 0 3px rgba(99, 102, 241, 0.2);
        }
        .btn-primary {
            background-color: #6366f1; /* Indigo button */
            color: #ffffff;
            padding: 0.75rem 1.5rem;
            border-radius: 0.75rem; /* More rounded button */
            font-weight: 600;
            transition: background-color 0.2s, transform 0.1s;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
        }
        .btn-primary:hover {
            background-color: #4f46e5; /* Darker indigo on hover */
            transform: translateY(-1px); /* Slight lift effect */
        }
        .btn-primary:active {
            transform: translateY(0); /* Press down effect */
        }
        .rating-label {
            font-weight: 600;
            color: #374151; /* Darker gray for labels */
        }
        .video-container {
            position: relative;
            width: 100%;
            padding-bottom: 56.25%; /* 16:9 Aspect Ratio */
            height: 0;
            overflow: hidden;
            border-radius: 0.75rem;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
        }
        .video-container iframe {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
        }
        .message-box {
            background-color: #ecfdf5; /* Light green for success */
            border: 1px solid #a7f3d0; /* Green border */
            color: #065f46; /* Dark green text */
            padding: 1rem;
            border-radius: 0.5rem;
            margin-top: 1.5rem;
            text-align: center;
            font-weight: 500;
        }
        .loading-spinner {
            border: 4px solid rgba(0, 0, 0, 0.1);
            border-left-color: #6366f1;
            border-radius: 50%;
            width: 24px;
            height: 24px;
            animation: spin 1s linear infinite;
            margin: 0 auto;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
    </style>
</head>
<body class="flex items-center justify-center min-h-screen p-4 sm:p-6 lg:p-8">
    <div class="w-full max-w-2xl card">
        <h1 class="text-3xl sm:text-4xl font-bold text-center text-gray-800 mb-8">
            Evaluacion Ceramista COEF
        </h1>

        <!-- Video Information Display Section (Always visible) -->
        <div id="videoInfo" class="mb-8 p-6 bg-blue-50 rounded-lg border border-blue-200">
            <h2 class="text-2xl font-semibold text-blue-800 mb-4">Video de YouTube:</h2>
            <div id="videoContainer" class="video-container">
                <!-- YouTube video will be loaded here by the API -->
                <div id="youtubeVideoFrame"></div>
            </div>
        </div>

        <!-- Evaluation Form -->
        <form id="evaluationForm">
            <h2 class="text-2xl font-semibold text-gray-800 mb-6 text-center">Evaluar el Video</h2>

            <!-- Nombre y Apellido -->
            <div class="mb-6">
                <label for="Nombre" class="block rating-label mb-2">
                    Nombre:
                </label>
                <input
                    type="text"
                    id="Nombre"
                    name="Nombre"
                    placeholder="Tu nombre"
                    class="input-field"
                    required
                />
            </div>
            <div class="mb-6">
                <label for="Apellido" class="block rating-label mb-2">
                    Apellido:
                </label>
                <input
                    type="text"
                    id="Apellido"
                    name="Apellido"
                    placeholder="Tu apellido"
                    class="input-field"
                    required
                />
            </div>

            <!-- Email -->
            <div class="mb-6">
                <label for="Email" class="block rating-label mb-2">
                    Correo Electrónico:
                </label>
                <input
                    type="email"
                    id="Email"
                    name="Email"
                    placeholder="tu.correo@ejemplo.com"
                    class="input-field"
                    required
                />
            </div>

            <!-- Base de colocacion -->
            <div class="mb-6">
                <label for="Base_de_colocacion" class="block rating-label mb-2">
                    1. Base de colocacion:
                </label>
                <select id="Base_de_colocacion" name="Base de colocacion" class="select-field" required>
                    <option value="">Seleccione una calificación</option>
                    <option value="1 - Bien limpio y algunas asperezas del contrapiso solamente">1 - Bien limpio y algunas asperezas del contrapiso solamente</option>
                    <option value="2 - Barriendo un poco es suficiente">2 - Barriendo un poco es suficiente </option>
                    <option value="3 - Da igual, el pegamento bueno siempre pega bien">3 - Da igual, el pegamento bueno siempre pega bien</option>
                </select>
            </div>

            <!-- Escuadras -->
            <div class="mb-6">
                <label for="Escuadras" class="block rating-label mb-2">
                    2. Escuadras:
                </label>
                <select id="Escuadras" name="Escuadras" class="select-field" required>
                    <option value="">Seleccione una calificación</option>
                    <option value="1 - Hilos formando escuadra perfecta 90°en ancho y largo">1 - Hilos formando escuadra perfecta 90°en ancho y largo </option>
                    <option value="2 - Sin hilos , solo hace mas lenta la tarea">2 - Sin hilos , solo hace mas lenta la tarea</option>
                    <option value="3 - Haciendo una tirada a lo largo con una sola pared">3 - Haciendo una tirada a lo largo con una sola pared</option>
                </select>
            </div>

            <!-- Colocacion ceramico -->
            <div class="mb-6">
                <label for="Colocacion_ceramico" class="block rating-label mb-2">
                    3. Colocacion ceramico:
                </label>
                <select id="Colocacion_ceramico" name="Colocacion ceramico" class="select-field" required>
                    <option value="">Seleccione una calificación</option>
                    <option value="1 - Ponemos una linea horizontal y los recortes con cada linea hasta llegar a la puerta">1 - Ponemos una linea horizontal y los recortes con cada linea hasta llegar a la puerta</option>
                    <option value="2 - Se coloca desde el final hacia la puerta de ingreso">2 - Se coloca desde el final hacia la puerta de ingreso</option>
                    <option value="3 - Alineados en escuadra con los hilos desde el ingreso se coloca completo en escuadra en lo largo y ancho y los recortes al final">3 - Alineados en escuadra con los hilos desde el ingreso se coloca completo en escuadra en lo largo y ancho y los recortes al final</option>
                    <option value="4 - Da igual mientras el dibujo quede bien">4 - Da igual mientras el dibujo quede bien</option>
                </select>
            </div>

            <!-- Juntas -->
            <div class="mb-6">
                <label for="Juntas" class="block rating-label mb-2">
                    4. Juntas :
                </label>
                <select id="Juntas" name="Juntas" class="select-field" required>
                    <option value="">Seleccione una calificación</option>
                    <option value="1 - Sin juntas para que quede mas perfecto">1 - Sin juntas para que quede mas perfecto</option>
                    <option value="2 - Con junta sin separador , a ojo es suficiente">2 - Con junta sin separador , a ojo es suficiente</option>
                    <option value="3 - Se usa separador con nivelador tipo cuña">3 - Se usa separador con nivelador tipo cuña</option>
                </select>
            </div>

            <!-- Preparacion de Pegamento -->
            <div class="mb-6">
                <label for="Preparacion_de_Pegamento" class="block rating-label mb-2">
                    5. Preparacion de Pegamento:
                </label>
                <select id="Preparacion_de_Pegamento" name="Preparacion de Pegamento" class="select-field" required>
                    <option value="">Seleccione una calificación</option>
                    <option value="1 - Se prepara mucho y se va usando">1 - Se prepara mucho y se va usando</option>
                    <option value="2 - Se prepara por habitacion a hacer respetando dosificiacion indicada en la bolsa o por capataz">2 - Se prepara por habitacion a hacer respetando dosificiacion indicada en la bolsa o por capataz</option>
                    <option value="3 - Se prepara hasta que quede homogenea y se endurece se le pone agua">3 - Se prepara hasta que quede homogenea y se endurece se le pone agua</option>
                </select>
            </div>

            <!-- General Comments -->
            <div class="mb-8">
                <label for="Comentarios_Adicionales" class="block rating-label mb-2">
                    Comentarios Adicionales:
                </label>
                <textarea
                    id="Comentarios_Adicionales"
                    name="Comentarios Adicionales"
                    rows="5"
                    placeholder="Escriba aquí cualquier comentario adicional sobre el video..."
                    class="textarea-field"
                ></textarea>
            </div>

            <div class="flex justify-center">
                <button type="submit" class="btn-primary w-full sm:w-auto">
                    Enviar Evaluación
                </button>
            </div>
        </form>

        <!-- Message Box for Submission Confirmation -->
        <div id="messageBox" class="message-box hidden">
            ¡Gracias por tu evaluación!
        </div>
        <div id="loadingMessage" class="message-box hidden bg-blue-100 border-blue-200 text-blue-700">
            <div class="loading-spinner"></div>
            <p class="mt-2">Enviando evaluación...</p>
        </div>
    </div>

    <script>
        // 1. Load the IFrame Player API code asynchronously.
        var tag = document.createElement('script');
        tag.src = "https://www.youtube.com/iframe_api";
        var firstScriptTag = document.getElementsByTagName('script')[0];
        firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);

        var player; // Global variable to hold the YouTube player object
        const VIDEO_ID = '9p-NReM4Yls'; // The fixed YouTube video ID

        // 2. This function creates an <iframe> (and YouTube player)
        //    after the API code downloads.
        function onYouTubeIframeAPIReady() {
            player = new YT.Player('youtubeVideoFrame', {
                videoId: VIDEO_ID,
                playerVars: {
                    'autoplay': 1, // Autoplay the video
                    'controls': 1, // Show player controls
                    'rel': 0, // Do not show related videos
                    'modestbranding': 1 // Use a minimalist YouTube logo
                },
                events: {
                    'onReady': onPlayerReady,
                    'onStateChange': onPlayerStateChange
                }
            });
        }

        // 3. The API will call this function when the video player is ready.
        function onPlayerReady(event) {
            // The video should autoplay due to playerVars, but explicitly call playVideo just in case.
            event.target.playVideo();

            // Setup Intersection Observer after player is ready
            const videoContainer = document.getElementById('videoContainer');
            if (videoContainer) {
                const options = {
                    root: null, // Use the viewport as the root
                    rootMargin: '0px',
                    threshold: 0.5 // Trigger when 50% of the video is visible
                };

                const videoObserver = new IntersectionObserver((entries, observer) => {
                    entries.forEach(entry => {
                        if (player) { // Ensure player object exists
                            if (entry.isIntersecting) {
                                // Video is in view, play it if not already playing
                                if (player.getPlayerState() !== YT.PlayerState.PLAYING && player.getPlayerState() !== YT.PlayerState.BUFFERING) {
                                    player.playVideo();
                                }
                            } else {
                                // Video is out of view, pause it if playing
                                if (player.getPlayerState() === YT.PlayerState.PLAYING) {
                                    player.pauseVideo();
                                }
                            }
                        }
                    });
                }, options);

                videoObserver.observe(videoContainer);
            }
        }

        // 4. The API calls this function when the player's state changes.
        //    The function indicates that when playing a video (state=1),
        //    the player should play for six seconds and then stop.
        function onPlayerStateChange(event) {
            // No specific action needed here for autoplay/pause on scroll,
            // but this function is part of the standard YouTube API setup.
        }

        document.addEventListener('DOMContentLoaded', () => {
            const evaluationForm = document.getElementById('evaluationForm');
            const messageBox = document.getElementById('messageBox');
            const loadingMessage = document.getElementById('loadingMessage');

            // IMPORTANT: Replace 'TU_URL_DE_APLICACION_WEB_AQUI' with your actual Google Apps Script Web App URL
            const SCRIPT_URL = 'https://script.google.com/macros/s/AKfycbzMg4qSG2Jw7EJsTKY7JhuTDFNbfwKkm1Hdd5ByRv7v-S9cnJQvAQqOiErRmuur9mnM/exec';
            console.log('SCRIPT_URL utilizada:', SCRIPT_URL); // Log the URL for debugging

            // Function to display custom message box
            function displayMessageBox(message, type) {
                loadingMessage.classList.add('hidden'); // Hide loading message
                messageBox.textContent = message;
                messageBox.classList.remove('hidden');
                if (type === 'success') {
                    messageBox.style.backgroundColor = '#ecfdf5';
                    messageBox.style.borderColor = '#a7f3d0';
                    messageBox.style.color = '#065f46';
                } else if (type === 'error') {
                    messageBox.style.backgroundColor = '#fee2e2';
                    messageBox.style.borderColor = '#fca5a5';
                    messageBox.style.color = '#991b1b';
                }
            }

            // Handle form submission
            evaluationForm.addEventListener('submit', async (event) => {
                event.preventDefault(); // Prevent default form submission

                messageBox.classList.add('hidden'); // Hide previous messages
                loadingMessage.classList.remove('hidden'); // Show loading message

                const formData = new FormData(evaluationForm);
                const data = {};
                // Use the 'name' attribute for form fields to match Google Apps Script 'e.parameter'
                // Ensure names match your Google Sheet headers exactly for correct mapping
                data['Nombre'] = formData.get('Nombre');
                data['Apellido'] = formData.get('Apellido');
                data['Email'] = formData.get('Email'); // New email field
                data['Base de colocacion'] = formData.get('Base de colocacion'); // Changed name attribute
                data['Escuadras'] = formData.get('Escuadras');
                data['Colocacion ceramico'] = formData.get('Colocacion ceramico'); // Changed name attribute
                data['Juntas'] = formData.get('Juntas');
                data['Preparacion de Pegamento'] = formData.get('Preparacion de Pegamento'); // Changed name attribute
                data['Comentarios Adicionales'] = formData.get('Comentarios Adicionales'); // Changed name attribute

                try {
                    const response = await fetch(SCRIPT_URL, {
                        method: 'POST',
                        mode: 'no-cors', // Required for Google Apps Script web app
                        headers: {
                            'Content-Type': 'application/x-www-form-urlencoded',
                        },
                        body: new URLSearchParams(data).toString(), // Encode data as URL-encoded string
                    });

                    // Since mode is 'no-cors', we can't directly read the response body.
                    // We assume success if no network error occurred.
                    displayMessageBox('¡Gracias por tu evaluación! Se ha enviado correctamente.', 'success');
                    evaluationForm.reset(); // Clear the form
                } catch (error) {
                    console.error('Error al enviar la evaluación:', error);
                    displayMessageBox('Hubo un error al enviar tu evaluación. Por favor, inténtalo de nuevo. Revisa la consola para más detalles.', 'error');
                }
            });
        });
    </script>
</body>
</html>
