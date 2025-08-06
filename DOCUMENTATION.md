# 🚀 MS Loading Screen - Premium Edition
## Complete Documentation & Setup Guide

---

## 📦 **Package Contents**
- ✅ Responsive Loading Screen
- ✅ Multi-Theme Support (4 different themes)
- ✅ Real-time Server Status API
- ✅ Background Slideshow & Video Support
- ✅ Multi-language Support (TR/EN/DE/FR/ES)
- ✅ Premium Animations
- ✅ Keyboard Shortcuts
- ✅ Mobile Compatible
- ✅ Easy Installation

---

## 🛠️ **Installation Steps**

### 1. File Structure
```
resources/
└── ms-loading/
    ├── fxmanifest.lua
    ├── html/
    │   ├── index.html
    │   ├── config.js    # MAIN CONFIGURATION FILE
    │   ├── js/script.js
    │   ├── css/style.css
    │   └── sounds/loading.mp3
    ├── images/
    │   ├── logo.png
    │   ├── gallery1.jpg
    │   ├── gallery2.jpg
    │   └── gallery3.jpg
    └── DOCUMENTATION.md
```

### 2. Add to server.cfg
```cfg
ensure ms-loading
```

### 3. Required Files
Add these image files to the `images/` folder:
- `logo.png` - Your server logo
- `gallery1.jpg` - Gallery image 1
- `gallery2.jpg` - Gallery image 2
- `gallery3.jpg` - Gallery image 3

### 4. Audio File
Add `loading.mp3` to the `html/sounds/` folder

---

## ⚙️ **Configuration Guide**

All settings are controlled from `html/config.js`. Edit this file to customize your loading screen.

### **Basic Server Information**
```javascript
serverInfo: {
  name: 'YOUR SERVER NAME',           // Server name displayed
  ip: 'yourserver.com',               // Server IP shown to players
  maxPlayers: 128,                    // Maximum player count
  currentPlayers: 0,                  // Current players (auto-updated with API)
  version: 'v1.0.0'                   // Server version
}
```

### **Staff Team Configuration**
```javascript
authorizedTeam: [
  { 
    name: "AdminName", 
    role: "owner", 
    discordUrl: "https://discord.com/users/YOUR_DISCORD_ID" 
  },
  { 
    name: "ModeratorName", 
    role: "moderator", 
    discordUrl: "https://discord.com/users/MODERATOR_ID" 
  }
]
```

**Available Roles:**
- `owner` - Red icon
- `moderator` - Blue icon  
- `developer` - Orange icon
- `support` - Green icon

### **Social Media Links**
```javascript
socialMedia: [
  { name: "Discord", url: "https://discord.gg/YOUR_INVITE", icon: "discord" },
  { name: "Twitter", url: "https://twitter.com/YOUR_PROFILE", icon: "twitter" },
  { name: "YouTube", url: "https://youtube.com/YOUR_CHANNEL", icon: "youtube" },
  { name: "Instagram", url: "https://instagram.com/YOUR_PROFILE", icon: "instagram" }
]
```

**Supported Icons:** discord, twitter, youtube, instagram, facebook, twitch

### **Server Rules**
```javascript
rules: [
  "No harassment in the server.",
  "Cheating is forbidden.",
  "Out-of-roleplay behavior will be punished.",
  "Respect the staff.",
  "Realism rule must be followed."
]
```

---

## 🎨 **Theme System**

### **Available Themes:**
1. **Default** - Blue gradient theme
2. **Dark** - Dark purple theme
3. **Neon** - Green neon theme
4. **Minimal** - Clean white theme

### **Changing Theme:**
```javascript
theme: {
  name: 'dark', // 'default', 'dark', 'neon', 'minimal'
}
```

### **Custom Colors:**
```javascript
theme: {
  name: 'default',
  customColors: {
    primary: '#4fc3f7',      // Main accent color
    secondary: '#3498db',     // Secondary color
    accent: '#e74c3c',        // Highlight color
    text: '#eaeaea'           // Text color
  }
}
```

---

## 🌅 **Background System**

