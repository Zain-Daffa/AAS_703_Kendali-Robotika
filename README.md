# bt_controller

```text
============================================================
BT_CONTROLLER - ROS 2 Behavior Tree Controller
============================================================

Deskripsi:
-----------
bt_controller adalah paket ROS 2 yang menggunakan BehaviorTree.CPP v3
untuk mengontrol robot (misal di Gazebo atau robot nyata).
Node custom tersedia untuk cek obstacle, gerak maju, putar, dan cek goal.

Struktur paket:
---------------
bt_controller/
├─ src/
│   └─ bt_main.cpp          # Main executable untuk BT
├─ include/
│   └─ bt_controller/
│       └─ IsGoalReached.h  # Node custom contoh
├─ bt_xml/
│   └─ simple_bt.xml        # Contoh Behavior Tree XML
├─ CMakeLists.txt
├─ package.xml
└─ README.md

Dependencies:
-------------
- ROS 2 (Humble, Rolling, Foxy)
- BehaviorTree.CPP v3
- geometry_msgs, sensor_msgs, nav_msgs

============================================================
INSTALASI
============================================================
1. Clone repo ke ROS 2 workspace:

   cd ~/dev_ws/src
   git clone <repo-url> bt_controller

2. Source ROS 2 environment:

   source /opt/ros/<ros2-distro>/setup.bash

3. Build paket:

   cd ~/dev_ws/
   colcon build --packages-select bt_controller
   source install/setup.bash

============================================================
MENJALANKAN BT
============================================================
1. Pastikan robot & sensor aktif

2. Jalankan BT controller:

   ros2 run bt_controller bt_main

============================================================
STRUKTUR NODE BT
============================================================
1. CheckObstacle (ConditionNode)
   - Mengecek jarak depan robot dengan LIDAR
   - RETURN: SUCCESS jika ada obstacle < 0.8 m, FAILURE jika aman

2. MoveForward (SyncActionNode)
   - Menggerakkan robot maju
   - Publikasi: /cmd_vel (linear.x = 0.5)

3. Rotate (SyncActionNode)
   - Memutar robot
   - Publikasi: /cmd_vel (angular.z = 0.8)

4. IsGoalReached (ConditionNode)
   - Mengecek apakah goal tercapai
   - RETURN: SUCCESS jika goal tercapai, FAILURE jika belum
   - TODO: ganti logika sesuai kebutuhan
