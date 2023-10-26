const int AUDIO_OUT = 8;
const int TRIGGER_OUT = 2;
const int ECHO_IN = 4;

const int bpm = 60;
const long millisecPerBeat = long((1000 * 60.0)/bpm);

const int noteA4 = 69;
const int noteG4 = 67;
const int noteF4 = 65;
const int noteE4 = 64;
const int noteD4 = 62;
const int noteDb4 = 61;

const float DISTANCE_THRESHOLD_IN_CM = 20.0;

float midi2hz(float midi) {
  return int(pow(2.0, (midi - 69.0) / 12.0) * 440.0);
}

bool isMotionDetected(){

  digitalWrite(TRIGGER_OUT, LOW);  
	delayMicroseconds(2);  
	digitalWrite(TRIGGER_OUT, HIGH);  
	delayMicroseconds(10);  
	digitalWrite(TRIGGER_OUT, LOW); 

  float duration = pulseIn(ECHO_IN, HIGH);  

  float distanceInCm = (duration*.0343)/2; 

  // Serial.println(distanceInCm);

	return distanceInCm < DISTANCE_THRESHOLD_IN_CM;
}

void makeTone(int note, float beat){
  tone(AUDIO_OUT, midi2hz(note));
  delay(long(millisecPerBeat * beat));
  noTone(AUDIO_OUT);
}

void makeSound(){
	makeTone(noteA4, 0.25);
  makeTone(noteG4, 0.25);
  makeTone(noteA4, 1);
  makeTone(noteG4, 0.125);
  makeTone(noteF4, 0.125);
  makeTone(noteE4, 0.125);
  makeTone(noteD4, 0.125);
  makeTone(noteDb4, 0.5);
  makeTone(noteD4, 1);
}	

void setup(){
	Serial.begin(9600);

  pinMode(TRIGGER_OUT, OUTPUT);
  pinMode(ECHO_IN, INPUT);

	pinMode(AUDIO_OUT, OUTPUT);

  // Serial.println(sprintf("ms/beat = %d", millisecPerBeat));
}

void loop(){
	if (isMotionDetected()){
    Serial.println("Motion Detected");
		makeSound();  
  }
  delay(1000);
}
