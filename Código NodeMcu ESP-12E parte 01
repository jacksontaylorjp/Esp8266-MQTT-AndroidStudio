#include <ESP8266WiFi.h>
#include <PubSubClient.h>
const char* ssid = "xxxxx"; 
const char* password =  "xxxxx";
const char* mqttServer = "xxxxxx"; 
const int mqttPort = xxxxxx; 
const char* mqttUser = "xxxxxx"; 
const char* mqttPassword = "xxxxxx"; 

WiFiClient espClient;
PubSubClient client(espClient);
/*
-------------------------------------------------
NodeMCU / ESP8266  |  NodeMCU / ESP8266  |
D0 = 16            |  D6 = 12            |
D1 = 5             |  D7 = 13            |
D2 = 4             |  D8 = 15            |
D3 = 0             |  D9 = 3             |
D4 = 2             |  D10 = 1            |
D5 = 14            |                     |
-------------------------------------------------
*/

const int LED1 = 2;
const int LED2 = 0;

void mqtt_callback(char* topic, byte* dados_tcp, unsigned int length);

void setup() { 
  
  pinMode(LED1, OUTPUT);
  pinMode(LED2, OUTPUT);
 
  Serial.begin(115200);
 
  WiFi.begin(ssid, password);
 
  while (WiFi.status() != WL_CONNECTED) 
  {   
     delay(100);
    Serial.println("Conectando a WiFi..");
  }
  Serial.println("Conectado!"); 
  client.setServer(mqttServer, mqttPort);
  client.setCallback(callback);
 
  while (!client.connected()) {
    Serial.println("Conectando ao servidor MQTT...");
    
    if (client.connect("Projeto", mqttUser, mqttPassword ))
    {
 
      Serial.println("Conectado ao servidor MQTT!");  
 
    } else {
 
      Serial.print("Falha ao conectar ");
      Serial.print(client.state());
      delay(2000);
 
    }
  }
 
  client.publish("Status ","Reiniciado!");
  client.publish("Placa","Em funcionamento!");
  client.subscribe("LED"); 
}

void callback(char* topic, byte* dados_tcp, unsigned int length) {
    for (int i = 0; i < length; i++) {
      }
  if ((char)dados_tcp[0] == 'L' && (char)dados_tcp[1] == '1') {
    digitalWrite(LED1, HIGH);   
  } else if((char)dados_tcp[0] == 'D' && (char)dados_tcp[1] == '1'){
    digitalWrite(LED1, LOW);  
  }
  if ((char)dados_tcp[0] == 'L' && (char)dados_tcp[1] == '2') {
    digitalWrite(LED2, HIGH);   
  } else if((char)dados_tcp[0] == 'D' && (char)dados_tcp[1] == '2'){
    digitalWrite(LED2, LOW);  
  }
} 

void loop() {        
     client.loop();
 }
