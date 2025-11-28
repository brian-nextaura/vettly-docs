---
layout: home

hero:
  name: Vettly
  text: Protect Your Users
  tagline: AI-powered content moderation that blocks harmful content before it reaches your community
  actions:
    - theme: brand
      text: Start Protecting
      link: /guide/getting-started
    - theme: alt
      text: Try Components
      link: /components/overview

features:
  - icon: 🛡️
    title: Real-Time Protection
    details: Block harmful content before your users see it - with instant feedback as they type

  - icon: 🎨
    title: Built-in Safety
    details: Drop-in React components that protect your community out of the box

  - icon: 🎬
    title: Multi-Modal Coverage
    details: Protect text, images, and videos - all checked before users see them

  - icon: ⚡
    title: Type-Safe SDK
    details: Full TypeScript support with comprehensive type definitions

  - icon: 🎯
    title: Flexible Policies
    details: Strict, moderate, or permissive - you decide what level of protection fits your platform

  - icon: 🚀
    title: Framework Integrations
    details: Works with React, Next.js, Express, Python, and more - in minutes, not months
---

## Quick Start

### Install

::: code-group

```bash [npm]
npm install @nextauralabs/vettly-react
```

```bash [bun]
bun add @nextauralabs/vettly-react
```

```bash [yarn]
yarn add @nextauralabs/vettly-react
```

:::

### Protect Your Users

```tsx
import { ModeratedTextarea } from '@nextauralabs/vettly-react'
import '@nextauralabs/vettly-react/styles.css'

function App() {
  return (
    <ModeratedTextarea
      apiKey="your-api-key"
      placeholder="Type something..."
      onModerationResult={(result) => {
        if (result.action === 'block') {
          // Harmful content blocked - your users never see it
        }
      }}
    />
  )
}
```

## Components

### ModeratedTextarea

Real-time protection with visual feedback:

- ✅ Blocks harmful content as users type
- ✅ Color-coded borders (green/yellow/red)
- ✅ Clear status messages
- ✅ Fully customizable

[View Component →](/components/textarea)

### ModeratedImageUpload

Protected image uploads:

- ✅ Drag & drop support
- ✅ Image preview
- ✅ Automatic protection on upload
- ✅ Visual feedback

[View Component →](/components/image-upload)

### ModeratedVideoUpload

Protected video uploads with frame analysis:

- ✅ Video preview with thumbnail
- ✅ Frame-by-frame protection
- ✅ Progress tracking
- ✅ Comprehensive error handling

[View Component →](/components/video-upload)

## Why Vettly?

**Trust takes time to earn. Toxic content destroys it instantly.**

Your users remember how they feel. One toxic comment, one harmful image, one bad experience - and they're gone. Vettly stops harmful content before it reaches your community.

| Feature | Vettly | Others |
|---------|--------|--------|
| **Multi-Modal Protection** | ✅ Text, Images, Videos | ⚠️ Usually text-only |
| **React Components** | ✅ Production-ready | ❌ Build your own |
| **Video Frame Analysis** | ✅ Advanced | ❌ Not available |
| **TypeScript** | ✅ Full support | ⚠️ Partial |
| **Real-time Feedback** | ✅ Built-in | ❌ Manual |
| **Framework Integrations** | ✅ React, Next.js, Express, Python | ❌ SDK only |

## Pricing

Peace of mind, starting free:

- **Text Protection**: FREE (OpenAI + Perspective)
- **Image Protection**: $0.0003 per image (~$3 per 10K)
- **Video Protection**: $0.001 per video (~$1 per 1K)

[View Full Pricing →](https://vettly.dev/pricing)

## Examples

See protection in action:

- [Social Feed](/examples/social-feed) - Social media with content protection
- [Forum](/examples/forum) - Discussion board with community safety
- [Chat App](/examples/chat) - Real-time chat that keeps users safe