### **Gradient Background (Default)**
```javascript
background: {
  type: 'gradient'
}
```

### **Image Slideshow**
```javascript
background: {
  type: 'slideshow',
  slideshow: {
    enabled: true,
    images: [
      'images/bg1.jpg',
      'images/bg2.jpg', 
      'images/bg3.jpg'
    ],
    duration: 5000,         // 5 seconds per image
    transition: 'fade'      // 'fade' or 'slide'
  }
}
```

### **Video Background**
```javascript
background: {
  type: 'video',
  video: {
    enabled: true,
    src: 'videos/background.mp4',
    overlay: true           // Adds dark overlay for readability
  }
}
```

---

## 📡 **Server Status API**

### **Enable Real-time Player Count:**
```javascript
serverInfo: {
  statusAPI: {
    enabled: true,
    endpoint: 'YOUR_API_ENDPOINT'
  }
}
```

### **API Options:**

#### **Option 1: CFX.re API (FREE)**
```javascript
endpoint: 'https://servers-frontend.fivem.net/api/servers/single/SERVER_ID'
```
**To find your Server ID:** Search your server on https://servers.fivem.net/

#### **Option 2: Custom PHP API**
Create `api/status.php` on your website:

```php
<?php
header('Content-Type: application/json');
header('Access-Control-Allow-Origin: *');

// FiveM server info
$server_ip = "YOUR_SERVER_IP";
$server_port = 30120;

$query_url = "http://{$server_ip}:{$server_port}/players.json";
$info_url = "http://{$server_ip}:{$server_port}/info.json";

try {
    $players_data = @file_get_contents($query_url);
    $server_info = @file_get_contents($info_url);
    
    $players = $players_data ? json_decode($players_data, true) : [];
    $info = $server_info ? json_decode($server_info, true) : [];
    
    $response = [
        "players" => count($players),
        "maxPlayers" => $info['vars']['sv_maxclients'] ?? 128,
        "status" => "online"
    ];
    
} catch (Exception $e) {
    $response = [
        "players" => 0,
        "maxPlayers" => 128,
        "status" => "offline"
    ];
}

echo json_encode($response);
?>
```

#### **Expected JSON Response:**
```json
{
  "players": 45,
  "maxPlayers": 128,
  "status": "online"
}
```

---

## 🌍 **Multi-language Support**

### **Available Languages:**
- Turkish (tr)
- English (en)
- German (de)
- French (fr)
- Spanish (es)

### **Change Language:**
```javascript
language: 'en', // 'tr', 'en', 'de', 'fr', 'es'
```

### **Add Custom Translations:**
```javascript
translations: {
  en: {
    rules: "Rules",
    gallery: "Gallery",
    authorizedTeam: "Authorized Team",
    welcome: "Welcome!",
    loading: "Loading..."
  },
  tr: {
    rules: "Kurallar",
    gallery: "Galeri", 
    authorizedTeam: "Yetkili Kadro",
    welcome: "Hoş geldiniz!",
    loading: "Yükleniyor..."
  }
}
```

---

## 🎭 **Loading Effects & Animations**

### **Progress Bar Styles:**
```javascript
loadingEffects: {
  progressBarStyle: 'neon',    // 'gradient', 'neon', 'minimal'
  spinnerType: 'dots',         // 'default', 'dots', 'pulse'
  textAnimation: 'typewriter', // 'fade', 'slide', 'typewriter'
  logoAnimation: 'bounce',     // 'pulse', 'rotate', 'bounce', 'none'
  particles: {
    count: 100,                // Number of particles
    color: '#4fc3f7',         // Particle color
    speed: 3                   // Animation speed
  }
}
```

### **Available Animations:**
- **Logo:** pulse, rotate, bounce, none
- **Text:** fade, slide, typewriter
- **Progress:** gradient, neon, minimal
- **Spinner:** default, dots, pulse

---

## 💬 **Loading Messages**

Messages are displayed based on loading percentage:

