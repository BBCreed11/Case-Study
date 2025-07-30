# Case-Study
Baltimore Voters Experience
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>The Baltimore Voter Experience: A Case Study</title>
    
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script> 
  <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700&display=swap" rel="stylesheet"> 
    <!-- Chosen Palette: Warm Neutrals -->
    <!-- Application Structure Plan: The application is structured as a narrative journey through the voter's experience, divided into four thematic sections: 1. Who Are the Voters? (Demographics), 2. The Information Challenge (How voters get informed and the obstacles), 3. The Voting Process (Positive and negative experiences), and 4. Empowering Voters (Conclusions & Recommendations). This thematic flow was chosen over the report's structure to create a more logical and engaging user experience. It allows users to first understand the participants, then the problems they face, their direct experiences, and finally, the proposed solutions, which is a more intuitive way to absorb the case study's findings. Navigation is handled by a sticky header, allowing users to jump between these key themes easily. -->
    <!-- Visualization & Content Choices: 
        - Participant Demographics: Goal: Inform. Method: A series of donut charts (Chart.js) to show age, income, and education distributions. Interaction: Hovering over chart segments reveals details. Justification: Donut charts are excellent for showing parts of a whole, making the demographic breakdown immediately clear.
        - Information Sources: Goal: Organize/Inform. Method: A dynamic bar chart (Chart.js) showing the popularity of different information sources. Interaction: Clicking on a category in the legend can toggle the visibility of that source type. Justification: A bar chart effectively compares the usage of different sources.
        - Voter Feelings: Goal: Inform (Qualitative). Method: A clickable grid of cards (HTML/Tailwind/JS). Interaction: Clicking a card reveals a specific quote from a participant. Justification: This interactive method presents qualitative data in a digestible and engaging way, preventing a wall of text.
        - Recommendations: Goal: Inform/Organize. Method: Two-column layout with clear headings and lists (HTML/Tailwind). Interaction: None needed. Justification: A clean, structured text layout is best for presenting actionable recommendations clearly.
        - CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    <style>
        body { font-family: 'Inter', sans-serif; }
        .chart-container { position: relative; width: 100%; max-width: 450px; margin-left: auto; margin-right: auto; height: 300px; max-height: 350px; }
        @media (min-width: 768px) { .chart-container { height: 350px; max-height: 400px; } }
        .nav-link { transition: color 0.3s, border-bottom-color 0.3s; }
        .nav-link.active { color: #3b82f6; border-bottom-color: #3b82f6; }
        .nav-link:not(.active) { border-bottom-color: transparent; }
        .content-section { display: none; }
        .content-section.active { display: block; }
        .quote-card { cursor: pointer; transition: transform 0.2s, box-shadow 0.2s; }
        .quote-card:hover { transform: translateY(-5px); box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05); }
    </style>
