---
layout: post
title: "Building the Interactive Scroll Wheel"
subtitle: How I experimented with horizontal scrolling and created something slick
date: 2025-05-24
tags: [webdev, design, personal]
---

A while back, I wanted to create something eye-catching on my personal website — something that felt modern and interactive.

I knew I wanted to add **horizontal scrolling** below the hero section — a smooth, timeline-like layout that users would encounter *after* they started scrolling down.

---

## 🛠️ What I Tried First

I experimented with a few options:

1. **Basic HTML horizontal scroll** with `overflow-x: scroll`
   → This worked, but looked boring and static.

2. **CSS snap scrolling**
   → This created a nice "section snap" effect — better, but still felt clunky on touchpads.

3. **JavaScript-powered smooth scroll on mousewheel/touch**
   → This gave me real control over the scroll behavior and animations.

---

## 🧪 The Final Setup I Chose

Here's what I ended up doing:

- I created a `#timeline-wrapper` section with horizontal `overflow-x` and disabled `overflow-y`
- Used `scroll-snap-type: x mandatory` for segment locking
- Styled `.timeline-item` blocks as 300px cards spaced apart
- Added `scroll-behavior: smooth` and `::-webkit-scrollbar { display: none; }` to make it feel like a native app

This allowed me to preserve vertical scroll elsewhere while giving a slick sideways carousel feel!

---

## 💡 What I Could Improve Later

If I revisit this feature, I might:

- Add **drag-to-scroll** support for better UX on mobile
- Use a library like [Locomotive Scroll](https://locomotivemtl.github.io/locomotive-scroll/) or [GSAP ScrollTrigger](https://greensock.com/scrolltrigger/) for buttery animations
- Make the scroll-triggered timeline **auto-start** on page load, then pause on hover

---

## 🚀 Final Thoughts

This was one of my favorite features to build — and even though it seems small, it added a lot of personality to my site. Sometimes, it's the small motion that makes a static portfolio feel *alive*.

If you want to try it too, just start small and tweak until it feels right.

Happy scrolling! 🌀
