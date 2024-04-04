from machine import Pin, ADC, I2C
import ssd1306
import time

# Definir los pines
PIN_FIRE_ANALOG = 14  #9 Usar el pin 34 para ESP32
PIN_FIRE_DIGITAL = 4

# Configuración de la pantalla OLED
i2c = I2C(-1, scl=Pin(16), sda=Pin(17))  # Configura la comunicación I2C
oled = ssd1306.SSD1306_I2C(128, 64, i2c)  # Inicializa la pantalla OLED

# Configurar el ADC para leer el valor analógico del sensor de fuego
adc = ADC(Pin(PIN_FIRE_ANALOG))
adc.atten(ADC.ATTN_11DB)  # Configurar atenuación para 0-3.6V

# Configurar el pin del sensor de fuego como entrada
fire_digital = Pin(PIN_FIRE_DIGITAL, Pin.IN)

# Función para mostrar el mensaje en la pantalla OLED
def mostrar_mensaje(mensaje):
    oled.fill(0)  # Borra la pantalla
    oled.text(mensaje, 0, 0)  # Muestra el mensaje en la pantalla
    oled.show()  # Actualiza la pantalla

# Ciclo principal
while True:
    firesensor_analog = adc.read()  # Leer el valor analógico del sensor de fuego
    firesensor_digital = fire_digital.value()  # Leer el valor digital del sensor de fuego

    if firesensor_analog < 1000:
        print("Fire detected")
        mostrar_mensaje("Fuego detectado")
    else:
        print("No fire detected")
        mostrar_mensaje("No hay fuego")

    time.sleep(0.1)
