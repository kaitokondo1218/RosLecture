# RosLecture

## ROS/MoveIt!によるマニピュレータの制御
terminal 1
```
roslaunch sixdofarm sixdofarm.launch
```
terminal 2
```
rviz
```
Fixed Frame を map から base に変更
rvizにAdd → RobotModelを追加  
スライダーを動かすとロボットの関節を自由に動かすことが出来る

```
roslaunch sixdofarm_moveit_config demo.launch
```
ボールを動かすと自由に関節を動かすことが出来る  
Start State を initial_pose, Goal State を standard_pose にして Plan&Execute を押すと指定した位置にリンクが動いてくれる




