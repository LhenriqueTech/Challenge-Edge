# Challenge Edge

## Descrição do Projeto:
Tinkercad.O projeto no Tinkercad é uma simulação de um sistema IoT que utiliza LEDs e um motor vibratório para representar eventos de uma corrida de Fórmula E. Os LEDs de diferentes cores acendem para indicar situações como "primeiro lugar", "pitstop", "acidente" e "fim de corrida". O motor vibratório é acionado para dar feedback físico sobre esses eventos.


Node-red. O projeto no Node-RED simula uma aplicação de IoT, permitindo monitorar eventos de uma corrida de Fórmula E, como "primeiro lugar", "pitstop", "acidente" e "fim de corrida". O fluxo exibe esses eventos em um dashboard interativo e integra uma API de clima para mostrar a temperatura do local da corrida. Essa simulação reflete como uma aplicação IoT coleta e processa dados de forma inteligente e em tempo real.

## Integrantes do grupo
- Pedro Guidotte Rm: 556630
- Cauã Rodrigues Rm: 555373
- Luiz Henrique Rm: 555235 
- Gabriel Ferreira Rm: 556476
- Felipe Xavier Rm: 556931

## Componentes Utilizados:
- 1 Arduino Uno R3
- 1 Placa de Ensaio
- 4 Resistores 330 Ω
- 1 Led Azul
- 1 Led Vermelho
- 1 Led Amarelo
- 1 Led Branco
- 1 Buzzer

## Link do Video


## Link da simulação no Tinkercad
https://www.tinkercad.com/things/k2r69nuvtGG-challenge-edge?sharecode=D4tLqTpKuc6FzwHcB3TKsrfVKckxGTC19ze2BjxXrgI

## Código do Projeto:

int ledAzul = 3;
int ledAmarelo = 4;
int ledVermelho = 5;
int ledBranco = 6;
int motor = 7;

void setup() {
  pinMode(ledAzul, OUTPUT);
  pinMode(ledAmarelo, OUTPUT);
  pinMode(ledVermelho, OUTPUT);
  pinMode(ledBranco, OUTPUT);
  pinMode(motor, OUTPUT);

  Serial.begin(9600);
  Serial.println("Sistema pronto. Digite 1, P, A ou F no monitor serial.");
}

void loop() {
  if (Serial.available() > 0) {
    char event = Serial.read();

    if (event == '1') {
      Serial.println("Primeiro lugar! Acendendo LED azul e ativando motor (vibração)...");
      digitalWrite(ledAzul, HIGH);
      digitalWrite(motor, HIGH);
      delay(500);
      digitalWrite(ledAzul, LOW);
      digitalWrite(motor, LOW);
      Serial.println("LED azul apagado e motor desligado.");
    }
    else if (event == 'P') {
      Serial.println("Carro no Pitstop! Acendendo LED amarelo e ativando motor (vibração)...");
      digitalWrite(ledAmarelo, HIGH);
      digitalWrite(motor, HIGH);
      delay(300);
      digitalWrite(ledAmarelo, LOW);
      digitalWrite(motor, LOW);
      Serial.println("LED amarelo apagado e motor desligado.");
    }
    else if (event == 'A') {
      Serial.println("Acidente detectado! Acendendo LED vermelho e ativando motor (vibração)...");
      digitalWrite(ledVermelho, HIGH);
      digitalWrite(motor, HIGH);
      delay(1000);
      digitalWrite(ledVermelho, LOW);
      digitalWrite(motor, LOW);
      Serial.println("LED vermelho apagado e motor desligado.");
    }
    else if (event == 'F') {
      Serial.println("Corrida finalizada! Piscando LED branco e ativando motor (vibração rápida)...");
      for (int i = 0; i < 5; i++) {
        digitalWrite(ledBranco, HIGH);
        digitalWrite(motor, HIGH);
        delay(200);
        digitalWrite(ledBranco, LOW);
        digitalWrite(motor, LOW);
        delay(200);
      }
      Serial.println("Fim de corrida! LED branco piscou 5 vezes.");
    }
    else {
      Serial.println("Comando inválido! Digite 1, P, A ou F.");
    }
  }
}
