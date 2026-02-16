---
title: Block Diagram, Protocol, and Message Structure
---

## Block Diagram



## Process Diagram

### Overview

The Process Diagram for our Drone Project is shown below. This diagram displays the what data will be sent, through UART protocol, around the subsystems and where it is intended to go.

```mermaid
%%{init: {'themeVariables': { 'fontSize': '30px'}}}%%
sequenceDiagram
    actor WebUser
    participant MS as Matthew
    participant A as Armando
    participant K as Khalid
    participant V as Vedaa
    participant MC as Manny
    participant L as Lia
    actor InPersonUser
autonumber
    InPersonUser-->>L: move arm to position<br>(X, Y, Z)
    L->>MS: Lia to Armando<br>move arm to position<br>(X, Y, Z)
    WebUser-->>MS: move arm to position<br>(X, Y, Z)
    MS->>A: Matthew to Armando<br>move arm to position<br>(X, Y, Z)
    A->>A: move arm,<br> trash msg
    InPersonUser-->>L: Set speed & Movement<br>[speed]
    L->>MS: Lia to Khalid<br>Set speed & Movement<br>[speed]
    WebUser-->>MS: Set speed & Movement<br>[speed]
    MS->>A: Matthew to Khalid<br>Set speed & Movement<br>[speed]
    A->>K: Matthew to Khalid<br>Set speed & Movement<br>[speed]
    K->>K: Set speed to [speed] and type of movement to [movement],<br>Trash msg
    loop each second
     A->>K: Armando to Everyone<br>Arm is at (X, Y, Z)
    K->>V: Armando to Everyone<br>Arm is at (X, Y, Z)
    V->>MC: Armando to Everyone<br>Arm is at (X, Y, Z)
    MC->>L: Armando to Everyone<br>Arm is at (X, Y, Z)
    L-->>InPersonUser: Display Arm position
    L->>MS: Armando to Everyone<br>Arm is at (X, Y, Z)
    MS-->>WebUser: Display Arm position
    MS->>MS: Display arm position,<br> trash msg.
    K->>V: Khalid to Everyone<br>My speed is [speed]
    V->>MC: Khalid to Everyone<br>My speed is [speed]
    MC->>L: Khalid to Everyone<br>My speed is [speed]
    L-->>InPersonUser: Display Speed
    L->>MS: Khalid to Everyone<br>My speed is [speed]
    MS-->>WebUser: Display Speed
    WebUser->>WebUser: Display speed,<br> trash msg.
      V->>MC: Vedaa to Everyone<br>Microphone output is<br>[sound]
      MC->>L: Vedaa to Everyone<br>Microphone output is<br>[sound]
      L-->>InPersonUser: Display Microphone<br>output wave
      L->>MS: Vedaa to Everyone<br>Microphone output is [sound]
      MS-->>WebUser: Display Microphone<br>output wave
    A->>K: Armando to Khalid<br>Okay to start driving
    K->>K: Turn on driving LED<br>, trash msg.
      InPersonUser-->>L: play sound number<br>[number]
      L->>MS: Lia to Vedaa<br>play sound number<br>[number]
    WebUser-->>MS: play sound number<br>[number]
    MS->>A: Matthew to Vedaa<br>play sound number<br>[number]
    A->>K: Matthew to Vedaa<br>play sound number<br>[number]
    K->>V: Matthew to Vedaa<br>play sound number<br>[number]
    V->>V: play sound number<br>[number],<br>Trash msg
    MC->>L: Manny to Matthew<br>Send Stream Status<br>[Stream Telemetry]
    L-->>InPersonUser: Send Stream Status<br>[Stream Telemetry]
    L->>MS: Manny to Matthew<br>Send Stream Status<br>[Stream Telemetry]
    MS->>WebUser: Send Stream Status<br>[Stream Telemetry]
    MC->>WebUser: Send MJPEG [Image Stream]
    end



```

## Message Types
### Overview:
All message type structure is described by the following:

    ---
    config:
    packet:
        bitsPerRow: 16
        bitWidth: 64
    ---
    packet-beta
    title Message
    0: "0x41"
    1: "0x5a"
    2: "Source ID"
    3: "Dest ID"
    4-61: "Message (Variable Length <= 58 Bytes)"
    62: "0x59"
    63: "0x42"
Byte 0 and 1 signify the start of the message and and 62 and 63 signify the end. Each board will receive messages on the UART chain but will only process it if byte 2: "source ID" matches theirs. If a board receives the a message that was intended for it, it will read the first bit of the message, byte 4, to determine which type of message it is, and use that info to carry out the command described in the following table using the remaining bytes of the message (bytes 5-61).

_Table 1: All message types and descriptions_

| Message type byte 1 (uint8_t) | Description |
| --- | --- |
| 1 | Arm position X, Y, and Z |
| 2 | Armando: arm position X, Y, and Z |
| 3 | Speed and movement type (forward, backward, turn left, turn right, or stop represented by 1 byte integer) |
| 4 | Khalid: my speed and movement type |
| 5 | Video feed stream information |
| 6 | Microphone audio stream information |
| 7 | Speaker audio # that corresponds to sound effect file on audio player (STRETCH GOAL) |

_Message Type 1: Arm XYZ position to Armando_ 

| Byte 1 (uint8_t) | Byte 3(uint8_t) | Byte 4(uint8_t) | Byte 5(uint8_t) |
| --- | --- | --- | --- |
| 1 | X (uint8_t) | Y (uint8_t) | Z (uint8_t) |

_Message Type 2: Arm XYZ position from Armando to HMI display and Webuser_

| Byte 1 (uint8_t) | Byte 3(uint8_t) | Byte 4(uint8_t) | Byte 5(uint8_t) |
| --- | --- | --- | --- |
| 2 | X (uint8_t) | Y (uint8_t) | Z (uint8_t) |

_Message Type 3: Speed and movement type to Khalid_

| Byte 1 (uint8_t) | Byte 3(uint8_t) | Byte 4(uint8_t) |
| --- | --- | --- |
| 3 | speed (uint8_t) | type (uint8_t) |

_Message type 4: Speed and movement type from Khalid to HMI display and webuser_

| Byte 1 (uint8_t) | Byte 3(uint8_t) | Byte 4(uint8_t) |
| --- | --- | --- |
| 4 | speed (uint8_t) | type (uint8_t) |

_Message type 5: Video feed stream information_

| Byte 1 (uint8_t) | Byte 3-58(char) |
| --- | --- |
| 5 | video_info_string |

_Message type 6: Microphone audio feed stream information_

| Byte 1 (uint8_t) | Byte 3-4 (uint16_t) |
| --- | --- |
| 6 | audio (uint16_t) |

_Message type 7: Speaker audio # (STRETCH GOAL)_

| Byte 1 (uint8_t) | Byte 3 (uint8_t) |
| --- | --- |
| 7 | audio # (uint8_t) |