# MotionDetector
How to use a pyroelectric infrared sensor (PIR) to detect movement.

![alt tag](https://github.com/adestefa/MotionDetector/blob/master/linearfresnel.gifpir2.jpg)

PIRs are basically made of a pyroelectric sensor that can detect levels of infrared radiation. They are often referred to as PIR, "Passive Infrared", "Pyroelectric", or "IR motion" sensors. Everything emits some low level radiation, the PIR sensor is designed to see this energy and has a simple way to use this to detect motion. The PIR sensor does not return distance to target, instead it compares two infrared images by splipting the sensor in half. Any difference between the heat signatures in both images will constitute movement and the sensor sends a high signal.

When a warm body passes by the first half of the sensor it causes a positive differential change between the two halves. When the warm body leaves the sensing area, the reverse happens and the sensor generates a negative differential change. These change pulses are what is detected.

# How are they so sensitive?

They are great for seeing movement and are widely used in home spotlights and commercial automatic doors. The plastic window covering holds the real secret. It has multiple facets molded into it to consolidate and focus the scattered infrared energy onto the sensor.

![alt tag](https://github.com/adestefa/MotionDetector/blob/master/linearfresnel.gif) 

Each individual facet is a Fresnel lens. They are famously used in lighthouses to direct and amplify light out. The Fresnel lens here is designed to amplify the scattered infrared energy in the opposite direction, from the room into the sensor by capturing and redirecting a larger area of energy than the actual sensor could read by itself.

Now that we understand the sensor, let's see how to drive it with an Arduino and some simple code.

This curciut will use an LED and a PIR sensor. Both will be connected to common ground and 5V. 

'int ledPin = 13;'    

'int inputPin = 2;'  

After setup, the loop is very simple and all we have to do is read for when the PIN we associate to the PIR sensore (2) in this case, goes high, we know the sensor has been tripped:

```
void loop(){
  val = digitalRead(inputPin);  // read input value
  if (val == HIGH) {            // check if the input is HIGH
    digitalWrite(ledPin, HIGH);  // turn LED ON
    if (pirState == LOW) {
      // we have just turned on
      Serial.println("Motion detected!");
      // We only want to print on the output change, not state
      pirState = HIGH;
    }
  } else {
    digitalWrite(ledPin, LOW); // turn LED OFF
    if (pirState == HIGH){
      // we have just turned of
      Serial.println("Motion ended!");
      // We only want to print on the output change, not state
      pirState = LOW;
    }
  }
}
```


