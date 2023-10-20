# SPD-1
SPD  TP parte 2 
link a tinkercad: https://www.tinkercad.com/things/dtKkMLNT86U-copy-of-spd-tp/editel?tenant=circuits


codigo:
#define A 10
#define B 11
#define C 5
#define D 6
#define E 7
#define F 9  
#define G 8

#define UNIDAD A4
#define DECENA A5
#define APAGADO 0

#define INTERRUPTOR_DESLIZANTE 2

int contador = 0;
bool sumaNumerosPrimos = true;

void setup()
{
  // Configurar pines de salida
  pinMode(A, OUTPUT);
  pinMode(B, OUTPUT);
  pinMode(C, OUTPUT);
  pinMode(D, OUTPUT);
  pinMode(E, OUTPUT);
  pinMode(F, OUTPUT);
  pinMode(G, OUTPUT);
  
  pinMode(UNIDAD, OUTPUT);
  pinMode(DECENA, OUTPUT);
  
  // Inicializar visualizadores
  digitalWrite(UNIDAD, HIGH);
  digitalWrite(DECENA, HIGH);
  
  // Configurar pin de interruptor deslizante como entrada
  pinMode(INTERRUPTOR_DESLIZANTE, INPUT_PULLUP);
  
  Serial.begin(9600);
}

void loop()
{
  int interruptorDeslizante = digitalRead(INTERRUPTOR_DESLIZANTE);
  
  if (interruptorDeslizante == HIGH){
    sumaNumerosPrimos = true;
  } else {
    sumaNumerosPrimos = false;
  }
  
  if(sumaNumerosPrimos){
    contador = sumarPrimo(contador);
  } else {
    contador++;
    if (contador > 99){
      contador = 0;
    }
  }
  
  mostrarNumero(contador);
}

int sumarPrimo(int num) {
  if (num < 2) return 2;
  
  while (true) {
    num++;
    if (esPrimo(num)) return num;
  }
}

bool esPrimo(int num) {
  if (num < 2) return false;
  for (int i = 2; i*i <= num; i++) {
    if (num % i == 0) return false;
  }
  return true;
}

void mostrarNumero(int numero){
  int unidad = numero % 10;  // Obtiene la unidad del número
  int decena = numero / 10; // Obtiene la decena del número

  // Mostrar en la unidad
  prenderDigito(UNIDAD);
  prenderNumero(unidad);

  
  delay(1000);

  // Apagar el visualizador de la unidad
  prenderDigito(APAGADO);

  // Mostrar en la decena
  prenderDigito(DECENA);
  prenderNumero(decena);

  
  delay(1000);

  // Apagar el visualizador de la decena
  prenderDigito(APAGADO);
}

void prenderDigito(int digito){
  if (digito == UNIDAD){
    digitalWrite(UNIDAD, LOW);
    digitalWrite(DECENA, HIGH);
  }
  else if (digito == DECENA){
    digitalWrite(UNIDAD, HIGH);
    digitalWrite(DECENA, LOW);
  }
  else{
    digitalWrite(UNIDAD, HIGH);
    digitalWrite(DECENA, HIGH);
  }
}

void prenderNumero(int numero){
  switch (numero) {
    case 0:
      digitalWrite(A, LOW);
      digitalWrite(B, LOW);
      digitalWrite(C, LOW);
      digitalWrite(D, LOW);
      digitalWrite(E, LOW);
      digitalWrite(F, LOW);
      digitalWrite(G, HIGH);
      break;

    case 1:
      digitalWrite(A, HIGH);
      digitalWrite(B, LOW);
      digitalWrite(C, LOW);
      digitalWrite(D, HIGH);
      digitalWrite(E, HIGH);
      digitalWrite(F, HIGH);
      digitalWrite(G, HIGH);
      break;

    case 2:
      digitalWrite(A, LOW);
      digitalWrite(B, LOW);
      digitalWrite(C, HIGH);
      digitalWrite(D, LOW);
      digitalWrite(E, LOW);
      digitalWrite(F, HIGH);
      digitalWrite(G, LOW);
      break;

    case 3:
      digitalWrite(A, LOW);
      digitalWrite(B, LOW);
      digitalWrite(C, LOW);
      digitalWrite(D, LOW);
      digitalWrite(E, HIGH);
      digitalWrite(F, HIGH);
      digitalWrite(G, LOW);
      break;

    case 4:
      digitalWrite(A, HIGH);
      digitalWrite(B, LOW);
      digitalWrite(C, LOW);
      digitalWrite(D, HIGH);
      digitalWrite(E, HIGH);
      digitalWrite(F, LOW);
      digitalWrite(G, LOW);
      break;

    case 5:
      digitalWrite(A, LOW);
      digitalWrite(B, HIGH);
      digitalWrite(C, LOW);
      digitalWrite(D, LOW);
      digitalWrite(E, HIGH);
      digitalWrite(F, LOW);
      digitalWrite(G, LOW);
      break;

    case 6:
      digitalWrite(A, LOW);
      digitalWrite(B, HIGH);
      digitalWrite(C, LOW);
      digitalWrite(D, LOW);
      digitalWrite(E, LOW);
      digitalWrite(F, LOW);
      digitalWrite(G, LOW);
      break;

    case 7:
      digitalWrite(A, LOW);
      digitalWrite(B, LOW);
      digitalWrite(C, LOW);
      digitalWrite(D, HIGH);
      digitalWrite(E, HIGH);
      digitalWrite(F, HIGH);
      digitalWrite(G, HIGH);
      break;

    case 8:
      digitalWrite(A, LOW);
      digitalWrite(B, LOW);
      digitalWrite(C, LOW);
      digitalWrite(D, LOW);
      digitalWrite(E, LOW);
      digitalWrite(F, LOW);
      digitalWrite(G, LOW);
      break;

    case 9:
      digitalWrite(A, LOW);
      digitalWrite(B, LOW);
      digitalWrite(C, LOW);
      digitalWrite(D, LOW);
      digitalWrite(E, HIGH);
      digitalWrite(F, LOW);
      digitalWrite(G, LOW);
      break;
  }
}

