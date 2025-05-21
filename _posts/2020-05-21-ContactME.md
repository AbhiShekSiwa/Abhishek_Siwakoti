---
layout: post
title: My Email! 
subtitle: You can send me a message!  
tags: [contact]
---

<style>
  .contact-section {
    max-width: 600px;
    margin: 2em auto;
    padding: 2em;
    background-color: #f9f9f9;
    border-radius: 12px;
    box-shadow: 0 4px 12px rgba(0,0,0,0.05);
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  }

  .contact-section h2 {
    text-align: center;
    font-size: 2em;
    margin-bottom: 0.25em;
  }

  .contact-section p {
    text-align: center;
    font-size: 1em;
    color: #666;
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
    border: 1px solid #ccc;
    border-radius: 8px;
    font-size: 1em;
    font-family: inherit;
    transition: border 0.2s ease;
  }

  .contact-section input:focus,
  .contact-section textarea:focus {
    border-color: #007bff;
    outline: none;
  }

  .contact-section button {
    padding: 0.75em;
    font-size: 1em;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }

  .contact-section button:hover {
    background-color: #0056b3;
  }

  #form-message {
    text-align: center;
    font-size: 1em;
    color: #28a745;
    margin-top: 1em;
  }

  @media (max-width: 600px) {
    .contact-section {
      padding: 1.5em;
    }
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
    emailjs.init("-PyNu_EXAs9e_mwF5"); // Your correct public key
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
