## State Space
#### Robot information parameter:
| Name | Description | 
| ------ | ------ |
| Pitch | pitch angle of gimbal |
| Yaw | yaw angle of gimbal |
| Angle | angle of chassis |
| Coordinate | coordinates of robot |

	
#### Competition information parameter:
| Name | Description | 
| ------ | ------ |
| Time | competition time |
| HP | blood volume |
| Bullet | bullets left |
| Heat | barrel heat |
| Supply-Use | supply times have used |
| Bonus-Time | defense bonus time left |
| Stay-Time | time stayed in the defense bonus zone |	
| Is-Use | whether defensive bonus has been used |	


## Observation or input of our model:
#### Self parameter:
| Name | Description | 
| ------ | ------ |
| HP | blood volume |
| Bullet | Bullets |
| Coordinate | coordinates |
| Console-Angle | console angle |	
| Heat| barrel heat |
| Time | competition time |
| Supply-Dis | distance from supply |
| Supply-Use | Replenishment times |	
| Defense-Dis | distance from the defense zone |
| Bonus-Time | bonus defense time left |
| Stay-Time | Time spent in the defense zone |
| Is-Use | Whether defensive bonus skills have been used |
#### Enemy parameter:
| Name | Description | 
| ------ | ------ |
| HP[1] | Blood volume |
| Coordinate[1] | Coordinates |
| Dis | Enemy better chariot distance |
| Supply-Dis| Distance from supply |
| Defense-Dis | Distance from the defense zone |

[1] If we get them 
