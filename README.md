# Plankton
Verified plant sacnner
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Plankton - Smart Plant Scanner</title>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    :root {
      --primary-green: #2e8b57;
      --light-green: #8fd694;
      --dark-green: #1a5f2b;
    }
    
    body {
      font-family: 'Poppins', sans-serif;
      margin: 0;
      padding: 0;
      background: linear-gradient(180deg, #f0f4f0 0%, #c8e6c9 100%);
      color: #333;
      position: relative;
      min-height: 100vh;
    }
    
    body::before {
      content: "";
      position: fixed;
      bottom: 0;
      left: 0;
      right: 0;
      height: 200px;
      background: url('https://placehold.co/1600x200/d1eddc/d1eddc') repeat-x;
      background-size: auto 200px;
      z-index: -1;
    }
    
    header {
      background-color: var(--primary-green);
      color: white;
      padding: 1.5rem 0;
      box-shadow: 0 4px 12px rgba(0,0,0,0.1);
    }
    
    .logo {
      font-weight: 700;
      font-size: 2rem;
      letter-spacing: -0.5px;
      margin-bottom: 0.5rem;
    }
    
    .tagline {
      font-weight: 300;
      font-size: 1.1rem;
    }
    
    .container {
      max-width: 800px;
      margin: 2rem auto;
      background: white;
      padding: 2.5rem;
      border-radius: 16px;
      box-shadow: 0 8px 24px rgba(0,0,0,0.08);
      position: relative;
      overflow: hidden;
    }
    
    .container::after {
      content: "";
      position: absolute;
      bottom: 0;
      left: 0;
      width: 100%;
      height: 8px;
      background: linear-gradient(90deg, var(--light-green), var(--primary-green));
    }
    
    .upload-area {
      border: 2px dashed #b1d8b7;
      border-radius: 12px;
      padding: 2rem;
      text-align: center;
      margin: 2rem 0;
      transition: all 0.3s ease;
      position: relative;
      background: #f9fcf9;
    }
    
    .upload-area:hover {
      border-color: var(--primary-green);
    }
    
    .upload-icon {
      font-size: 3rem;
      color: var(--primary-green);
      margin-bottom: 1rem;
    }
    
    .upload-btn {
      background: var(--primary-green);
      color: white;
      border: none;
      padding: 0.8rem 1.8rem;
      border-radius: 50px;
      font-weight: 500;
      cursor: pointer;
      transition: all 0.3s ease;
      display: inline-block;
      margin-top: 1rem;
    }
    
    .upload-btn:hover {
      background: var(--dark-green);
      transform: translateY(-2px);
    }
    
    .result {
      background: #f5faf5;
      border-radius: 12px;
      padding: 1.5rem;
      margin-top: 2rem;
      border-left: 4px solid var(--primary-green);
    }
    
    .plant-image {
      width: 100%;
      max-height: 300px;
      object-fit: cover;
      border-radius: 8px;
      margin-bottom: 1rem;
    }
    
    .plant-name {
      color: var(--dark-green);
      margin-bottom: 1rem;
    }
    
    .info-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
      gap: 1rem;
      margin-top: 1.5rem;
    }
    
    .info-card {
      background: white;
      padding: 1rem;
      border-radius: 8px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.05);
    }
    
    .info-card h3 {
      color: var(--primary-green);
      margin-bottom: 0.5rem;
      font-size: 1rem;
    }
    
    .discovery-section {
      margin-top: 3rem;
      padding-top: 2rem;
      border-top: 1px solid #e0f2e0;
    }
    
    .discovery-form {
      display: grid;
      gap: 1rem;
      margin-top: 1.5rem;
    }
    
    .form-group {
      text-align: left;
    }
    
    .form-group label {
      display: block;
      margin-bottom: 0.5rem;
      font-weight: 500;
    }
    
    .form-group input,
    .form-group textarea {
      width: 100%;
      padding: 0.8rem;
      border: 1px solid #c8e6c9;
      border-radius: 8px;
      font-family: inherit;
    }
    
    .form-group textarea {
      min-height: 100px;
    }
    
    .submit-btn {
      background: var(--primary-green);
      color: white;
      border: none;
      padding: 0.8rem 2rem;
      border-radius: 50px;
      font-weight: 500;
      cursor: pointer;
      transition: all 0.3s ease;
      justify-self: start;
      margin-top: 0.5rem;
    }
    
    .submit-btn:hover {
      background: var(--dark-green);
    }
    
    @media (max-width: 768px) {
      .container {
        padding: 1.5rem;
        margin: 1rem;
      }
      
      .info-grid {
        grid-template-columns: 1fr;
      }
    }
  </style>
