# Middle Earth Interactive Map

## Project Overview
An interactive, mobile-friendly map of Middle Earth built with vanilla HTML, CSS, and JavaScript. Features pan/zoom navigation, clickable location markers with lore descriptions, and a search function.

## File Structure
```
├── index.html          # Main application (single-file, self-contained)
├── map.png             # 8K Middle Earth map image by Kerem Yurtseven
├── start-server.command # Mac launcher script for local development
└── CLAUDE.md           # This file
```

## Running Locally
The app requires a local server due to browser CORS restrictions on file:// URLs.

```bash
# Option 1: Python
python3 -m http.server 8000

# Option 2: Node.js
npx serve .

# Option 3: Mac - double-click start-server.command
```

Then open http://localhost:8000

## Technical Details

### Architecture
- **Single HTML file** with embedded CSS and JavaScript (no build step required)
- **Vanilla JS** - no frameworks or dependencies
- **CSS custom properties** for theming
- **Touch-first design** with mouse support

### Key Features
- Pan: Click/touch drag
- Zoom: Mouse wheel, pinch gesture, or +/- buttons
- Search: Filter locations by name
- Info panel: Tap markers to view location lore
- Responsive: Adapts layout for mobile vs desktop

### Coordinate System
Location markers use percentage-based coordinates (0-100) relative to the map image dimensions:
```javascript
{
    id: 'shire',
    name: 'The Shire',
    subtitle: 'Homeland of the Hobbits',
    x: 18.5,  // percentage from left
    y: 32,    // percentage from top
    description: '...'
}
```

### Styling
- **Fonts**: Cinzel (headers), Crimson Text (body) via Google Fonts
- **Colors**: Parchment palette (--parchment, --ink, --gold variants)
- **Design language**: Medieval/fantasy aesthetic matching the map style

## Potential Enhancements
- [ ] Add journey paths (Fellowship route, Bilbo's journey, etc.)
- [ ] Category filters (cities, forests, mountains, fortresses)
- [ ] Different marker styles by location type
- [ ] Fog of war / progressive reveal mode
- [ ] Audio narration for locations
- [ ] Timeline slider showing different ages
- [ ] Save/share specific map views via URL params
- [ ] Offline PWA support with service worker
- [ ] Additional locations (currently 24 major sites)

## Development Notes

### Adding New Locations
Add entries to the `locations` array in index.html:
```javascript
{
    id: 'unique-id',
    name: 'Display Name',
    subtitle: 'Short descriptor',
    x: 50,  // percentage 0-100
    y: 50,  // percentage 0-100
    description: 'Full lore description...'
}
```

### Adjusting Marker Positions
Use browser dev tools to find coordinates:
1. Open the map and zoom to the location
2. In console: `scale`, `translateX`, `translateY` show current view state
3. Click the map and calculate: `x = (clickX - translateX) / scale / imageWidth * 100`

### Mobile Considerations
- Uses `100dvh` for proper mobile viewport handling
- Touch events handle single-finger pan and two-finger pinch zoom
- Info panel slides up from bottom on mobile, appears as sidebar on desktop
- `user-scalable=no` prevents double-tap zoom conflicts

## Attribution
Map artwork: "8K Middle Earth" by Kerem Yurtseven
