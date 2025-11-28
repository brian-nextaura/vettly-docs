# Component Overview

Vettly provides production-ready React components that protect your community from harmful content - before users ever see it.

## Available Components

### ModeratedTextarea

Real-time protection as users type.

```tsx
import { ModeratedTextarea } from '@nextauralabs/vettly-react'

<ModeratedTextarea
  apiKey="your-key"
  placeholder="Type a comment..."
  policyId="moderate"
/>
```

**Features:**
- ✅ Blocks harmful content as users type
- ✅ Visual feedback (color-coded borders)
- ✅ Clear status messages
- ✅ Prevents unsafe content submission
- ✅ Fully accessible

[View Details →](/components/textarea)

---

### ModeratedImageUpload

Protected image uploads with drag-and-drop.

```tsx
import { ModeratedImageUpload } from '@nextauralabs/vettly-react'

<ModeratedImageUpload
  apiKey="your-key"
  onUpload={(file, result) => {
    if (result.safe) {
      // Safe to show your community
    }
  }}
/>
```

**Features:**
- ✅ Drag & drop support
- ✅ Image preview
- ✅ Automatic protection on upload
- ✅ File validation
- ✅ Progress indicator

[View Details →](/components/image-upload)

---

### ModeratedVideoUpload

Protected video uploads with frame-by-frame analysis.

```tsx
import { ModeratedVideoUpload } from '@nextauralabs/vettly-react'

<ModeratedVideoUpload
  apiKey="your-key"
  maxDuration={60}
  extractFrames={5}
/>
```

**Features:**
- ✅ Video preview with thumbnail
- ✅ Frame-by-frame protection
- ✅ Progress tracking
- ✅ Per-frame analysis
- ✅ Comprehensive feedback

[View Details →](/components/video-upload)

---

### useModeration Hook

Build your own protected UI.

```tsx
import { useModeration } from '@nextauralabs/vettly-react'

const { check, result, loading } = useModeration({
  apiKey: 'your-key'
})

// Check any content
await check({
  content: 'User text',
  policyId: 'moderate'
})

if (result.action === 'block') {
  // Harmful content blocked - your users never see it
}
```

**Features:**
- ✅ Full control over UI
- ✅ Loading states
- ✅ Error handling
- ✅ TypeScript types

[View Details →](/components/use-moderation)

---

## Common Props

All components share these common props:

```typescript
interface CommonProps {
  // Required
  apiKey: string

  // Optional
  policyId?: 'strict' | 'moderate' | 'permissive'
  baseUrl?: string
  debounceMs?: number
  blockUnsafe?: boolean

  // Callbacks
  onModerationResult?: (result: ModerationResult) => void
  onError?: (error: Error) => void
}
```

## Protection Levels

| Policy | Use Case | Protection Level |
|--------|----------|------------------|
| `strict` | Schools, kids apps, enterprise | Maximum protection |
| `moderate` | Social apps, forums, comments | Balanced |
| `permissive` | Gaming, creative writing | Fewer restrictions |

## Styling

### Default Styles

Import the default stylesheet:

```tsx
import '@nextauralabs/vettly-react/styles.css'
```

### Custom Styles

Override CSS variables:

```css
:root {
  --vettly-safe-color: #22c55e;
  --vettly-warning-color: #eab308;
  --vettly-unsafe-color: #ef4444;
  --vettly-border-width: 2px;
  --vettly-transition: all 0.2s ease;
}
```

Or use custom class names:

```tsx
<ModeratedTextarea
  className="my-custom-textarea"
  apiKey="your-key"
/>
```

## TypeScript Support

All components are fully typed:

```typescript
import type {
  ModeratedTextareaProps,
  ModeratedImageUploadProps,
  ModeratedVideoUploadProps,
  ModerationResult,
  ModerationStatus
} from '@nextauralabs/vettly-react'
```

## Next Steps

Explore each component in detail:

- [ModeratedTextarea →](/components/textarea)
- [ModeratedImageUpload →](/components/image-upload)
- [ModeratedVideoUpload →](/components/video-upload)
- [useModeration Hook →](/components/use-moderation)
