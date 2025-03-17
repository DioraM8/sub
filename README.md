<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Assignment Submission System</title>
    <style>
        body {
            font-family: 'Poppins', sans-serif;
            margin: 0;
            padding: 0;
            background: linear-gradient(135deg, #8A2BE2, #4169E1, #FF69B4);
            text-align: center;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            color: white;
            padding: 20px;
        }
        .container {
            max-width: 600px;
            width: 100%;
            background: rgba(255, 255, 255, 0.9);
            padding: 30px;
            border-radius: 15px;
            box-shadow: 10px 10px 30px rgba(0, 0, 0, 0.3);
            color: black;
            margin-bottom: 20px;
        }
        h2 {
            color: #6A0DAD;
            margin-top: 0;
        }
        label {
            display: block;
            margin: 15px 0 5px;
            text-align: left;
            font-weight: bold;
        }
        input[type="text"], input[type="date"], input[type="file"] {
            width: 100%;
            padding: 10px;
            margin: 5px 0 15px;
            border-radius: 8px;
            border: 1px solid #ccc;
            box-sizing: border-box;
        }
        .button {
            margin-top: 15px;
            display: inline-block;
            padding: 12px 25px;
            background: linear-gradient(135deg, #9370DB, #8A2BE2);
            color: white;
            text-decoration: none;
            font-size: 16px;
            border-radius: 8px;
            box-shadow: 5px 5px 15px rgba(0, 0, 0, 0.3);
            transition: all 0.3s ease-in-out;
            cursor: pointer;
            border: none;
        }
        .button:hover {
            background: linear-gradient(135deg, #8A2BE2, #9370DB);
            transform: translateY(-2px);
        }
        .nav-link {
            margin-top: 20px;
            color: white;
            text-decoration: none;
            font-weight: bold;
            padding: 8px 20px;
            background: rgba(255, 255, 255, 0.2);
            border-radius: 20px;
            transition: all 0.3s ease;
        }
        .nav-link:hover {
            background: rgba(255, 255, 255, 0.3);
            transform: scale(1.05);
        }
        .student-info {
            margin-bottom: 20px;
            border-bottom: 1px solid #ddd;
            padding-bottom: 15px;
        }
        ul {
            list-style-type: none;
            padding: 0;
        }
        li {
            background: #f4f4f4;
            margin: 15px 0;
            padding: 15px;
            border-radius: 8px;
            text-align: left;
            transition: transform 0.3s ease;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        }
        li:hover {
            transform: translateY(-5px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }
        .file-link {
            display: inline-block;
            margin-top: 10px;
            padding: 5px 15px;
            background: #e0e0e0;
            border-radius: 20px;
            text-decoration: none;
            color: #6A0DAD;
            transition: background 0.3s ease;
        }
        .file-link:hover {
            background: #d0d0d0;
        }
        .empty-message {
            font-style: italic;
            color: #777;
            padding: 20px;
        }
        .page {
            display: none;
            width: 100%;
            max-width: 800px;
        }
        .active {
            display: block;
        }
        .tab-buttons {
            margin-bottom: 20px;
        }
        .tab-button {
            padding: 10px 20px;
            background: rgba(255, 255, 255, 0.2);
            border: none;
            color: white;
            margin: 0 5px;
            border-radius: 20px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s ease;
        }
        .tab-button:hover {
            background: rgba(255, 255, 255, 0.3);
        }
        .tab-button.active {
            background: rgba(255, 255, 255, 0.4);
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
        }
    </style>
</head>
<body>
    <div class="tab-buttons">
        <button class="tab-button active" onclick="showPage('submission-page')">Submit Assignment</button>
        <button class="tab-button" onclick="showPage('assignments-page')">View Assignments</button>
    </div>

    <!-- Submission Page -->
    <div id="submission-page" class="page active">
        <div class="container">
            <h2>Submit Your Assignment</h2>
            <div class="student-info">
                <p><strong>Name:</strong> Muslimova Diyorakhon</p>
                <p><strong>Student ID:</strong> 2417494</p>
            </div>
            <form id="assignmentForm">
                <label for="title">Assignment Title:</label>
                <input type="text" id="title" name="title" required>
                
                <label for="due-date">Due Date:</label>
                <input type="date" id="due-date" name="due-date" required>
                
                <label for="file">Upload File:</label>
                <input type="file" id="file" name="file" required>
                
                <button type="submit" class="button">Submit Assignment</button>
            </form>
        </div>
    </div>

    <!-- Assignments Page -->
    <div id="assignments-page" class="page">
        <div class="container">
            <h2>Submitted Assignments</h2>
            <div class="student-info">
                <p><strong>Name:</strong> Muslimova Diyorakhon</p>
                <p><strong>Student ID:</strong> 2417494</p>
            </div>
            <ul id="submissionList">
                <li class="empty-message">No assignments submitted yet.</li>
            </ul>
        </div>
    </div>

    <script>
        // Show the selected page
        function showPage(pageId) {
            // Hide all pages
            document.querySelectorAll('.page').forEach(page => {
                page.classList.remove('active');
            });
            
            // Show the selected page
            document.getElementById(pageId).classList.add('active');
            
            // Update button states
            document.querySelectorAll('.tab-button').forEach(button => {
                button.classList.remove('active');
            });
            
            // Find the button that called this function and make it active
            event.target.classList.add('active');
            
            // If showing assignments page, refresh the list
            if (pageId === 'assignments-page') {
                displaySubmissions();
            }
        }

        // Handle form submission
        document.getElementById("assignmentForm").addEventListener("submit", function(event) {
            event.preventDefault();
            
            let title = document.getElementById("title").value;
            let dueDate = document.getElementById("due-date").value;
            let file = document.getElementById("file").files[0];
            
            if (title && dueDate && file) {
                let reader = new FileReader();
                reader.onload = function(e) {
                    let fileData = {
                        title: title,
                        dueDate: dueDate,
                        fileName: file.name,
                        fileUrl: e.target.result
                    };
                    let submissions = JSON.parse(localStorage.getItem("submissions")) || [];
                    submissions.push(fileData);
                    localStorage.setItem("submissions", JSON.stringify(submissions));
                    
                    // Reset form
                    document.getElementById("assignmentForm").reset();
                    
                    // Show success message
                    alert("Assignment submitted successfully!");
                    
                    // Switch to assignments page
                    showPage('assignments-page');
                    document.querySelectorAll('.tab-button')[1].classList.add('active');
                    document.querySelectorAll('.tab-button')[0].classList.remove('active');
                };
                reader.readAsDataURL(file);
            }
        });

        // Display submissions
        function displaySubmissions() {
            let submissions = JSON.parse(localStorage.getItem("submissions")) || [];
            let submissionList = document.getElementById("submissionList");
            submissionList.innerHTML = "";
            
            if (submissions.length === 0) {
                submissionList.innerHTML = "<li class='empty-message'>No assignments submitted yet.</li>";
            } else {
                submissions.forEach((sub, index) => {
                    let li = document.createElement("li");
                    
                    // Format the date to be more readable
                    let formattedDate = new Date(sub.dueDate).toLocaleDateString('en-US', {
                        year: 'numeric', 
                        month: 'long', 
                        day: 'numeric'
                    });
                    
                    li.innerHTML = `
                        <h3>${sub.title}</h3>
                        <p><strong>Due Date:</strong> ${formattedDate}</p>
                        <a href="${sub.fileUrl}" download="${sub.fileName}" class="file-link">
                            <i class="fas fa-download"></i> ${sub.fileName}
                        </a>
                        <button onclick="deleteSubmission(${index})" class="button" style="background: #ff6b6b; padding: 5px 10px; margin-left: 10px;">Delete</button>
                    `;
                    submissionList.appendChild(li);
                });
            }
        }
        
        // Delete a submission
        function deleteSubmission(index) {
            if (confirm("Are you sure you want to delete this assignment?")) {
                let submissions = JSON.parse(localStorage.getItem("submissions")) || [];
                submissions.splice(index, 1);
                localStorage.setItem("submissions", JSON.stringify(submissions));
                displaySubmissions();
            }
        }
        
        // Initialize the page
        window.onload = function() {
            displaySubmissions();
        };
    </script>
</body>
</html>
