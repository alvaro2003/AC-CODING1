# AC-CODING1
//DECLARA LED
const int vermelho = 5;
const int verde = 6;
const int amar = 7;

bool estadoLedVermelho = false;

 //DECLARA BOTÃO
const int botao1 = 2;
const int botao2 = 3;
unsigned long lastDebounceTime1 = 0;
unsigned long lastDebounceTime2 = 0;
const int botaoDelay = 100;

void setup()
{
  pinMode(A0, INPUT);
  pinMode(A1, INPUT);
  pinMode(vermelho, OUTPUT);
  pinMode(verde, OUTPUT);
  pinMode(amar, OUTPUT);
  
  Serial.begin(9600);
  Serial.println("AC1-byte slayers proj1 2021");
}
 //LIGAR LEDS
void loop()
{
  if((millis() - lastDebounceTime1) > botaoDelay && digitalRead(botao1)){
      Serial.println("botao 1 apertado");
    ledVermelho(true);
      lastDebounceTime1 = millis();
  }
  if((millis() - lastDebounceTime2) > botaoDelay && digitalRead(botao2)){
      Serial.println("botao 2 apertado");
    ledVermelho(false);
      lastDebounceTime2 = millis();
  }
  if(getTemperatura() > 15){
    ledAmar(true);
    Serial.println("temepatura elevada");
  }else{
      ledAmar(false);
    Serial.println("temepatura ideal");
  }
      if(getLuminosidade() > 5){
    ledVerde(true);
    Serial.println("luminosidade elevada");
  }else{
      ledVerde(false);
    Serial.println("luminosidade ideal");
  }
  delay(10);
}
 //DECLARA FUNÇÃO LED
void ledVermelho(bool estado){
 digitalWrite(vermelho,estado);
}
void ledVerde(bool estado){
 digitalWrite(verde,estado);  
}
void ledAmar(bool estado){
    digitalWrite(amar,estado);
}

int getTemperatura(){
      int temperaturaC;
    temperaturaC = map(((analogRead(A0) - 20) * 3.04), 0, 1023, -40, 125);
      return temperaturaC;
} 
 //LUMINOSIDADE
int getLuminosidade(){
      int luminosidade;
    luminosidade = map(analogRead(A1), 6, 619, -3, 10);
      return luminosidade;
}
![image](https://user-images.githubusercontent.com/78906921/113325488-e4987300-92ee-11eb-980f-ad2a9299a610.png)
