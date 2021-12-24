+++
title = "Verbinden mit AWS IoT Core"
weight = 30
pre = "<b>c. </b>"
+++

In diesem Kapitel konfigurieren, erstellen und flashen Sie Ihre Gerätefirmware, die eine Verbindung zu AWS IoT Core herstellt. Um eine Verbindung zu AWS IoT Core herzustellen und mit diesem zu kommunizieren, müssen Sie Ihr Gerät mit Wi-Fi-Anmeldeinformationen und der URL Ihres AWS-Endpunkts konfigurieren. Die Konnektivität wird durch die vorbereiteten Zertifikate im Microchip ATECC608 Trust&amp;GO vereinfacht, die unserem AWS IoT-Ding zugewiesen und an eine Sicherheitsrichtlinie aus dem vorherigen Kapitel angehängt sind. Sie müssen keine Zertifikate von AWS IoT Core abrufen oder Ihre eigenen generieren. Zum Konfigurieren, Erstellen und Flashen unserer Firmware auf den Espressif ESP32-D0WD verwenden Sie das ESP-IDF.

## Konfigurieren der ESP32-Firmware
Die Konfiguration Ihres Quellcodes wird über [Kconfig](https://www.kernel.org/doc/html/latest/kbuild/kconfig-language.html) abgewickelt. Kconfig ist das gleiche Konfigurationssystem, das vom Linux-Kernel verwendet wird, und hilft dabei, die verfügbaren Konfigurationsoptionen (Symbole) in einer Baumstruktur zu vereinfachen. 

Sie können das Konfigurationsmenü aus dem **Blink-Hello-World** Verzeichniss des Repositorys aufrufen:
```bash
idf.py menuconfig
```
{{< img "idf_menuconfig-aws_endpoint.en.webp" "Configuring Core2 for AWS IoT EduKit with idf.py menuconfig" >}}
Hier werden Sie die Konfiguration einstellen. Verwenden Sie die Richtungstasten auf Ihrer Tastatur, wählen Sie dann **AWS IoT EduKit Configuration** aus dem Menü. Stellen Sie Ihre **WiFi SSID** und Ihr **WiFi Password** mit Ihren Wi-FI-Anmeldedaten ein. Wenn Sie fertig sind, drücken Sie die *s-Taste* auf Ihrer Tastatur, um zu speichern, bestätigen Sie den Speicherort der Datei mit der *Eingabetaste*, gefolgt von *q* zum Beenden.

{{% notice warning %}}
Stellen Sie sicher, dass Ihre SSID für ein 2,4-GHz-Netzwerk ist. Der ESP32-D0WD auf der M5Stack Core2 for AWS-Hardware unterstützt kein 5GHz-Wi-Fi.
{{% /notice %}}

## Erstellen der ESP32-Firmware
Das Erstellen der Firmware ist einfach, kann aber beim ersten Mal eine ganze Weile dauern. ESP-IDF verwendet CMAKE als Build-System und verlinkt alle notwendigen Dateien und beginnt mit der Kompilierung des Codes zu einer flashbaren Binärdatei im ELF-Format, die auf das Gerät geflasht werden kann.
```bash
idf.py build
```

## Alte Firmware löschen
Wenn Sie die Einführung oder die Alexa-Demo abgeschlossen haben, empfiehlt es sich, den Flash-Speicher Ihres Geräts zu löschen. Der Flash-Speicher ist in separate Partitionen aufgeteilt, in denen die Anwendungsdaten, OTA-Daten und Schlüssel gespeichert sind. Die anderen Walk-Throughs verwenden eine andere Partitionstabelle als in diesem Lernprogramm und könnten Probleme verursachen, wenn sie nicht gelöscht werden. Ersetzen Sie **<<DEVICE_PORT>>** durch den seriellen Port, an den Ihr Core2 for AWS IoT EduKit-Gerät angeschlossen ist:
```bash
idf.py erase_flash  -p <<DEVICE_PORT>>
```

## Flashen der ESP32-Firmware und Überwachung der Geräteausgabe über die serielle Schnittstelle
Um die soeben erstellte Firmware zu flashen und alle Ausgaben des Geräts über die serielle Verbindung anzuzeigen geben sie den folgenden Befehl ein:
```bash
idf.py flash monitor -p <<DEVICE_PORT>>
```
Sobald das Gerät geflasht ist, wird es neu gestartet und die Anwendung ausgeführt. Sie sollten sehen, dass sich das Gerät mit Ihrem WLAN-Netzwerk verbindet, eine sichere MQTT-Verbindung zu AWS IoT Core herstellt, das voreingestellte MQTT-Thema abonniert und beginnt, Nachrichten zu senden.

## Zwischenfazit
In diesem Kapitel haben Sie Ihr Gerät erfolgreich kompiliert, geflasht und somit die aktiven seriellen Ausgaben überwacht. Mit dem AWS IoT Device SDK for Embedded C hat sich die Hardware beim MQTT Message Broker (AWS IoT Core) authentifiziert und ist bereit, Nachrichten zu empfangen.

Sie sind nun bereit für das letzte Kapitel in diesem Lernprogramm, das [Blinken der LED](/de/blinky-hello-world/blinking-the-leds.html).


---
{{% button href="https://github.com/aws-samples/aws-iot-edukit-tutorials/discussions" icon="far fa-question-circle" %}}Community support{{% /button %}} {{% button href="https://github.com/m5stack/Core2-for-AWS-IoT-EduKit/issues" icon="fas fa-bug" %}}Report bugs{{% /button %}}