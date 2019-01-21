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
| ConsoleAngle | console angle |	
| BarrelTemperature| barrel heat |
| LeftTime | the remaining time of the game |
| SupplyDis | distance from supply |
| SupplyUse | Replenishment times |	
| DefenseDis | distance from the defense zone |
| DefenseTime | Remaining defense time |
| DefenseStayTime | Time spent in the defense zone |
| DefenseUse | Whether defensive bonus skills have been used |
#### Enemy state parameter:
##### Good enemy vehicle  status parameters
| parameter name | parameter mean | 
| ------ | ------ |
| GoodHP | Blood volume |
| GoodCoordinate | Coordinates |
| GoodDis | Enemy better chariot distance |
| GoodBatteryDirection | Fortress orientation |	
| GoodSupplyDis| Distance from supply |
| GoodDefenseDis | Distance from the defense zone |
##### Bad enemy vehicle status parameters
| parameter name | parameter mean | 
| ------ | ------ |
| BadHP | Blood volume |
| BadCoordinate | Coordinates |
| BadDis | Enemy better chariot distance |
| BadBatteryDirection | Fortress orientation |	
| BadSupplyDis| Distance from supply |
| BadDefenseDis | Distance from the defense zone |


