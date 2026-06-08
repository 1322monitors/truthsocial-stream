# truthsocial-stream

Real-time Truth Social monitor in Python. Streams new truths, retruths and
quote chains for the accounts you track, over a WebSocket. No Truth Social
login, no scraping, no polling loop.

There's no official Truth Social API, so the options are basically: run a
scraper yourself (truthbrush etc.) and eat the polling latency + IP blocks, or
use a managed feed. This example uses the [1322](https://1322.io) Truth Social
feed which pushes posts as they're detected (a few hundred ms typically). Posts
from political accounts move prediction markets fast, so push beats polling here.

Background + comparison of the approaches:
https://1322.io/blog/truth-social-api-guide
Platform page: https://1322.io/platforms/truth

## run

```bash
pip install -r requirements.txt
API_KEY=your-key WS_URL=wss://truth.1322.io/your-ws-path python main.py
```

## event shape

```json
{
  "platform": "truth",
  "eventType": "post",
  "handle": "someaccount",
  "content": "...",
  "isRepost": false,
  "quotedPost": { "handle": "other", "text": "..." },
  "timestamp": "2026-06-12T12:00:00Z"
}
```

Pair it with a news feed if you trade on this — a truth corroborated by a
headline within seconds is a much stronger signal than one alone.
