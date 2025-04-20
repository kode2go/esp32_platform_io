# esp32_platform_io

```
pip install platformio
```

```
platformio --version
```

```
mkdir wifi_scan_pio
cd wifi_scan_pio
platformio init --board esp32dev
```

Output:

wifi_scan_pio/
├── platformio.ini         <-- Build config
└── src/
    └── main.cpp           <-- Your sketch goes here

> Copy code:

```
#include <Arduino.h>
#include <WiFi.h>

void setup() {
  Serial.begin(115200);
  WiFi.mode(WIFI_STA);
  WiFi.disconnect();
  delay(100);
  Serial.println("Setup done");
}

void loop() {
  Serial.println("Scan start");
  int n = WiFi.scanNetworks();
  Serial.println("Scan done");
  if (n == 0) {
    Serial.println("no networks found");
  } else {
    Serial.print(n);
    Serial.println(" networks found");
    for (int i = 0; i < n; ++i) {
      Serial.printf("%2d | %-32.32s | %4ld | %2ld | ",
        i + 1, WiFi.SSID(i).c_str(), WiFi.RSSI(i), WiFi.channel(i));
      Serial.println();
      delay(10);
    }
  }
  WiFi.scanDelete();
  delay(5000);
}
```

```
platformio run
```

```
platformio run --target upload --upload-port COM9
```

```
platformio device monitor -p COM9 -b 115200
```
