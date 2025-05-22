---
layout: page
title: My Resume
permalink: /resume/
---

<style>
.resume-buttons {
  text-align: center;
  margin: 1.5em 0 1em;
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
#download-link-wrapper button {
  background-color: #28a745;
}
#download-link-wrapper button:hover {
  background-color: #1e7e34;
}
.resume-container {
  position: relative;
  max-width: 850px;
  margin: auto;
}
#resume-canvas {
  border: 1px solid #ccc;
  display: block;
  max-width: 100%;
  height: auto;
  margin: auto;
}
.side-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background-color: rgba(0, 0, 0, 0.5);
  border: none;
  color: white;
  font-size: 1.5rem;
  padding: 10px 15px;
  cursor: pointer;
  z-index: 2;
  border-radius: 5px;
  transition: background-color 0.2s ease;
}
.side-btn:hover {
  background-color: rgba(0, 0, 0, 0.7);
}
.side-btn.left {
  left: 0;
}
.side-btn.right {
  right: 0;
}
</style>

<h2 style="text-align:center;">My Resume</h2>
<p style="text-align:center;">Select which version you'd like to view:</p>

<div class="resume-buttons">
  <button onclick="loadResume('short')">View Shortened Resume</button>
  <button onclick="loadResume('full')">View Full Resume</button>
</div>

<!-- Canvas and Navigation Arrows -->
<div class="resume-container" id="resume-wrapper">
  <button class="side-btn left" id="prev-btn" onclick="prevPage()" style="display: none;">&#10094;</button>
  <canvas id="resume-canvas"></canvas>
  <button class="side-btn right" id="next-btn" onclick="nextPage()" style="display: none;">&#10095;</button>
</div>

<!-- Download Button -->
<div class="resume-buttons" id="download-link-wrapper" style="text-align: center;">
  <a id="download-link" href="/assets/pdfs/Abhishek_Siwakoti_Resume_Short.pdf" download target="_blank">
    <button>📥 Download PDF</button>
  </a>
</div>

<!-- PDF.js + Custom Script -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.4.120/pdf.min.js"></script>
<script>
  const canvas = document.getElementById('resume-canvas');
  const ctx = canvas.getContext('2d');
  let pdfDoc = null;
  let currentPage = 1;
  let totalPages = 1;
  let rendering = false;
  let pendingPage = null;
  let currentType = 'short';

  const scale = 1.5;
  const resumePaths = {
    short: '/assets/pdfs/Abhishek_Siwakoti_Resume_Short.pdf',
    full: '/assets/pdfs/Abhishek_Siwakoti_Resume_Full.pdf'
  };

  const prevBtn = document.getElementById('prev-btn');
  const nextBtn = document.getElementById('next-btn');
  const downloadLink = document.getElementById('download-link');

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

      // Update navigation buttons
      if (currentType === 'full') {
        prevBtn.style.display = num > 1 ? 'block' : 'none';
        nextBtn.style.display = num < totalPages ? 'block' : 'none';
      }
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

      // Show nav only for full resume
      if (type === 'full' && totalPages > 1) {
        prevBtn.style.display = 'none';
        nextBtn.style.display = 'block';
      } else {
        prevBtn.style.display = 'none';
        nextBtn.style.display = 'none';
      }

      // Update download link
      downloadLink.href = resumePaths[type];
    });
  }

  // Load short version by default
  document.addEventListener("DOMContentLoaded", () => {
    loadResume('short');
  });
</script>