</head>
<body class="bg-gray-50 text-gray-800">

    <header class="bg-white shadow-md sticky top-0 z-50">
        <nav class="container mx-auto px-6 py-4">
            <ul class="flex justify-center space-x-4 sm:space-x-8">
                <li><a href="#demographics" class="nav-link text-sm sm:text-base font-medium text-gray-600 hover:text-blue-500 border-b-2 pb-1">The Voters</a></li>
                <li><a href="#information" class="nav-link text-sm sm:text-base font-medium text-gray-600 hover:text-blue-500 border-b-2 pb-1">The Information Challenge</a></li>
                <li><a href="#experience" class="nav-link text-sm sm:text-base font-medium text-gray-600 hover:text-blue-500 border-b-2 pb-1">The Voting Experience</a></li>
                <li><a href="#recommendations" class="nav-link text-sm sm:text-base font-medium text-gray-600 hover:text-blue-500 border-b-2 pb-1">Empowering Voters</a></li>
            </ul>
        </nav>
    </header>

    <main class="container mx-auto p-4 sm:p-8">
        <div class="text-center mb-12">
            <h1 class="text-4xl md:text-5xl font-bold text-gray-900 mb-2">The Baltimore Voter Experience</h1>
            <p class="text-lg text-gray-600 max-w-3xl mx-auto">An interactive summary of a case study on the barriers faced by low-income and low-literacy voters in Baltimore City during the 2020 election.</p>
        </div>

        <section id="demographics" class="content-section">
            <div class="text-center mb-10">
                <h2 class="text-3xl font-bold text-gray-900">Who Are the Voters?</h2>
                <p class="mt-2 text-gray-600 max-w-2xl mx-auto">This section provides a snapshot of the six participants in the study. Understanding their backgrounds is the first step to understanding their experiences. All participants identified as Democrats.</p>
            </div>
            <div class="grid md:grid-cols-3 gap-8">
                <div class="bg-white p-6 rounded-lg shadow">
                    <h3 class="text-xl font-semibold text-center mb-4">Age Distribution</h3>
                    <div class="chart-container">
                        <canvas id="ageChart"></canvas>
                    </div>
                </div>
                <div class="bg-white p-6 rounded-lg shadow">
                    <h3 class="text-xl font-semibold text-center mb-4">Income Levels</h3>
                    <div class="chart-container">
                        <canvas id="incomeChart"></canvas>
                    </div>
                </div>
                <div class="bg-white p-6 rounded-lg shadow">
                    <h3 class="text-xl font-semibold text-center mb-4">Education Levels</h3>
                    <div class="chart-container">
                        <canvas id="educationChart"></canvas>
                    </div>
                </div>
            </div>
        </section>

        <section id="information" class="content-section">
            <div class="text-center mb-10">
                <h2 class="text-3xl font-bold text-gray-900">The Information Challenge</h2>
                <p class="mt-2 text-gray-600 max-w-2xl mx-auto">Voters face significant hurdles in getting accurate and understandable information. This section explores where they turn for news and the confusion that often results.</p>
            </div>
            <div class="grid md:grid-cols-2 gap-8 items-center">
                <div class="bg-white p-6 rounded-lg shadow">
                    <h3 class="text-xl font-semibold text-center mb-4">Primary Information Sources</h3>
                    <div class="chart-container mx-auto" style="height: 400px; max-height: 450px;">
                        <canvas id="sourcesChart"></canvas>
                    </div>
                </div>
                <div class="space-y-4">
                    <div class="bg-white p-6 rounded-lg shadow">
                        <h3 class="text-xl font-semibold mb-2">Key Areas of Misinformation</h3>
                        <ul class="list-disc list-inside text-gray-700 space-y-1">
                            <li>Number of available polling places.</li>
                            <li>Belief that mail-in voting was a temporary COVID-19 measure.</li>
                            <li>Lack of knowledge about the Electoral College.</li>
                            <li>Unaware of poll watchers or the recount process.</li>
                        </ul>
                    </div>
                    <div class="bg-white p-6 rounded-lg shadow">
                        <h3 class="text-xl font-semibold mb-2">The Media's Double-Edged Sword</h3>
                        <p class="text-gray-700"><strong class="text-red-600">Hindrances:</strong> Conflicting reports between social media and traditional news, the spread of rumors, and perceived bias created confusion.</p>
                        <p class="text-gray-700 mt-2"><strong class="text-green-600">Aids:</strong> Despite the confusion, widespread media campaigns were effective in encouraging people to get out and vote.</p>
                    </div>
                </div>
            </div>
        </section>

        <section id="experience" class="content-section">
            <div class="text-center mb-10">
                <h2 class="text-3xl font-bold text-gray-900">The Voting Experience</h2>
                <p class="mt-2 text-gray-600 max-w-2xl mx-auto">This section explores what voters found helpful and challenging during the voting process, along with their feelings as the election unfolded. Click on a card to read a direct quote.</p>
            </div>
            <div class="grid md:grid-cols-2 gap-8">
                <div class="bg-white p-6 rounded-lg shadow">
                    <h3 class="text-xl font-semibold mb-3 text-green-700">What Went Well (Helpful)</h3>
                    <ul class="list-disc list-inside space-y-2 text-gray-700">
                        <li>Information on specific candidates was easy to find online.</li>
                        <li>Mail-in voting was seen as easy and convenient.</li>
                        <li>In-person voting lines were not long.</li>
                        <li>Paper ballots were preferred over touch screens for speed and hygiene.</li>
                    </ul>
                </div>
                <div class="bg-white p-6 rounded-lg shadow">
                    <h3 class="text-xl font-semibold mb-3 text-red-700">What Was Difficult (Challenging)</h3>
                    <ul class="list-disc list-inside space-y-2 text-gray-700">
                        <li>Ballots were lengthy and used confusing language.</li>
                        <li>Voters lacked confidence in filling out the ballot correctly.</li>
                        <li>Concerns about where and when to drop off mail-in ballots.</li>
                        <li>Confusion over changes to polling place locations.</li>
                    </ul>
                </div>
            </div>
             <div class="mt-10">
                <h3 class="text-2xl font-bold text-center text-gray-900 mb-6">Voter Sentiments</h3>
                <div class="grid sm:grid-cols-2 lg:grid-cols-3 gap-4" id="quotesGrid">
                </div>
                <div id="modal" class="fixed inset-0 bg-black bg-opacity-50 z-50 hidden items-center justify-center">
                    <div class="bg-white p-8 rounded-lg shadow-2xl max-w-md w-full mx-4">
                        <p id="modalText" class="text-lg text-gray-700 mb-4"></p>
                        <button id="closeModal" class="bg-blue-500 text-white px-4 py-2 rounded-lg hover:bg-blue-600">Close</button>
                    </div>
                </div>
            </div>
        </section>

        <section id="recommendations" class="content-section">
            <div class="text-center mb-10">
                <h2 class="text-3xl font-bold text-gray-900">Empowering Voters: The Path Forward</h2>
                <p class="mt-2 text-gray-600 max-w-2xl mx-auto">The study concludes with clear, actionable recommendations aimed at breaking down barriers and making the voting process more accessible and understandable for everyone.</p>
            </div>
            <div class="grid md:grid-cols-2 gap-8">
                <div class="bg-white p-6 rounded-lg shadow">
                    <h3 class="text-2xl font-semibold mb-4">1. Focus on Education</h3>
                    <p class="mb-4 text-gray-600">A fundamental lack of knowledge about the voting process itself was a major barrier. Education is the key to empowerment.</p>
                    <ul class="list-disc list-inside space-y-2 text-gray-700">
                        <li>Integrate education into voter registration drives.</li>
                        <li>Offer virtual classes to explain the voting process.</li>
                        <li>Use social media to share simple, clear educational content.</li>
                        <li>Provide easy-to-understand guides on where and when to vote.</li>
                        <li>Remind voters about the importance of all elections, not just presidential ones.</li>
                    </ul>
                </div>
                <div class="bg-white p-6 rounded-lg shadow">
                    <h3 class="text-2xl font-semibold mb-4">2. Simplify the Ballot</h3>
                    <p class="mb-4 text-gray-600">The language on ballots is a significant hurdle. The study found ballot measures were written at a graduate school reading level.</p>
                    <ul class="list-disc list-inside space-y-2 text-gray-700">
                        <li>Advocate for plain language on all official ballots.</li>
                        <li>Rewrite ballot measures to be understood by someone with a 6th-grade reading level.</li>
                        <li>Ensure voters can understand what they are voting for without needing outside help.</li>
                    </ul>
                </div>
            </div>
        </section>

    </main>

    <footer class="text-center py-6 mt-12 bg-gray-100">
        <p class="text-gray-500">This interactive summary was generated based on the case study "Low Income and Low Literacy Voters" by Meghan, Sade, Toni, and Gema.</p>
    </footer>

    <script>
        document.addEventListener('DOMContentLoaded', function () {
            const navLinks = document.querySelectorAll('.nav-link');
            const contentSections = document.querySelectorAll('.content-section');

            function updateActiveState(hash) {
                let activeSection = document.querySelector(hash);
                if (!activeSection) {
                    activeSection = document.getElementById('demographics');
                    window.location.hash = '#demographics';
                }

                navLinks.forEach(link => {
                    link.classList.toggle('active', link.getAttribute('href') === window.location.hash);
                });

                contentSections.forEach(section => {
                    section.classList.toggle('active', section.id === activeSection.id);
                });
            }

            navLinks.forEach(link => {
                link.addEventListener('click', function (e) {
                    e.preventDefault();
                    const targetId = this.getAttribute('href');
                    window.location.hash = targetId;
                });
            });

            window.addEventListener('hashchange', () => updateActiveState(window.location.hash));
            updateActiveState(window.location.hash || '#demographics');

            const chartColors = {
                bg: ['#a7f3d0', '#bfdbfe', '#fecaca', '#e5e7eb', '#ddd6fe', '#fde68a'],
                border: ['#34d399', '#60a5fa', '#f87171', '#9ca3af', '#a78bfa', '#fbbf24']
            };

            const chartOptions = {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: {
                        position: 'bottom',
                    },
                }
            };

            new Chart(document.getElementById('ageChart'), {
                type: 'doughnut',
                data: {
                    labels: ['18-30', '31-50', '51-70'],
                    datasets: [{
                        label: 'Age Distribution',
                        data: [3, 2, 1],
                        backgroundColor: chartColors.bg,
                        borderColor: chartColors.border,
                        borderWidth: 1
                    }]
                },
                options: chartOptions
            });

            new Chart(document.getElementById('incomeChart'), {
                type: 'doughnut',
                data: {
                    labels: ['< $25k', '$30-35k', '$36-50k', '> $50k (Recent Job Loss)'],
                    datasets: [{
                        label: 'Income Levels',
                        data: [3, 1, 1, 1],
                        backgroundColor: chartColors.bg,
                        borderColor: chartColors.border,
                        borderWidth: 1
                    }]
                },
                options: chartOptions
            });

            new Chart(document.getElementById('educationChart'), {
                type: 'doughnut',
                data: {
                    labels: ['Some College', 'Associates Degree'],
                    datasets: [{
                        label: 'Education Levels',
                        data: [3, 3],
                        backgroundColor: chartColors.bg.slice(0, 2),
                        borderColor: chartColors.border.slice(0, 2),
                        borderWidth: 1
                    }]
                },
                options: chartOptions
            });
            
            new Chart(document.getElementById('sourcesChart'), {
                type: 'bar',
                data: {
                    labels: ['Social Media', 'News Outlets', 'Ads', 'Personal Network'],
                    datasets: [{
                        label: 'Information Source Types',
                        data: [4, 6, 2, 3],
                        backgroundColor: chartColors.bg,
                        borderColor: chartColors.border,
                        borderWidth: 1
                    }]
                },
                options: {
                    ...chartOptions,
                    indexAxis: 'y',
                    plugins: { legend: { display: false } }
                }
            });

            const quotes = [
                { text: "I feel better now that is over. I was excited to actually go and vote." },
                { text: "It's up for grabs like I'm excited and then I'm anxious like the figure out you know who's going to win..." },
                { text: "I feel the same, I'm a little anxious to see who's going to win... I knew it was going to be a long drawn out process." },
                { text: "Well the type of president we have...we could have had Mary Poppins as a Democrat... I would have voted for her." },
                { text: "I feel pretty optimistic, but I shudder thinking [of] Trump’s shenanigans. He is desperate to hold on to power." },
                { text: "It was my first time seeing a ballot in person so it was a little foreign to me. None the less it was straightforward but lengthy..." }
            ];

            const quotesGrid = document.getElementById('quotesGrid');
            const modal = document.getElementById('modal');
            const modalText = document.getElementById('modalText');
            const closeModal = document.getElementById('closeModal');

            quotes.forEach(quote => {
                const card = document.createElement('div');
                card.className = 'quote-card bg-white p-4 rounded-lg shadow-md flex items-center justify-center text-center';
                const p = document.createElement('p');
                p.className = 'text-gray-600 italic';
                p.textContent = `"${quote.text.substring(0, 40)}..."`;
                card.appendChild(p);
                card.addEventListener('click', () => {
                    modalText.textContent = `"${quote.text}"`;
                    modal.classList.remove('hidden');
                    modal.classList.add('flex');
                });
                quotesGrid.appendChild(card);
            });

            closeModal.addEventListener('click', () => {
                modal.classList.add('hidden');
                modal.classList.remove('flex');
            });
            modal.addEventListener('click', (e) => {
                if (e.target === modal) {
                    modal.classList.add('hidden');
                    modal.classList.remove('flex');
                }
            });
        });
    </script>
</body>
</html>
