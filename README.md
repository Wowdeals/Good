<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LootDeals</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <header>
        <h1>Welcome to LootDeals</h1>
    </header>
    <main>
        <div id="dealContainer"></div>
    </main>
    <footer>
        <!-- Footer content here -->
    </footer>
    <script src="script.js"></script>
</body>
</html>
const express = require('express');
const app = express();
const PORT = process.env.PORT || 3000;

// Serve static files
app.use(express.static('public'));

// Sample daily deal data
const dailyDeal = {
    title: "50% off on Electronics!",
    description: "Get amazing deals on electronics items today only.",
    link: "https://example.com/electronics-deals"
};

// Route to get daily deal data
app.get('/api/daily-deal', (req, res) => {
    res.json(dailyDeal);
});

// Start server
app.listen(PORT, () => {
    console.log(`Server is running on port ${PORT}`);
});
window.onload = async () => {
    try {
        const response = await fetch('/api/daily-deal');
        const deal = await response.json();
        displayDeal(deal);
    } catch (error) {
        console.error('Error fetching daily deal:', error);
    }
};

function displayDeal(deal) {
    const dealContainer = document.getElementById('dealContainer');
    const dealHTML = `
        <div class="deal">
            <h2>${deal.title}</h2>
            <p>${deal.description}</p>
            <a href="${deal.link}" target="_blank">View Deal</a>
        </div>
    `;
    dealContainer.innerHTML = dealHTML;
}
