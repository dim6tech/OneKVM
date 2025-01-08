### Introduction

The mouse jiggler is a feature to simulate mouse movement. It prevents the system from entering sleep mode, standby mode, or activating the screen protection. This feature is especially useful when there are lengthy processes running on the target host (such as software installation), and the user needs to monitor the process with side-view functionality. It eliminates the need for manually moving the mouse to prevent the screen protection from starting.

### Activation
To enable the mouse jiggler feature, you must update to the latest version and add some configurations in `/etc/kvmd/override.yaml`.

The line `active: true` will allow the mouse jiggler feature to automatically activate and run after a reboot. If you do not want this, you can remove this line.

```yaml
kvmd:
    hid:
        jiggler:
            enabled: true
            active: true
```

After adding the configuration, you need to restart the `kvmd` service for the changes to take effect.

```bash
sudo systemctl restart kvmd
```

![PixPin_2024-06-30_19-39-44](./assets/mouse_jiggler/PixPin_2024-06-30_19-39-44.png)


### Algorithm

When the mouse jiggler feature is enabled, the program counts down the time since the last user input (any keyboard or mouse action). If no input occurs for **60 seconds**, the jiggler will perform a mouse movement, then wait for 60 seconds before repeating the process.

- **Absolute Mode**: The coordinates are converted based on the screen resolution: `(-100, -100), wait, (100, 100), wait...`
- **Relative Mode**: `(-10, -10), wait, (10, 10), wait...`

Even if the web page is closed, the mouse jiggler feature will continue to work in the background.

Of course, this feature will not interfere with the user's normal work. If the user is interacting with the keyboard or mouse, the program will not cause any disturbance until it detects idle time exceeding the **60-second** threshold.