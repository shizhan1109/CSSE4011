# Athena‐yellow

We are team Athena‐yellow!

Our wiki <https://github.com/shizhan1109/Athena-yellow/wiki/Index>

Our team members: Zhan Shi, Huantao Li


## Scenario Description
The primary objective of Athena-yellow is to develop a highly functional and user-friendly multi-display system that seamlessly integrates hardware and software components. 

## Team Member List and Roles

48323626, Zhan Shi : Develop the blue board software. Set up the Bluetooth communication protocol. Coordinate software development tasks. Spearheaded the development of software for the M5 board using zephyr.

46435244, Huantao Li : Develop the m5 board software. Implement GUI features. Integrate sensor functionalities. Modify the overall design when developing m5 by zephyr. Test and debug the m5 board.

Our Team photo:![f07b50b5be926adcfd38b5b67149386](https://github.com/shizhan1109/Athena-yellow/assets/80838084/3b50257d-849e-4f5c-8f7c-9c885ae798e1)


## This is our timeline.

| time   | progress                                                                          |
| ------ | --------------------------------------------------------------------------------- |
| week9  | Show image and animation on one display                                           |
| week10 | Use TCP trans from client to sever(display), Show ip on display, Connect to Wi-Fi |
| week11 | Show image and screen casting on 9 displays                                       |
| week12 | Fixing bugs and preparing demo                                                    |

## Devices

- 9 m5stack core2
- 1 nRF52840 DK(blue board)
- 1 GUI on PC

## KPIs

- **MotionTracking sensor**. Shaking on, shaking off. A fast way to switch on and off screen.
- **Performance**. FPS > 1 which is low because compromises for the sake of time synchronization.
- **Auto wifi connecting**. Bluetooth advertising Wi-Fi information. No need input or fix configuration.
- **GUI**. Synchronized display 9 screens states.
- **Computer vision**. Integrate image processing technic like image filtering and edge detection.(planed but not done)
- **More than image**: We achieve screen casting.



## DIKW

![image](https://github.com/shizhan1109/Athena-yellow/assets/80838084/d1e2cfdc-3a25-4ee8-a864-81aba5bf2205)

Data:
Pixels: The individual points of color that make up images.
Frames: The sequential images that create animation.
These elements are fundamental but lack context and meaning without further processing.

Information:
Meaningful Images: Combining pixels to form recognizable images.
Interesting Animations: Sequencing frames to create engaging visual content.
At this stage, the system transforms raw data into a format that can convey specific messages or tell a story, making it useful for display purposes.

Knowledge:
Assembling Displays: Configuring multiple M5Core2 displays to function as a larger, cohesive display unit.
System Synchronization: Ensuring that all screens are perfectly synchronized to provide a seamless visual experience.
Here, the system leverages the structured information to create a unified display environment, enabling more complex applications and interactions.

Wisdom:
Cross-Screen Operation and Self-Assembled Displays:
This includes enabling displays to function collectively, adapting dynamically to new configurations, and optimizing for user interactions and environmental conditions.

## Overview

![image](https://github.com/shizhan1109/Athena-yellow/assets/80838084/856e87d5-0ac6-4b45-af45-918d94dd5734)


## Network

![image](https://github.com/shizhan1109/Athena-yellow/assets/80838084/8670f2df-11c8-4128-be67-93b0e6b9c85e)


## Deploy

**Initialize**

1. FLash the 9 m5core2s,
2. Connect WiFi lihuantao.

**Reach network**

1. Push reset button. M5core2s shows *waiting for Wi-Fi*. In the GUI, all the M5 icons turn red.
2. Input Wi-Fi configuration `wifi csse4011demo-csse4011` in the blue board. The blue board will advertising configuration.
3. The M5core2s connect to the new Wi-Fi, and show SSID, mac addr and IP on display. The 9 displays synchronize by NTP server.
4. The M5core2s register IP to router, the GUI collects 9 IPs through mDNS protocol. In the GUI, click **search** button, the connected m5core2s' icons turn green. Place the m5 to the corresponding location.

**Let's play**

7. In the GUI, click **run**, start screen casting.
8. Show one image in 9 displays. Shake it to turn on display.
9. Play an animation and even a video.

## Sensor

MotionTracking MPU-6886

We utilize gravity accelerometers along the X, Y, and Z axes! Any axe changes will trun on/off display.

![image](https://github.com/shizhan1109/Athena-yellow/assets/80838084/649c4ccb-1c05-4762-be15-e990ea7cf896)
![image](https://github.com/shizhan1109/Athena-yellow/assets/80838084/390f1c4b-f714-478d-89f5-aba7e5102c82)


## Build this project

### m5_zephyr (abandon)
<https://docs.zephyrproject.org/latest/boards/m5stack/m5stack_core2/doc/index.html>
<https://github.com/IlievIliya92/esp32_zephyr>

west config build.board m5stack_core2/esp32/procpu  
west build m5_zephyr -p -DSSID="csse4011demo" -DPSK="csse4011"  
west flash  
west espressif monitor  

### m5_arduino
- select board: M5Stack-Core2
- flash: m5_arduino\m5_tcp_server\m5_tcp_server.ino

### blue
west build Athena-yellow/blue --pristine
west flash
minicom -c on -D /dev/ttyACM0

### GUI
python3 GUI\pyqt.py

## Logging
west build zephyr/tests/bluetooth/shell --pristine

minicom -c on -D /dev/ttyACM0

set once
*D8:16:AD:C5:7D:29*
bt id-create D8:16:AD:C5:7D:29
bt id-show

bt adv-create conn-scan identity
bt adv-info
*csse4011demo-csse4011*
bt adv-data 1609637373653430313164656d6f2d6373736534303131
bt adv-start

`wifi csse4011demo-csse4011`

rm -rf ~/cheese/Athena-yellow/.git;cp -r ~/Documents/Athena-yellow/.git ~/cheese/Athena-yellow/
