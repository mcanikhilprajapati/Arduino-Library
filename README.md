# Arduino
A short Android library to communicate with Arduino through usb.

# Gradle

    compile 'me.aflak.libraries:arduino:1.0'

# Usage

    Arduino arduino = new Arduino(this);
    arduino.registerReceiver(new ArduinoListener() {
        @Override
        public void onArduinoAttached(UsbDevice device) {
            arduino.open(device);
        }

        @Override
        public void onArduinoDetached() {
            // arduino detached from phone
        }

        @Override
        public void onArduinoMessage(byte[] bytes) {
            String message = new String(bytes);
            // new message received from arduino
        }

        @Override
        public void onArduinoOpened() {
            // you can start the communication
            String str = "Hello Arduino !";
            arduino.sendMessage(str.getBytes());
        }
    });
    
    @Override
    protected void onDestroy() {
        super.onDestroy();
        arduino.closeArduino();
        arduino.unregisterReceiver();
    }

# Arduino Side

Example code which sends back every character received

    void setup() {
      Serial.begin(9600);
    }

    void loop() {
      if(Serial.available()){
        char c = Serial.read();
        Serial.print(c);
      }
    }

# Special thanks

This code is using UsbSerial library : [https://github.com/felHR85/UsbSerial](https://github.com/felHR85/UsbSerial)
