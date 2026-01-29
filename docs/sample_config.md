# Sample Configuration

Add the module to your `config.js` file:

```javascript
{
    module: "MMM-S3Photos",
    position: "fullscreen_below",    // standard Magic mirror regions (fullscreen_below should be used if setting wallpaper as display style)

    config: {
        syncTimeHours: 1,           // How often to check for new photos/videos (1 = hourly)
        cacheLifeDays: 0,           // 0 = never clean cache, otherwise days between cache purges
        displayDurationSeconds: 60,  // How long to show each photo/video
        transitionDurationSeconds: 1.5, // How long (seconds) the transition animation takes
        
        // Display Style Options
        displayStyle: "absolute",   // Choose one:
                                    // "wallpaper" (fills entire screen)
                                    // "fill" (fills container region)
                                    // "fit-display" (maintains aspect ratio while filling display)
                                    // "absolute" (fixed size)
        applyBlur: false,           // Adds a blurred background in empty spaces
        
        // Only used when displayStyle is "absolute", omit if not using absolute mode
        absoluteOptions: {           
            enabled: false,
            side: "horizontal",      // "horizontal" = fixed width, "vertical" = fixed height
            size: 400,               // Size in pixels for the fixed dimension
            blurContainer: {
                width: 500,          // Only used if applyBlur is true and displayStyle is absolute
                height: 500          // Defines the size of the blur effect container
            }
        },
        
        // Photo Order Options
        displayOrder: "random",     // Choose one:
                                    // "random" (completely random)
                                    // "random_dedupe" (won't repeat until all media are shown)
                                    // "newest_first" (chronological, newest media first)
                                    // "oldest_first" (chronological, oldest media first)
        
        // Video Settings
        video: {
            enabled: true,           // Enable/disable video playback
            autoplay: true,          // Auto-start videos when displayed
            muted: true,             // Mute videos (required for autoplay in most browsers)
            loop: false,             // Loop individual videos
            controls: false,         // Show video controls (play/pause/volume)
            preload: 'metadata',     // Preload strategy: 'none', 'metadata', or 'auto'
            videosOnly: false        // Show only videos (filter out images) - useful for testing
        },
        
        // Attribution Settings
        attribution: {
            enabled: true,          
            attributions: {
                "samples": "Sample Photos by Pexels",     // In this example: "vacation_folder" is the folder name and "Summer 2023" will be displayed.
                "selfies": "Selfieshot Selfies",          // In this example: "family_folder" is the folder name and "Family Photos" will be displayed.
                "videos": "My Video Collection"           // Attribution works for both photos and videos
            },
            position: "static",      // "static" or "dynamic"
            corner: "bottom-right", // Only used if position is "static"
                                   // "top-left", "top-right", "bottom-left", "bottom-right"
            relativeTo: "display"   // Choose one:
                                   // "display" (relative to screen)
                                   // "image" (relative to photo/video boundaries)
                                   // "container" (relative to MM region)
        },
        selfieUploads: false,  // Whether to process and upload photos from MMM-Selfieshot
        selfieFolder: "selfies" // S3 folder name for selfieshot uploads
    }
}
```

## Video Configuration Examples

### Example 1: Mixed Photos and Videos (Default)
```javascript
video: {
    enabled: true,
    autoplay: true,
    muted: true,
    loop: false,
    controls: false,
    preload: 'metadata',
    videosOnly: false
}
```

### Example 2: Videos Only Mode
Perfect for testing or creating a dedicated video display:
```javascript
video: {
    enabled: true,
    autoplay: true,
    muted: true,
    loop: false,
    controls: false,
    preload: 'metadata',
    videosOnly: true  // Only show videos, filter out all images
}
```

### Example 3: Looping Videos with Controls
```javascript
video: {
    enabled: true,
    autoplay: true,
    muted: false,      // Unmute videos
    loop: true,        // Loop each video
    controls: true,    // Show playback controls
    preload: 'auto',   // Preload entire video
    videosOnly: false
}
```

### Example 4: Disable Video Playback
Show only images:
```javascript
video: {
    enabled: false  // Videos will be skipped
}
```

## Video Recommendations

For best performance on Raspberry Pi, use MP4 with H.264 codec at 720p or 1080p resolution.
