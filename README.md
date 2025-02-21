# Виконала самостійно Слобожан Софія РПЗ-23А
Work-case 2
### Installation of Hypervisor

1. **Choosing a Hypervisor**: I chose **QEMU(It was aimed at updating "Virtual Box" drivers)** due to its flexibility and support for various architectures.

### Basic Actions in QEMU

#### 1. Creating a New Virtual Machine
- **Install QEMU**: If you haven't installed QEMU yet, you can do so using your package manager. For example, on Ubuntu, you can run:
  ```bash
  sudo apt update
  sudo apt install qemu qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils
  ```
- **Create a Disk Image**: Use the following command to create a new disk image for your virtual machine:
  ```bash
  qemu-img create -f qcow2 my_vm_image.qcow2 20G
  ```
- **Launch the Virtual Machine**: Use the following command to start the virtual machine with an ISO image:
  ```bash
  qemu-system-x86_64 -hda my_vm_image.qcow2 -boot d -cdrom path_to_your_iso.iso -m 2048
  ```
  Replace `path_to_your_iso.iso` with the path to your desired operating system ISO.

#### 2. Selecting/Adding Available Hardware for the Virtual Machine
- **Configure CPU and RAM**: You can specify the number of CPU cores and RAM when launching the VM. For example:
  ```bash
  qemu-system-x86_64 -hda my_vm_image.qcow2 -m 2048 -smp 2
  ```
- **Add Network Interface**: To add a network interface, you can use the `-netdev` and `-device` options. For example, to use a user-mode network stack:
  ```bash
  -netdev user,id=mynet0 -device e1000,netdev=mynet0
  ```

#### 3. Configuring Network and Connecting to Wi-Fi
- **Bridged Networking**: If you want to connect to a Wi-Fi network, you can set up a bridged network. This requires additional configuration on your host system. You can use the following command to specify a bridge:
  ```bash
  -netdev tap,ifname=tap0,script=no,downscript=no,id=mynet0 -device e1000,netdev=mynet0
  ```
  Make sure to create the tap interface and configure it properly.

#### 4. Working with External Storage Devices (Flash Drives)
- **Access USB Devices**: To pass a USB device to the virtual machine, you can use the `-usb` and `-device` options. For example:
  ```bash
  -usb -device usb-host,hostbus=1,hostaddr=2
  ```
  Replace `hostbus` and `hostaddr` with the appropriate values for your USB device, which you can find using the `lsusb` command.

### Installing a GNU/Linux Operating System

1. **Installing a GNU/Linux Distribution**:
   - Start the virtual machine using the command provided above with the ISO image.
   - Follow the installation instructions to complete the process.

### Creating a Second Virtual Machine

1. **Installing a Minimal Configuration of GNU/Linux**:
   - Create a new disk image for the second virtual machine:
     ```bash
     qemu-img create -f qcow2 my_vm_image_minimal.qcow2 20G
     ```
   - Launch the virtual machine with a minimal ISO (e.g., Ubuntu Server):
     ```bash
     qemu-system-x86_64 -hda my_vm_image_minimal.qcow2 -boot d -cdrom path_to_minimal_iso.iso -m 2048
     ```
   - Install the system without a graphical interface by following the installation instructions.

2. **Installing the GNOME Desktop Environment**:
   - Open a terminal in the installed system.
   - Execute the command:
     ```bash
     sudo apt update
     sudo apt install ubuntu-desktop
     ```
   - After the installation is complete, reboot the system.

3. **Installing a Second Desktop Environment**:
   - For example, to install the XFCE desktop environment, execute the command:
     ```bash
     sudo apt install xubuntu-desktop
     ```
   - After the installation is complete, reboot the system.

### Comparing GNOME and XFCE

#### GNOME
- **Interface**: Modern, with a focus on simplicity and ease of use.
- **Customization**: Offers various extensions and themes, but can be more complex to customize.
- **Performance**: Generally heavier on system resources compared to XFCE.

#### XFCE
- **Interface**: Lightweight and straightforward, designed for speed and efficiency.
- **Customization**: Highly customizable with a variety of plugins and themes, easier to modify.
- **Performance**: Uses fewer system resources, making it suitable for older hardware or systems with limited resources.

### Conclusion
Both GNOME and XFCE have their strengths and weaknesses. GNOME provides a modern and polished experience, while XFCE is lightweight and highly customizable, making it a great choice for users who prioritize performance and simplicity.
### screenshots of works:
![IMG_5666](https://github.com/user-attachments/assets/171278de-5b0a-4d80-b6ad-ca6c26d8200d)
![IMG_5664](https://github.com/user-attachments/assets/6b5e8bd6-bc15-40b3-8ce3-cdda08d03c3d)
![IMG_5667](https://github.com/user-attachments/assets/b9f0f979-71af-4017-8b47-24d061351ef6)
### Conclusion
Overall, this exercise provided a comprehensive understanding of virtualization, operating system installation, and desktop environment management. It equipped us with the knowledge and skills necessary to effectively utilize QEMU and GNU/Linux systems, paving the way for further exploration and experimentation in the field of virtualization and system administration.

