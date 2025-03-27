# noetic_ws

Ubuntu22.04源码编译ros noetic。（理论上20.04也是可以这么编译装ros noetic）

注意：如果系统存在多个ros环境，则source ros环境的setup.bash不能放在~/.bashrc，需要每次在终端手动source指定ros版本。


## 1.安装依赖
```
sudo apt install python3-rosdep python3-rosinstall-generator python3-vcstools python3-vcstool build-essential

sudo apt install libqt5widgets5  qtcreator qtbase5-dev qt5-qmake cmake

sudo apt install sip-dev python3-sip-dev python3-pyqt5.sip
sudo apt install python3-pyqt5.sip python3-pyqt5 pyqt5-dev 

sudo apt install libopencv-dev
sudo apt install libassimp-dev python3-pyassimp

```

## 2.更换rosdep源
```
# 手动模拟 rosdep init
sudo mkdir -p /etc/ros/rosdep/sources.list.d/
sudo curl -o /etc/ros/rosdep/sources.list.d/20-default.list https://mirrors.tuna.tsinghua.edu.cn/github-raw/ros/rosdistro/master/rosdep/sources.list.d/20-default.list
# 为 rosdep update 换源
export ROSDISTRO_INDEX_URL=https://mirrors.tuna.tsinghua.edu.cn/rosdistro/index-v4.yaml
rosdep update

# 每次 rosdep update 之前，均需要增加该环境变量# 为了持久化该设定，可以将其写入 .bashrc 中，例如
echo 'export ROSDISTRO_INDEX_URL=https://mirrors.tuna.tsinghua.edu.cn/rosdistro/index-v4.yaml' >> ~/.bashrc
```

## 3.设置rosdep
```
sudo rosdep init
rosdep update
```

## 4. 下载noetic源码
```
git clone https://github.com/hyxhope/noetic_ws.git
```

## 5. 编译安装
```
cd noetic_ws
rosdep install -r --from-paths src --ignore-src --rosdistro noetic -y
./src/catkin/bin/catkin_make_isolated --install -DCMAKE_BUILD_TYPE=Release
```

## 6. 测试
```
source noetic_ws/install_isolated/setup.bash
roscore
```

## 7. change_cpp.py的功能
Check目录下所有的CMakeList.txt文件，将c++版本改为c++17
