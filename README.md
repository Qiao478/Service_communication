# Service_communication
如果出现了某个包无法运行的情况
1.刷新环境变量重新运行
2.检查功能包有没有存在：ros2 pkg prefix 包名
例：ros2 pkg prefix cpp02_service
3.检查功能包下有没有可执行文件：ls -l ~功能包路径
例：ls -l ~/ros2_workspace/ws01_plumbing/install/cpp02_service/lib/cpp02_service/
一、定义服务接口消息
1.创建并编辑.srv文件：在本案例中，.srv文件包含请求数据（两个整型字段）和响应数据（一个整型字段）
在base_interfaces_demo文件下新建srv文件夹，srv文件夹下新建Addints.srv文件
2.编辑配置文件
(1)package.xml
如果base_interfaces_demo文件下没有添加过任何接口，则配置步骤同话题通信(各种依赖）
如果base_interfaces_demo文件下已经添加过其他接口，则不用进行任何修改
(2)CMakeList.txt文件
若干base_interfaces_demo文件下没有配置过任何接口，则配置步骤同话题通信（即需要配置相应代码将.srv文件转换成对应的C++和Python文件）
如果base_interfaces_demo文件下已经添加过其他接口，则只需要添加映射，添加内容为"srv/Addints.srv"，添加后的文件内容如下：
rosidl_generate_interfaces(${PROJECT_NAME}
  "msg/Student.msg"
  "srv/Addints.srv"

)


3.编译
4.调试
. install/setup.bash
ros2 interfaces show base_interfaces_demo/srv/Addints
若编写成功则终端输出的内容与srv文件内容一致

二、实现
C++
1.服务端通信
在功能包cpp02_service的src目录下新建C++文件的名——service.cpp
2.编辑配置文件
在CMakeList.txt文件中添加dem02_client的配置文件
add_executable(dem02_client src/dem02_client.cpp)
target_compile_features(dem01_server PUBLIC c_std_99 cxx_std_17)  # Require C99 and C++17
ament_target_dependencies(
  dem02_client
  "rclcpp"
  "base_interfaces_demo"
)

