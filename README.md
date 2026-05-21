# nav2_min

nav2에서 필요한 노드만 경량화.

---

## 패키지 설치


**Humble (Ubuntu 22.04)**
```bash
sudo apt update
sudo apt install ros-humble-navigation2 ros-humble-nav2-bringup
```

설치 후 환경 설정:
```bash
source /opt/ros/humble/setup.bash
```

---

## Localization 실행 방법

### Step 1 — Localization Launch

```bash
ros2 launch nav2_bringup localization_launch.py \
  map:=/파일주소/my_slam_map.yaml \
  use_sim_time:=false \
  params_file:=/파일주소/nav2_params.yaml
```

### Step 2 — RViz2 실행

```bash
rviz2
```
