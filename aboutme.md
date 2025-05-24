---
layout: page
title: About Me
subtitle: The Aerospace Dreamer Who Builds, Breaks, and Rebuilds
permalink: /aboutme/
---

<style>
  body {
    background: linear-gradient(135deg, #004d40, #00796b, #48a999);
    color: white;
    font-family: 'Segoe UI', sans-serif;
    padding: 6rem 2rem;
    max-width: 1000px;
    margin: auto;
    line-height: 1.8;
    font-size: 1.1rem;
  }

  .box-success {
    background: rgba(255, 255, 255, 0.15);
    padding: 1rem;
    border-radius: 8px;
    margin: 2rem 0;
  }

  .box-warning {
    background: rgba(255, 255, 255, 0.10);
    padding: 1rem;
    border-left: 5px solid #ffee58;
    border-radius: 4px;
    margin: 2rem 0;
  }

  table {
    width: 100%;
    border-collapse: collapse;
    margin: 1.5rem 0;
    background: rgba(255, 255, 255, 0.1);
  }

  th, td {
    padding: 0.85rem;
    border: 1px solid rgba(255, 255, 255, 0.3);
    text-align: left;
    color: white;
  }

  blockquote {
    background: rgba(0, 0, 0, 0.2);
    padding: 1rem 1.5rem;
    border-left: 4px solid #ffee58;
    border-radius: 6px;
    margin: 1.5rem 0;
    color: #f0f0f0;
    font-style: italic;
  }
</style>

Hey there — welcome to my digital corner of the universe. This page is where you get to learn a bit more about *who I am*, *what I care about*, and *why aerospace isn't just my major — it's my mission*.

{: .box-success}

...

{% raw %}
<script>
  const garmadonImg = document.getElementById('garmadon-img');
  let clickCount = 0;
  garmadonImg.addEventListener('click', () => {
    clickCount++;
    if (clickCount === 5) {
      garmadonImg.src = "/assets/img/Garmadon.JPG";
      garmadonImg.alt = "Sweet Garmadon";
    }
  });
</script>
{% endraw %}
