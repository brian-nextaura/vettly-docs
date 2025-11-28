# What is Vettly?

**Trust takes time to earn. Toxic content destroys it instantly.**

Vettly is AI-powered content moderation that protects your users from harmful content - before they ever see it. Your users don't see what Vettly blocks. They just feel safe.

## The Problem

One bad experience can undo months of community building. One toxic comment can drive users away forever. Your users remember how they feel - and negativity sticks.

User-generated content can contain:

- 🚫 Hate speech and harassment
- 🚫 Spam and scams
- 🚫 NSFW/inappropriate images
- 🚫 Violence and graphic content
- 🚫 Personal information (PII)
- 🚫 Bot-generated spam

Manually moderating content doesn't scale, and building your own AI moderation system is complex and expensive.

## The Solution

Vettly protects your community with:

1. **Production-ready React components** that block harmful content in real-time
2. **TypeScript SDK** for custom protection implementations
3. **Multi-modal AI** that checks text, images, and videos before users see them
4. **Real-time feedback** so users know immediately when content crosses the line
5. **Framework integrations** for Next.js, Express, Python, and more

## How It Works

### 1. Simple Integration

```tsx
<ModeratedTextarea
  apiKey="your-key"
  placeholder="Type something..."
/>
```

### 2. Real-Time Protection

As users type, Vettly:
- Debounces API calls (configurable)
- Checks content against AI moderation
- Returns instant results

### 3. Visual Feedback

Components provide automatic feedback:
- 🟢 Green border = Safe for your community
- 🟡 Yellow border = Warning
- 🔴 Red border = Blocked

### 4. Take Action

```tsx
onModerationResult={(result) => {
  if (result.action === 'block') {
    // Harmful content blocked - your users never see it
  }
}}
```

## Multi-Modal Protection

### Text Protection

- Toxicity & hate speech
- Spam detection
- PII detection
- Bot activity

### Image Protection

- NSFW content
- Violence & gore
- Inappropriate imagery
- Visual spam

### Video Protection

- Frame-by-frame analysis
- Thumbnail generation
- Comprehensive scanning
- Progress tracking

## Key Features

### For Developers

- ✅ **TypeScript-first** - Full type safety
- ✅ **Zero config** - Works out of the box
- ✅ **Customizable** - Override any behavior
- ✅ **Framework agnostic** - Use anywhere
- ✅ **Minutes, not months** - Integrate quickly

### For Your Users

- ✅ **Real-time feedback** - Know immediately
- ✅ **Clear messaging** - Understand why
- ✅ **Fast responses** - Sub-second latency
- ✅ **Accessible** - WCAG compliant
- ✅ **Safe community** - They just feel safe

## Use Cases

### Social Platforms

Protect posts, comments, and messages in real-time.

```tsx
<ModeratedTextarea
  policyId="moderate"
  onModerationResult={handleComment}
/>
```

### Marketplaces

Check product listings for prohibited items.

```tsx
<ModeratedImageUpload
  policyId="strict"
  blockUnsafe
/>
```

### Forums & Communities

Keep discussions safe and on-topic.

```tsx
const client = new ModerationClient({ apiKey })
const result = await client.check({ content: post.body, policyId: 'moderate' })
```

### Dating Apps

Protect users from harassment and NSFW content.

```tsx
<ModeratedVideoUpload
  policyId="strict"
  maxDuration={30}
/>
```

## Pricing

Peace of mind, starting free:

- Text protection: FREE (unlimited)
- Image protection: $0.0003 per image
- Video protection: $0.001 per video

No monthly fees, no minimums, no surprises.

## Next Steps

Ready to protect your community?

- [Getting Started →](/guide/getting-started)
- [Browse Components →](/components/overview)
- [View Examples →](/examples/social-feed)
