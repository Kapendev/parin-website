<p align="center">
    <a href="./pages.html">
        <img src="../assets/snake_x20.png" alt="Moon Sprite" width="120" height="128">
    </a>
</p>

# Cheatsheet

### parin.engine

```d
Font toFont(Texture texture, int tileWidth, int tileHeight);
Flip oppositeFlip(Flip flip, Flip fallback);
IStr[] envArgs();
int randi();
float randf();
void randomize(int seed);
void randomize();

Vec2 toScreenPoint(Vec2 position, Camera camera, Viewport viewport = Viewport());
Vec2 toWorldPoint(Vec2 position, Camera camera, Viewport viewport = Viewport());
IStr assetsPath();
IStr toAssetsPath(IStr path);
bool canUseAssetsPath();
void setCanUseAssetsPath(bool value);
IStr[] droppedFilePaths();
ref LStr prepareTempText();
Fault loadRawTextIntoBuffer(IStr path, ref LStr buffer);
Result!LStr loadRawText(IStr path);
Result!IStr loadTempText(IStr path);
Result!Texture loadRawTexture(IStr path);
TextureId loadTexture(IStr path);
Result!Font loadRawFont(IStr path, int size, int runeSpacing, int lineSpacing, IStr32 runes = "");
FontId loadFont(IStr path, int size, int runeSpacing, int lineSpacing, IStr32 runes = "");
Result!Font loadRawFontFromTexture(IStr path, int tileWidth, int tileHeight);
FontId loadFontFromTexture(IStr path, int tileWidth, int tileHeight);
Result!Sound loadRawSound(IStr path, float volume, float pitch);
SoundId loadSound(IStr path, float volume, float pitch);
Fault saveText(IStr path, IStr text);

void freeResources();
void openUrl(IStr url = "https://github.com/Kapendev/parin");
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
bool isWindowResized();
void setBackgroundColor(Color value);
void setBorderColor(Color value);
void setWindowMinSize(int width, int height);
void setWindowMaxSize(int width, int height);
Fault setWindowIconFromFiles(IStr path);
EngineViewportInfo engineViewportInfo();
Font engineFont();
Filter defaultFilter();
Wrap defaultWrap();
void setDefaultFilter(Filter value);
void setDefaultWrap(Wrap value);
void setEngineViewportFilter(Filter value);
float masterVolume();
void setMasterVolume(float value);
bool isResolutionLocked();
void lockResolution(int width, int height);
void unlockResolution();
void toggleResolution(int width, int height);

int screenWidth();
int screenHeight();
Vec2 screenSize();
int windowWidth();
int windowHeight();
Vec2 windowSize();
int resolutionWidth();
int resolutionHeight();
Vec2 resolution();
Vec2 mouse();
int fps();
double elapsedTime();
long elapsedTickCount();
float deltaTime();
Vec2 deltaMouse();
float deltaWheel();
Vec2 measureTextSize(Font font, IStr text, DrawOptions options = DrawOptions());
Vec2 measureTextSize(FontId font, IStr text, DrawOptions options = DrawOptions());

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

void playSound(ref Sound sound);
void playSound(SoundId sound);
void stopSound(ref Sound sound);
void stopSound(SoundId sound);
void pauseSound(ref Sound sound);
void pauseSound(SoundId sound);
void resumeSound(ref Sound sound);
void resumeSound(SoundId sound);
void updateSound(ref Sound sound);
void updateSound(SoundId sound);

void drawRect(Rect area, Color color = white);
void drawHollowRect(Rect area, float thickness, Color color = white);
void drawVec2(Vec2 point, float size, Color color = white);
void drawCirc(Circ area, Color color = white);
void drawHollowCirc(Circ area, float thickness, Color color = white);
void drawLine(Line area, float size, Color color = white);
void drawTextureArea(Texture texture, Rect area, Vec2 position, DrawOptions options = DrawOptions());
void drawTextureArea(TextureId texture, Rect area, Vec2 position, DrawOptions options = DrawOptions());
void drawTexture(Texture texture, Vec2 position, DrawOptions options = DrawOptions());
void drawTexture(TextureId texture, Vec2 position, DrawOptions options = DrawOptions());
void drawTexturePatch(Texture texture, Rect area, Rect target, bool isTiled, DrawOptions options = DrawOptions());
void drawTexturePatch(TextureId texture, Rect area, Rect target, bool isTiled, DrawOptions options = DrawOptions());
void drawViewportArea(Viewport viewport, Rect area, Vec2 position, DrawOptions options = DrawOptions());
void drawViewport(Viewport viewport, Vec2 position, DrawOptions options = DrawOptions());
void drawRune(Font font, dchar rune, Vec2 position, DrawOptions options = DrawOptions());
void drawRune(FontId font, dchar rune, Vec2 position, DrawOptions options = DrawOptions());
void drawText(Font font, IStr text, Vec2 position, DrawOptions options = DrawOptions());
void drawText(FontId font, IStr text, Vec2 position, DrawOptions options = DrawOptions());
void drawDebugText(IStr text, Vec2 position, DrawOptions options = DrawOptions());
```

<br>
Links:
[Pages](./pages.html)
[GitHub](https://github.com/Kapendev/parin)
[X](https://x.com/Kapendev)
[Bluesky](https://bsky.app/profile/kapendev.bsky.social)
[Itch](https://kapendev.itch.io/)
