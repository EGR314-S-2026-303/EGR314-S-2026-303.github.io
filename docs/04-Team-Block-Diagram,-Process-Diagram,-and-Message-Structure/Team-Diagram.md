---
title: Block Diagram, Protocol, and Message Structure
---

## Block Diagram



## Process Diagram

```mermaid

sequenceDiagram

%%{init: {'themeVariables': { 'fontSize': '48px' }}}%%


    actor WebUser
    participant MS as Matthew
    participant A as Armando
    participant K as Khalid

    participant V as Vedaa
    participant MC as Manny
    participant L as Lia
    actor InPersonUser
autonumber
    InPersonUser-->>L: move arm to position (X, Y, Z)
    L->>MS: Lia to Armando<br>move arm to position (X,Y,Z)
    WebUser-->>MS: move arm to position (X, Y, Z)
    MS->>A: Matthew to Armando<br>move arm to position (X, Y, Z)
    A->>A: move arm,<br> trash msg
    InPersonUser-->>L: Set speed and type of movement to [speed]
    L->>MS: Lia to Khalid<br>Set speed and type of movement to [speed]
    WebUser-->>MS: Set speed and type of movement to [speed]
    MS->>A: Matthew to Khalid<br>Set speed and type of movement to [speed]
    A->>K: Matthew to Khalid<br>Set speed and type of movement to [speed]
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
      V->>MC: Vedaa to Everyone<br>Microphone output is [sound]
      MC->>L: Vedaa to Everyone<br>Microphone output is [sound]
      L-->>InPersonUser: Display Microphone output wave
      L->>MS: Vedaa to Everyone<br>Microphone output is [sound]
      MS-->>WebUser: Display Microphone output wave
    A->>K: Armando to Khalid<br>Okay to start driving
    K->>K: Turn on driving LED<br>, trash msg.

    MC->>L: Manny to Matthew<br>Send Stream Status[Stream Telemetry]
    L-->>InPersonUser: Send Stream Status [Stream Telemetry]
    L->>MS: Manny to Matthew<br>Send Stream Status [Stream Telemetry]
MS-->>WebUser: Send Image [Video Stream]
    end
```

## Message Types
_Table 1: All message types and descriptions_
| Message type byte 1-2 (uint16_t) | Description |
| --- | --- |
| 1 | Arm position X, Y, and Z |
| 2 | Armando: arm position X, Y, and Z |
| 3 | Speed and movement type (forward, backward, turn left, turn right, or stop represented by 1 byte integer) |
| 4 | Khalid: my speed and movement type |
| 5 | Video feed stream information |
| 6 | Microphone audio stream information |
| 7 | Speaker audio # that corresponds to sound effect file on audio player (STRETCH GOAL) |

_Message Type 1: Arm XYZ position to Armando_ 

| Byte 1-2 (uint16_t) | Byte 3(uint8_t) | Byte 4(uint8_t) | Byte 5(uint8_t) |
| --- | --- | --- | --- |
| 1 | X (uint8_t) | Y (uint8_t) | Z (uint8_t) |

_Message Type 2: Arm XYZ position from Armando to HMI display and Webuser_

| Byte 1-2 (uint16_t) | Byte 3(uint8_t) | Byte 4(uint8_t) | Byte 5(uint8_t) |
| --- | --- | --- | --- |
| 2 | X (uint8_t) | Y (uint8_t) | Z (uint8_t) |

_Message Type 3: Speed and movement type to Khalid_

| Byte 1-2 (uint16_t) | Byte 3(uint8_t) | Byte 4(uint8_t) |
| --- | --- | --- |
| 3 | speed (uint8_t) | type (uint8_t) |

_Message type 4: Speed and movement type from Khalid to HMI display and webuser_

| Byte 1-2 (uint16_t) | Byte 3(uint8_t) | Byte 4(uint8_t) |
| --- | --- | --- |
| 4 | speed (uint8_t) | type (uint8_t) |

_Message type 5: Video feed stream information_

| Byte 1-2 (uint16_t) | Byte 3-58(char) |
| --- | --- |
| 5 | video_info_string |

_Message type 6: Microphone audio feed stream information_

| Byte 1-2 (uint16_t) | Byte 3-4 (uint16_t) |
| --- | --- |
| 6 | audio (uint16_t) |

_Message type 7: Speaker audio # (STRETCH GOAL)_

| Byte 1-2 (uint16_t) | Byte 3 (uint8_t) |
| --- | --- |
| 7 | audio # (uint8_t) |