# Project Diana
This project is to create a framework for capturing and conserving analog video in digital form for eternity. The analog NTSC, PAL or SECAM signal will be recorded with a high enough bandwidth to ensure signal integrity depending of the quality level of the input signal.

# Format specifications
Project Diana specifies two different file formats for different purposes
* [Composite video](<#File-format-specification-for-composite-formats>)
* [RF file format for Tapes, discs and more](#RF-file-format)
---
## File format specification for composite formats
Each frame contains one second of NTSC, PAL or SECAM compsite video material.

### **Space requirement and quality (bandwidth) levels**
There are 4 bandwidth levels specified for different source materials
* LEVEL 0: 48dB SNR and 6.3MHz bandwidth: 12582908 byte per second - VHS, Beta3, ...
* LEVEL 1: 48dB SNR and 8.4MHz bandwidth: 16777212 byte per second - SVHS, BVeta2, ...
* LEVEL 2: 96dB SNR and 6.3MHz bandwidth: 25165820 byte per second - Beta1, CED, LaserDisc, ...
* LEVEL 3: 96dB SNR and 8.4MHz bandwidth: 33554428 byte per second - LaserDisc, Beta1, Studio Masters, ...

### Frame structure

| SYNC   | Info Byte | Data                   |
|--------|-----------|-                       |
| 02C9AD | 43        | 33554428 bytes of data |

### **Magic synchronization byte sequence**
```
02C9AD
```

### **INFO BYTE**
```
BITS 0-1 : Format; 00=NTSC 01=PAL 10=SECAM 11=INVALID
BITS 2-5 : Format extension [table](<#Format extension table>)
BITS 6-6 : Bandwidth; 0=6.3 1=8.4 (MHz) (Note: For 48dB SNR it's 6291454 or 8388606 Hz, but for 96dB SNR it's 6291455 and 8388607 Hz)
BITS 7-7 : SNR; 0=48 1=96 (dB) / 0=8 1=16 (bits)
```

### **DATA - One second per frame**
```
For 96dB SNR and 8.4MHz bandwidth: 33554428 byte per frame (second)
For 96dB SNR and 6.3MHz bandwidth: 25165820 byte per frame (second)
For 48dB SNR and 8.4MHz bandwidth: 16777212 byte per frame (second)
For 48dB SNR and 6.3MHz bandwidth: 12582908 byte per frame (second)
```
### **Format extension table**
* PAL
    ```
    0000=PAL-B
    ```
*... to be continued*


## RF file format
*... to be continued*