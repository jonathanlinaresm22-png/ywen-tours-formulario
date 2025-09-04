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
        .message-modal, .preview-modal {
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
        .message-content, .preview-content {
            background-color: white;
            padding: 2rem;
            border-radius: 12px;
            text-align: center;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
            max-width: 600px;
            transition: transform 0.3s ease-in-out;
            max-height: 90vh;
            overflow-y: auto;
        }
        .message-content h3, .preview-content h3 {
            font-size: 1.5rem;
            font-weight: bold;
            margin-bottom: 1rem;
        }
        .preview-item {
            display: flex;
            justify-content: space-between;
            padding: 0.5rem 0;
            border-bottom: 1px dashed #e5e7eb;
        }
        .preview-item:last-child {
            border-bottom: none;
        }
        .preview-label {
            font-weight: 600;
            color: #4b5563;
        }
        .preview-value {
            color: #1f2937;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1 class="text-3xl font-bold text-center mb-6 text-gray-800">Generador de Recibos Ywen Tours</h1>
        <form id="reciboForm" method="post">
            <div class="radio-group">
                <input type="radio" id="nuevo" name="opcion_formulario" value="nuevo" class="hidden" checked>
                <label for="nuevo">Nuevo recibo de pago</label>

                <input type="radio" id="actualizacion" name="opcion_formulario" value="actualizacion" class="hidden">
                <label for="actualizacion">Actualización de pago</label>
            </div>

            <div id="formContent" class="initial-hidden">
                <div id="nuevoReciboSection" class="form-section active">
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
