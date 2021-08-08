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
<br /> 
```
roslaunch sixdofarm_moveit_config demo.launch
```
ボールを動かすと自由に関節を動かすことが出来る  
Start State を initial_pose, Goal State を standard_pose にして Plan&Execute を押すと指定した位置にリンクが動いてくれる
<br /> 
<br /> 
<br /> 
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
<br /> 
<br /> 
<br /> 
```
roslaunch sixdofarm_moveit_config sixdofarm_moveit.launch
```
Gazebo と rviz が同時に立ち上がり, Start State と Goal State を指定して Plan&Execute を押すと Gazebo 上のモデルも同じように動く
<br /> 
<br /> 
<br /> 
## Gazebo 上での移動ロボットモデルの構築
```
roslaunch wheel_robot wheel_robot.launch
```
Gazebo 上に 4 輪モデルが表示される
<br /> 
<br /> 
<br /> 
terminal 1
```
roslaunch wheel_robot wheel_robot_control.launch
```
terminal 2
```
rqt
```
terminal 1 で Gazebo と rviz が起動し，terminal 2 の rqt で 4 輪モデルを動かすことが出来る
<br /> 
<br /> 
<br /> 
## 移動ロボットで地図を作成(slam gmapping)
terminal 1
```
roslaunch wheel_robot wheel_robot.launch
```
terminal 2
```
roslaunch wheel_robot_gmapping wheel_robot_gmapping.launch
```
terminal 3
```
rqt
```
terminal 4
```
rviz
```
terminal 1 で Gazebo が起動する  
地図作成するために Gazebo 上にオブジェクトを配置しておく  
terminal 2 で地図を作製するための launch ファイルが立ち上がる  
rviz に Add → RobotModel，Map を追加し，rqtで動かして出来上がる地図を確認しながら地図を作製していく
<br /> 
<br /> 
<br /> 
```
rosrun map_server map_saver -f test
```
地図を保存したいディレクトリに移動し，実行する  
test は好きなファイル名
<br /> 
<br /> 
<br /> 
## 差動2輪移動ロボットの作り方
```
roslaunch diff_mobile_robot diff_mobile_gazebo.launch
```
部屋の中に置かれた 2 輪モデルが Gazebo 上に表示される
<br /> 
<br /> 
<br /> 
## 差動2輪移動ロボットのナビゲーション
terminal 1
```
roslaunch diff_mobile_robot diff_mobile_gazebo.launch
```
terminal 2
```
roslaunch diff_mobile_robot amcl.launch
```
terminal 3
```
rviz
```
terminal 4
```
rqt
```
terminal 1 で Gazebo が起動する  
terminal 2 でナビゲーション用の launch ファイルが起動する  
terminal 3 で rviz を起動し，Add → RobotModel，Map，PoseArray を追加する  
Map の Topic を/map に，PoseArray の Topic を particlecloud に変更する  
rqt でロボットを動かすとパーティクルの矢印が収束することが分かる
<br /> 
<br /> 
<br /> 
terminal 1
```
roslaunch diff_mobile_robot diff_mobile_gazebo.launch
```
terminal 2
```
roslaunch diff_mobile_robot gmapping.launch
```
terminal 3
```
rviz
```
terminal 4
```
roslaunch diff_mobile_robot diff_mobile_robot_nav.launch
```
terminal 3 で rviz を起動し，Add → RobotModel，Map を追加する  
Map の Topic を/map に変更する  
terminal 4 を実行すると，作成した waypoint に従って 2 輪モデルが動き出す
