# **The design of reward function**

We can define the advantages of current situation by a reward function, and evaluate the current operation by the difference of the reward function between two time points. The reward function can be divided into five modules: danger degree, supply reward, defense bonus reward, team cooperation reward and limitation of map obstacles. Finally, we use `TeamworkValue()` as a reward function for a combat vehicle.

## **1. Danger degree**
Definition of danger degree: It mainly evaluates the current blood volume of the car and the remaining time of game. The less blood volume or the more time rest means the situation is more dangerous. Because the rule mentions that if the car is killed, our opponent can get all score, and obviously our attack ability will decrease, so when the blood volume approaches zero, the danger degree tends to infinite. concrete assessment strategies are as follows:

### **Game remaining time**
time and blood can be understood as a liner relationship, so the danger degree and time should also be liner relationship

```
Dangerous() ∝ time
```

### **Blood Volume**
When the amount of blood is large, it can be more aggressive. Therefore, the cost of former part of the blood can be regarded linear function. When the blood volume is below a certain limit, it becomes vulnerable to being killed, so it needs to pay more attention to his own safety. The cost of later part of the blood can be regarded as exponential function.

```
if HP >= limit:
    Dangerous() = Constant1 * (2000 - HP)
else:
    Dangerous() = Constant2 ** ((limit - HP) / HP) + Constant1 * (2000 - HP)

(limit = 400, Constant1 = 0.25, Constant2 = 7)
```

### **Optimization of confrontational games**
This game is a confrontational game, according to the game mechanism, car need to make more complex decisions according to the enemy's state, such as through the barrel overheating, do more damages to the enemy. In order to achieve this, we need to combine the enemy's state with ours. Therefore, the evaluation of the danger degree is defined by the difference of the `Dangerous()` between the enemy and ourselves. In addition, SelfProtect is defined as a `selfp` parameter, which can be used to adjust the degree of radical process. The larger the value, the more attention to its own security.

```
ValueDan = -Selfp * Dangerous(self) + (1 - Selfp) * SUM(Dangerous(enemy))

(Selfp = 0.3)
```

## **2. Supply reward**
The evaluation of supply can be divided into two parts: the reward for bullet number and the punishment based on the distance from the supply site when the bullet is lack.

### **Reward of bullet number**
The more bullets, the more times it may hit the enemy, so there will be an incentive score for each bullet, and in the process of supply, more bullets will be obtained due to the incentive mechanism of the number of bullets.

<a href="https://www.codecogs.com/eqnedit.php?latex=BulletReward=Constant3*Bullet" target="_blank"><img src="https://latex.codecogs.com/gif.latex?BulletReward=Constant3*Bullet" title="BulletReward=Constant3*Bullet" /></a>

<a href="https://www.codecogs.com/eqnedit.php?latex=(Constant3=1)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?(Constant3=1)" title="(Constant3=1)" /></a>

### **Punishment mechanism**
When the bullet is lack, it can be regarded as the lack of fighting ability, so we need to make the car as close as possible to the supply site and get the supply. Therefore, we need to set up a punishment mechanism. If the bullet is lack and the car is far from the supply site, we need to deduct a certain score. For the definition of bullet shortage, we can set a constant <a href="https://www.codecogs.com/eqnedit.php?latex=limitBullet" target="_blank"><img src="https://latex.codecogs.com/gif.latex?limitBullet" title="limitBullet" /></a>. Punishment is imposed according to the distance from the supply site. If the number of bullets is greater than this, there is no punishment, and the exponential function <a href="https://www.codecogs.com/eqnedit.php?latex=Constant4^{limitBullet-Bullet}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Constant4^{limitBullet-Bullet}" title="Constant4^{limitBullet-Bullet}" /></a> can satisfy the division of whether the bullet is scarce, so the punish mechanism is defined like follow. 

<a href="https://www.codecogs.com/eqnedit.php?latex=BulletPunish=Constant4^{(limitBullet-Bullet)*SupplyDis*Constant5}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?BulletPunish=Constant4^{(limitBullet-Bullet)*SupplyDis*Constant5}" title="BulletPunish=Constant4^{(limitBullet-Bullet)*SupplyDis*Constant5}" /></a>

