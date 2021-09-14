// Firmware de Integração dos Atuadores e Sensores
// Carro Desviando de Obstáculos
//

//******************************************************************************************
// Definições de Constantes
#define trigE  3                 // Pino Trigger Sensor Esquerda
#define echoE  4                 // Pino Echo Sensor Esquerda
#define trigD 12                 // Pino Trigger Sensor Direita 
#define echoD 11                 // Pino Echo Sensor Direita 
#define ENA   10                 // Pino de habilitação do motor da Direita
#define IN1    9                 // Pino de ativação Motor da direita no sentido Anti-Horário  
#define IN2    8                 // Pino de ativação Motor da direita no sentido Horário   
#define IN3    7                 // Pino de ativação Motor da esquerda no sentido Anti-Horário   
#define IN4    6                 // Pino de ativação Motor da esquerda no sentido Horário  
#define ENB    5                 // Pino de habilitação do motor da Esquerda   

//******************************************************************************************
// Protótipos de Funções Auxiliares
int sensorE(void);               // Retorna a distância do obstáculo em milimetros
int sensorD(void);               // Retorna a distância do obstáculo em milimetros
void movAvante(unsigned char);   // Aciona motores para avançar em linha reta
void movRe(unsigned char);       // Aciona motores para recuar  em curva
void movCurvaDireita(void);      // Aciona motores para desviar à direita
void movCurvaEsquerda(void);     // Aciona motores para desviar à esqueda

//******************************************************************************************
// Variáveis Globais
int distE, distD;

//******************************************************************************************
// Configurações de Inicialização do Arduino
void setup()
{
  Serial.begin(9600);
  pinMode(trigE,  OUTPUT);
  pinMode(trigD,  OUTPUT);
  pinMode(echoE, INPUT);
  pinMode(echoD, INPUT);
  pinMode(IN1, OUTPUT);
  pinMode(IN2, OUTPUT);
  pinMode(IN3, OUTPUT);
  pinMode(IN4, OUTPUT);
  pinMode(ENA, OUTPUT);
  pinMode(ENB, OUTPUT);


}

//******************************************************************************************
// Lógica Principal em Execução Cíclica
void loop()
{

  distE = sensorE();
  delay(10);
  distD = sensorD();
  delay(10);

  Serial.print("Sensor E: ");
  Serial.print(distE);
  Serial.print("  Sensor D: ");
  Serial.println(distD);
  //delay(1000);
  //||


  if ((distD == 0) && (distE == 0) || (distD == 0) && (distE > 200) || (distD > 200) && (distE == 0) || (distD > 200) && (distE > 200)) // Anda para frente
  {
    movAvante(190);
    delay(50);
    Serial.println("va em frente");
  }
  if (  ((distE > 0) && (distE < 200 )) && (distD > 200) || ( (distE > 0 ) && (distE < 200) && (distD == 0) ) ) // Vira para direita
  {
    movCurvaDireita();
    delay(150);
    movAvante(0);
    delay(10);
    Serial.println("vire a direita");
  }

  if ( ( ( (distD > 0) && (distD < 200) ) && (distE > 200) ) || ( ( (distD > 0) && (distD < 200) )&& (distE == 0) ) ) // Vira para esquerda
  {
    movCurvaEsquerda();
    delay(150);
    movAvante(0);
    delay(10);
    Serial.println("vire a esquerda");
  }
  if ( ( (distE > 0) && (distE < 200) )&& ( (distD > 0) && (distD < 200) ) ) // DA RÈ
  {
    movRe(120);
    delay(400);
    Serial.println("dê ré");
  }
}

//******************************************************************************************
// Implementações das Funções Auxiliares do Projeto

int sensorE(void)
{
  digitalWrite(trigE, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigE, LOW);
  return (10 * pulseIn(echoE, HIGH, 3500) / 58); // milimetros
}

int sensorD(void)
{
  digitalWrite(trigD, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigD, LOW);
  return (10 * pulseIn(echoD, HIGH, 3500) / 58); // milimetros
}

#define IN1    9                 // Pino de ativação Motor da direita no tras
#define IN2    8                 // Pino de ativação Motor da direita frent
#define IN3    7                 // Pino de ativação Motor da esquerda tras  
#define IN4    6                 // Pino de ativação Motor da esquerda frent 

void movAvante(unsigned char vel)
{
  analogWrite(ENA, vel);
  analogWrite(ENB, vel);
  Serial.println("1");
  digitalWrite(IN1, LOW);
  digitalWrite(IN2, HIGH);
  digitalWrite(IN3, LOW);
  digitalWrite(IN4, HIGH);
}

void movRe(unsigned char vel)
{
  analogWrite(ENA, vel);
  analogWrite(ENB, vel);
  Serial.println("2");
  digitalWrite(IN1, HIGH);
  digitalWrite(IN2, LOW);
  digitalWrite(IN3, HIGH);
  digitalWrite(IN4, LOW);
}

void movCurvaDireita()
{
  analogWrite(ENA, 100);
  analogWrite(ENB, 150);
  Serial.println("3");
  digitalWrite(IN1, HIGH);
  digitalWrite(IN2, LOW);
  digitalWrite(IN3, LOW);
  digitalWrite(IN4, HIGH);
}

void movCurvaEsquerda()
{
  analogWrite(ENA, 150);
  analogWrite(ENB, 100);
  Serial.println("foi");
  digitalWrite(IN1, LOW);
  digitalWrite(IN2, HIGH);
  digitalWrite(IN3, HIGH);
  digitalWrite(IN4, LOW);
}
