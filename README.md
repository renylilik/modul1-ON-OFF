# modul1-ON-OFF
// Modul Praktikum 1 - Sistem Kendali On-Off
// Nama Tim : Gelayy
// Nama Anggota 1 : Siti Redyta Cahyani
// Nama Anggota 2 : Reny Lilik Badriah
// Deklarasi Variabel Sensor
int sensor1 = A0;
int sensor2 = A1;
int sensor3 = A2;
int sensor4 = A3;
int sensor5 = A4;
int sensor6 = A5;
int baca_sensor[6];

//pin buat enable
int pinEnable =4;
int pinEnable2 = 2;

//pin buat motor kiri
int motor_kiri1 = 5;
int motor_kiri2 = 6;

//pin buat motor kanan
int motor_kanan1 = 3;
int motor_kanan2 = 11;

void setup()
{
  //pinmode input sensor
  pinMode(sensor1, INPUT);
  pinMode(sensor2, INPUT);
  pinMode(sensor3, INPUT);
  pinMode(sensor4, INPUT);
  pinMode(sensor5, INPUT);
  pinMode(sensor6, INPUT);
   
  //pinmode output sensor
  pinMode(pinEnable, OUTPUT);
  pinMode(pinEnable2, OUTPUT);
  pinMode(motor_kiri1, OUTPUT);
  pinMode(motor_kiri2, OUTPUT);
  pinMode(motor_kanan1, OUTPUT);
  pinMode(motor_kanan2, OUTPUT);
  
  Serial.begin(9600);
}

void readsensor() { // untuk membaca sensor kemudian menyimpan Array
  baca_sensor[0] = analogRead(sensor1);
  baca_sensor[1] = analogRead(sensor2);
  baca_sensor[2] = analogRead(sensor3);
  baca_sensor[3] = analogRead(sensor4);
  baca_sensor[4] = analogRead(sensor5);
  baca_sensor[5] = analogRead(sensor6);
  
  Serial.println(baca_sensor[0]);
}

void loop(){
    
    readsensor();
    if (baca_sensor[0] < 34 && baca_sensor[1] < 34 && 
        baca_sensor[2] > 34 && baca_sensor[3] > 34 && 
        baca_sensor[4] > 34 && baca_sensor[5] > 34){
        //motor kanan aktif
      	digitalWrite(pinEnable, HIGH);
        digitalWrite(motor_kiri1, LOW);
        digitalWrite(motor_kiri2, LOW);
        
        digitalWrite(pinEnable2, HIGH);
        digitalWrite(motor_kanan1, HIGH);
        digitalWrite(motor_kanan2, LOW);
    }
    else if (baca_sensor[0] > 34 && baca_sensor[1] > 34 && 
             baca_sensor[2] < 34 && baca_sensor[3] < 34 && 
             baca_sensor[4] > 34 && baca_sensor[5] > 34){
      	//kedua motor aktif
        digitalWrite(pinEnable, HIGH);
        digitalWrite(motor_kiri1, HIGH);
        digitalWrite(motor_kiri2, LOW);
        
        digitalWrite(pinEnable2, HIGH);
        digitalWrite(motor_kanan1, HIGH);
        digitalWrite(motor_kanan2, LOW);
    }
    else if (baca_sensor[0] > 34 && baca_sensor[1] > 34 && 
             baca_sensor[2] > 34 && baca_sensor[3] > 34 && 
             baca_sensor[4] < 34 && baca_sensor[5] < 34){
      	//motor kiri aktif
        digitalWrite(pinEnable, HIGH);
        digitalWrite(motor_kiri1, HIGH);
        digitalWrite(motor_kiri2, LOW);
        
        digitalWrite(pinEnable2, HIGH);
        digitalWrite(motor_kanan1, LOW);
        digitalWrite(motor_kanan2, LOW);
    }
    else if (baca_sensor[0] > 34 && baca_sensor[1] > 34 && 
             baca_sensor[2] > 34 && baca_sensor[3] > 34 && 
             baca_sensor[4] > 34 && baca_sensor[5] > 34){
      	//STOP CONDITION
        digitalWrite(pinEnable, HIGH);
        digitalWrite(motor_kiri1, LOW);
        digitalWrite(motor_kiri2, LOW);
        
        digitalWrite(pinEnable2, HIGH);
        digitalWrite(motor_kanan1, LOW);
        digitalWrite(motor_kanan2, LOW);
    }
  else{}
}