</head>
<body>
  <header>
    <div class="container" style="background: transparent; box-shadow: none; padding: 1.5rem 0;">
      <div class="logo">PLANKTON</div>
      <div class="tagline">Discover. Scan. Learn About Plants</div>
    </div>
  </header>
  
  <div class="container">
    <h1 style="font-size: 1.8rem; font-weight: 600; color: var(--dark-green); margin-bottom: 1rem;">Smart Plant Scanner</h1>
    <p style="color: #557d5e;">Upload a photo of any plant to identify it and learn about its properties</p>
    
    <div class="upload-area" id="uploadArea">
      <div class="upload-icon">
        <svg xmlns="http://www.w3.org/2000/svg" width="64" height="64" fill="currentColor" viewBox="0 0 16 16">
          <path d="M4.502 9a1.5 1.5 0 1 0 0-3 1.5 1.5 0 0 0 0 3z"/>
          <path d="M14.002 13a2 2 0 0 1-2 2h-10a2 2 0 0 1-2-2V5A2 2 0 0 1 2 3a2 2 0 0 1 2-2h10a2 2 0 0 1 2 2v8a2 2 0 0 1-2 2zm-1-4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h5.5a.5.5 0 0 1 0 1H5a1 1 0 0 0-1 1v6a1 1 0 0 0 1 1h6a1 1 0 0 0 1-1V9.5a.5.5 0 0 1 1 0V9z"/>
        </svg>
      </div>
      <p style="color: #5e7d64;">Drag & drop your plant photo here</p>
      <p style="color: #7a9a80; font-size: 0.9rem; margin-top: 0.5rem;">or</p>
      <input type="file" id="plantUpload" accept="image/*" style="display: none;" />
      <button class="upload-btn" onclick="document.getElementById('plantUpload').click()">Select File</button>
    </div>
    
    <div class="result" id="resultContainer" style="display: none;">
      <img id="plantImagePreview" src="" class="plant-image" alt="Uploaded plant image showing Tulsi plant with green leaves" />
      <h2 class="plant-name">Identified Plant: <span id="plantName">Tulsi (Holy Basil)</span></h2>
      
      <div class="info-grid">
        <div class="info-card">
          <h3>Common Names</h3>
          <p id="plantNames">Tulsi (Hindi), Holy Basil (English), तुलसी (Marathi)</p>
        </div>
        
        <div class="info-card">
          <h3>Medicinal Uses</h3>
          <p id="plantUses">Used in Ayurveda, improves immunity, cures cold and cough</p>
        </div>
        
        <div class="info-card">
          <h3>Origin</h3>
          <p id="plantOrigin">Indian subcontinent</p>
        </div>
        
        <div class="info-card">
          <h3>Care Tips</h3>
          <p id="plantCare">Needs sunlight, water every 2 days, grow in small pots</p>
        </div>
      </div>
    </div>
    
    <div class="discovery-section">
      <h2 style="font-size: 1.4rem; color: var(--dark-green);">Discover a New Plant?</h2>
      <p style="color: #5e7d64;">Help us expand our database by submitting information about plants we haven't identified yet</p>
      
      <div class="discovery-form">
        <div class="form-group">
          <label for="newPlantName">Plant Name (if known)</label>
          <input type="text" id="newPlantName" placeholder="Enter common or scientific name">
        </div>
        
        <div class="form-group">
          <label for="newPlantPhoto">Upload Photos (multiple allowed)</label>
          <input type="file" id="newPlantPhoto" accept="image/*" multiple>
        </div>
        
        <div class="form-group">
          <label for="newPlantLocation">Where did you find this plant?</label>
          <input type="text" id="newPlantLocation" placeholder="City, Country or specific location">
        </div>
        
        <div class="form-group">
          <label for="newPlantDescription">Description & Characteristics</label>
          <textarea id="newPlantDescription" placeholder="Describe leaves, flowers, height, smell, etc."></textarea>
        </div>
        
        <div class="form-group">
          <label for="newPlantUses">Known Uses (medicinal, culinary, etc.)</label>
          <textarea id="newPlantUses" placeholder="Describe any known uses for this plant"></textarea>
        </div>
        
        <button class="submit-btn">Submit Discovery</button>
      </div>
    </div>
  </div>

  <script>
    // Handle plant image upload and display result
    const plantUpload = document.getElementById('plantUpload');
    const uploadArea = document.getElementById('uploadArea');
    const resultContainer = document.getElementById('resultContainer');
    const plantImagePreview = document.getElementById('plantImagePreview');
    
    // Drag and drop functionality
    uploadArea.addEventListener('dragover', (e) => {
      e.preventDefault();
      uploadArea.style.borderColor = '#2e8b57';
      uploadArea.style.backgroundColor = '#e8f5e9';
    });
    
    uploadArea.addEventListener('dragleave', () => {
      uploadArea.style.borderColor = '#b1d8b7';
      uploadArea.style.backgroundColor = '#f9fcf9';
    });
    
    uploadArea.addEventListener('drop', (e) => {
      e.preventDefault();
      uploadArea.style.borderColor = '#b1d8b7';
      uploadArea.style.backgroundColor = '#f9fcf9';
      
      if (e.dataTransfer.files.length) {
        plantUpload.files = e.dataTransfer.files;
        showResult();
      }
    });
    
    plantUpload.addEventListener('change', showResult);
    
    function showResult() {
      const file = plantUpload.files[0];
      if (file) {
        const reader = new FileReader();
        reader.onload = function(e) {
          plantImagePreview.src = e.target.result;
          resultContainer.style.display = 'block';
          
          // Scroll to result section
          resultContainer.scrollIntoView({ behavior: 'smooth' });
        }
        reader.readAsDataURL(file);
      }
    }
    
    // In a real app, you would have actual plant identification API calls here
    // For this demo, we're just displaying the uploaded image
    
    // Handle new plant discovery submission
    const submitBtn = document.querySelector('.submit-btn');
    submitBtn.addEventListener('click', () => {
      const plantName = document.getElementById('newPlantName').value;
      const plantLocation = document.getElementById('newPlantLocation').value;
      
      if (!plantName && !plantLocation) {
        alert('Please provide at least a plant name or location');
        return;
      }
      
      // In a real app, you would send this data to your server
      alert('Thank you for your submission! Our botanists will review this information.');
      
      // Reset form
      document.getElementById('newPlantName').value = '';
      document.getElementById('newPlantPhoto').value = '';
      document.getElementById('newPlantLocation').value = '';
      document.getElementById('newPlantDescription').value = '';
      document.getElementById('newPlantUses').value = '';
    });
  </script>
</body>
</html>
