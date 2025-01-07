<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GitHub Profile & Contributions</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background: #f5f5f5;
            color: #333;
        }
        .header {
            text-align: center;
            margin-top: 20px;
        }
        .header img {
            border-radius: 50%;
            max-width: 120px;
        }
        .github-info {
            text-align: center;
            margin: 20px;
        }
        .github-info h1 {
            font-size: 36px;
        }
        .github-info p {
            font-size: 18px;
        }
        .github-contributions {
            margin-top: 30px;
        }
        .github-contributions h2 {
            text-align: center;
            font-size: 28px;
        }
        .contributions-list {
            list-style-type: none;
            padding: 0;
        }
        .contribution-item {
            border-bottom: 1px solid #ddd;
            padding: 10px;
            margin-bottom: 10px;
        }
        .contribution-item p {
            margin: 0;
        }
        .footer {
            text-align: center;
            margin-top: 40px;
        }
    </style>
</head>
<body>

    <div class="header">
        <img src="https://avatars.githubusercontent.com/u/61685594?v=4" alt="Sunil Rathod">
        <h1>Hi there 👋</h1>
        <p>I'm Danavath Sunil Rathod, a passionate Software Developer from India specializing in Backend Development</p>
        <p><a href="https://github.com/sunilrathod098">Check out my GitHub!</a></p>
        <p><a href="https://sunilrathod-dashboard-sunilrathod098s-projects.vercel.app/">Check out my Portfolio!</a></p>
        <p><a href="https://www.linkedin.com/in/danavath-sunil-rathod-683853202//">Check out my LinkedIn!</a></p>
    </div>

    <div class="github-info">
        <h1>A passionate Software Developer from India</h1>
        <p>🌱 Currently learning: **ReactJS, TypeScript, Data Structures & Algorithms**</p>
        <p>💬 Ask me about: **NodeJS, ExpressJS, MongoDB, ReactJS, JavaScript,Python, MERN-Stack and Data Analytics**</p>
        <p>📫 Reach me at: **sunilrajputhrathod@gmail.com** | **(+19) 9022080237**</p>
    </div>

    <div class="github-contributions">
        <h2>Recent GitHub Contributions</h2>
        <ul class="contributions-list" id="contributions-list">
            <!-- Contributions will be dynamically added here -->
        </ul>
    </div>

    <script>
        const githubUsername = "sunilrathod098"; // Your GitHub username

        // Function to fetch commits and events from GitHub API
        async function fetchGitHubContributions() {
            try {
                // Fetching commits and events using GitHub API
                const commitsResponse = await fetch(`https://api.github.com/users/${githubUsername}/events`);
                const commitsData = await commitsResponse.json();

                if (commitsData && commitsData.length > 0) {
                    // Extract relevant data (commit messages, event types, etc.)
                    const contributionsList = document.getElementById("contributions-list");
                    contributionsList.innerHTML = ''; // Clear the list before adding new data

                    commitsData.forEach(event => {
                        const eventItem = document.createElement("li");
                        eventItem.classList.add("contribution-item");

                        let eventDescription = '';

                        // Check if event is a push event (commits)
                        if (event.type === "PushEvent") {
                            eventDescription = `${event.actor.login} pushed to ${event.repo.name}.`;
                            if (event.payload.commits && event.payload.commits.length > 0) {
                                eventDescription += ` Commit message: ${event.payload.commits[0].message}`;
                            }
                        }

                        // Check if event is a pull request event
                        if (event.type === "PullRequestEvent") {
                            eventDescription = `${event.actor.login} opened a pull request on ${event.repo.name}.`;
                        }

                        // Add event description to the list
                        eventItem.innerHTML = `<p>${eventDescription}</p>`;
                        contributionsList.appendChild(eventItem);
                    });
                } else {
                    console.log('No contributions found');
                }
            } catch (error) {
                console.error("Error fetching GitHub data:", error);
            }
        }

        // Fetch and display GitHub contributions when page loads
        window.onload = function () {
            fetchGitHubContributions();
        };
    </script>

    <div class="footer">
        <p>🚀 &nbsp;Connect with me:</p>
        <a href="https://twitter.com/sunilrathod098" target="blank">Twitter</a> | 
        <a href="https://www.linkedin.com/in/danavathsunilrathod/" target="blank">LinkedIn</a> | 
        <a href="https://instagram.com/sunilrathod098" target="blank">Instagram</a>
    </div>

</body>
</html>
