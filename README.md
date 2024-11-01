# ESPOffice LVGL Screensaver

LVGL screensaver for ESPHome inspired by the famous DVD logo bouncing around on the screen. Everytime the ESP logo hits the wall it will change direction and color. It started out with the default color, so that color is used initially. After that it uses an red, green or blue logo randomly. Hopefully, over a period of time, all pixels have been hit with every color and therefor the change is smaller for a burn-in. It's just a fun project.

Due to my screen being square, I could not do 1px speed horizontally and vertically because then it would bounce around on the same lines all the time. Therefor every bounce a random number of pixels will be calculated as new speed. This will also change the angle in which the logo moves.

[![ESPOffice](https://img.youtube.com/vi/6b0i3Eq9Wrc/0.jpg)](https://www.youtube.com/watch?v=6b0i3Eq9Wrc)

## Installation

Just copy the `globals`, `image`, `number`, `lvgl` -> `on_idle` + `top_layer` and `script` components into your yaml. Copy the `images` folder to next your yaml. Review the `resume_lvgl` script and the `on_idle` items. Alter `screenWidth`, `screenHeight`, `imgWidth` and `imgHeight` if needed, make sure the image sizes are equal to all the sizes of logos under `image`.

Add the `screensaver_script` to all the components that will wake up the screen
```yaml
    on_value:
      then:
        - script.execute:
            id: screensaver_script
```

## Notes

The screen needs to be redrawn, to realise that screensaver script will resume the screen, and after drawing the screen will be put to pause again. Due to this, the global variable `lvgl_is_paused` is introduced. Use that variable to determine if your device is paused. I even doubt if `lvgl.pause` is still desirable.

Because my math doesn't math, I have used logic. I think it can be more efficient with some better code, PR if your math maths.