```javascript
loadingMessages: {
  0: "Connecting to server...",
  10: "Checking game files...",
  20: "Loading character data...",
  30: "Preparing world map...",
  40: "Loading vehicles and objects...",
  50: "Getting player data...",
  60: "Checking server rules...",
  70: "Final adjustments...",
  80: "Preparing roleplay environment...",
  90: "Completing connection...",
  100: "Welcome!"
}
```

---

## ⌨️ **Keyboard Shortcuts**

- **M** or **Space** - Toggle music on/off
- **Tab** - Navigate through elements

---

## 📱 **Responsive Design**

### **Automatic Adaptations:**
- ✅ Mobile devices - Sidebars hidden below 720px
- ✅ Small screens - Logo and text scale down below 420px
- ✅ Tablet support - All elements adjust automatically
- ✅ All resolutions - Perfect display on any screen

---

## 🔧 **Troubleshooting**

### **Images Not Showing**
- Add required files to `images/` folder
- Check `fxmanifest.lua` files list
- Verify file names match exactly

### **Music Not Playing**
- Ensure `html/sounds/loading.mp3` exists
- Check audio format is `.mp3`
- Verify file is not corrupted

### **API Not Working**
- Check API endpoint CORS settings
- Verify JSON response format is correct
- Test API endpoint in browser

### **Theme Not Changing**
- Clear browser cache (Ctrl+F5)
- Check config.js syntax
- Verify theme name is correct

### **Animations Not Working**
- Ensure CSS files are loaded correctly
- Check browser console for errors
- Verify loadingEffects configuration

---

## 🚀 **Performance Tips**

### **Optimize Images:**
- Use compressed JPG/PNG files
- Recommended sizes: Logo 300x300px, Gallery 500x300px
- Keep total size under 5MB

### **API Optimization:**
- Use caching to reduce server load
- Implement rate limiting
- Use HTTPS for security

### **Loading Speed:**
- Minimize image file sizes
- Use CDN for external resources
- Test loading times regularly

---

## 📊 **Features Comparison**

| Feature | Basic | Premium |
|---------|-------|---------|
| Responsive Design | ✅ | ✅ |
| Basic Themes | ✅ | ✅ |
| Advanced Themes | ❌ | ✅ |
| Server Status API | ❌ | ✅ |
| Background Slideshow | ❌ | ✅ |
| Video Background | ❌ | ✅ |
| Multi-language | ❌ | ✅ |
| Premium Animations | ❌ | ✅ |
| Keyboard Shortcuts | ❌ | ✅ |
| Documentation | Basic | Complete |

---

## 💰 **License & Usage**

### **What's Included:**
- ✅ Commercial use license
- ✅ Unlimited servers
- ✅ Free updates for 1 year
- ✅ Basic support via Discord
- ✅ Customization allowed

### **Restrictions:**
- ❌ Source code resale prohibited
- ❌ Redistribution not allowed
- ❌ Claiming authorship forbidden

---

## 📞 **Support & Updates**

### **Getting Help:**
- **Discord:** [Support Server](https://discord.gg/yoursupport)
- **Email:** support@metascripts.com
- **Documentation:** This guide
- **Updates:** Automatic via Discord announcements

### **Reporting Issues:**
When reporting problems, please include:
1. Loading screen version
2. Browser/FiveM version
3. Error message (if any)
4. Steps to reproduce

---

## 🎯 **Quick Start Checklist**

- [ ] Extract files to `resources/ms-loading/`
- [ ] Add to `server.cfg`
- [ ] Edit `html/config.js` with your info
- [ ] Add logo.png and gallery images
- [ ] Add loading.mp3 audio file
- [ ] Test in browser first
- [ ] Test in FiveM
- [ ] Configure API (optional)
- [ ] Customize theme/colors
- [ ] Set up social media links

---

## 🔄 **Version History**

### **v1.0.0 - Premium Edition**
- ✅ Initial release
- ✅ 4 theme system
- ✅ Server status API
- ✅ Multi-language support
- ✅ Premium animations
- ✅ Complete documentation

---

**© 2025 Meta Scripts - Premium FiveM Loading Screen**
**Thank you for choosing our loading screen! 🚀**
