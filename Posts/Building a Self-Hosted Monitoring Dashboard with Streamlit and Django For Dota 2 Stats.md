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
Ever wondered when you play your best games of Dota 2? Whether you're improving over time? Or which heroes bring you the highest winrate? I recently set out to answer those questions using Streamlit and OpenDota, and the result was a fun self-hosted dashboard that shows my gameplay statistics visually and interactively.

In this post, I’ll walk you through how I built it — from collecting the data to building the visualizations — and how you can build your own.
### 📊 What I Wanted to Analyze

I wanted to understand:

- ✅ My total matches, wins, losses, and winrate
    
- 🏆 My most successful heroes
    
- 📅 Which days of the week I perform best
    
- ⏰ What times are most effective for me to play (coming soon)
    

---

### 🔗 Getting Data from OpenDota

OpenDota provides a free API where you can get public match data based on your Steam ID. Here's how I pulled the data:

```python
import requests

def get_player_matches(account_id, limit=1000):
    url = f"https://api.opendota.com/api/players/{account_id}/matches?limit={limit}"
    response = requests.get(url)
    return response.json()
```

Once the data is fetched, I processed it into metrics like total matches, winrate, most played heroes, and grouped match outcomes by day of the week.
### 📦 Streamlit: The Perfect Fit for Personal Dashboards

Streamlit lets you build beautiful dashboards in Python without the need for frontend code. It’s ideal for quick data apps like this.

Here’s a sample of the data I prepared for visualizing weekly performance:

```
{
    "Monday": {"Matches": 300, "Wins": 210},
    "Tuesday": {"Matches": 250, "Wins": 140},
    ...
}
```

```python
import pandas as pd

df = pd.DataFrame([
    {
        "Day": day,
        "Wins": stats["Wins"],
        "Matches": stats["Matches"],
        "Losses": stats["Matches"] - stats["Wins"],
        "Winrate": round(stats["Wins"] / stats["Matches"] * 100, 2)
    }
    for day, stats in data.items()
])
```

### 📈 Visualizing with Altair

Using Altair, I built an interactive bar chart that shows winrate per day, with tooltips for details:

```python
import altair as alt
import streamlit as st

chart = alt.Chart(df).mark_bar().encode(
    x="Day",
    y="Winrate",
    tooltip=["Day", "Winrate", "Wins", "Losses", "Matches"]
).properties(
    title="Winrate by Day of the Week",
    width=500,
    height=300
)

st.altair_chart(chart)
```

This way, I could hover over each day and immediately see how many matches I played, how many I won, and what the winrate was.

---

### 🦸 Most Successful Heroes

Using the same approach, I displayed my most successful heroes in another bar chart, showing how often I picked them and their winrate. This helped me see which heroes I truly perform well with (and which I should maybe retire 😅).

---

### 🧠 Insights So Far

- I have a noticeably better winrate mid-week than on weekends.
    
- Certain heroes consistently give me better results (even if they’re not always the meta pick).
    
- My overall performance is more stable than I expected, but there are definitely days where I tilt.
    

---

### 🛠 What’s Next?

I plan to:

- Add heatmaps for **best time of day to play**
    
- Track improvement across **patches**
    
- See correlation between **match duration and winrate**
    
- Auto-refresh the dashboard using OpenDota data every few days
    

---

### 📌 Conclusion

Building this dashboard was not only helpful to improve at Dota 2, but also a great exercise in working with data, APIs, and visualization tools. Streamlit made it fast to iterate and beautiful to use.

If you're a gamer who codes — or a data analyst who games — give it a try. Whether it’s Dota 2, League of Legends, or even chess.com data, you can build something awesome with just a bit of Python.

---

Let me know if you’d like the code or want help setting up your own version!

> 💬 _You can view the project and more on [my GitHub](#)_
