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
<br /> 
<br /> 
a
```
roslaunch sixdofarm_moveit_config demo.launch
```
ボールを動かすと自由に関節を動かすことが出来る  
Start State を initial_pose, Goal State を standard_pose にして Plan&Execute を押すと指定した位置にリンクが動いてくれる



## Gazebo によるマニピュレータのシミュレーション
terminal 1
```
roslaunch sixdofarm_gazebo sixdofarm.launch
```
terminal 2
```
roslaunch sixdofarm_control sixdofarm_control.launch
```
terminal 3
```
rostopic pub -1 /sixdofarm/joint2_position_controller/command std_msgs/Float64 "data: 1.5"
```
terminal 1 を起動するとGazebo が立ち上がり，色付けされ地面に固定されたリンクが表示される  
terminal 3 を実行すると指定された通りにリンクが動く  
terminal 3 を rqt に変えると PID ゲインの調整等が出来る




