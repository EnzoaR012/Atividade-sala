# Atividade-sala
Enzo Araujo de Rezende e Guilherme Valença
Novo codigo:
const int PIN_BUTTON = 2;
const int PIN_RED    = 13;
const int PIN_YELLOW = 12;
const int PIN_GREEN  = 11;

class LED {
  private:
    uint8_t pin;
    int color;
    bool state;

  public:
    LED(int p, int c) : pin(p), color(c), state(false) {}

    void begin() {
      pinMode(pin, OUTPUT);
      digitalWrite(pin, LOW);
      state = false;
    }

    void turnOn() {
      digitalWrite(pin, HIGH);
      state = true;
    }

    void turnOff() {
      digitalWrite(pin, LOW);
      state = false;
    }
};

class Button {
  private:
    int pin;
    bool lastReading;
    bool debouncedState;
    unsigned long lastTime;
    unsigned long debounceDelay;

  public:
    Button(int p, unsigned long d = 15)
      : pin(p),
        lastReading(HIGH),
        debouncedState(HIGH),
        lastTime(0),
        debounceDelay(d) {}

    void begin() { pinMode(pin, INPUT_PULLUP); }

    bool pressed() {
      bool reading = digitalRead(pin);

      if (reading != lastReading) {
        lastTime = millis();
        lastReading = reading;
      }

      if ((millis() - lastTime) > debounceDelay) {
        if (reading != debouncedState) {
          debouncedState = reading;
          if (debouncedState == LOW) {
            return true;
          }
        }
      }
      return false;
    }

    bool isDown() const { return debouncedState == LOW; }
};

LED red(PIN_RED, 1);
LED yellow(PIN_YELLOW, 2);
LED green(PIN_GREEN, 3);
Button button(PIN_BUTTON, 15);

void setup() {
  red.begin();
  yellow.begin();
  green.begin();
  button.begin();
}

void loop() {
  if (button.pressed()) {
    red.turnOn();
    delay(2000);

    red.turnOff();
    yellow.turnOn();
    delay(2000);

    yellow.turnOff();
    green.turnOn();
    delay(2000);

    green.turnOff();
  }
}

Codigo antigo:
int buttonState = 0;
void setup()
{
  pinMode(2, INPUT);
  pinMode(11, OUTPUT);
  pinMode(12, OUTPUT);
  pinMode(13, OUTPUT);
}
void loop()
{
  buttonState = digitalRead(2);
  if (buttonState == HIGH){
    delay(15);
    if (buttonState == HIGH){
      digitalWrite(13, HIGH);
      digitalWrite(12, LOW);
      digitalWrite(11, LOW);
      delay(2000);
      digitalWrite(13, LOW);
      digitalWrite(12, HIGH);
      digitalWrite(11, LOW);
      delay(2000);
      digitalWrite(13, LOW);
      digitalWrite(12, LOW);
      digitalWrite(11, HIGH);
      delay(2000);
    }
  }
}
LINK do TINKERCAD; https://www.tinkercad.com/things/avoIuKQ9LUr/editel?sharecode=1e_Z__CTUZW1nlfbWP-2gkXPVFTCLjazkofq7KCUemc






