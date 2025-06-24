# roblox-like-counter
const express = require("express");
const fetch = require("node-fetch");
const app = express();
const PORT = process.env.PORT || 3000;

const UNIVERSE_ID = "101804282839462";

app.get("/likes", async (req, res) => {
	try {
		const response = await fetch(`https://games.roblox.com/v1/games?universeIds=${UNIVERSE_ID}`);
		const data = await response.json();
		const likes = data.data[0].upVotes;
		res.json({ likes });
	} catch (err) {
		res.status(500).json({ error: "Failed to fetch likes" });
	}
});

app.listen(PORT, () => console.log("Server running on port", PORT));
