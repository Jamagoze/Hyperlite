# Config hooks (LSPosed)

Five small LSPosed modules ported from a personal HyperCeiler setup, for a Redmi Pad SE on HyperOS 1.0 (Android 14).
Every option is a constant at the top of the module's `Hook.java`. Change it, rebuild, reinstall.

| Module (app name) | Zip | LSPosed scope |
|---|---|---|
| Home Config | `highend_home.zip` | `com.miui.home` |
| Framework Config | `framework_hook.zip` | System Framework |
| SystemUI Config | `systemui_hook.zip` | `com.android.systemui` |
| SystemUI Plugin Config | `plugin_hook.zip` | `com.android.systemui` |
| Settings Config | `settings_hook.zip` | `com.android.settings` |

## Build and install
1. Put the zips and `.github/workflows/build.yml` in the repo root. Pushing a zip (or "Run workflow") builds it.
2. Download the APKs from the workflow artifacts and install them.
3. LSPosed: enable each module with only the scope listed above. Reboot (Framework needs it); for the others force stop the target app.
4. Turn off the matching HyperCeiler scopes so the hooks don't run twice.

To change an option: edit the constant in `app/src/main/java/com/jama/<module>/Hook.java` inside the zip, keep the zip name, push.

---

## Home Config (`highend_home.zip`)

### Device level
| Constant | Default | Effect |
|---|---|---|
| `HIGH_END` | true | Launcher treats the device as high-end: device and CPU level 2, no lite or simple animations, complete animations, blur and widget features on. Includes a name-pattern scan of launcher classes plus HyperCeiler's exact device-level hooks. |

### Widgets
| Constant | Default | Effect |
|---|---|---|
| `MIUI_WIDGETS` | true | MIUI widgets show up as normal widgets in the picker. |
| `WIDGET_TO_MINUS` | true | Any widget can be dragged to the minus-one screen. |
| `WIDGET_RESIZABLE` | true | All widgets resizable in both directions, minimum sizes removed. |
| `WIDGET_HIDE_TITLE` | true | Hides widget titles. |
| `WIDGET_ALL_ANIM` | true | Transition animation for every widget. |

### Icon titles
| Constant | Default | Effect |
|---|---|---|
| `TITLE_SIZE_DESKTOP` | 10 | App label size on the home screen, in sp (12 = stock). |
| `TITLE_SIZE_DRAWER` | 12 | App label size in the drawer. If both are 12 the hook is off. |
| `HIDE_REPORT_TEXT` | true | Removes the report text in the uninstall dialog. |
| `NEW_INSTALL_INDICATOR_OFF` | true | Removes the "new install" dot. |
| `DOWNLOAD_ANIMATION` | true | Enables the download progress animation on icons. |

### Dock
| Constant | Default | Effect |
|---|---|---|
| `DISABLE_RECENTS_ICON` | true | No recent-app icons in the dock. |
| `UNLOCK_HOTSEAT` | true | Dock icon limit raised to 99. |
| `HOTSEAT_LAYOUT` | false | Master switch for the three values below. Off because 150 dp broke the dock. |
| `HOTSEAT_HEIGHT_DP` | 150 | Dock height (stock is about 60). |
| `HOTSEAT_MARGIN_TOP_DP` | 1 | Dock top margin. |
| `HOTSEAT_MARGIN_BOTTOM_DP` | 5 | Dock bottom margin. |

### Recents
| Constant | Default | Effect |
|---|---|---|
| `RECENT_HIDE_CLEAN_UP` | true | Hides the clear-all button. |
| `RECENT_REMOVE_ICON` | true | Hides the app icon in each card header. |
| `RECENT_BLUR_LEVEL` | 4 | 4 = simple blur (blur type 0, no complete blur). Any other value disables the hook. |
| `TASK_HORIZONTAL_1` / `_2` | 0.5 | Card scale in the horizontal layout (not landscape / landscape). 1.0 = stock. |
| `TASK_VERTICAL` | 0.5 | Card scale in the vertical layout. |
| `TASK_CORNER_DP` | 25 | Card corner radius in dp (20 = stock, hook off). |
| `ANIM_TITLE` | 1.3 | Multiplier on the icon-to-app animation response (1 = off). |
| `ANIM_RECENT` | 1.6 | Transition animation ratio (1 = off). |

