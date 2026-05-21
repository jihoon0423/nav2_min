# nav2_min

Nav2에서 **필요한 노드만 경량화**한 ROS2 패키지. 
전체 Nav2 스택 대신 `map_server`, `amcl`, `planner_server`, `lifecycle_manager` 4개 노드만 실행.

---

## 패키지 구조

```
nav2_min/
├── src/
│   └── nav2_global_costmap_only/
│       ├── launch/
│       │   └── global_costmap_only_4nodes.launch.py   # 경량화 launch 파일
│       ├── CMakeLists.txt
│       └── package.xml
├── nav2_params.yaml   # Nav2 파라미터 설정 파일
└── README.md
```

---

## 실행 노드 구성

| 노드 | 역할 |
|------|------|
| `map_server` | 저장된 맵 로드 |
| `amcl` | 파티클 필터 기반 위치 추정 |
| `planner_server` | 전역 경로 계획 (NavFn) | 안켜도 되긴하는 노드 같긴함
| `lifecycle_manager` | 위 3개 노드 lifecycle 자동 관리 |

---

## 의존성 설치

```bash
sudo apt update
sudo apt install ros-humble-navigation2 ros-humble-nav2-bringup
```

```bash
source /opt/ros/humble/setup.bash
```

---

## 빌드

```bash
cd ~/your_ws
colcon build --packages-select nav2_global_costmap_only
source install/setup.bash
```

---

## 실행 방법

### 방법 1 — 경량화 launch 파일 (이 패키지)

```bash
ros2 launch nav2_global_costmap_only global_costmap_only_4nodes.launch.py \
  map:=/파일주소/my_slam_map.yaml \
  use_sim_time:=false \
  params_file:=/파일주소/nav2_params.yaml
```

### 방법 2 — nav2_bringup 전체 localization launch

```bash
ros2 launch nav2_bringup localization_launch.py \
  map:=/파일주소/my_slam_map.yaml \
  use_sim_time:=false \
  params_file:=/파일주소/nav2_params.yaml
```
---

## RViz2 실행

```bash
rviz2
```

확인할 토픽: `/map`, `/amcl_pose`

---
