# VHDL-1er-Proyecto

**Integrantes:**
- Pablo Collazos
- Sergio Cruz
- Cristian Cuastumal

```mermaid
flowchart TD
    %% ================================
    %% BLOQUE PRINCIPAL
    %% ================================
    subgraph TOP["Bloque Principal (TOP)"]
        direction TB
        FSM["FSM de Control Principal
        - Estados: Espera, Moneda, Asignación, Puerta, Emergencia"]
        Procesamiento["Módulo de Procesamiento
        - Contador de tiempo
        - Comparador de parqueadero lleno
        - Detector de monedas 500/1000
        - Generadores de parpadeo (500 ms / 2 s)"]
        MotorPuerta["Control Motor y Puerta
        - Arranque / Paro
        - Inversión de giro
        - Temporizador apertura (30s) y cierre (50s)"]
        Salidas["Módulo de Salidas
        - Torre de luces (Rojo/Verde/Amarillo)
        - Display 7 segmentos
        - LEDs de alerta
        - Alarma sonora"]
    end

    %% ================================
    %% ENTRADAS
    %% ================================
    subgraph Entradas["Entradas"]
        TECLADO["Teclado Matricial"]
        SENSORES["Sensores de ocupación de puestos"]
        BOTON_EMERG["Botón de Emergencia"]
        MONEDAS["Detector de monedas 500/1000"]
    end

    %% ================================
    %% CONEXIONES
    %% ================================
    TECLADO --> FSM
    SENSORES --> FSM
    BOTON_EMERG --> FSM
    MONEDAS --> Procesamiento
    FSM --> Procesamiento
    FSM --> MotorPuerta
    FSM --> Salidas
    Procesamiento --> Salidas
    Procesamiento --> FSM

    %% ================================
    %% SALIDAS
    %% ================================
    subgraph Dispositivos["Dispositivos de Salida"]
        LUCES["Torre de Luces"]
        DISPLAY["Display de 7 Segmentos"]
        ALARMA["Alarma Sonora"]
        LEDS["LEDs de alerta"]
        MOTOR["Motor y Puerta"]
    end

    Salidas --> LUCES
    Salidas --> DISPLAY
    Salidas --> ALARMA
    Salidas --> LEDS
    MotorPuerta --> MOTOR
