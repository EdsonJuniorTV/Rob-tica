#define ledVermelho 15
#define ledVerde 02
#define pinoPotenciometro 34

void emitirAlarme(int vezes) {
  for(int contador = 0; contador < vezes; contador++) {
    digitalWrite(ledVermelho,HIGH);
    delay(1000);
    digitalWrite(ledVermelho,LOW);
    delay(1000);
  }
}

bool verificarTemperaturaCritica(int pino, int limite) {
  int valorLido = analogRead(pino);

  Serial.print("Valor Sensor: ");
  Serial.println(valorLido);

  if(valorLido > limite) {
    return true;
  } else {
    return false;
  }
}

void statusNormal() {
  digitalWrite(ledVerde,HIGH);
  digitalWrite(ledVermelho,LOW);
}

void setup() {
  Serial.begin(9600);
  pinMode(ledVermelho,OUTPUT);
  pinMode(ledVerde,OUTPUT);
}

void loop() {
  bool resultado = verificarTemperaturaCritica(pinoPotenciometro, 400);

  if(resultado == true) {
    emitirAlarme(10);
  }

  statusNormal();
  delay(2000);
}
