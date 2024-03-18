# ID24-TeamB

## TAs ##
- Primary TA: Grace
- Secondary TA: Ellen

## Project: Intelligent Interactive Museum Art Exploration Device ##

## Goal 
Utilize 3D printing technology for creating intelligent replicas and integrate holographic projection with ChatGPT-powered artificial intelligence voice to provide museum visitors with a more interactive experience, fostering a deeper understanding and appreciation of artworks.

## Timeline 
- 11th March 
- 18th March 
- 3 Week easter break 
- 15th April 
- 22nd April 

## Prototype 1 
### James Webb Technologies
- Why the James Webb telescope?
  - The latest telescope, sent out in 2021
  - Has a unique origami feature where the telescope will fold on itself
  - Having a smart replica for users to see how it folds can enhance the experience + current exhibits does not show it
  - Showcasing the images from the telescope provides a more immersie experience

- James Webb Deployment sequence: https://webbtelescope.org/contents/media/videos/1058-Video
- 3D STL file: https://www.printables.com/model/109816-unfolding-james-webb-space-telescope-jwst
- Current exhibitions for James webb
  - https://www.nasa.gov/missions/webb/nasas-webb-telescope-inspires-artechouse-exhibit-public-art/
  - https://hk.space.museum/en/web/spm/exhibitions/permanent-exhibition/jwst.html

![image](https://github.com/UoB-Interactive-Devices/ID24-TeamB/assets/89033445/22ead702-fa92-47d1-bda9-9ef964106080)

### 4 Confirmed features:
1. Projection with MPU6050 and project different image
2. Light sensitive to the sun, red LED starts blinking because too hot (finished)
3. Closing closes the projection
4. ChatGPT voice recognition?

## Reference
### 3D Object Visualization using Interactive Holographic Projection
    https://ieeexplore.ieee.org/abstract/document/9297919

## Thesis
https://www.overleaf.com/9798541461hjnprxnddsvw#2e7680



# Implementation of MPU6050 control projector
#include <Wire.h>
#include <MPU6050.h>

MPU6050 mpu;

void setup() {
  Serial.begin(115200);
  Wire.begin();
  mpu.initialize();
  if (!mpu.testConnection()) {
    Serial.println("MPU6050 connection failed");
    while(1);
  }
}

void loop() {
  // 结构体用于存储加速度和陀螺仪数据
  int16_t ax, ay, az;
  int16_t gx, gy, gz;

  // 读取原始加速度和陀螺仪值
  mpu.getMotion6(&ax, &ay, &az, &gx, &gy, &gz);

  // 发送数据到串口
  Serial.print("aX = "); Serial.print(ax);
  Serial.print(" | aY = "); Serial.print(ay);
  Serial.print(" | aZ = "); Serial.print(az);
  Serial.print(" | gX = "); Serial.print(gx);
  Serial.print(" | gY = "); Serial.print(gy);
  Serial.print(" | gZ = "); Serial.println(gz);

  delay(100); // 稍作延迟以便观察
}




# Accept code in python and control image changes

import serial
import time

# 更换成你的串口名
ser = serial.Serial('COM3', 115200, timeout=1)
time.sleep(2) # 等待连接稳定

try:
    while True:
        if ser.in_waiting > 0:
            line = ser.readline().decode('utf-8').rstrip()
            print(line)
            # 根据line的值来显示不同的图片
            # 这里需要你根据实际情况来编写代码
except KeyboardInterrupt:
    print("程序结束")
finally:
    ser.close()




