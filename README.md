# digital-sand-clock
digital sand clock using ardiuno and led matrix
#include <LedControl.h>

// Pins for MAX7219: DIN=11, CLK=13, CS=10
LedControl lc = LedControl(11, 13, 10, 1);

unsigned long previousMillis = 0;
const long interval = 200;  // delay between frames (ms)

byte frame = 0;

// Sand clock frames — 8 rows, 8 columns
byte sandClockFrames[8][8] = {
  {
    B11111111,
    B11111111,
    B11111111,
    B11111111,
    B00000000,
    B00000000,
    B00000000,
    B00000000
  },
  {
    B11111111,
    B11111111,
    B11111111,
    B00000000,
    B00000000,
    B00000000,
    B00000000,
    B00000000
  },
  {
    B11111111,
    B11111111,
    B00000000,
    B00000000,
    B00011000,
    B00000000,
    B00000000,
    B00000000
  },
  {
    B11111111,
    B00000000,
    B00000000,
    B00011000,
    B00111100,
    B00011000,
    B00000000,
    B00000000
  },
  {
    B00000000,
    B00000000,
    B00011000,
    B00111100,
    B01111110,
    B00111100,
    B00011000,
    B00000000
  },
  {
    B00000000,
    B00000000,
    B00000000,
    B01111110,
    B11111111,
    B11111111,
    B01111110,
    B00000000
  },
  {
    B00000000,
    B00000000,
    B00000000,
    B00000000,
    B11111111,
    B11111111,
    B11111111,
    B11111111
  },
  {
    B00000000,
    B00000000,
    B00000000,
    B00000000,
    B00000000,
    B00000000,
    B11111111,
    B11111111
  }
};

void setup() {
  lc.shutdown(0, false);  // Wake up display
  lc.setIntensity(0, 8);  // Set brightness (0-15)
  lc.clearDisplay(0);     // Clear display
}

void loop() {
  unsigned long currentMillis = millis();
  if (currentMillis - previousMillis >= interval) {
    previousMillis = currentMillis;

    for (int row = 0; row < 8; row++) {
      lc.setRow(0, row, sandClockFrames[frame][row]);
    }

    frame++;
    if (frame >= 8) frame = 0;
  }
}
