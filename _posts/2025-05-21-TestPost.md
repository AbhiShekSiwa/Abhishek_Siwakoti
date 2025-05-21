---
layout: post
title: Aerospace Projects Portfolio
subtitle: From rocket simulations to space robotics
tags: [projects, aerospace, portfolio]
author: Abhishek Siwakoti
---

Welcome to my aerospace projects portfolio! Each section showcases a different project I’ve worked on, with interactive image galleries to show progress, results, and final implementations.

---

## 🚀 Rocket Nozzle Optimization

I designed and simulated a bell-shaped rocket nozzle to optimize exhaust expansion using MATLAB and ANSYS.

<div class="carousel" id="carousel-1">
  <button class="carousel-btn prev" onclick="plusSlides(-1, 0)">&#10094;</button>
  <div class="carousel-images">
    <img src="/assets/img/rocketimg1.png" class="carousel-image active" alt="Rocket simulation 1">
    <img src="/assets/img/rocketimg2.png" class="carousel-image" alt="Rocket simulation 2">
    <img src="/assets/img/rocketimg3.png" class="carousel-image" alt="Rocket simulation 3">
  </div>
  <button class="carousel-btn next" onclick="plusSlides(1, 0)">&#10095;</button>
</div>

---

## 🛰️ Satellite Attitude Control

Built a 3-axis stabilized CubeSat simulator with reaction wheels and PID controllers in Simulink.

<div class="carousel" id="carousel-2">
  <button class="carousel-btn prev" onclick="plusSlides(-1, 1)">&#10094;</button>
  <div class="carousel-images">
    <img src="/assets/img/satimg1.gif" class="carousel-image active" alt="CubeSat sim 1">
    <img src="/assets/img/satimg2.gif" class="carousel-image" alt="CubeSat sim 2">
  </div>
  <button class="carousel-btn next" onclick="plusSlides(1, 1)">&#10095;</button>
</div>

---

## 🛫 Supersonic Wind Tunnel Data Analysis

Analyzed Mach flow behavior and shock formation through supersonic nozzles using Python and data from CFD labs.

<div class="carousel" id="carousel-3">
  <button class="carousel-btn prev" onclick="plusSlides(-1, 2)">&#10094;</button>
  <div class="carousel-images">
    <img src="/assets/img/windimg1.jpg" class="carousel-image active" alt="Wind tunnel plot 1">
    <img src="/assets/img/windimg2.jpg" class="carousel-image" alt="Wind tunnel plot 2">
  </div>
  <button class="carousel-btn next" onclick="plusSlides(1, 2)">&#10095;</button>
</div>

---

### Want to collaborate or learn more? [Contact me!](/my-email)
{: .box-note}

---

## Carousel Script + Styles

Add this block below your post content or into `_includes/scripts.html` for reuse:

```html
<style>
.carousel {
  position: relative;
  max-width: 700px;
  margin: auto;
  margin-top: 1em;
}
.carousel-images {
  position: relative;
  overflow: hidden;
}
.carousel-image {
  display: none;
  width: 100%;
  border-radius: 10px;
}
.carousel-image.active {
  display: block;
}
.carousel-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background-color: rgba(0,0,0,0.4);
  color: white;
  border: none;
  font-size: 2em;
  cursor: pointer;
  padding: 0 12px;
  z-index: 1;
}
.carousel-btn.prev { left: 0; }
.carousel-btn.next { right: 0; }
</style>

<script>
let slideIndices = [1, 1, 1]; // One per carousel

function plusSlides(n, carouselIndex) {
  showSlides(slideIndices[carouselIndex] += n, carouselIndex);
}

function showSlides(n, carouselIndex) {
  const carousels = document.querySelectorAll('.carousel');
  const images = carousels[carouselIndex].querySelectorAll('.carousel-image');

  if (n > images.length) slideIndices[carouselIndex] = 1;
  if (n < 1) slideIndices[carouselIndex] = images.length;

  images.forEach(img => img.classList.remove('active'));
  images[slideIndices[carouselIndex] - 1].classList.add('active');
}

document.addEventListener("DOMContentLoaded", () => {
  for (let i = 0; i < slideIndices.length; i++) {
    showSlides(slideIndices[i], i);
  }
});
</script>
