## State Space
#### Robot Param:
| Name | Dtype | Description | 
| ------ | ------ | ------ |
| Pitch | float | pitch angle of gimbal |
| Yaw | float | yaw angle of gimbal |
| Angle | float | angle of chassis |
| X | float | absolute coordinate of robots on x-axis |
| Y | float | absolute coordinate of robots on y-axis |

	
#### Competition Param:
| Name | Dtype | Description | 
| ------ | ------ | ------ |
| Time | float | competition time |
| HP | float | blood volume |
| Bullet | int | bullets left |
| Heat | float | barrel heat |
| Use-Supply | int | supply times have used |
| Time-Bonus | float | defense bonus time left |
| Time-Stay | float | time stayed in the defense bonus zone |	
| Is-Use | bool | whether defensive bonus has been used |	


## Model inputs

#### 1. full `Robot Param` and `Competition Param` of self-robots

#### 2. observed or predicted `Robot Param` and `Competition Param` of enemy-robots

#### 3. computed params below of self-robots and enemy-robots
| Name | Dtype | Description |
| ------ | ------ | ------ |
| Dis-Supply | float | distance[1] to supply |
| Dis-Defense | float | distance to the defense bonus zone |
| Dis-Robots | float | distance between robots |

[1] All distances refer to motion planning distance.
