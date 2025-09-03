<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Generador de Recibos Ywen Tours</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f3f4f6;
            color: #333;
            line-height: 1.6;
        }
        .container {
            max-width: 800px;
            margin: 2rem auto;
            padding: 2rem;
            background-color: #fff;
            border-radius: 12px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
        }
        .form-section {
            display: none;
        }
        .form-section.active {
            display: block;
        }
        .form-field {
            margin-bottom: 1rem;
        }
        label {
            display: block;
            font-weight: 600;
            margin-bottom: 0.5rem;
            color: #4b5563;
        }
        /* Estilos generales para inputs de texto y selects */
        input[type="text"], select {
            width: 100%;
            padding: 0.75rem;
            border: 1px solid #d1d5db;
            border-radius: 8px;
            font-size: 1rem;
            transition: all 0.2s ease-in-out;
        }
        /* Estilos específicos para inputs de tipo number sin borde */
        input[type="number"] {
            -webkit-appearance: textfield; /* Safari y Chrome */
            -moz-appearance: textfield;    /* Firefox */
            appearance: textfield;
            width: 100%;
            font-size: 1rem;
            border: none;
            outline: none;
            padding: 0;
        }
        input[type="number"]::-webkit-inner-spin-button,
        input[type="number"]::-webkit-outer-spin-button {
            -webkit-appearance: none;
            margin: 0;
        }
        input[type="text"]:focus, input[type="number"]:focus, select:focus {
            border-color: #3b82f6;
            box-shadow: 0 0 0 2px rgba(59, 130, 246, 0.25);
            outline: none;
        }
        .button {
            display: inline-block;
            padding: 0.75rem 1.5rem;
            background-color: #3b82f6;
            color: #fff;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            transition: background-color 0.2s ease-in-out;
            font-weight: 600;
        }
        .button:hover {
            background-color: #2563eb;
        }
        .radio-group {
            display: flex;
            gap: 1rem;
            margin-bottom: 1rem;
        }
        .radio-group label {
            background-color: #e5e7eb;
            padding: 0.75rem 1.5rem;
            border-radius: 8px;
            cursor: pointer;
            transition: background-color 0.2s ease-in-out;
        }
        .radio-group input:checked + label {
            background-color: #3b82f6;
            color: #fff;
        }
        .grid-2 {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 1rem;
        }

        /* Nuevos estilos para el campo de moneda */
        .currency-input-wrapper {
            display: flex;
            align-items: center;
            border: 1px solid #d1d5db;
            border-radius: 8px;
            padding: 0.75rem;
            background-color: #fff;
            transition: all 0.2s ease-in-out;
        }
        .currency-input-wrapper:focus-within {
            border-color: #3b82f6;
            box-shadow: 0 0 0 2px rgba(59, 130, 246, 0.25);
            outline: none;
        }
        .currency-input-wrapper::before {
            content: '$';
            margin-right: 0.5rem;
            color: #6b7280;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1 class="text-3xl font-bold text-center mb-6">Generador de Recibos Ywen Tours</h1>
        <form id="reciboForm" action="https://hook.us2.make.com/yiafilrgobtbilmys64wun75g5x0nwky" method="post">
            <div class="radio-group">
                <input type="radio" id="nuevo" name="opcion_formulario" value="nuevo" class="hidden" checked>
                <label for="nuevo">Nuevo recibo de pago</label>

                <input type="radio" id="actualizacion" name="opcion_formulario" value="actualizacion" class="hidden">
                <label for="actualizacion">Actualización de pago</label>
            </div>

            <!-- Sección de campos para Nuevo Recibo -->
            <div id="nuevoReciboSection" class="form-section active">
                <h2 class="text-2xl font-semibold mb-4">Datos del Cliente</h2>
                <div class="form-field">
                    <label for="Nombre_Cliente">Nombre del Cliente</label>
                    <input type="text" id="Nombre_Cliente" name="Nombre_Cliente" required>
                </div>
                <div class="form-field">
                    <label for="Numero_Telefono_Cliente">Número de teléfono del cliente</label>
                    <input type="text" id="Numero_Telefono_Cliente" name="Numero_Telefono_Cliente" required>
                </div>

                <h2 class="text-2xl font-semibold mt-6 mb-4">Detalles del Viaje</h2>
                <div class="form-field">
                    <label for="Concepto_Viaje">Concepto del Viaje</label>
                    <textarea id="Concepto_Viaje" name="Concepto_Viaje" class="w-full p-2 border border-gray-300 rounded-md" rows="3" required></textarea>
                </div>

                <div class="grid-2">
                    <div class="form-field">
                        <label for="Tipo_Viaje">Tipo de viaje</label>
                        <select id="Tipo_Viaje" name="Tipo_Viaje">
                            <option value="Terrestre">Terrestre</option>
                            <option value="Aéreo">Aéreo</option>
                        </select>
                    </div>
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
                </div>

                <div class="grid-2">
                    <div class="form-field">
                        <label for="Punto_Encuentro">Punto de encuentro</label>
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
                    <div id="otroPuntoField" class="form-field" style="display:none;">
                        <label for="Otro_Punto">Ingresar otro punto</label>
                        <input type="text" id="Otro_Punto" name="Otro_Punto">
                    </div>
                </div>

                <h2 class="text-2xl font-semibold mt-6 mb-4">Conceptos y Pagos</h2>

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

                <div id="tarifaAdulto" class="form-field hidden">
                    <label for="Tarifa_Adultos">Tarifa de Adultos</label>
                    <input type="number" id="Tarifa_Adultos" name="Tarifa_Adultos">
                </div>
                <div id="tarifaMenor" class="form-field hidden">
                    <label for="Tarifa_Menores">Tarifa de Menores</label>
                    <input type="number" id="Tarifa_Menores" name="Tarifa_Menores">
                </div>

                <div class="form-field flex items-center gap-2">
                    <input type="checkbox" id="Tarifa_Adicional_Checkbox" name="Tarifa_Adicional_Checkbox">
                    <label for="Tarifa_Adicional_Checkbox" class="mb-0">Añadir tarifa adicional</label>
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
                <h2 class="text-2xl font-semibold mb-4">Actualizar Pago</h2>
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

            <button type="submit" class="button w-full mt-6">Enviar</button>
        </form>
    </div>

    <script>
        const nuevoReciboRadio = document.getElementById('nuevo');
        const actualizacionRadio = document.getElementById('actualizacion');
        const nuevoReciboSection = document.getElementById('nuevoReciboSection');
        const actualizacionPagoSection = document.getElementById('actualizacionPagoSection');
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
        const numeroReciboAct = document.getElementById('Numero_Recibo_Actualizacion');
        const fechaPagoAct = document.getElementById('Fecha_Pago_Actualizacion');
        const montoPagoAct = document.getElementById('Monto_Pago_Actualizacion');

        function toggleSections() {
            if (nuevoReciboRadio.checked) {
                nuevoReciboSection.classList.add('active');
                actualizacionPagoSection.classList.remove('active');
            } else {
                nuevoReciboSection.classList.remove('active');
                actualizacionPagoSection.classList.add('active');
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
                otroPuntoField.style.display = 'block';
                otroPuntoField.querySelector('input').setAttribute('required', 'required');
            } else {
                otroPuntoField.style.display = 'none';
                otroPuntoField.querySelector('input').removeAttribute('required');
            }
        });

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

        cantidadAdultos.addEventListener('change', toggleTarifaFields);
        cantidadMenores.addEventListener('change', toggleTarifaFields);

        window.onload = function() {
            toggleSections();
        }
    </script>
</body>
</html>
