---
layout: inner
title: Business Card
permalink: /businesscard/
---

<div id="business-card" style="text-align: center;">
  <img src="/img/photo.jpg" alt="Laurenz Grote" style="width: 150px; height: 150px; border-radius: 50%; object-fit: cover; margin-bottom: 1em;">

  <h2 style="margin-bottom: 0.2em;">{{ site.admin_name }}</h2>
  <p style="color: #777;">{{ site.description }}</p>

  <p>
    <i class="fa fa-envelope"></i> <a id="card-email" href="mailto:{{ site.email }}">{{ site.email }}</a>
  </p>

  {% if site.linkedin_username != '' %}
  <p>
    <i class="fa fa-linkedin"></i> <a href="https://linkedin.com/in/{{ site.linkedin_username }}">LinkedIn</a>
  </p>
  {% endif %}

  {% if site.github_username != '' %}
  <p>
    <i class="fa fa-github"></i> <a href="https://github.com/{{ site.github_username }}">GitHub</a>
  </p>
  {% endif %}

  <hr>

  <h3>QR Code</h3>
  <p style="color: #777;">Scan to save contact</p>
  <div id="qrcode" style="display: inline-block;"></div>
</div>

<script src="/js/qrcode.js"></script>
<script>
(function() {
  var defaultEmail = "{{ site.email }}";
  var name = "{{ site.admin_name }}";
  var linkedin = "{{ site.linkedin_username }}";
  var github = "{{ site.github_username }}";
  var url = "{{ site.url }}";

  // Allow overriding email via query parameter
  var params = new URLSearchParams(window.location.search);
  var email = params.get("email") || defaultEmail;

  // Update displayed email
  var emailEl = document.getElementById("card-email");
  emailEl.textContent = email;
  emailEl.href = "mailto:" + email;

  // Build vCard
  var nameParts = name.split(" ");
  var lastName = nameParts.length > 1 ? nameParts.pop() : "";
  var firstName = nameParts.join(" ");

  var vcard = [
    "BEGIN:VCARD",
    "VERSION:3.0",
    "N:" + lastName + ";" + firstName + ";;;",
    "FN:" + name,
    "EMAIL:" + email,
    "URL:" + url
  ];
  if (linkedin) {
    vcard.push("X-SOCIALPROFILE;type=linkedin:https://linkedin.com/in/" + linkedin);
  }
  if (github) {
    vcard.push("X-SOCIALPROFILE;type=github:https://github.com/" + github);
  }
  vcard.push("END:VCARD");

  var vcardString = vcard.join("\n");

  // Generate QR code
  var qr = qrcode(0, "M");
  qr.addData(vcardString);
  qr.make();
  document.getElementById("qrcode").innerHTML = qr.createSvgTag({ cellSize: 4, margin: 4 });
})();
</script>
