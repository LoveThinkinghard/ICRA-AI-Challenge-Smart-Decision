## Definition of State Space
#### Robot information parameter:
| Name | Description | 
| ------ | ------ |
| Pitch | pitch angle of gimbal |
| Yaw | yaw angle of gimbal |
| Angle | angle of chassis |
| Coordinate | coordinates of robot |

	
#### Game information parameter:
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


## State parameter of the robot:
#### Self state parameter:
| parameter name | parameter mean | 
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
#### Enemy state parameter:
##### Good enemy vehicle  status parameters
| parameter name | parameter mean | 
| ------ | ------ |
| Good-HP | Blood volume |
| Good-Coordinate | Coordinates |
| Good-Dis | Enemy better chariot distance |
| Good-Battery-Direction | Fortress orientation |	
| Good-Supply-Dis| Distance from supply |
| Good-Defense-Dis | Distance from the defense zone |
##### Bad enemy vehicle status parameters
| parameter name | parameter mean | 
| ------ | ------ |
| Bad-HP | Blood volume |
| Bad-Coordinate | Coordinates |
| Bad-Dis | Enemy better chariot distance |
| Bad-Battery-Direction | Fortress orientation |	
| Bad-Supply-Dis| Distance from supply |
| Bad-Defense-Dis | Distance from the defense zone |