### Drawer, folders, other
| Constant | Default | Effect |
|---|---|---|
| `DRAWER_ALL` | true | Drops the first category so the drawer shows "all apps". |
| `FOLDER_RECOMMEND_OFF` | true | Hides the folder recommend-apps switch. |
| `FOLDER_VERTICAL_SPACING_DP` | 60 | Folder row spacing in dp (0 = off). |
| `FOLDER_TITLE_CENTER` | true | Centered folder title with marquee when long. |
| `TOAST_SLIDE_AGAIN` | true | Suppresses the "slide again" toast. |
| `OPT_LAUNCH_DELAY` | true | Removes the app launch finish-callback delay. |
| `SEEK_POINTS_HIDE` | true | Page indicator hidden except in edit mode. |
| `SHORTCUT_COUNT` | true | Long-press shortcut menu shows up to 20 items. |
| `QUICK_BACK` | true | Quick-back gesture (swipe up-and-back to switch to the previous app). |
| `MAX_FREEFORM` | true | Launcher can open more than one floating window (dock "Floating window", recents). Works together with `FREEFORM_COUNT` in Framework. |

---

## Framework Config (`framework_hook.zip`)

| Constant | Default | Effect |
|---|---|---|
| `DISABLE_72H` | true | No forced password/PIN every 72 hours. |
| `SAFE_VOLUME` | true | Safe media volume warning disabled. |
| `SPEED_INSTALL` | true | Speed install v2 supported. |
| `NO_MIUI_LITE` | true | MIUI lite checks report false. |
| `LOW_API` | true | Install apps targeting old SDK levels. |
| `NO_PERSISTENT` | true | Installed apps can't claim the persistent flag. |
| `ANDROID_INSTALLER` | true | Uses the Android package installer instead of the MIUI one. |
| `QUICK_SCREENSHOT` | true | Power + volume screenshot chord delay set to 0. |
| `FREEFORM_COUNT` | true | Maximum floating windows raised to 256. |
| `FREEFORM_BUBBLE` | true | Multi-freeform supported (bubbles). |
| `FREEFORM_BLACKLIST` | true | Freeform blacklist emptied, non-resizable apps allowed in windows. |
| `FOREGROUND_PIN` | true | Foreground pin always available. |
| `THIRD_THEME` | true | Third-party themes pass the DRM check. |
| `NO_CLEANER` | true | Disables the MIUI memory cleaner and process killers. |
| `NO_GESTURE_MONITOR` | true | Disables the MIUI gesture monitor. |
| `HOOK_ENTRY` | true | HyperCeiler's hook-entry flag (battery notification listener). |
| `PROTECTED_PACKAGE` | true | Protected packages can be disabled. |

Not included: core patches (signature and shared-user bypass), sticky floating windows.

---

## SystemUI Config (`systemui_hook.zip`)

### Status bar
| Constant | Default | Effect |
|---|---|---|
| `ICONS` | see below | Per-icon visibility table. |
| `DATA_SAVER_MODE` | 2 | Data saver icon: 0 stock, 1 always, 2 never. |
| `DOUBLE_TAP_SLEEP` | true | Double tap the status bar to turn the screen off. |
| `HIDE_BAR_BEFORE_SCREENSHOT` | true | Status bar hidden while a screenshot is taken. |
| `HIDE_STRONG_TOAST` | true | Hides the smart strong toast. |
| `HIDE_PERCENT_MARK` | true | Hides the % sign in the battery percentage. |
| `NOTIF_ICONS_MAX` | 1 | Max notification icons in the status bar (0 = off). |

`ICONS` codes: 0 stock, 1 show, 2 hide in status bar and control center, 11 hide in status bar only, 12 hide in control center only.
Defaults: hidden (2): vpn, alarm_clock, nfc, zen, wifi, demo_wifi, airplane, location, speakerphone, hotspot, bluetooth, bluetooth_handsfree_battery. Status bar only (11): headset, wireless_headset.

