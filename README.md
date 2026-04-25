<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Certificate Upload</title>
  <style>
    * {
      box-sizing: border-box;
      font-family: Arial, sans-serif;
    }

    body {
      margin: 0;
      min-height: 100vh;
      background: linear-gradient(135deg, #e8f0ff, #ffffff);
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 20px;
    }

    .container {
      width: 100%;
      max-width: 750px;
      background: white;
      border-radius: 20px;
      padding: 30px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.12);
    }

    h1 {
      text-align: center;
      color: #1d3557;
      margin-bottom: 10px;
    }

    .subtitle {
      text-align: center;
      color: #555;
      margin-bottom: 30px;
    }

    .upload-box {
      border: 2px dashed #457b9d;
      border-radius: 16px;
      padding: 30px;
      text-align: center;
      background: #f8fbff;
    }

    input[type="file"] {
      margin-top: 15px;
    }

    .btn {
      margin-top: 20px;
      background: #1d3557;
      color: white;
      border: none;
      padding: 12px 25px;
      border-radius: 10px;
      cursor: pointer;
      font-size: 16px;
    }

    .btn:hover {
      background: #457b9d;
    }

    .preview {
      margin-top: 30px;
      display: none;
    }

    .preview h2 {
      color: #1d3557;
      font-size: 22px;
    }

    img, iframe {
      width: 100%;
      max-height: 500px;
      border-radius: 12px;
      border: 1px solid #ddd;
      margin-top: 15px;
    }

    .file-name {
      margin-top: 12px;
      color: #333;
      font-weight: bold;
    }

    .note {
      margin-top: 20px;
      background: #fff3cd;
      padding: 12px;
      border-radius: 10px;
      color: #664d03;
      font-size: 14px;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Certificate Upload Website</h1>
    <p class="subtitle">Upload your certificate image or PDF and preview it here.</p>

    <div class="upload-box">
      <h2>Upload Certificate</h2>
      <p>Select JPG, PNG, or PDF file</p>
      <input type="file" id="certificateInput" accept="image/*,.pdf" />
      <br />
      <button class="btn" onclick="previewCertificate()">Upload & Preview</button>
    </div>

    <div class="preview" id="previewArea">
      <h2>Uploaded Certificate</h2>
      <p class="file-name" id="fileName"></p>
      <div id="filePreview"></div>
    </div>

    <div class="note">
      Note: This demo only previews the file on your device. To save certificates online, you need hosting and a database/server.
    </div>
  </div>

  <script>
    function previewCertificate() {
      const input = document.getElementById('certificateInput');
      const previewArea = document.getElementById('previewArea');
      const filePreview = document.getElementById('filePreview');
      const fileName = document.getElementById('fileName');

      if (!input.files || input.files.length === 0) {
        alert('Please select a certificate first.');
        return;
      }

      const file = input.files[0];
      const fileURL = URL.createObjectURL(file);

      fileName.textContent = 'File name: ' + file.name;
      filePreview.innerHTML = '';

      if (file.type.startsWith('image/')) {
        const img = document.createElement('img');
        img.src = fileURL;
        img.alt = 'Certificate Preview';
        filePreview.appendChild(img);
      } else if (file.type === 'application/pdf') {
        const iframe = document.createElement('iframe');
        iframe.src = fileURL;
        iframe.height = '500';
        filePreview.appendChild(iframe);
      } else {
        filePreview.innerHTML = '<p>This file type cannot be previewed.</p>';
      }

      previewArea.style.display = 'block';
    }
  </script>
</body>
</html>
