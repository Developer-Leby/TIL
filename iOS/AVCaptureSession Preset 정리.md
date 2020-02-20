# AVCaptureSession Preset 정리

```objective-c
+-----------------------+--------------+---------------------------------+---------------+
|        Device         |    Camera    |     AVCaptureSessionPreset      |  Resolution   |
+-----------------------+--------------+---------------------------------+---------------+
| iPhone 4S             | FRONT        |                                 |               |
|                       |              | AVCaptureSessionPresetPhoto     | 640x480       |
|                       |              | AVCaptureSessionPresetHigh      | 640x480       |
|                       |              | AVCaptureSessionPresetMedium    | 480x360       |
|                       |              | AVCaptureSessionPresetLow       | 192x144       |
|                       |              | AVCaptureSessionPreset640x480   | 640x480       |
|                       |              | AVCaptureSessionPreset1280x720  | not supported |
|                       |              | AVCaptureSessionPreset1920x1080 | not supported |
|                       | BACK         |                                 |               |
|                       |              | AVCaptureSessionPresetPhoto     | 3264x2448     |
|                       |              | AVCaptureSessionPresetHigh      | 1920x1080     |
|                       |              | AVCaptureSessionPresetMedium    | 480x360       |
|                       |              | AVCaptureSessionPresetLow       | 192x144       |
|                       |              | AVCaptureSessionPreset640x480   | 640x480       |
|                       |              | AVCaptureSessionPreset1280x720  | 1280x720      |
|                       |              | AVCaptureSessionPreset1920x1080 | 1920x1080     |
+-----------------------+--------------+---------------------------------+---------------+
| iPhone 5/5C/5S/6/6+   |              |                                 |               |
|                       | FRONT        |                                 |               |
|                       |              | AVCaptureSessionPresetPhoto     | 1280x960      |
|                       |              | AVCaptureSessionPresetHigh      | 1280x720      |
|                       |              | AVCaptureSessionPresetMedium    | 480x360       |
|                       |              | AVCaptureSessionPresetLow       | 192x144       |
|                       |              | AVCaptureSessionPreset640x480   | 640x480       |
|                       |              | AVCaptureSessionPreset1280x720  | 1280x720      |
|                       |              | AVCaptureSessionPreset1920x1080 | not supported |
|                       | BACK         |                                 |               |
|                       |              | AVCaptureSessionPresetPhoto     | 3264x2448     |
|                       |              | AVCaptureSessionPresetHigh      | 1920x1080     |
|                       |              | AVCaptureSessionPresetMedium    | 480x360       |
|                       |              | AVCaptureSessionPresetLow       | 192x144       |
|                       |              | AVCaptureSessionPreset640x480   | 640x480       |
|                       |              | AVCaptureSessionPreset1280x720  | 1280x720      |
|                       |              | AVCaptureSessionPreset1920x1080 | 1920x1080     |
+-----------------------+--------------+---------------------------------+---------------+
| iPhone 6S/6S          |              |                                 |               |
|                       | FRONT camera |                                 |               |
|                       |              | AVCaptureSessionPresetPhoto     | 1280x960      |
|                       |              | AVCaptureSessionPresetHigh      | 1280x720      |
|                       |              | AVCaptureSessionPresetMedium    | 480x360       |
|                       |              | AVCaptureSessionPresetLow       | 192x144       |
|                       |              | AVCaptureSessionPreset640x480   | 640x480       |
|                       |              | AVCaptureSessionPreset1280x720  | 1280x720      |
|                       |              | AVCaptureSessionPreset1920x1080 | not supported |
|                       | BACK camera  |                                 |               |
|                       |              | AVCaptureSessionPresetPhoto     | 4032x3024     |
|                       |              | AVCaptureSessionPresetHigh      | 1920x1080     |
|                       |              | AVCaptureSessionPresetMedium    | 480x360       |
|                       |              | AVCaptureSessionPresetLow       | 192x144       |
|                       |              | AVCaptureSessionPreset640x480   | 640x480       |
|                       |              | AVCaptureSessionPreset1280x720  | 1280x720      |
|                       |              | AVCaptureSessionPreset1920x1080 | 1920x1080     |
+-----------------------+--------------+---------------------------------+---------------+
| iPad 2                |              |                                 |               |
|                       | FRONT        |                                 |               |
|                       |              | AVCaptureSessionPresetPhoto     | 640x480       |
|                       |              | AVCaptureSessionPresetHigh      | 640x480       |
|                       |              | AVCaptureSessionPresetMedium    | 480x360       |
|                       |              | AVCaptureSessionPresetLow       | 192x144       |
|                       |              | AVCaptureSessionPreset640x480   | 640x480       |
|                       |              | AVCaptureSessionPreset1280x720  | not supported |
|                       |              | AVCaptureSessionPreset1920x1080 | not supported |
|                       | BACK         |                                 |               |
|                       |              | AVCaptureSessionPresetPhoto     | 960x720       |
|                       |              | AVCaptureSessionPresetHigh      | 1280x720      |
|                       |              | AVCaptureSessionPresetMedium    | 480x360       |
|                       |              | AVCaptureSessionPresetLow       | 192x144       |
|                       |              | AVCaptureSessionPreset640x480   | 640x480       |
|                       |              | AVCaptureSessionPreset1280x720  | 1280x720      |
|                       |              | AVCaptureSessionPreset1920x1080 | not supported |
+-----------------------+--------------+---------------------------------+---------------+
| iPad 3                |              |                                 |               |
|                       | FRONT        |                                 |               |
|                       |              | AVCaptureSessionPresetPhoto     | 640x480       |
|                       |              | AVCaptureSessionPresetHigh      | 640x480       |
|                       |              | AVCaptureSessionPresetMedium    | 480x360       |
|                       |              | AVCaptureSessionPresetLow       | 192x144       |
|                       |              | AVCaptureSessionPreset640x480   | 640x480       |
|                       |              | AVCaptureSessionPreset1280x720  | not supported |
|                       |              | AVCaptureSessionPreset1920x1080 | not supported |
|                       | BACK         |                                 |               |
|                       |              | AVCaptureSessionPresetPhoto     | 2592x1936     |
|                       |              | AVCaptureSessionPresetHigh      | 1920x1080     |
|                       |              | AVCaptureSessionPresetMedium    | 480x360       |
|                       |              | AVCaptureSessionPresetLow       | 192x144       |
|                       |              | AVCaptureSessionPreset640x480   | 640x480       |
|                       |              | AVCaptureSessionPreset1280x720  | 1280x720      |
|                       |              | AVCaptureSessionPreset1920x1080 | 1920x1080     |
+-----------------------+--------------+---------------------------------+---------------+
| iPad 4/Air            |              |                                 |               |
| iPad Mini 1/2/3       |              |                                 |               |
| iPod 5G               |              |                                 |               |
|                       | FRONT        |                                 |               |
|                       |              | AVCaptureSessionPresetPhoto     | 1280x960      |
|                       |              | AVCaptureSessionPresetHigh      | 1280x720      |
|                       |              | AVCaptureSessionPresetMedium    | 480x360       |
|                       |              | AVCaptureSessionPresetLow       | 192x144       |
|                       |              | AVCaptureSessionPreset640x480   | 640x480       |
|                       |              | AVCaptureSessionPreset1280x720  | 1280x720      |
|                       |              | AVCaptureSessionPreset1920x1080 | not supported |
|                       | BACK         |                                 |               |
|                       |              | AVCaptureSessionPresetPhoto     | 2592x1936     |
|                       |              | AVCaptureSessionPresetHigh      | 1920x1080     |
|                       |              | AVCaptureSessionPresetMedium    | 480x360       |
|                       |              | AVCaptureSessionPresetLow       | 192x144       |
|                       |              | AVCaptureSessionPreset640x480   | 640x480       |
|                       |              | AVCaptureSessionPreset1280x720  | 1280x720      |
|                       |              | AVCaptureSessionPreset1920x1080 | 1920x1080     |
+-----------------------+--------------+---------------------------------+---------------+
| iPad Air 2            |              |                                 |               |
| iPad Mini 4           |              |                                 |               |
| iPad Pro              |              |                                 |               |
|                       | FRONT        |                                 |               |
|                       |              | AVCaptureSessionPresetPhoto     | 1280x960      |
|                       |              | AVCaptureSessionPresetHigh      | 1280x720      |
|                       |              | AVCaptureSessionPresetMedium    | 480x360       |
|                       |              | AVCaptureSessionPresetLow       | 192x144       |
|                       |              | AVCaptureSessionPreset640x480   | 640x480       |
|                       |              | AVCaptureSessionPreset1280x720  | 1280x720      |
|                       |              | AVCaptureSessionPreset1920x1080 | not supported |
|                       | BACK         |                                 |               |
|                       |              | AVCaptureSessionPresetPhoto     | 3264x2448     |
|                       |              | AVCaptureSessionPresetHigh      | 1920x1080     |
|                       |              | AVCaptureSessionPresetMedium    | 480x360       |
|                       |              | AVCaptureSessionPresetLow       | 192x144       |
|                       |              | AVCaptureSessionPreset640x480   | 640x480       |
|                       |              | AVCaptureSessionPreset1280x720  | 1280x720      |
|                       |              | AVCaptureSessionPreset1920x1080 | 1920x1080     |
+-----------------------+--------------+---------------------------------+---------------+
| iPod Touch 5          |              |                                 |               |
|                       | FRONT        |                                 |               |
|                       |              | AVCaptureSessionPresetPhoto     | 1280x960      |
|                       |              | AVCaptureSessionPresetHigh      | 1280x720      |
|                       |              | AVCaptureSessionPresetMedium    | 480x360       |
|                       |              | AVCaptureSessionPresetLow       | 192x144       |
|                       |              | AVCaptureSessionPreset640x480   | 640x480       |
|                       |              | AVCaptureSessionPreset1280x720  | 1280x720      |
|                       |              | AVCaptureSessionPreset1920x1080 | not supported |
|                       | BACK         |                                 |               |
|                       |              | AVCaptureSessionPresetPhoto     | 2592x1936     |
|                       |              | AVCaptureSessionPresetHigh      | 1920x1080     |
|                       |              | AVCaptureSessionPresetMedium    | 480x360       |
|                       |              | AVCaptureSessionPresetLow       | 192x144       |
|                       |              | AVCaptureSessionPreset640x480   | 640x480       |
|                       |              | AVCaptureSessionPreset1280x720  | 1280x720      |
|                       |              | AVCaptureSessionPreset1920x1080 | 1920x1080     |
+-----------------------+--------------+---------------------------------+---------------+
| iPod Touch 6          |              |                                 |               |
|                       | FRONT        |                                 |               |
|                       |              | AVCaptureSessionPresetPhoto     | 1280x960      |
|                       |              | AVCaptureSessionPresetHigh      | 1280x720      |
|                       |              | AVCaptureSessionPresetMedium    | 480x360       |
|                       |              | AVCaptureSessionPresetLow       | 192x144       |
|                       |              | AVCaptureSessionPreset640x480   | 640x480       |
|                       |              | AVCaptureSessionPreset1280x720  | 1280x720      |
|                       |              | AVCaptureSessionPreset1920x1080 | not supported |
|                       | BACK         |                                 |               |
|                       |              | AVCaptureSessionPresetPhoto     | 3264x2448     |
|                       |              | AVCaptureSessionPresetHigh      | 1920x1080     |
|                       |              | AVCaptureSessionPresetMedium    | 480x360       |
|                       |              | AVCaptureSessionPresetLow       | 192x144       |
|                       |              | AVCaptureSessionPreset640x480   | 640x480       |
|                       |              | AVCaptureSessionPreset1280x720  | 1280x720      |
|                       |              | AVCaptureSessionPreset1920x1080 | 1920x1080     |
+-----------------------+--------------+---------------------------------+---------------+
```

 