### Navigation and windows
| Constant | Default | Effect |
|---|---|---|
| `HIDE_NAV_BAR` | true | Navigation bar removed. |
| `REMOVE_MULTIWIN_SWITCH` | true | Removes the top pill (full screen / split / small window / close) and its gap on normal windows. Floating and picture-in-picture windows keep theirs. |
| `DISABLE_MULTIWIN_SWITCH` | true | Hides the small dot of the multi-window switch. |
| `DISABLE_BOTTOM_BAR` | true | Removes the bottom caption bar of windows. |
| `NOTIF_FREEFORM` | true | Notifications can open in a floating window. |

### Control center
| Constant | Default | Effect |
|---|---|---|
| `OLD_CONTROL_CENTER` | true | Master switch for the grid values below. |
| `QS_COLS` / `QS_COLS_H` | 7 / 8 | Tile columns, portrait / landscape. |
| `QS_ROWS` / `QS_ROWS_H` | 5 / 3 | Tile rows, portrait / landscape. |
| `QQS_COLS` / `QQS_COLS_H` | 7 / 8 | Quick tiles in the collapsed header. |
| `CC_UNLOCK_OLD` | true | Allows the old control center style. |
| `CC_AUTO_CLOSE` | true | Tapping a tile collapses the panel. |
| `CC_UNIMPORTANT_NOTICE` | true | Unimportant notifications stay visible. |

### Media
| Constant | Default | Effect |
|---|---|---|
| `MEDIA_CUSTOM_ACTIONS` | true | Shows custom action buttons on the media card. |
| `MEDIA_SQUIGGLY` | true | Squiggly progress bar. |

### Lock screen and clipboard
| Constant | Default | Effect |
|---|---|---|
| `UNLOCK_CLIPBOARD` | true | Copied text shows the clipboard preview and can be edited. Image clips (screenshots) are ignored to avoid a second popup. |
| `LOCK_DOUBLE_TAP` | true | Double tap on the lock screen to turn the screen off. |
| `LOCK_HIDE_STATUS_BAR` | true | Hides the lock screen status bar. |
| `LOCK_BLOCK_EDITOR` | true | Blocks the lock screen editor. |
| `LOCK_NO_BLE_TOAST` | true | Hides the "unlocked by Bluetooth" toast. |

---

## SystemUI Plugin Config (`plugin_hook.zip`)

Hooks the `miui.systemui.plugin` classes (control center, volume) once SystemUI loads them.

| Constant | Default | Effect |
|---|---|---|
| `HIDE_EDIT_BUTTON` | true | Hides the tile edit button in the control center. |
| `TILE_SUPER_BLUR` | true | Super blur blend colors on tiles, cards and the ringer buttons. |
| `DEFAULT_PLUGIN_THEME` | true | Plugin uses the default theme. |

---

## Settings Config (`settings_hook.zip`)

| Constant | Default | Effect |
|---|---|---|
| `INTERNATIONAL_BUILD` | true | Sets the international build flag, unlocking global-ROM settings. |
| `UNLOCK_UI_MODE` | true | Shows the auto UI mode setting. |
| `SAFE_WIFI` | true | Saved Wi-Fi networks get a Password button that shows the password. |
| `SPEED_MODE` | true | Speed mode tools in developer options. |
| `MAX_FPS` | true | Force peak refresh rate option. |
| `APPS_FREEZER` | true | Cached apps freezer option. |
| `OVERLAY_PERMISSION` | true | Direct jump to an app's draw-over-apps page. |
| `ACCESSIBILITY_PERMISSION` | true | Direct jump to an app's accessibility service page. |
| `NO_UNKNOWN_VERIFY` | true | No verification when installing from unknown sources. |
| `ANTI_QUES` | true | Device and hotspot names accept any text. |
| `AI_IMAGE` | true | AI image, MEMC and super resolution options unlocked. |
| `MORE_NOTIFICATION` | true | Importance, badge and lock screen options always shown. |

---

## Troubleshooting
- Nothing changes: check the module is enabled in LSPosed with the exact scope above, then force stop the app (reboot for Framework).
- Each hook logs a line starting with its module name (for example `UiHook`) when a class or method is missing. Check LSPosed Logs, or run `su -c "logcat -d | grep -E 'FrameworkHook|HighEndHome|UiHook|PluginHook|SettingsHook'"`.
- After a crash, `su -c 'dumpsys dropbox --print system_app_crash'` shows the stack trace.
- One setting misbehaves: set its constant to `false` and rebuild. Hooks are independent.
