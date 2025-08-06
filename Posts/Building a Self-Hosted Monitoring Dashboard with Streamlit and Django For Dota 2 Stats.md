---
weight: 4
title: Building a Self-Hosted Monitoring Dashboard with Streamlit and Django
date: 2025-07-30
draft: false
author: Vincent
description: Building a Self-Hosted Monitoring Dashboard with Streamlit and Django
tags:
  - IT
categories:
  - IT
---
## 🎮 Building a Dota 2 Stats Dashboard with Streamlit and OpenDota

As a developer and avid Dota 2 player, I wanted a personal project that could combine my passion for gaming with data engineering and visualization. With the **OpenDota API** providing extensive match data, I decided to build a dashboard using **Streamlit**, a Python framework designed for quickly building interactive web apps for data science and machine learning.

The goal? To track my personal match history, identify patterns like the best times of day or week to play, and see whether I’m actually improving over time. Along the way, I got to apply skills in API integration, data wrangling, and front-end visualization—all in Python.

### What I Wanted to Analyze

I wanted to understand:

- ✅ My total matches, wins, losses, and winrate
- 🏆 My most successful heroes
- 📅 Which days of the week I perform best
- ⏰ What days are the most effective to play

---

### 🔗 Getting Data from OpenDota

OpenDota provides a free API where you can get public match data based on your Steam ID. Here's how I pulled the data:

```python
import requests, json
from datetime import datetime

class DotaApi:
	
	def __init__(self, player_id):
		self.base_url = "https://api.opendota.com"
		self.player_id = player_id
	
	def get_matches(self):
		url = f"{self.base_url}/api/players/{self.player_id}/matches"
		payload = {}
		headers = {}
		response = requests.request("GET", url, headers=headers, data=payload)
		data = response.json()
		return data
	
	def get_heroes(self):
		url = f"{self.base_url}/api/heroes"
		payload = {}
		headers = {}
		response = requests.request("GET", url, headers=headers, data=payload)
		data = response.json()
		return data
```

Once the data is fetched, I processed it into metrics like total matches, winrate, most played heroes, and grouped match outcomes by day of the week.
### 📦 Streamlit: The Perfect Fit for Personal Dashboards

Streamlit lets you build beautiful dashboards in Python without the need for frontend code. It’s ideal for quick data apps like this.
### Visualizing Metrics
**`st.metric`** — to display key stats like winrate, total matches, and hero success rates in a quick-glance format.

```python
col1, col2, col3, col4 = st.columns(4)

with col1:
	option = st.selectbox(
	"Select Game Mode Info",
	("All", "Ranked", "Normal"),
)

data_win = get_winrate(username, option)
col2.metric("🎮 Total Matches", data_win["total_matches"])
col3.metric("✅ Wins", data_win["wins"])
col4.metric("❌ Losses", data_win["losses"])
  

st.metric("📈 Winrate", f"{data_win["winrate"]:.2f}%", delta=f"{(data_win["winrate"] - 50):.2f}%")
```

### Visualizing Plotly Pie Chart
**Plotly Pie Chart** — to show the distribution matches in Radian and Dire by winrate, with a fully interactive and styled pie chart.

```Python
df = pd.DataFrame({
	'Side': ['Radiant', 'Dire'],
	'Wins': [data_win["radiant_wins"], data_win["dire_wins"]]
})
col1, col2, col3 = st.columns([1, 1, 2])
fig = px.pie(df, values='Wins', names='Side',
	color_discrete_sequence=['#2ecc71', '#e74c3c'],
	hole=0.3) # makes it a donut chart
  

fig.update_layout(
	showlegend=True,
	paper_bgcolor='rgba(0,0,0,0)', # transparent background
	plot_bgcolor='rgba(0,0,0,0)',
	font_color='white'
)

with col1:
	st.subheader("📊 Radian & Dire Winrate")
	st.plotly_chart(fig, use_container_width=True)
```

### Visualizing with Dataframe
**`st.dataframe`** — to let me explore raw stats in a sortable and searchable table to get my most successful heroes.

```python
df_heroes = pd.DataFrame.from_dict(data_win["most_successful_heroes"], orient="index")
df_heroes["winrate"] = (df_heroes["wins"] / df_heroes["matches"] * 100).round(2)
df_heroes = df_heroes.sort_values(by="wins", ascending=False)
with col2:
	st.subheader("🏆 Most Played Heroes")
	st.dataframe(df_heroes)
```

### 📈 Visualizing with Altair
**Altair Bar Chart** — to analyze winrates by day of the week and time, allowing me to understand when I perform best.

```python
df = pd.DataFrame([
{
	"Day": day,
	"Wins": stats["wins"],
	"Matches": stats["matches"],
	"Losses": stats["matches"] - stats["wins"],
	"Winrate": round(stats["wins"] / stats["matches"] * 100, 2)
}

for day, stats in data_win["days_data"].items()])
	day_order = ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"]
	df["Day"] = pd.Categorical(df["Day"], categories=day_order, ordered=True)
	df = df.sort_values("Day")
  
with col3:
	st.subheader("📊 Best Days to Play")
	# Create Altair bar chart
	chart = alt.Chart(df).mark_bar().encode(
	x=alt.X("Day", title="Day of the Week"),
	y=alt.Y("Winrate", title="Winrate (%)"),
	tooltip=["Day", "Winrate", "Wins", "Losses", "Matches"]
	).properties(
		title="Winrate by Day of the Week",
		width=500,
		height=300
	)
	st.altair_chart(chart, use_container_width=False)
```

### Final Result
A demo of the final program is live at https://rangerstats.veitnexus.com/ 
Github Repo: https://github.com/PizzaMGx/dotastats

![[Pasted image 20250605110417.png]]
---

### 📌 Conclusion

Building this Dota 2 stats dashboard with **Streamlit** and the **OpenDota API** was not only a fun side project, but also a valuable exercise in full-stack data handling. From fetching and processing raw JSON data, to designing intuitive visualizations with tools like Plotly and Altair, this project tied together several key programming skills: **API integration**, **data transformation**, and **frontend visualization**.

What I appreciate most is how quickly I was able to go from idea to a fully deployed, interactive dashboard—without needing to spin up a full frontend stack. Streamlit handled the UI elegantly, and with just Python, I could focus on insights rather than infrastructure.

Whether you're a data nerd, a Dota player, or both—this kind of personal project is a great way to learn, experiment, and even discover patterns in your own gameplay.

---

Let me know if you’d like the code or want help setting up your own version!

