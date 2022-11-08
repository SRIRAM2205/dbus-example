# dbus-example
This repo contains information about how to create a method or properties from a dbus interface.

Steps to create new method (or) property:
1. Go to phosphor dbus interfaces->Yaml->Users, and edit the file **manager interface.yaml** 
2. In that add the name of method which is to be created (calculator is the new method in this example).

3. After bitbaking this new virtual functions corresponding to this method will get added to the users.hpp file 
4. You can locate that file in this path->**tmp/work/arm1176jzs-openbmc-linux-gnueabi/phosphor-dbus-interfaces/1.0+git999-r1/image/usr/include/xyz/openbmc_project/User/Manager**
5. Copy that function declaration and add it to the Phosphor-user-manager->user_mgr.hpp.
6. Now define the function in user_mgr.cpp
7. After this bitbake obmc-phosphor-image and check for any errors.
8. After succesful build open qemu and give the following commands,
        busctl introspect xyz.openbmc_project.User.Manager /xyz/openbmc_project/user
        you can see our method added into that respective bus service
        **Calculator                            method    uuu        u   ** 
9. Now you can call our method using following command **busctl call xyz.openbmc_project.User.Manager /xyz/openbmc_project/user xyz.openbmc_project.User.Manager Calculator uuu 10 20 1** Here the flag (uuu) denotes three integer and (10 20) are values passed as arguments (1) denotes addition as we defined the user_mgr.cpp.
10. We can see following output in the screen **u 30** 
