# IoT-Payment-Robotic-Integration | Zettle Integration
Full-stack integration connecting Zettle (PayPal) APIs with an ESP32 robotic arm using Python. Automates physical product delivery based on real-time digital transactions.

![Python](https://img.shields.io/badge/Backend-Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![C++](https://img.shields.io/badge/Firmware-C%2B%2B-00599C?style=for-the-badge&logo=c%2B%2B&logoColor=white)
![Platform](https://img.shields.io/badge/Hardware-ESP32-E7352C?style=for-the-badge&logo=espressif&logoColor=white)
![API](https://img.shields.io/badge/API-Zettle%20by%20PayPal-00457C?style=for-the-badge&logo=paypal&logoColor=white)

## Descripción del Proyecto

Este proyecto es un sistema de automatización **Cyber-Físico** que integra transacciones financieras en tiempo real con acciones robóticas físicas. 

El sistema monitorea una cuenta comercial de **Zettle (PayPal)** para detectar ventas específicas (ej. "Coca Cola"). Al confirmar una transacción válida, el backend procesa la orden y envía comandos vía **TCP/IP** a un controlador embebido **ESP32**, el cual acciona un **Brazo Robótico de 4 Grados de Libertad (DOF)** y un sistema de válvulas para dispensar el producto automáticamente.

### Objetivo
Eliminar la intervención humana en el proceso de entrega de productos, creando un puente directo entre la **Venta Digital (Fintech)** y la **Entrega Física (Automatización)**.

---


### Flujo de Datos
1.  **Venta:** El cliente paga con tarjeta en la terminal Zettle.
2.  **Polling:** El script de Python consulta la API de Zettle (`OAuth 2.0`).
3.  **Procesamiento:** Se verifica si la venta corresponde a un producto dispensable.
4.  **Comunicación:** Se envía la orden vía Socket TCP local al ESP32.
5.  **Actuación:** El ESP32 coordina los servomotores (PCA9685) y relevadores para servir la bebida.

---

## Stack Tecnológico

### Backend (Python)
* **Requests:** Consumo de API REST (Zettle Purchase API).
* **OAuth 2.0:** Gestión segura de tokens y autenticación (`token_manager.py`).
* **Sockets:** Comunicación de baja latencia con el hardware.
* **JSON:** Persistencia local de órdenes procesadas para evitar duplicados.

### Firmware (C++ / Arduino IDE)
* **WiFi.h:** Conectividad de red para el ESP32.
* **Adafruit_PWMServoDriver:** Control preciso de 16 canales PWM (I2C).
* **Lógica de Control:** Máquina de estados para movimientos suaves del brazo robótico.

### Hardware
* Microcontrolador **ESP32**.
* Driver **PCA9685** (Control de Servos).
* Brazo Robótico (4 Servomotores MG996R).
* Sistema de Válvulas (Módulos de Relevador).

---

## Estructura del Repositorio

```text
├── Backend/
│   ├── main.py              # Script principal de orquestación
│   ├── token_manager.py     # Manejo de autenticación OAuth (Refresh Tokens)
│   ├── purchase_processor.py # Lógica de negocio y filtrado de ventas
│   └── ...
├── Firmware/
│   └── FINAL.ino            # Código C++ para el ESP32
└── README.md                # Documentación
