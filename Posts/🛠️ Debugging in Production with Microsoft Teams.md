---
weight: 4
title: 🛠️ Debugging in Production with Microsoft Teams
date: 2025-07-22
draft: false
author: Vincent
description: 🛠️ Debugging in Production with Microsoft Teams
tags:
  - IT
categories:
  - IT
---
### 👨‍💻 How to Use a Python Decorator for Real-Time Alerts

When your application hits production, **visibility** becomes critical. Whether it's a flaky scheduled job, a broken API call, or a user-facing web endpoint throwing 500s — you need to know *now*, not when someone files a bug report.

## 🎯 Goal

In this post, I'll walk you through how I:

- Set up a **Microsoft Teams workflow channel**
- Built a flexible Python `@notify_on_error` decorator
- Automatically send alerts to Teams whenever something fails

---

## 🪛 Step 1: Create a Teams Workflow Channel

1. Go to your **Microsoft Teams** workspace.
2. Select or create a channel where you want alerts.
3. Click the `...` next to the channel → **Connectors**.
4. Add the **Incoming Webhook** connector.
5. Name it (e.g., `Prod Alerts`) and copy the generated **Webhook URL**.

Now you've got a URL where you can POST messages to land directly in your Teams channel 🎉.

---

## 🧰 Step 2: The `@notify_on_error` Decorator

Here’s a simple version of the decorator I use. It takes a `context` parameter (e.g. `"web"`, `"job"`, `"api"`) and notifies Teams if the wrapped function fails.

```python
import requests
import traceback
from functools import wraps

TEAMS_WEBHOOK_URL = "https://outlook.office.com/webhook/..."  # 👈 Replace with your own

def notify_on_error(context: str = "general"):
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            try:
                return func(*args, **kwargs)
            except Exception as e:
                tb = traceback.format_exc()
                payload = {
                    "text": (
                        f"🚨 **{context.upper()} ERROR**\n\n"
                        f"**Function**: `{func.__name__}`\n"
                        f"**Time**: {now}\n\n"
                        f"```\n{tb}\n```"
                    )
                }
                requests.post(TEAMS_WEBHOOK_URL, json=payload)
                raise
        return wrapper
    return decorator
```

## 🎁 Bonus Tips

- Add Slack-style formatting or color with Teams Adaptive Cards if you want fancier messages.
    
- Use different webhook URLs per environment or function type for better filtering.

## 🧭 Final Thoughts

Monitoring errors directly in Teams helps me:

✅ Respond faster  
✅ Avoid context switching  
✅ Collaborate on fixes with my team in real-time

Give it a try and watch your **mean time to detection** drop! ⏱️