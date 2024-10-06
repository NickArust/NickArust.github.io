<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Nickolas Arustamyan's Site</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
    }
    .container {
      display: flex;
    }
    .sidebar {
      width: 20%;
      height: 100vh;
      position: fixed;
      top: 0;
      left: 0;
      padding: 20px;
      border-right: 1px solid #ddd;
      background-color: #f7f7f7;
    }
    .sidebar ul {
      list-style-type: none;
      padding: 0;
    }
    .sidebar ul li {
      margin-bottom: 10px;
    }
    .sidebar ul li a {
      text-decoration: none;
      color: #333;
      font-weight: bold;
    }
    .sidebar ul li a:hover {
      color: #007bff;
    }
    .content {
      margin-left: 22%;
      padding: 20px;
      width: 75%;
    }
    h2, h3 {
      color: #333;
    }
  </style>
</head>
<body>
  <div class="container">
    <!-- Sidebar Section -->
    <div class="sidebar">
      <h2>Contents</h2>
      <ul>
        <li><a href="#summary">Summary</a></li>
        <li><a href="#education">Education</a></li>
        <li><a href="#publications">Publications</a></li>
        <li><a href="#research">Research</a></li>
        <li><a href="#projects">Projects</a></li>
      </ul>
    </div>

    <!-- Main Content Section -->
    <div class="content">
      <h2 id="summary">Summary</h2>
      <p>
        I am a Ph.D student in Mathematics with a strong background in Scientific Computing and Machine Learning. My research focuses on developing numerical algorithms for problems and combining these tools with ML models to get better results, and I have a particular interest in Inverse Scattering Problems and Digital Twins. I am currently a Ph.D student in Mathematics at the University of Central Florida and am working under Dr. Carlos Borges.
      </p>

      <h2 id="education">Education</h2>
      <ul>
        <li><strong>Ph.D. in Mathematics</strong><br> University of Central Florida, 2024 – Present</li>
        <li><strong>B.S. in Mathematics</strong><br> University of Florida, 2021-2024</li>
        <li><strong>B.S. in Statistics</strong><br> University of Florida, 2021-2024</li>
      </ul>

      <h2 id="publications">Publications</h2>
      <ol>
        <li><strong>Curriculum Learning for Inverse Scattering Problems</strong><br>
          Authors: Nickolas Arustamyan, Carlos Borges, Jiequn Han, Jeremy Hoskins<br>
          <em>Pending Submission</em>, 2024.</li>

        <li><strong>Mixup Barcodes: Quantifying Topological Interactions between Point Clouds</strong><br>
          Authors: Nickolas Arustamyan, Hubert Wagner, Matthew Wheeler, Peter Bubenik<br>
          <em>SoCG</em>, 2024.<br>
          <a href="https://arxiv.org/abs/2402.15058">Link to Preprint</a></li>

        <li><strong>On the Number of Equilibria Balancing Newtonian Point Masses with a Central Force</strong><br>
          Authors: Nickolas Arustamyan, Erik Lundberg, Zvi Rosen, Sean Perry, Christopher Cox<br>
          <em>Journal of Mathematical Physics</em>, 2021.<br>
          <a href="https://arxiv.org/abs/2106.11416">Link to Preprint</a></li>
      </ol>

      <h2 id="research">Research</h2>
      <h3>Curriculum Learning for Inverse Scattering</h3>
      <p>
        <strong>Overview:</strong> I utilize Curriculum Learning models trained on multi-frequency data to generate initial guesses that are then fed into inverse problem solvers. These solvers utilize a Recursive Linearization architecture to converge to the true solution.
      </p>
      <p>
        <strong>Results:</strong> Our results show comparable results to models not using Curriculum Learning, as expected. What is most interesting is that we are able to still get these results even when using less data, up to 50% less in some cases.
      </p>
      <p>
        <strong>Technologies:</strong> MATLAB, Python, Tensorflow
      </p>

      <h2 id="projects">Projects</h2>
      <h3>Real-Time Speech Enhancement System Using Deep Learning</h3>
      <p>
        <strong>Description:</strong> Implemented a Denoising Autoencoder combined with spectral subtraction to suppress background noises while preserving speech quality. The model was optimized for deployment on a Raspberry Pi using TFLite, achieving sub-100ms processing latency to enable real-time performance. System evaluation using industry-standard metrics (PESQ, STOI) demonstrated a 30% improvement in speech quality over baseline DSP methods.
      </p>
      <p>
        <strong>Technologies:</strong> Python, PyTorch, TFLite, ONNX, NumPy, C++
      </p>
    </div>
  </div>
</body>
</html>