<a href="https://www.codecogs.com/eqnedit.php?latex=(Constant4=4,Constant5=1,limitBullet=8)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?(Constant4=4,Constant5=1,limitBullet=8)" title="(Constant4=4,Constant5=1,limitBullet=8)" /></a>

### **Supply reward define**
Two mechanisms mention above reflect the bullet situation together, so

<a href="https://www.codecogs.com/eqnedit.php?latex=ValueBullet=BulletReward-BulletPunish" target="_blank"><img src="https://latex.codecogs.com/gif.latex?ValueBullet=BulletReward-BulletPunish" title="ValueBullet=BulletReward-BulletPunish" /></a>

## **3. Defense bonus reward**
The evaluation of Defense bonus can be divided into two parts: the reward for defensive Buff and reward for defensive Buff duration.

### **Reward for defending Buff**
Having a defensive Buff can reduces the potential damage by half, so reward the defensive Buff status. 

<a href="https://www.codecogs.com/eqnedit.php?latex=DefenseBuffReward=[DefenseTime>0]&space;*&space;Constant6" target="_blank"><img src="https://latex.codecogs.com/gif.latex?DefenseBuffReward=[DefenseTime>0]&space;*&space;Constant6" title="DefenseBuffReward=[DefenseTime>0] * Constant6" /></a>

<a href="https://www.codecogs.com/eqnedit.php?latex=(Constant6=100)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?(Constant6=100)" title="(Constant6=100)" /></a>

### **Reward for defensive Buff duration**
Because the longer the Buff defense lasts, the later it is deferred, the less damage the car will suffer and the better situation will be, the reward mechanism will be set for the Buff's duration to optimize the situation in the future.

<a href="https://www.codecogs.com/eqnedit.php?latex=DefenseTimeReward=&space;DenfenseTime&space;*&space;Constant7" target="_blank"><img src="https://latex.codecogs.com/gif.latex?DefenseTimeReward=&space;DenfenseTime&space;*&space;Constant7" title="DefenseTimeReward= DenfenseTime * Constant7" /></a>

<a href="https://www.codecogs.com/eqnedit.php?latex=(Constant7=5)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?(Constant7=5)" title="(Constant7=5)" /></a>

### **Defense bonus reward define**
Two mechanisms mention above reflect the defensive Buff together, so

<a href="https://www.codecogs.com/eqnedit.php?latex=ValueDefense=DefenseBuffReward&plus;DenfenseTimeReward" target="_blank"><img src="https://latex.codecogs.com/gif.latex?ValueDefense=DefenseBuffReward&plus;DenfenseTimeReward" title="ValueDefense=DefenseBuffReward+DenfenseTimeReward" /></a>

## **4. Team cooperation reward**
The reward function of a combat vehicle can be evaluated from the above three perspectives:

<a href="https://www.codecogs.com/eqnedit.php?latex=Value&space;=&space;ValueDan&space;&plus;&space;ValueBullet&space;&plus;&space;ValueDefense\\" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Value&space;=&space;ValueDan&space;&plus;&space;ValueBullet&space;&plus;&space;ValueDefense\\" title="Value = ValueDan + ValueBullet + ValueDefense\\" /></a>

But there are two cars on the same side of the game, we need to consider their collaborative ability. We not only use Value to define the current situation of a car, but also consider the reward function of the team-mates. In this way, our cars can have overall view and not only consider themselves, and achieve team spirit.

<a href="https://www.codecogs.com/eqnedit.php?latex=TeamworkValue&space;=&space;Constant8&space;*&space;Value(self)&space;&plus;&space;(1-Constant8)&space;*&space;\frac{\sum&space;Value_i}{2}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?TeamworkValue&space;=&space;Constant8&space;*&space;Value(self)&space;&plus;&space;(1-Constant8)&space;*&space;\frac{\sum&space;Value_i}{2}" title="TeamworkValue = Constant8 * Value(self) + (1-Constant8) * \frac{\sum Value_i}{2}" /></a>

<a href="https://www.codecogs.com/eqnedit.php?latex=(Constant8=0.7)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?(Constant8=0.7)" title="(Constant8=0.7)" /></a>
