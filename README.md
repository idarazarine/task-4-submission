## README for Task 4
# Creation of URDF for Kuka-iiwa-14 arm using meshes

The meshes provided in the repository for task 4 were cloned into a workspace
To view the meshes, I installed MeshLab using:

```bash
sudo apt install meshlab
```

To view a mesh of a link, I ran:

```bash
meshlab link_0.dae
``` 
I also used VSCode to view the .dae files of the meshes, in addition to MeshLab. I created a workspace and a ROS 2 package.
I added the meshes to my description package and created a folder called URDF in the folder
I added a file named kuka-iiwa-14.urdf to my URDF folder and started writing.
This is the format I used for my link and joint definitions:

```bash
<link name = "base_link">
        <visual>
            <origin rpy="0.0 0.0 0.0" xyz="0.0 0.0 0.0"/>
            <geometry>
                <mesh filename = "package://kuka-iiwa-14_description/meshes/link_0.dae" scale = "1.0 1.0 1.0"/>
            </geometry>
        </visual>
    </link>

    <joint name="base_to_link1" type="revolute">
        <origin xyz="0.0 0.0 0.0"  rpy="0.0 0.0 0.0"/>
        <parent link="base_link"/>
        <child link="link_1"/>
        <axis xyz="0.0 0.0 1.0"/>
        <limit lower="-2.967" upper="2.967" effort="10.0" velocity="1.0"/>
    </joint>
```
I did this for all 7 links and 6 joints. I checked the URDF before launching using:

```bash
check_urdf kuka-iiwa-14_description
```

This was the result:
<img width="972" height="339" alt="image" src="https://github.com/user-attachments/assets/13ef5718-2208-4fe5-992c-045587a57422" />

I also checked the URDF using the URDF preview on VS Code

Whilst writing and running the URDF, I ran into some challenges, such as:
1. Figuring out the axes and origins of the joints
2. What values to use for the effort and velocity in the limit tag
3. The robot arm jerks or moves on its own when launched in RViz

After checking, I launched the URDF using:
```bash
colcon build
source opt/ros/humble/setup.bash
source install/setup.bash
ros2 launch urdf_tutorial display.launch.py model:=$PWD/kuka-iiwa-14_description/urdf/kuka-iiwa-14.urdf
```

This was the result:
<img width="963" height="446" alt="image" src="https://github.com/user-attachments/assets/32383bd8-335f-40d5-8dab-57ca50ae1e72" />
<img width="320" height="444" alt="Screenshot 2025-10-31 205648" src="https://github.com/user-attachments/assets/4ea539c4-2c85-4329-8ba8-4f7df19f4e1c" />





