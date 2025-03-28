<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BMI Calculator</title>
    <link rel="shortcut icon" href="body-mass-index.png" type="image/x-icon">
    <link rel="stylesheet" href="enhanced_main.css">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.10.0/gsap.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.10.0/ScrollToPlugin.min.js"></script>
        
    <style>
        body {
            background: linear-gradient(135deg, #cfd9df 0%, #e2ebf0 100%);
            font-family: 'Arial', sans-serif;
            color: #333;
        }
        .bmi-wrapper {
            background: #ffffff;
            border: 1px solid #ccc;
            box-shadow: 0px 8px 20px rgba(0, 0, 0, 0.1);
        }
    </style>
</head>

<body>
    <div class="container my-5">
        <div class="bmi-wrapper">
            <!-- Input Section -->
            <div class="text-center">
                <h2 class="display-6">BMI Calculator</h2>
                <div class="image-container">
                    <div class="image-item">
                        <img class="profile-img"
                            src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcS-Juxva6Lc3s7MGkKDCRFykoYLiVVgiVAXYg&s"
                            alt="Male">
                        <p>Male</p>
                    </div>
                    <div class="image-item">
                        <img class="profile-img"
                            src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcT93RDHnuQZW7bF7PRijgcZXrcKIOw3VZeT78uC0C1t80KE_FqUuOkGRTvbMcz0yQLsXBk&usqp=CAU"
                            alt="Female">
                        <p>Female</p>
                    </div>
                </div>
                <form id="bmi-form">
                    <div class="mb-3">
                        <label for="weight-unit" class="form-label">Units</label>
                        <select id="weight-unit" class="form-select" required>
                            <option value="kg">kg/m</option>
                            <option value="lbs">lbs/inches</option>
                        </select>
                    </div>
                    <div class="mb-3">
                        <label for="age" class="form-label">Age</label>
                        <input type="number" class="form-control" placeholder="Enter your age" id="age" required>
                    </div>
                    <div class="mb-3">
                        <label for="weight" class="form-label">Weight</label>
                        <input type="number" class="form-control" placeholder="Enter your weight" id="weight" required>
                    </div>
                    <div class="mb-3">
                        <label for="height" class="form-label">Height</label>
                        <input type="number" class="form-control" placeholder="Enter your height" id="height" required>
                    </div>
                    <button type="button" onclick="calculateBMI()" class="btn btn-primary w-100">Calculate BMI</button>
                </form>
            </div>
            <!-- BMI Result Section -->
            <div id="result-section" class="bmi-result text-center my-5" style="display:none;">
                <h3>Your BMI Result</h3>
                <div id="display-result" class="display-result mb-4"></div>
                <h4>
                    <p id="bmi-meaning" class="fw-bold"></p>
                </h4>
                <div class="bmi-result-container">
                    <p class="display-result">Your BMI is: <span id="bmiValue"></span></p>
                    <progress id="bmiProgress" value="0" max="100"></progress>
                </div>
                
            </div>
            <br>
            <!-- what you bmi means -->
            <div class="card p-4 mb-4">

                <div id="bmimeans-section" class="mt-2" style="display:none;">
                    <h3 class="text-center">What your BMI score means</h3>
                    <div id="bmi-means" class="alert alert-info mt-3"></div>
                </div>
            </div>
            <!-- Lifestyle Routines Section -->
            <div class="card p-4 mb-4">
                <div id="routine-section" class="mt-2" style="display:none;">
                    <h3 class="text-center">Lifestyle Routines Based on Your BMI</h3>
                    <div id="routine-description" class="alert alert-info mt-3"></div>
                </div>
            </div>
            <!-- BMI Chart -->
            <div class="card p-4 mb-4">
                <h4 class="text-center mb-3">BMI Chart</h4>
                <table class="table table-striped">
                    <thead class="table-dark">
                        <tr>
                            <th>Category</th>
                            <th>BMI Range</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td>Severely Underweight</td>
                            <td>&lt; 16.0</td>
                        </tr>
                        <tr>
                            <td>Underweight</td>
                            <td>16.0 - 18.5</td>
                        </tr>
                        <tr>
                            <td>Normal</td>
                            <td>18.5 - 24.9</td>
                        </tr>
                        <tr>
                            <td>Overweight</td>
                            <td>25.0 - 29.9</td>
                        </tr>
                        <tr>
                            <td>Obese Class I</td>
                            <td>30.0 - 34.9</td>
                        </tr>
                        <tr>
                            <td>Obese Class II</td>
                            <td>35.0 - 39.9</td>
                        </tr>
                        <tr>
                            <td>Obese Class III</td>
                            <td>&gt; 40.0</td>
                        </tr>
                    </tbody>
                </table>
            </div>
            <!-- Introduction Section -->
            <div class="card p-4 mb-4">
                <h2 class="text-center">Introduction to the Body Mass Index (BMI)</h2>
                <p>BMI is a common way to estimate body fat based on your weight and height. It helps determine if your
                    weight falls within a healthy range. Simply weighing yourself isn’t enough since taller people can
                    weigh
                    more but still be healthier than shorter, heavier individuals.</p>
                <p>BMI lets you see if your weight is suitable for your body type. Though not a perfect measure of body
                    fat, BMI is still useful for identifying health risks, especially those related to extra weight.
                    Doctors
                    also use BMI to help figure out medicine doses, as those with higher BMIs often need stronger doses.
                </p>
            </div>
            <!-- Benefits Section -->
            <div class="benefits">
                <h2>
                    <center>Why Use a BMI Calculator ?</center>
                </h2><br>
                <p>Using a BMI calculator is a convenient way to determine your BMI score quickly. Below are some key
                    reasons to use this tool:</p><br>
                <div class="benefits-box">
                    <div class="benefit-item">
                        <p>Health Monitoring</p>
                    </div>
                    <div class="benefit-item">
                        <p>Fitness Guidance</p>
                    </div>
                    <div class="benefit-item">
                        <p>Weight Assessment</p>
                    </div>
                    <div class="benefit-item">
                        <center>
                            <p>Wellness Tracking</p>
                        </center>
                    </div>
                </div>
            </div>
            <!-- How to Calculate BMI Section -->
            <div class="card p-4 mb-4">
                <h2 class="text-center">How to Calculate BMI</h2>
                <ol>
                    <li>Multiply your height by itself (height X height).</li>
                    <li>Divide your weight by the result from the first step.</li>
                </ol>
                <div class="text-center">
                    <h5>International System of Units (SI)</h5>
                    <p>BMI = weight (kg) ÷ (height (m))²</p>
                    <h5>Imperial System</h5>
                    <p>BMI = weight (lb) ÷ (height (inches))² × 703</p>
                </div>
            </div>

            <!-- Go to Top Button -->
            <div class="text-center">
                <a href="#top" class="btn btn-secondary">
                    Click here to know your Body Mass Index (BMI)
                </a>
            </div>
        </div>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js"></script>
    <script src="enhanced_main.js"></script>
</body>

</html>


