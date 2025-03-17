<p align="center">
    <a href="./pages.html">
        <img src="../assets/darin_x20.png" alt="Darin Sprite" width="120" height="128">
    </a>
</p>

# Tour

Welcome to the Parin game engine tour.
This page will go over each feature of the engine and provide examples of how to use them.
If you notice anything missing or would like to contribute, feel free to create an [issue](https://github.com/Kapendev/parin/issues)!

## 1. Getting Started

This guide shows how to install Parin and its dependencies using [DUB](https://dub.pm/).
To begin, make a new folder and run inside the following commands to create a new project:

```cmd
dub init -n
dub run parin:setup
```

If everything is set up correctly,
there should be some new files inside the folder.
Three of them are particularly important:

* source: Contains the source code of the game.
* assets: Contains the assets of the game.
* web: Used for exporting the game to the web.

Additionally, an app.d file is inside the source folder that looks like this:

```d
import parin;

void ready() {
    lockResolution(320, 180);
}

bool update(float dt) {
    drawDebugText("Hello world!", Vec2(8));
    return false;
}

void finish() { }

mixin runGame!(ready, update, finish);
```

This code will create a window that displays the message "Hello world!".
Here is a breakdown of how it works:

1. The Ready Function

    ```d
    void ready() {
        lockResolution(320, 180);
    }
    ```

    This function is the starting point of the game.
    It is called once when the game starts and, in this example, locks the game resolution to 320x180.

2. The Update Function

    ```d
    bool update(float dt) {
        drawDebugText("Hello world!", Vec2(8));
        return false;
    }
    ```

    This function is the main loop of the game.
    It is called every frame while the game is running and, in this example, draws the message "Hello world!" at position (8, 8).
    The `return false` statement at the end indicates that the game should continue running.
    If `true` were returned, then the game would stop running.

3. The Finish Function

    ```d
    void finish() { }
    ```

    This function is the ending point of the game.
    It is called once when the game ends and, in this example, does nothing.

4. The Mixin

    ```d
    mixin runGame!(ready, update, finish);
    ```

    This mixin sets up a main function that opens a window and calls the ready, update and finish functions.
    By default, the window has a size of 960x540.

In essence, a Parin game typically relies on three functions:

* A ready function.
* An update function.
* A finish function.

To run the game, use the following command:

```cmd
dub run
```

And that's it for the basics.
As a fun exercise, try changing the message to "DVD" and make it bounce inside the window.

**Tip:** The font used here has characters that have a size of 6x12.

## 2. Modules

Parin consists of the following modules:

* parin.engine: Core engine functionality
* parin.map: Tile map utilities
* parin.platformer: Physics engine
* parin.sprite: Sprite utilities
* parin.story: Dialogue system
* parin.timer: Time utilities
* parin.ui: Immediate mode UI

The `parin.engine` module is the only mandatory module for creating a game.
All other modules are optional and can be included as needed.
The `import parin;` statement in the example above is a convenience import that includes all modules.

## 3. Input

Parin provides a set of input functions inside the `parin.engine` module.
These include:

```d
bool isDown(char key);
bool isDown(Keyboard key);
bool isDown(Mouse key);
bool isDown(Gamepad key, int id = 0);

bool isPressed(char key);
bool isPressed(Keyboard key);
bool isPressed(Mouse key);
bool isPressed(Gamepad key, int id = 0);

bool isReleased(char key);
bool isReleased(Keyboard key);
bool isReleased(Mouse key);
bool isReleased(Gamepad key, int id = 0);

Keyboard dequeuePressedKey();
dchar dequeuePressedRune();

Vec2 wasd();
Vec2 wasdPressed();
Vec2 wasdReleased();
Vec2 mouse();
Vec2 deltaMouse();
float deltaWheel();
```

Below are examples showing how to use these input functions to move text.

* Using the Mouse

    ```d
    bool update(float dt) {
        drawDebugText("Text", mouse);
        return false;
    }
    ```

* Using the Arrow Keys

    ```d
    auto position = Vec2(8);

    bool update(float dt) {
        position.x += Keyboard.right.isDown - Keyboard.left.isDown;
        position.y += Keyboard.down.isDown - Keyboard.up.isDown;
        drawDebugText("Text", position);
        return false;
    }
    ```

* Using the WASD Keys

    ```d
    auto position = Vec2(8);

    bool update(float dt) {
        position.x += 'd'.isDown - 'a'.isDown;
        position.y += 's'.isDown - 'w'.isDown;
        drawDebugText("Text", position);
        return false;
    }
    ```

* Using the WASD or Arrow Keys

    ```d
    auto position = Vec2(8);

    bool update(float dt) {
        position += wasd;
        drawDebugText("Text", position);
        return false;
    }
    ```

## 4. Drawing

Parin provides a set of drawing functions inside the `parin.engine` module.
These include:

```d
void drawRect(Rect area, Color color = white);
void drawHollowRect(Rect area, float thickness, Color color = white);
void drawCirc(Circ area, Color color = white);
void drawHollowCirc(Circ area, float thickness, Color color = white);
void drawVec2(Vec2 point, float size, Color color = white);
void drawLine(Line area, float size, Color color = white);

void drawTexture(TextureId texture, Vec2 position, DrawOptions options = DrawOptions());
void drawTextureArea(TextureId texture, Rect area, Vec2 position, DrawOptions options = DrawOptions());
void drawTexturePatch(TextureId texture, Rect area, Rect target, bool isTiled, DrawOptions options = DrawOptions());
void drawRune(FontId font, dchar rune, Vec2 position, DrawOptions options = DrawOptions());
void drawText(FontId font, IStr text, Vec2 position, DrawOptions options = DrawOptions(), TextOptions extraOptions = TextOptions());
void drawDebugText(IStr text, Vec2 position, DrawOptions options = DrawOptions(), TextOptions extraOptions = TextOptions());

void drawViewport(Viewport viewport, Vec2 position, DrawOptions options = DrawOptions());
void drawViewportArea(Viewport viewport, Rect area, Vec2 position, DrawOptions options = DrawOptions());
```

### Draw Options

Draw options are used for configuring drawing parameters.

```d
struct DrawOptions {
    Vec2 origin = Vec2(0.0f);
    Vec2 scale = Vec2(1.0f);
    float rotation = 0.0f;
    Color color = white;
    Hook hook = Hook.topLeft;
    Flip flip = Flip.none;
}
```

Here is a breakdown of what every option is:

* origin: The origin point of the drawn object. This value can be used to force a specific origin.
* scale: The scale of the drawn object.
* rotation: The rotation of the drawn object, in degrees.
* color: The color of the drawn object, in RGBA.
* hook: A value representing the origin point of the drawn object when origin is zero.
* flip: A value representing flipping orientations.

There is also an additional options type for text drawing.

```d
struct TextOptions {
    float visibilityRatio = 1.0f;
    int alignmentWidth = 0;
    ushort visibilityCount = 0;
    Alignment alignment = Alignment.left;
    bool isRightToLeft = false;
}
```

Here is a again a breakdown of what every option is:

* visibilityRatio: Controls the visibility ratio of the text when visibilityCount is zero, where 0.0 means fully hidden and 1.0 means fully visible.
* alignmentWidth: The width of the aligned text. It is used as a hint and is not enforced.
* visibilityCount: Controls the visibility count of the text. This value can be used to force a specific character count.
* alignment: A value represeting alignment orientations.
* isRightToLeft: Indicates whether the content of the text flows in a right-to-left direction.

Below are examples showing how to use these options to change how text looks.

* Changing the Origin and Scale

    ```d
    bool update(float dt) {
        auto options = DrawOptions(Hook.center);
        options.scale = Vec2(4 + sin(elapsedTime * 4));
        drawDebugText("Text", resolution * Vec2(0.5), options);
        return false;
    }
    ```

* Changing the Origin and Visibility Ratio

    ```d
    bool update(float dt) {
        auto options = DrawOptions(Hook.center);
        auto extra = TextOptions(fmod(elapsedTime, 2.0));
        drawDebugText("Hello.\nThis is some text.", resolution * Vec2(0.5), options, extra);
        return false;
    }
    ```

## 5. Sound

Parin provides a set of sound functions inside the `parin.engine` module.

```d
void playSound(Sound sound);
void stopSound(Sound sound);
void pauseSound(Sound sound);
void resumeSound(Sound sound);
void updateSound(Sound sound);
```

Below are examples showing how to use these sound functions.

* Playing a Sound

    ```d
    SoundId sound;

    bool update(float dt) {
        updateSound(sound);
        if (Keyboard.space.isPressed) playSound(sound);
        return false;
    }
    ```

* Pausing and Resuming a Sound

    ```d
    SoundId sound;

    bool update(float dt) {
        updateSound(sound);
        if (Keyboard.space.isPressed) playSound(sound);
        if (Keyboard.esc.isPressed) {
            if (sound.isPlaying) pauseSound(sound);
            else resumeSound(sound);
        }
        return false;
    }
    ```

## 6. Loading and Saving Resources

Parin provides a set of loading and saving functions inside the `parin.engine` module.
These include:

```d
TextureId loadTexture(IStr path);
FontId loadFont(IStr path, int size, int runeSpacing, int lineSpacing, IStr32 runes = "");
FontId loadFontFromTexture(IStr path, int tileWidth, int tileHeight);
SoundId loadSound(IStr path, float volume, float pitch, bool isLooping);

Result!Texture loadRawTexture(IStr path);
Result!Font loadRawFont(IStr path, int size, int runeSpacing, int lineSpacing, IStr32 runes = "");
Result!Font loadRawFontFromTexture(IStr path, int tileWidth, int tileHeight);
Result!Sound loadRawSound(IStr path, float volume, float pitch, bool isLooping);

Fault loadRawTextIntoBuffer(IStr path, ref LStr buffer);
Result!LStr loadRawText(IStr path);
Result!IStr loadTempText(IStr path);
Fault saveText(IStr path, IStr text);
```

Functions that start with the word load or save will always try to read/write resources from/to the assets folder.
They handle both forward slashes and backslashes in file paths, ensuring compatibility across operating systems.
Additionally, resources are separated into three groups. Raw, managed and temporary.

### Raw Resources

Raw resources are managed directly by the user.

### Managed Resources

Managed resources are managed by the engine, meaning that they can be safely shared throughout the code and are automatically invalidated when freed.

### Temporary Resources

Temporary resources are only valid until the function that provided them is called again.

## 7. Sprites and Tile Maps

Sprites and tile maps can be implemented in various ways.
To avoid enforcing a specific approach, Parin provides optional modules for these features, allowing users to include or omit them as needed.
Parin provides a sprite type inside the `parin.sprite` module and a tile map type inside the `parin.map` module.

<br>
Links:
[Pages](./pages.html)
[GitHub](https://github.com/Kapendev/parin)
[X](https://x.com/Kapendev)
[Bluesky](https://bsky.app/profile/kapendev.bsky.social)
[Itch](https://kapendev.itch.io/)
