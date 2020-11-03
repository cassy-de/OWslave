# OWslave
OneWire Slave DIY Module



 ATtiny 25, intern 8MHz
 PB4 als Autoincrement-Counters.A, low-aktiv (Pegel), alle 10 Sekunden ein Count
 PB3 ist abgehängt von Counters.B, dafür machen PB0 und PB1 den I2C-Bus für den SRF02 auf 

 lfuse 62
 hfuse DF
 efuse FF


-------------
Zur Firmware:
Die I2C-Libs werden zusätzlich eingebunden, die I2C-Adresse des SRF02 ist fix 0xE0, er wird mit cm als Rückgabewert programmiert. Die Interrupts von
PB3 und PB4 sind disabled, denn PB3 (Counters.B) wird nicht benötigt (ist Messwert des SRF02), und PB4 (Counters.A) wird in der main{} gepollt, dann 10 Sekunden Pause und wieder von vorne, also eigentlich straightforward gelöst. Die I2C-Routine sind atomar gesetzt, dass hier kein IRQ dazwischenfunkt. Somit kann es passieren, dass u.U. der OWFS/OWserver das Device nicht erreicht. Aber lieber in FHEM einen alten Messwert fortschreiben, als einen definitiv falschen eintragen. Achso, in der ISR sind die beiden Increments gelöscht. Und die Extra-Inits für den ATtiny2313 habe ich gleich aus dem Quellcode geschmissen, somit liest es sich etwas leichter.


-------------
OWServer Anzeige:

address 1DA2D984000102F3
counters.ALL 5, 136
counters.A 5
counters.B 136
crc8 F3
family 1D
id A2D984000102

Passt alles soweit, der Brenner lief testweise 55 Sekunden (counters.A ist 5), und bis zum Heizöl sind es  136 cm.

Viel Spass beim Testen.

cassy

