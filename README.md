<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>AI CV Generator</title>
  <style>
    body { font-family: Arial, sans-serif; padding: 20px; max-width: 600px; margin: auto; }
    input, textarea, button { width: 100%; margin: 10px 0; padding: 8px; }
    button { background-color: green; color: white; border: none; cursor: pointer; }
    pre { background: #f0f0f0; padding: 10px; white-space: pre-wrap; }
  </style>
</head>
<body>
  <h2>AI CV Generator (KES 100)</h2>
  <input type="text" id="name" placeholder="Full Name" />
  <input type="text" id="email" placeholder="Email" />
  <input type="text" id="phone" placeholder="Phone Number" />
  <textarea id="objective" placeholder="Career Objective"></textarea>
  <textarea id="education" placeholder="Education"></textarea>
  <textarea id="experience" placeholder="Experience"></textarea>
  <textarea id="skills" placeholder="Skills"></textarea>
  <input type="text" id="jobType" placeholder="Target Job Type" />
  <button onclick="payAndGenerateCV()">Pay with M-Pesa & Generate CV</button>
  <div id="output" style="margin-top: 20px;"></div>
  <script>
    async function payAndGenerateCV() {
      const data = {
        name: document.getElementById('name').value,
        email: document.getElementById('email').value,
        phone: document.getElementById('phone').value,
        objective: document.getElementById('objective').value,
        education: document.getElementById('education').value,
        experience: document.getElementById('experience').value,
        skills: document.getElementById('skills').value,
        jobType: document.getElementById('jobType').value
      };

      const res = await fetch('/api/pay', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(data)
      });

      const result = await res.json();

      if (result.success) {
        document.getElementById('output').innerHTML = `<pre>${result.cv}</pre>`;
      } else {
        alert("Payment failed: " + result.message);
      }
    }
  </script>
</body>
</html>
