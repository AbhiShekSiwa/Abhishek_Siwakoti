---
layout: page
title: My Resume
permalink: /resume/
---

<style>
.resume-buttons {
  text-align: center;
  margin-bottom: 1.5em;
}
.resume-buttons button {
  margin: 0 10px;
  padding: 10px 20px;
  font-size: 1em;
  border: none;
  background-color: #007acc;
  color: white;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.2s ease;
}
.resume-buttons button:hover {
  background-color: #005fa3;
}
#resume-canvas {
  border: 1px solid #ccc;
  display: block;
  margin: auto;
  max-width: 100%;
}
.resume-nav {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 1rem;
  margin-top: 1rem;
}
.resume-nav button {
  padding: 8px 16px;
  font-size: 1em;
  border: none;
  background-color: #444;
  color: white;
  border-radius: 5px;
  cursor: pointer;
}
</style>

<h2 style="text-align:center;">My Resume</h2>
<p style="text-align:center;">Select which version you'd like to view:</p>

<div class="resume-buttons">
  <button onclick="loadResume('short')">View Shortened Resume</button>
  <button onclick="loadResume('full')">View Full Resume</button>
</div>

<div class="resume-nav" id="nav-buttons" style="display: none;">
  <button onclick="prevPage()">⬅ Prev</button>
  <span>Page <span id="page-num">1</span> of <span id="page-count">?</span></span>
  <button onclick="nextPage()">Next ➡</button>
</div>

<div style="display: flex; justify-content: center; margin-bottom: 2em;">
  <canvas id="resume-canvas"></canvas>
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.4.120/pdf.min.js"></script>
<script>
  const canvas = document.getElementById('resume-canvas');
  const ctx = canvas.getContext('2d');
  let pdfDoc = null;
  let currentPage = 1;
  let rendering = false;
  let pendingPage = null;
  let totalPages = 1;
  let currentType = 'short'; // 'short' or 'full'

  const scale = 1.5;
  const resumePaths = {
    short: '/assets/pdfs/Abhishek_Siwakoti_Resume_Short.pdf',
    full: '/assets/pdfs/Abhishek_Siwakoti_Resume_Full.pdf'
  };

  pdfjsLib.GlobalWorkerOptions.workerSrc = 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.4.120/pdf.worker.min.js';

  function renderPage(num) {
    rendering = true;
    pdfDoc.getPage(num).then(page => {
      const viewport = page.getViewport({ scale });
      canvas.height = viewport.height;
      canvas.width = viewport.width;

      const renderContext = { canvasContext: ctx, viewport: viewport };
      page.render(renderContext).promise.then(() => {
        rendering = false;
        if (pendingPage !== null) {
          renderPage(pendingPage);
          pendingPage = null;
        }
      });

      document.getElementById('page-num').textContent = num;
    });
  }

  function queueRenderPage(num) {
    if (rendering) {
      pendingPage = num;
    } else {
      renderPage(num);
    }
  }

  function prevPage() {
    if (currentPage <= 1) return;
    currentPage--;
    queueRenderPage(currentPage);
  }

  function nextPage() {
    if (currentPage >= totalPages) return;
    currentPage++;
    queueRenderPage(currentPage);
  }

  function loadResume(type) {
    currentType = type;
    currentPage = 1;

    pdfjsLib.getDocument(resumePaths[type]).promise.then(pdf => {
      pdfDoc = pdf;
      totalPages = pdf.numPages;
      renderPage(currentPage);

      const nav = document.getElementById('nav-buttons');
      if (type === 'full' && totalPages > 1) {
        nav.style.display = 'flex';
        document.getElementById('page-count').textContent = totalPages;
      } else {
        nav.style.display = 'none';
      }
    });
  }

  // Auto-load shortened resume on page load
  document.addEventListener("DOMContentLoaded", () => {
    loadResume('short');
  });
</script>
