# Yocto Project Implementation Guide

This guide outlines the steps taken to achieve various tasks using the Yocto Project.

## 1. Create Your Own Layer

To create your own layer, follow these steps:

- Navigate to your Yocto build directory.
- Run the command `yocto-layer create <layer-name>` to create a new layer.
- Customize your layer by adding recipes, configuration files, etc.
- Add your layer to the `bblayers.conf` file located in `conf` directory of your Yocto build.

## 2. Create Image

To create a custom image, follow these steps:

- Define your custom image recipe by creating a `.bb` file in your layer's `recipes-core/images/` directory.
- Specify the packages you want to include in your image.
Example:
![image bb](https://github.com/mgtera200/Embedded-Linux-NTI/assets/127119775/07128953-cd10-4b61-9cd4-fd00389851e0)


## 3. Write Hello World Recipe with C

To create a Hello World recipe using C and compile it within a meta-layer, follow these steps:

- Create a new recipe file with a `.bb` extension in your custom layer's `recipes-example` directory.
- Write a simple C program, e.g., `hello.c`, and place it in your recipe's source directory.
- Write the recipe to compile and install the C program into the working directory of bitbake during the build process.

Example for simple hello world:


![main c](https://github.com/mgtera200/Embedded-Linux-NTI/assets/127119775/87f8859f-725d-473e-9f71-64f61770cefb)



Example for the recipe:


![edit](https://github.com/mgtera200/YOCTO/assets/127119775/e8f941d2-8d5f-4f6b-976f-695ec48e84ab)



## 4. Add C Package to Image

To add the compiled C Hello World application to your custom image, follow these steps:

- Modify your custom image recipe to include the compiled C Hello World application as a package to be installed into the image.
- Ensure that the recipe for the Hello World application is included in the `IMAGE_INSTALL` variable in your custom image recipe.


## 5. Change Hostname of Image

To change the hostname of your custom image using a `.bbappend` file in a custom recipe, follow these steps:

- Create a `base-files_%.bbappend` file for the `base-files` recipe located in your custom layer's `recipes-core/base-files` directory.
- Add the necessary modifications to change the hostname in the `.bbappend` file.

Example:


![bbappend](https://github.com/mgtera200/Embedded-Linux-NTI/assets/127119775/b9b7088b-cc5b-4eea-be08-d2fe3859f89b)

## 6. Change Download and Sstate to Shared Folder

To change the download and sstate cache directories to a shared folder, follow these steps:

- Modify the `conf/local.conf` file in your Yocto build directory.
- Set the `DL_DIR` and `SSTATE_DIR` variables to point to the shared folder you want.

## 7. Create Distro

To create a custom distribution, follow these steps:

- Define your custom distribution configuration by creating a `.conf` file in your custom layer's `conf/distro` directory.
- Customize your distribution settings such as package selection, distro features and init process.
- Include your custom distribution in the `local.conf` file of your Yocto build.

Example for systemd distro:


![systemd](https://github.com/mgtera200/Embedded-Linux-NTI/assets/127119775/42a5002e-83b6-4d24-934e-74e1105c837a)

## 8. Build Your Customized Image for qemux86_64 Machine

To build your customized image for the qemux86_64 machine, follow these steps:

- Set the machine variable in your local configuration to `qemux86_64`.
- Run the bitbake command `bitbake tera-minimal -k` to build your customized image for the specified machine.

## 9. Test Your Image Using runqemu

To test your customized image using runqemu, follow these steps:

- Launch the runqemu tool with the appropriate parameters `runqemu nographic qemux86-64`
- Verify that the image boots successfully and is functional within the QEMU emulator environment.

My result:


![result](https://github.com/mgtera200/Embedded-Linux-NTI/assets/127119775/2bc248d4-37de-4ef3-a668-a1cb4b0df80c)

## 10. Download the meta-raspberrypi Layer and Edit local.conf

Before proceeding with building for Raspberry Pi 4 (rpi4-64), download the meta-raspberrypi layer and make the necessary edits to the local.conf file:

- Add the meta-raspberrypi layer to your Yocto project's `conf/bblayers.conf` file.
- Edit the `local.conf` file to set the machine to `raspberrypi4-64` and include the desired image types.

```bash
MACHINE ??= "raspberrypi4-64"
IMAGE_FSTYPES = "tar.xz ext3 rpi-sdimg"
```

## 11. Build Your Customized Image for Raspberry Pi 4 (rpi4-64)
To build your customized image for the Raspberry Pi 4 (rpi4-64), follow these steps:

- Run the bitbake command to build your customized image for the specified machine `bitbake tera-minimal -k`.

## 11. Test Your Image on Hardware Using SSH
To test your customized image on your Raspberry Pi 4 hardware using SSH, follow these steps:

 - Flash the SD card with the built image for Raspberry Pi 4.
 - Boot the Raspberry Pi 4 with the flashed SD card.
 - Once the Raspberry Pi 4 is booted, SSH into the device using its IP address and login credentials.
 - Verify that the customized image is functional and all desired features are working as expected.

My final result:


![rpi4](https://github.com/mgtera200/Embedded-Linux-NTI/assets/127119775/6a5b2f99-af14-491b-b4c6-8aafb09b15e5)

