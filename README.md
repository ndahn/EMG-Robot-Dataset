# About this dataset
This dataset was recorded by Mohammed Fakih as part of his bachelor thesis in July 2022. Data was recorded from 6 females and 6 males between 16 and 46 years with no known muscular particularities. The data was recorded from the right arm using 5 Myoware sensors (generation 1) and an GY-521 IMU. Each sensor was attached to an MCP 3221 ADC, which in turn were chained together using the I2C protocol (I2C fast, i.e. 400kHz). 

Due to the fact that sensors were in series, reading values would take multiple clock cycles and the way the code for reading data was written, the resulting sampling frequency was about 500Hz. The code used for reading, preprocessing and live-processing the data can be found at (EMG-Robot)[https://github.com/ndahn/EMG-Robot]. 

When recording data, sensors were placed above the following muscles
* Biceps
* Triceps 
* Brachioradialis 
* Pronator teres
* Supinator

The IMU was attached to the back of the wrist. This order of muscles corresponds to the order of the channels in the CSV files (emg_0 to emg_4). After the EMG sensors, the IMU's accelerometer and gyroscope readings were recorded. The final column (_dt_) is the time since the beginning of the last readout. Since sensors could not be read in parallel, the recorded signals would be staggered if timestamps were recorded for each sensor.

During the recording, participants were initially resting their arm on an arm rest in a relaxed position. They were then asked to go through a series of motions, briefly stopping after each. Their are 4 positions of forearm flexion, roughly corresponding to 0, 30, 60 and 90° relative to the starting position; as well as 3 positions of forearm supination, corresponding to 0, 90 and 180°, where 0° corresponds to palm facing downwards. The order of motions was chosen in such a way that all possible combinations as well as all possible transitions would be covered (e.g. moving from 90° to 30° flexion at 180° supination).

The following table illustrates the order of motions. 

| flexion | supination |
| --- | --- |
| 0°, 30°, 60°, 90°  | 0°, 90°, 0° |
| 90°, 60°, 30°, 0° | 90°, 0°, 90° |
| 0°, 60°, 30°, 90° | 180°, 0°, 180° |
| 90°, 30°, 60°, 0° | 0°, 180, 0° |
| 0°, 90°, 60°, 30° | 90°, 180°, 90° |
| 30°, 60°, 90°, 0° | 180°, 90°, 180° |

When moving between flexion angles, the supination would be maintained. Once the new flexion is reached, the participant would iterate over the supinations and then proceed to the next flexion angle. For example, the first line of the above table means that the participant would start at 0° flexion and rotate their forearm to 0°, then 90°, then back to 0° supination. Then they would move to 30° flexion and repeat these supinations. This continues until they reach 90° flexion. 

Ideally, participants should wait at least 1-2s after each movement, but due to the length of the recording (about 30 minutes) participants would often only make very short breaks, especially towards the end. 

If you need more information or feel like anything was unclear, feel free to drop me a message or open an issue and I will do my best to answer!