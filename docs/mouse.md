### Introduction


On the One-KVM website, the virtual mouse device has two modes: **Absolute Mode** and **Relative Mode**. 
- In **Absolute Mode**, the input device transmits the exact coordinates of the cursor movement (X, Y), similar to how a touchscreen or graphics tablet works. 
- In **Relative Mode**, only the relative offset from the current position (dX, dY) is transmitted, and the input device itself is unaware of the absolute position, which is similar to how a regular mouse operates.

By default, One-KVM uses Absolute Mode, which is the most convenient for users and software. However, BIOS/UEFI may sometimes not fully support this mode. In such cases, you can switch the mouse mode to Relative Mode in the settings.

In Relative Mode, when you click on the video stream window in One-KVM, the browser will capture your mouse, and will remain captured until you press the **Esc key** to release it.

When using the virtual mouse in Relative Mode, a large number of events are generated, which may result in slow transmission speeds over the network or make BIOS/UEFI drivers perceive the response as slow. To address this issue, the program uses vector optimization for mouse events. To activate these optimizations, you can enable the "Squash mouse moves" mode in the menu under "System" -> "Squash mouse moves". If you encounter issues with mouse acceleration, you can try disabling it. This is currently the compromised solution.

![PixPin_2024-06-30_19-40-12](./assets/mouse/PixPin_2024-06-30_19-40-12.png)

In addition, the VNC service currently does not support the virtual mouse in Relative Mode. This is because the recommended clients do not support the QEMU pointer motion change extension. Additionally, mobile browsers do not support the virtual mouse in Relative Mode.