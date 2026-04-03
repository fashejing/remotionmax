---
name: remotionmax
description: >
  Create Remotion animations, open in editor, and start preview in one command.
  Use when user wants to create animated videos with Remotion, open the project in VS Code or Cursor,
  and start the live preview server.
  Triggers on: create animation, remotion preview, open video editor, start remotion, animation studio.
---

# RemotionMAX - Animation Studio in One Click

Create stunning Remotion animations, open in your favorite editor, and preview in real-time.

## What is RemotionMAX?

RemotionMAX combines three steps into one:
1. **Create** - Generate animation code based on your theme
2. **Open** - Launch in VS Code or Cursor
3. **Preview** - Start live preview server

## Usage

### Interactive Mode (Recommended)

Simply trigger the skill:
```bash
remotionmax
```

The skill will ask for:
1. **Animation theme** - What kind of animation do you want?
2. **Project name** - Name your project
3. **Editor choice** - VS Code or Cursor
4. **Project location** - Defaults to `/Users/fsj/Documents/emowowo remotion`

### Command Line Mode

```bash
# Auto mode with defaults
bash ~/.agents/skills/remotionmax/scripts/launch.sh --auto

# With all options
bash ~/.agents/skills/remotionmax/scripts/launch.sh \
  --theme "neon cyberpunk logo" \
  --name "cyberpunk-animation" \
  --editor "cursor"
```

## Animation Themes

When you describe your animation theme, RemotionMAX can create:

| Theme Type | Examples |
|:---|:---|
| **Logo Animations** | Neon glow, pixel morph, rainbow glitch |
| **Text Effects** | Wave text, holographic, color wave |
| **Particles** | Fireworks, floating orbs, star field |
| **Abstract** | Geometric shapes, morphing blobs |
| **Retro** | 8-bit pixel art, arcade style |
| **Futuristic** | Cyberpunk, holographic, sci-fi HUD |

## Animation Code Examples

### Neon Glow Logo
```tsx
import { useCurrentFrame, interpolate, spring } from 'remotion';

export const NeonLogo: React.FC = () => {
  const frame = useCurrentFrame();
  const scale = spring({ frame, fps: 30, config: { damping: 10 } });

  return (
    <div style={{ backgroundColor: '#0a0a0f', flex: 1, justifyContent: 'center', alignItems: 'center' }}>
      <div style={{
        fontSize: 120,
        color: '#ff00ff',
        textShadow: '0 0 20px #ff00ff, 0 0 40px #ff00ff, 0 0 60px #ff00ff',
        transform: `scale(${scale})`,
      }}>
        EMOWOWO
      </div>
    </div>
  );
};
```

### Rainbow Glitch Effect
```tsx
import { useCurrentFrame, interpolate } from 'remotion';

export const RainbowGlitch: React.FC = () => {
  const frame = useCurrentFrame();
  const glitchX = interpolate(frame, [0, 10, 20], [0, -10, 0]);

  return (
    <div style={{ backgroundColor: '#000', flex: 1 }}>
      <div style={{ transform: `translateX(${glitchX}px)` }}>
        {/* Pixel art logo here */}
      </div>
    </div>
  );
};
```

### Particle System
```tsx
export const Particles: React.FC = () => {
  const frame = useCurrentFrame();

  return (
    <div style={{ backgroundColor: '#0f0f1a', flex: 1, position: 'relative' }}>
      {Array.from({ length: 50 }).map((_, i) => {
        const x = (i * 137 + frame * 2) % 1920;
        const y = 540 + Math.sin(frame * 0.05 + i) * 300;
        return (
          <div key={i} style={{
            position: 'absolute',
            left: x,
            top: y,
            width: 8,
            height: 8,
            borderRadius: '50%',
            backgroundColor: ['#ff0080', '#00ff80', '#8000ff'][i % 3],
            boxShadow: '0 0 10px currentColor',
          }} />
        );
      })}
    </div>
  );
};
```

## Core Remotion APIs

For complete API reference, see [references/remotion-api.md](references/remotion-api.md).

### useCurrentFrame()
Get current frame number (0-indexed):
```tsx
const frame = useCurrentFrame();
```

### interpolate()
Map values between ranges with easing:
```tsx
const opacity = interpolate(frame, [0, 30], [0, 1]);
const x = interpolate(frame, [0, 100], [0, 500], {
  extrapolateLeft: 'clamp',
  extrapolateRight: 'clamp',
  easing: Easing.bezier(0.4, 0, 0.2, 1),
});
```

### spring()
Physics-based animation:
```tsx
const scale = spring({
  fps,
  frame,
  config: { damping: 10, mass: 1, stiffness: 100 },
  delay: 10,
});
```

### Easing Functions
```tsx
Easing.linear
Easing.ease
Easing.in(Easing.ease)
Easing.out(Easing.ease)
Easing.inOut(Easing.ease)
Easing.bounce
Easing.elastic(1)
Easing.back(0.5)
```

## Workflow

```
1. You describe your animation theme
       ↓
2. RemotionMAX generates animation code options
       ↓
3. You select your preferred animation
       ↓
4. Project is created with remotion-build
       ↓
5. Animation code is written to the project
       ↓
6. You choose editor (VS Code or Cursor)
       ↓
7. Editor opens with the project
       ↓
8. Preview server starts automatically
       ↓
9. Open the preview URL to see your animation!
```

## After Launch

### Preview
- Open http://localhost:3456 (or the port shown)
- See your animation in real-time
- Edit code and watch changes instantly

### Render
```bash
# Render as MP4
npx remotion render MyVideo out/video.mp4

# Render as GIF
npx remotion render MyVideo out/anim.gif --codec=gif

# Render single frame
npx remotion still MyVideo out/frame.png --frame=30
```

## Project Structure

```
{project-name}/
├── src/
│   ├── index.tsx          # Root with registerRoot()
│   └── {AnimationName}.tsx  # Your animation
├── public/
├── package.json
├── tsconfig.json
└── node_modules/
```

## Tips

- **Real-time preview** - Changes to code update instantly in the browser
- **Composition selector** - Click the Remotion Studio logo to switch between compositions
- **Frame-by-frame** - Use the timeline to scrub through frames
- **Export** - When happy, render to MP4 or GIF

## Resources

- [Remotion Docs](https://www.remotion.dev/docs)
- [Timing Functions](https://www.remotion.dev/docs/interpolate)
- [Spring Animation](https://www.remotion.dev/docs/spring)
- [Easing Functions](https://easings.net/)