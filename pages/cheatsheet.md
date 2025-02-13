<p align="center">
    <a href="./pages.html">
        <img src="../assets/snake_x20.png" alt="Moon Sprite" width="120" height="128">
    </a>
</p>

# Cheatsheet

Welcome to the Parin cheatsheet.
If you notice anything missing or would like to contribute, feel free to create an [issue](https://github.com/Kapendev/parin/issues)!

### parin.engine

```d
// [App]
int screenWidth();
int screenHeight();
Vec2 screenSize();
int windowWidth();
int windowHeight();
Vec2 windowSize();
int resolutionWidth();
int resolutionHeight();
Vec2 resolution();
EngineViewportInfo engineViewportInfo();

int fps();
double elapsedTime();
long elapsedTickCount();
float deltaTime();

bool isWindowResized();
void setBackgroundColor(Color value);
void setBorderColor(Color value);
void setWindowMinSize(int width, int height);
void setWindowMaxSize(int width, int height);
Fault setWindowIconFromFiles(IStr path);

bool isPixelSnapped();
void setIsPixelSnapped(bool value);
void toggleIsPixelSnapped();
bool isPixelPerfect();
void setIsPixelPerfect(bool value);
void toggleIsPixelPerfect();
bool isCursorVisible();
void setIsCursorVisible(bool value);
void toggleIsCursorVisible();
bool isFullscreen();
void setIsFullscreen(bool value);
void toggleIsFullscreen();

IStr[] envArgs();
IStr assetsPath();
IStr toAssetsPath(IStr path);
bool canUseAssetsPath();
void setCanUseAssetsPath(bool value);
IStr[] droppedFilePaths();
void openUrl(IStr url = "https://github.com/Kapendev/parin");
void freeResources();

// [Input]
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

// [Drawing]
void drawRect(Rect area, Color color = white);
void drawHollowRect(Rect area, float thickness, Color color = white);
void drawCirc(Circ area, Color color = white);
void drawHollowCirc(Circ area, float thickness, Color color = white);
void drawVec2(Vec2 point, float size, Color color = white);
void drawLine(Line area, float size, Color color = white);

void drawTexture(Texture texture, Vec2 position, DrawOptions options = DrawOptions());
void drawTextureArea(Texture texture, Rect area, Vec2 position, DrawOptions options = DrawOptions());
void drawTexturePatch(Texture texture, Rect area, Rect target, bool isTiled, DrawOptions options = DrawOptions());

void drawViewport(Viewport viewport, Vec2 position, DrawOptions options = DrawOptions());
void drawViewportArea(Viewport viewport, Rect area, Vec2 position, DrawOptions options = DrawOptions());

void drawRune(Font font, dchar rune, Vec2 position, DrawOptions options = DrawOptions());
void drawText(Font font, IStr text, Vec2 position, DrawOptions options = DrawOptions());
void drawDebugText(IStr text, Vec2 position, DrawOptions options = DrawOptions());

// [Sound]
void playSound(Sound sound);
void stopSound(Sound sound);
void pauseSound(Sound sound);
void resumeSound(Sound sound);
void updateSound(Sound sound);

// [Loading/Saving]
TextureId loadTexture(IStr path);
FontId loadFont(IStr path, int size, int runeSpacing, int lineSpacing, IStr32 runes = "");
FontId loadFontFromTexture(IStr path, int tileWidth, int tileHeight);
SoundId loadSound(IStr path, float volume, float pitch);

Result!Texture loadRawTexture(IStr path);
Result!Font loadRawFont(IStr path, int size, int runeSpacing, int lineSpacing, IStr32 runes = "");
Result!Font loadRawFontFromTexture(IStr path, int tileWidth, int tileHeight);
Result!Sound loadRawSound(IStr path, float volume, float pitch);

Fault loadRawTextIntoBuffer(IStr path, ref LStr buffer);
Result!LStr loadRawText(IStr path);
Result!IStr loadTempText(IStr path);
Fault saveText(IStr path, IStr text);

// [Random]
int randi();
float randf();
void randomize(int seed);
void randomize();

// [Enums]
enum Flip : ubyte {
    none,
    x,
    y,
    xy,
}

enum Alignment : ubyte {
    left,
    center,
    right,
}

enum Filter : ubyte {
    nearest,
    linear,
}

enum Wrap : ubyte {
    clamp,
    repeat,
}

enum Blend : ubyte {
    alpha,
    additive,
    multiplied,
    add,
    sub,
}

enum Keyboard : ushort {
    none,
    a,
    b,
    c,
    d,
    e,
    f,
    g,
    h,
    i,
    j,
    k,
    l,
    m,
    n,
    o,
    p,
    q,
    r,
    s,
    t,
    u,
    v,
    w,
    x,
    y,
    z,
    n0,
    n1,
    n2,
    n3,
    n4,
    n5,
    n6,
    n7,
    n8,
    n9,
    nn0,
    nn1,
    nn2,
    nn3,
    nn4,
    nn5,
    nn6,
    nn7,
    nn8,
    nn9,
    f1,
    f2,
    f3,
    f4,
    f5,
    f6,
    f7,
    f8,
    f9,
    f10,
    f11,
    f12,
    left,
    right,
    up,
    down,
    esc,
    enter,
    tab,
    space,
    backspace,
    shift,
    ctrl,
    alt,
    win,
    insert,
    del,
    home,
    end,
    pageUp,
    pageDown,
}

enum Mouse : ushort {
    none,
    left,
    right,
    middle,
}

enum Gamepad : ushort {
    none,
    left,
    right,
    up,
    down,
    y,
    x,
    a,
    b,
    lt,
    lb,
    lsb,
    rt,
    rb,
    rsb,
    back,
    start,
    middle,
}

// [Structs]
struct DrawOptions {
    Vec2 origin = Vec2(0.0f);
    Vec2 scale = Vec2(1.0f);
    float rotation = 0.0f;
    Color color = white;
    Hook hook = Hook.topLeft;
    Flip flip = Flip.none;
    Alignment alignment = Alignment.left;
    int alignmentWidth = 0;
    float visibilityRatio = 1.0f;
    bool isRightToLeft = false;
}

struct TextureId {
    int width();
    int height();
    Vec2 size();
    void setFilter(Filter value);
    void setWrap(Wrap value);
    bool isValid();
    void free();
}

struct FontId {
    int runeSpacing();
    int lineSpacing();
    int size();
    void setFilter(Filter value);
    void setWrap(Wrap value);
    bool isValid();
    void free();
}

struct SoundId {
    bool isPaused();
    bool isPlaying();
    float time();
    float duration();
    float progress();
    void setVolume(float value);
    void setPitch(float value);
    void setPan(float value);
    bool isValid();
    void free();
}
```

<br>
Links:
[Pages](./pages.html)
[GitHub](https://github.com/Kapendev/parin)
[X](https://x.com/Kapendev)
[Bluesky](https://bsky.app/profile/kapendev.bsky.social)
[Itch](https://kapendev.itch.io/)
