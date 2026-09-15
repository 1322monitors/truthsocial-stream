# truthsocial-stream

Real-time Truth Social monitor in Python: streams new truths, retruths and quote chains for the accounts you track, over a WebSocket, with no Truth Social login and no polling loop on your side. Since August 1, 2026 there is an official Truth Social API: Trump Media's Truth API, a licensed institutional feed of about 10 of the platform's highest-ranking accounts with an archive back to 2022 (Fortune reported on August 12, 2026 that more than ten customers pay $60,000-$100,000 per month). It is not a public self-serve developer API and does not cover arbitrary accounts. For any account you choose, the options are still a scraper you maintain yourself or a managed feed; this example uses 1322's independent Truth Social feed, which typically delivers in 150-250ms (around 50ms average on the dedicated @realDonaldTrump and @WhiteHouse priority delivery), with plans from $300 per month. Maintained by the 1322 team.

Posts from political accounts move prediction markets fast, so push beats polling here.

Background + comparison of the approaches:
https://1322.io/blog/truth-social-api-guide
Platform page: https://1322.io/platforms/truth
Tracking one high-signal account (e.g. Trump) in real time: https://1322.io/track/trump-truth-social

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

## Related

- [1322-python](https://github.com/SisoSol/1322-python) - async Python client for every 1322 feed
- [prediction-market-router](https://github.com/SisoSol/prediction-market-router) - keyword match + webhook router
- [social-monitor-examples/truthsocial](https://github.com/SisoSol/social-monitor-examples/tree/main/truthsocial) - the minimal consumer
