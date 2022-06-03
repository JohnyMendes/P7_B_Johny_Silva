# Johny Silva Mendes
# PRACTICA 7  : Buses de comunicación III (I2S)

## Ejercicio Practico 2 reproducir un archivo WAVE en ESP32 desde una tarjeta SD externa

### Código del programa
```cpp
#include "Audio.h"
#include "SD.h"
#include "FS.h"

// Digital I/O used
#define SD_CS          5
#define SPI_MOSI      23
#define SPI_MISO      19
#define SPI_SCK       18
#define I2S_DOUT      25
#define I2S_BCLK      27
#define I2S_LRC       26

Audio audio;

void setup(){

    Serial.begin(115200);

    pinMode(SD_CS, OUTPUT);
    digitalWrite(SD_CS, HIGH);
    SPI.begin(SPI_SCK, SPI_MISO, SPI_MOSI);
    SD.begin(SD_CS);
    audio.setPinout(I2S_BCLK, I2S_LRC, I2S_DOUT);
    audio.setVolume(15); // 0...21
    audio.connecttoFS(SD, "Ensoniq-ZR-76-01-Dope-77.wav");
}

void loop(){
    audio.loop();
}

// optional
void audio_info(const char *info){
    Serial.print("info        "); Serial.println(info);
}
void audio_id3data(const char *info){  //id3 metadata
    Serial.print("id3data     ");Serial.println(info);
}
void audio_eof_mp3(const char *info){  //end of file
    Serial.print("eof_mp3     ");Serial.println(info);
}
void audio_showstation(const char *info){
    Serial.print("station     ");Serial.println(info);
}
void audio_showstreaminfo(const char *info){
    Serial.print("streaminfo  ");Serial.println(info);
}
void audio_showstreamtitle(const char *info){
    Serial.print("streamtitle ");Serial.println(info);
}
void audio_bitrate(const char *info){
    Serial.print("bitrate     ");Serial.println(info);
}
void audio_commercial(const char *info){  //duration in sec
    Serial.print("commercial  ");Serial.println(info);
}
void audio_icyurl(const char *info){  //homepage
    Serial.print("icyurl      ");Serial.println(info);
}
void audio_lasthost(const char *info){  //stream URL played
    Serial.print("lasthost    ");Serial.println(info);
}
void audio_eof_speech(const char *info){
    Serial.print("eof_speech  ");Serial.println(info);
}
```

### Funcionamiento 

Primeramente, se usará 3 librerías. También se tendrá que definir los diferentes puertos que se usarán para la recepción y transmisión de datos. Los pines SPI_MOSI,SPI_MISO,SPI_SCK y SPI_CS són los de la tarjeta SD.

```cpp
#include "Audio.h"
#include "SD.h"
#include "FS.h"

// Digital I/O used
#define SD_CS          5
#define SPI_MOSI      23
#define SPI_MISO      19
#define SPI_SCK       18
#define I2S_DOUT      25
#define I2S_BCLK      27
#define I2S_LRC       26
```
Luego, se declarará una variable del tipo Audio donde se guardará el sonido y sus caracterísiticas. 

**Setup:** se inicia el puerto serie y se realiza la conexión entre el lector de tarjetas y el bus SPI. Finalmente, se configura la variable Audio en la se debe asignar los pines del bus I2C, ajustar el volumen pertinente y leer el archivo desde el file source.

```cpp
Audio audio;

void setup(){

    Serial.begin(115200);

    pinMode(SD_CS, OUTPUT);
    digitalWrite(SD_CS, HIGH);
    SPI.begin(SPI_SCK, SPI_MISO, SPI_MOSI);
    SD.begin(SD_CS);
    audio.setPinout(I2S_BCLK, I2S_LRC, I2S_DOUT);
    audio.setVolume(15); // 0...21
    audio.connecttoFS(SD, "Ensoniq-ZR-76-01-Dope-77.wav");
}
```

**Loop:** función necesaria para reproducir el audio

```cpp
void loop(){
    audio.loop();
}
```

### Salida por Terminal 
Para el montaje de esta practica mi compañero y yo no hemos podido llevarlo a cabo porque no disponiamos del material necesario y no pudimos utilizar el material de otros compañeros.
