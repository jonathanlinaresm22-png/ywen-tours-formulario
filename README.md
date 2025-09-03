<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Generador de Recibos Ywen Tours</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f7f9fc;
            color: #333;
            line-height: 1.6;
        }
        .container {
            max-width: 800px;
            margin: 1.5rem auto;
            padding: 1.5rem;
            background-color: #fff;
            border-radius: 12px;
            box-shadow: 0 6px 20px rgba(0, 0, 0, 0.08);
            transition: all 0.3s ease-in-out;
        }
        @media (min-width: 768px) {
            .container {
                margin: 2rem auto;
                padding: 2rem;
            }
        }
        .form-section {
            display: none;
            opacity: 0;
            transition: opacity 0.5s ease-in-out;
        }
        .form-section.active {
            display: block;
            opacity: 1;
        }
        .form-field {
            margin-bottom: 1.25rem;
        }
        label {
            display: block;
            font-weight: 600;
            margin-bottom: 0.5rem;
            color: #4b5563;
            font-size: 0.95rem;
        }
        input[type="text"], select, input[type="date"], textarea {
            width: 100%;
            padding: 0.75rem;
            border: 1px solid #e5e7eb;
            border-radius: 8px;
            font-size: 1rem;
            transition: all 0.2s ease-in-out;
            background-color: #f9fafb;
        }
        input[type="number"] {
            -webkit-appearance: textfield;
            -moz-appearance: textfield;
            appearance: textfield;
            width: 100%;
            font-size: 1rem;
            border: none;
            outline: none;
            padding: 0;
            background-color: transparent;
        }
        input[type="number"]::-webkit-inner-spin-button,
        input[type="number"]::-webkit-outer-spin-button {
            -webkit-appearance: none;
            margin: 0;
        }
        input[type="text"]:focus, input[type="number"]:focus, select:focus, input[type="date"]:focus, textarea:focus {
            border-color: #3b82f6;
            box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.25);
            outline: none;
            background-color: #fff;
        }
        .button {
            display: inline-block;
            padding: 0.75rem 1.5rem;
            background-color: #2563eb;
            color: #fff;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            transition: background-color 0.2s ease-in-out, transform 0.1s ease-in-out;
            font-weight: 600;
            letter-spacing: 0.05em;
        }
        .button:hover {
            background-color: #1d4ed8;
            transform: translateY(-2px);
        }
        .button:active {
            transform: translateY(0);
        }
        .radio-group {
            display: flex;
            flex-wrap: wrap;
            gap: 1rem;
            margin-bottom: 1.5rem;
        }
        .radio-group label {
            background-color: #eef2ff;
            color: #4338ca;
            padding: 0.75rem 1.5rem;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.2s ease-in-out;
            border: 1px solid #c7d2fe;
            font-weight: 500;
            flex-grow: 1;
            text-align: center;
        }
        .radio-group input:checked + label {
            background-color: #3b82f6;
            color: #fff;
            box-shadow: 0 2px 8px rgba(59, 130, 246, 0.2);
            border-color: #3b82f6;
        }
        .grid-2 {
            display: grid;
            grid-template-columns: 1fr;
            gap: 1.25rem;
        }
        @media (min-width: 768px) {
            .grid-2 {
                grid-template-columns: 1fr 1fr;
            }
        }
        .currency-input-wrapper {
            display: flex;
            align-items: center;
            border: 1px solid #e5e7eb;
            border-radius: 8px;
            padding: 0.75rem;
            background-color: #f9fafb;
            transition: all 0.2s ease-in-out;
        }
        .currency-input-wrapper:focus-within {
            border-color: #3b82f6;
            box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.25);
            outline: none;
            background-color: #fff;
        }
        .currency-input-wrapper::before {
            content: '$';
            margin-right: 0.5rem;
            color: #6b7280;
            font-weight: 500;
        }
        .section-title {
            position: relative;
            margin-top: 2rem;
            margin-bottom: 1.5rem;
            font-size: 1.5rem;
            font-weight: 700;
            color: #1f2937;
        }
        .initial-hidden {
            display: none;
            opacity: 0;
        }
        /* Estilos para el modal de mensaje */
        .message-modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            display: none;
            justify-content: center;
            align-items: center;
            z-index: 100;
        }
        .message-content {
            background-color: white;
            padding: 2rem;
            border-radius: 12px;
            text-align: center;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
            max-width: 400px;
            transition: transform 0.3s ease-in-out;
        }
        .message-content h3 {
            font-size: 1.5rem;
            font-weight: bold;
            margin-bottom: 1rem;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1 class="text-3xl font-bold text-center mb-6 text-gray-800">Generador de Recibos Ywen Tours</h1>
        <!-- Se ha eliminado el 'action' del formulario para manejar el envío con JS -->
        <form id="reciboForm" method="post">
            <div class="radio-group">
                <input type="radio" id="nuevo" name="opcion_formulario" value="nuevo" class="hidden">
                <label for="nuevo">Nuevo recibo de pago</label>

                <input type="radio" id="actualizacion" name="opcion_formulario" value="actualizacion" class="hidden">
                <label for="actualizacion">Actualización de pago</label>
            </div>

            <div id="formContent" class="initial-hidden">
                <!-- Sección de campos para Nuevo Recibo -->
                <div id="nuevoReciboSection" class="form-section">
                    <h2 class="section-title">Datos del Cliente</h2>
                    <div class="grid-2">
                        <div class="form-field">
                            <label for="Nombre_Cliente">Nombre del Cliente</label>
                            <input type="text" id="Nombre_Cliente" name="Nombre_Cliente" required>
                        </div>
                        <div class="form-field">
                            <label for="Numero_Telefono_Cliente">Número de teléfono del cliente</label>
                            <input type="text" id="Numero_Telefono_Cliente" name="Numero_Telefono_Cliente" required>
                        </div>
                    </div>

                    <h2 class="section-title">Detalles del Viaje</h2>
                    <div class="grid-2">
                        <div class="form-field">
                            <label for="Destino_Viaje">Destino del Viaje</label>
                            <input type="text" id="Destino_Viaje" name="Destino_Viaje" required>
                        </div>
                        <div class="form-field">
                            <label for="Tipo_Viaje">Tipo de Viaje</label>
                            <select id="Tipo_Viaje" name="Tipo_Viaje">
                                <option value="Terrestre">Terrestre</option>
                                <option value="Aéreo">Aéreo</option>
                            </select>
                        </div>
                    </div>
                    <div class="form-field">
                        <label for="Concepto_Viaje">Concepto del Viaje</label>
                        <textarea id="Concepto_Viaje" name="Concepto_Viaje" rows="3" required></textarea>
                    </div>

                    <div class="grid-2">
                        <div class="form-field">
                            <label for="Tipo_Habitacion">Tipo de habitación</label>
                            <select id="Tipo_Habitacion" name="Tipo_Habitacion">
                                <option value="N/A">N/A</option>
                                <option value="Cuádruple">Cuádruple</option>
                                <option value="Triple">Triple</option>
                                <option value="Doble">Doble</option>
                                <option value="Privada">Privada</option>
                            </select>
                        </div>
                        <div class="form-field">
                            <label for="Punto_Encuentro">Punto de salida</label>
                            <select id="Punto_Encuentro" name="Punto_Encuentro">
                                <option value="Paloma de la Paz">Paloma de La Paz (Morelos)</option>
                                <option value="Toks Jacarandas">Toks Jacarandas (Morelos)</option>
                                <option value="Mega de Tejalpa">Mega de Tejalpa (Morelos)</option>
                                <option value="Crucero de Atlihuayan">Crucero de Atlihuayan (Morelos)</option>
                                <option value="Mega los Arcos">Mega los Arcos (Morelos)</option>
                                <option value="Plaza Perisur">Plaza Perisur (CDMX)</option>
                                <option value="Plaza Satélite">Plaza Satélite (CDMX)</option>
                                <option value="Otro">Otro</option>
                            </select>
                        </div>
                    </div>
                    <div id="otroPuntoField" class="form-field hidden">
                        <label for="Otro_Punto">Ingresar otro punto</label>
                        <input type="text" id="Otro_Punto" name="Otro_Punto">
                    </div>

                    <h2 class="section-title">Conceptos y Pagos</h2>
                    <div class="grid-2">
                        <div class="form-field">
                            <label for="Cantidad_Adultos">Adultos</label>
                            <select id="Cantidad_Adultos" name="Cantidad_Adultos">
                                <option value="0">0</option>
                                <option value="1">1</option>
                                <option value="2">2</option>
                                <option value="3">3</option>
                                <option value="4">4</option>
                                <option value="5">5</option>
                                <option value="6">6</option>
                                <option value="7">7</option>
                                <option value="8">8</option>
                            </select>
                        </div>
                        <div class="form-field">
                            <label for="Cantidad_Menores">Menores</label>
                            <select id="Cantidad_Menores" name="Cantidad_Menores">
                                <option value="0">0</option>
                                <option value="1">1</option>
                                <option value="2">2</option>
                                <option value="3">3</option>
                                <option value="4">4</option>
                                <option value="5">5</option>
                                <option value="6">6</option>
                                <option value="7">7</option>
                                <option value="8">8</option>
                            </select>
                        </div>
                    </div>
                    
                    <div class="grid-2">
                        <div id="tarifaAdulto" class="form-field hidden">
                            <label for="Tarifa_Adultos">Tarifa de Adultos</label>
                            <div class="currency-input-wrapper">
                                <input type="number" id="Tarifa_Adultos" name="Tarifa_Adultos">
                            </div>
                        </div>
                        <div id="tarifaMenor" class="form-field hidden">
                            <label for="Tarifa_Menores">Tarifa de Menores</label>
                            <div class="currency-input-wrapper">
                                <input type="number" id="Tarifa_Menores" name="Tarifa_Menores">
                            </div>
                        </div>
                    </div>

                    <div class="form-field">
                        <label for="Pago_Realizado_Nuevo">Monto del Primer Pago</label>
                        <div class="currency-input-wrapper">
                            <input type="number" id="Pago_Realizado_Nuevo" name="Pago_Realizado_Nuevo" required>
                        </div>
                    </div>
                    <div class="form-field">
                        <label for="Fecha_Primer_Pago">Fecha del Primer Pago</label>
                        <input type="date" id="Fecha_Primer_Pago" name="Fecha_Primer_Pago" required>
                    </div>

                    <div class="form-field flex items-center gap-2">
                        <input type="checkbox" id="Tarifa_Adicional_Checkbox" name="Tarifa_Adicional_Checkbox">
                        <label for="Tarifa_Adicional_Checkbox" class="mb-0 font-normal">Añadir tarifa adicional</label>
                    </div>
                    <div id="tarifaAdicional" class="form-field hidden">
                        <div class="grid-2">
                            <div>
                                <label for="Concepto_Adicional">Concepto Adicional</label>
                                <input type="text" id="Concepto_Adicional" name="Concepto_Adicional">
                            </div>
                            <div>
                                <label for="Monto_Adicional">Monto Adicional</label>
                                <div class="currency-input-wrapper">
                                    <input type="number" id="Monto_Adicional" name="Monto_Adicional">
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Sección de campos para Actualización de Pago -->
                <div id="actualizacionPagoSection" class="form-section">
                    <h2 class="section-title">Actualizar Pago</h2>
                    <div class="form-field">
                        <label for="Numero_Recibo_Actualizacion">Número de Recibo</label>
                        <input type="text" id="Numero_Recibo_Actualizacion" name="Numero_Recibo_Actualizacion" required>
                    </div>
                    <div class="form-field">
                        <label for="Fecha_Pago_Actualizacion">Fecha del Nuevo Pago</label>
                        <input type="date" id="Fecha_Pago_Actualizacion" name="Fecha_Pago_Actualizacion" required>
                    </div>
                    <div class="form-field">
                        <label for="Monto_Pago_Actualizacion">Monto del Nuevo Pago</label>
                        <div class="currency-input-wrapper">
                            <input type="number" id="Monto_Pago_Actualizacion" name="Monto_Pago_Actualizacion" required>
                        </div>
                    </div>
                </div>
                <!-- Botón de envío -->
                <button type="submit" class="button w-full mt-6">Enviar</button>
            </div>
        </form>
    </div>

    <!-- Modal para mostrar mensajes -->
    <div id="messageModal" class="message-modal">
        <div class="message-content">
            <h3 id="messageTitle"></h3>
            <p id="messageText"></p>
            <button onclick="document.getElementById('messageModal').style.display = 'none'" class="button mt-4">Aceptar</button>
        </div>
    </div>

    <script>
        // Aquí va tu URL de Make.com
        const WEBHOOK_URL = "https://hook.us2.make.com/yiafilrgobtbilmys64wun75g5x0nwky";

        const nuevoReciboRadio = document.getElementById('nuevo');
        const actualizacionRadio = document.getElementById('actualizacion');
        const nuevoReciboSection = document.getElementById('nuevoReciboSection');
        const actualizacionPagoSection = document.getElementById('actualizacionPagoSection');
        const formContent = document.getElementById('formContent');
        const tarifasAdicionales = document.getElementById('tarifaAdicional');
        const tarifasAdicionalesCheckbox = document.getElementById('Tarifa_Adicional_Checkbox');
        const puntoEncuentroSelect = document.getElementById('Punto_Encuentro');
        const otroPuntoField = document.getElementById('otroPuntoField');
        const cantidadAdultos = document.getElementById('Cantidad_Adultos');
        const cantidadMenores = document.getElementById('Cantidad_Menores');
        const tarifaAdulto = document.getElementById('tarifaAdulto');
        const tarifaMenor = document.getElementById('tarifaMenor');
        const conceptoAdicional = document.getElementById('Concepto_Adicional');
        const montoAdicional = document.getElementById('Monto_Adicional');
        const messageModal = document.getElementById('messageModal');
        const messageTitle = document.getElementById('messageTitle');
        const messageText = document.getElementById('messageText');
        
        // Función para mostrar el modal de mensaje
        function showMessage(title, message, isSuccess = true) {
            messageTitle.textContent = title;
            messageText.textContent = message;
            messageTitle.style.color = isSuccess ? '#16a34a' : '#dc2626';
            messageModal.style.display = 'flex';
        }

        // Function to toggle between sections
        function toggleSections() {
            formContent.classList.remove('initial-hidden');
            if (nuevoReciboRadio.checked) {
                nuevoReciboSection.classList.add('active');
                actualizacionPagoSection.classList.remove('active');
            } else {
                nuevoReciboSection.classList.remove('active');
                actualizacionPagoSection.classList.add('active');
            }
        }

        // Function to toggle rate fields
        function toggleTarifaFields() {
            if (parseInt(cantidadAdultos.value) > 0) {
                tarifaAdulto.classList.remove('hidden');
            } else {
                tarifaAdulto.classList.add('hidden');
            }

            if (parseInt(cantidadMenores.value) > 0) {
                tarifaMenor.classList.remove('hidden');
            } else {
                tarifaMenor.classList.add('hidden');
            }
        }

        nuevoReciboRadio.addEventListener('change', toggleSections);
        actualizacionRadio.addEventListener('change', toggleSections);
        
        tarifasAdicionalesCheckbox.addEventListener('change', function() {
            if (this.checked) {
                tarifasAdicionales.classList.remove('hidden');
                conceptoAdicional.setAttribute('required', 'required');
                montoAdicional.setAttribute('required', 'required');
            } else {
                tarifasAdicionales.classList.add('hidden');
                conceptoAdicional.removeAttribute('required');
                montoAdicional.removeAttribute('required');
            }
        });
        
        puntoEncuentroSelect.addEventListener('change', function() {
            if (this.value === 'Otro') {
                otroPuntoField.classList.remove('hidden');
                otroPuntoField.querySelector('input').setAttribute('required', 'required');
            } else {
                otroPuntoField.classList.add('hidden');
                otroPuntoField.querySelector('input').removeAttribute('required');
            }
        });

        cantidadAdultos.addEventListener('change', toggleTarifaFields);
        cantidadMenores.addEventListener('change', toggleTarifaFields);

        // Agregamos el event listener para el envío del formulario
        document.getElementById('reciboForm').addEventListener('submit', async function(event) {
            // Evita que el formulario se envíe de forma tradicional y recargue la página
            event.preventDefault();

            // Deshabilita el botón para evitar envíos duplicados
            const submitButton = event.target.querySelector('button[type="submit"]');
            submitButton.disabled = true;
            submitButton.textContent = 'Enviando...';
            submitButton.classList.add('opacity-50', 'cursor-not-allowed');

            // Recopila los datos del formulario de forma dinámica
            const formData = new FormData(event.target);
            const data = {};
            for (let [key, value] of formData.entries()) {
                // Solo incluye los campos que son visibles para el formulario activo
                const inputElement = event.target.querySelector(`[name="${key}"]`);
                if (inputElement && inputElement.offsetParent !== null) {
                    data[key] = value;
                }
            }

            try {
                // Envía los datos al webhook de Make.com
                const response = await fetch(WEBHOOK_URL, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json'
                    },
                    body: JSON.stringify(data)
                });

                if (!response.ok) {
                    throw new Error(`Error en el servidor: ${response.status}`);
                }

                // Espera la respuesta del servidor
                const result = await response.json();
                console.log('Éxito:', result);

                // Muestra el mensaje de éxito
                showMessage('¡Recibo Enviado!', 'El formulario se ha enviado correctamente a Make.com.', true);
                event.target.reset(); // Reinicia el formulario

            } catch (error) {
                console.error('Error:', error);
                // Muestra un mensaje de error
                showMessage('Error de Envío', 'Ocurrió un error al enviar el formulario. Por favor, inténtalo de nuevo.', false);
            } finally {
                // Habilita el botón de nuevo
                submitButton.disabled = false;
                submitButton.textContent = 'Enviar';
                submitButton.classList.remove('opacity-50', 'cursor-not-allowed');
            }
        });

        window.onload = function() {
            toggleSections();
            toggleTarifaFields(); 
        }
    </script>
</body>
</html>
