---
layout: page
title: My Email!
subtitle: You can send me a message!
---

<style>
  body {
    background: linear-gradient(135deg, #7F00FF, #3f51b5);
    color: white;
    font-family: 'Segoe UI', sans-serif;
  }

  .contact-section {
    max-width: 600px;
    margin: 3rem auto;
    padding: 2rem;
    background-color: rgba(255, 255, 255, 0.1);
    border-radius: 12px;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
  }

  .contact-section h2 {
    text-align: center;
    font-size: 2em;
    margin-bottom: 0.25em;
    color: #ffffff;
  }

  .contact-section p {
    text-align: center;
    font-size: 1em;
    color: #dddddd;
    margin-bottom: 2em;
  }

  .contact-section form {
    display: flex;
    flex-direction: column;
    gap: 1em;
  }

  .contact-section input,
  .contact-section textarea {
    padding: 0.75em;
    border: none;
    border-radius: 8px;
    font-size: 1em;
    font-family: inherit;
    background: rgba(255, 255, 255, 0.2);
    color: white;
  }

  .contact-section input::placeholder,
  .contact-section textarea::placeholder {
    color: #eeeeee;
  }

  .contact-section button {
    padding: 0.75em;
    font-size: 1em;
    background-color: #ffffff;
    color: #7F00FF;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    transition: background-color 0.3s ease;
    font-weight: bold;
  }

  .contact-section button:hover {
    background-color: #f0f0f0;
  }

  #form-message {
    text-align: center;
    font-size: 1em;
    color: #a0ffcc;
    margin-top: 1em;
  }
</style>


<section id="contact" class="contact-section">
  <h2>Contact Me</h2>
  <p>All messages go straight to my personal inbox :-)</p>

  <form id="contact-form">
    <input type="text" name="from_name" placeholder="Your Name" required>
    <input type="email" name="from_email" placeholder="Your Email" required>
    <textarea name="message" placeholder="Your Message..." rows="6" required></textarea>
    <button type="submit">Send Message</button>
    <p id="form-message"></p>
  </form>
</section>

<script src="https://cdn.jsdelivr.net/npm/emailjs-com@3/dist/email.min.js"></script>
<script>
  (function() {
    emailjs.init("-PyNu_EXAs9e_mwF5"); // Replace with your public key
  })();

  document.getElementById('contact-form').addEventListener('submit', function(e) {
    e.preventDefault();

    emailjs.sendForm('service_ow1h2de', 'template_anxr1ib', this)
      .then(function() {
        document.getElementById("form-message").innerText = "Your message has been sent. Thank you!";
        document.getElementById("contact-form").reset();
      }, function(error) {
        document.getElementById("form-message").innerText = "Something went wrong. Please try again.";
        console.error(error);
      });
  });
</script>
