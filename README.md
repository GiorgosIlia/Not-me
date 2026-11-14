# Δεν είμαι! / Not Me! — Party Games (version 2.3.1)

Two online party games, **Στο Περίπου / Ballpark** and **Impostor**, in **Greek and English**. The app is called **«Δεν είμαι!»** in Greek and **"Not Me!"** in English, and the name switches with the language. One person creates a room and sends the link, and everyone plays from their own phone. There's no database and nobody needs an account: **the host's phone runs the room**, and the other phones connect directly to it.

## Files

| File | What it is |
|---|---|
| `index.html` | The whole app |
| `config.js` | Optional: settings for a relay (TURN) server, only if some players can't connect (see Troubleshooting). Leave it as it is. |

## 1. Put it online (5 minutes, free)

The app must be opened from a real **https** web address. Sending people the file itself won't work.

**Netlify Drop (easiest)**
1. Go to **https://app.netlify.com/drop** and sign up for free (so the site stays up permanently).
2. Drag this whole folder onto the page.
3. You get a link like `https://something.netlify.app`. In Netlify you can rename it (Site configuration → Change site name), e.g. `parea-games.netlify.app`.

To update the app later, drag the new folder onto the same site (Deploys → drag and drop).

*(GitHub Pages or Firebase Hosting work just as well. Any static hosting with https is fine.)*

## Try it alone first

On the start screen tap **🤖 Δοκίμασε με bots / Try with bots**. You get a room with 3 computer players right on your phone, and it works even without internet. Bots answer questions and vote by themselves (they don't give clues out loud, so press *Vote now* when you're ready).

## 2. Test it once

1. Open the link on two phones, both on the **same Wi-Fi**. One creates a room and the other joins with the code. This should work right away.
2. Then switch one phone to **mobile data** and try again. If it connects, your carriers are fine. If not, see Troubleshooting.

## 3. Play

1. Open the link, type your name, and tap **Δημιούργησε δωμάτιο**. You're the host 👑.
2. Tap **📤 Στείλε σύνδεσμο** and send it to the group. Friends open it, type their name and they're in (or they type the 4-letter code).
3. The host picks the game. Everyone plays from their own phone.

**The host's phone is the server**, so:
- Keep the app open and in front, and don't lock the screen. The app asks the phone to keep the screen on, but don't switch to other apps for long.
- If the host's page reloads by accident, it reopens the same room and everyone reconnects by themselves.
- If the host taps **Έξοδος**, the room closes for everyone.
- If a player loses connection, the game doesn't wait for them, and they reconnect automatically.

## Languages

- The app starts in Greek on Greek phones and in English everywhere else. Players can switch any time with the 🇬🇷/🇬🇧 buttons on the start screen, or the ΕΛ/EN button at the top during a game.
- **Mixed groups work:** each phone shows the questions, the secret word and all messages in its own language, in the same room. A Greek player and an English player get the same question, each in their own language.
- All 55 questions and all 140 Impostor words exist in both languages.

## How it works (in short)

- Phones talk to each other over **WebRTC** (encrypted). The free **PeerJS** matchmaking server only introduces the phones to each other at the start. Game data goes directly between phones.
- The host's phone keeps all the game data and only sends each player what they're allowed to see. The Impostor's phone never receives the secret word, and nobody receives the correct answer or the other players' ranges before the reveal.
- **Version check:** every phone reports its version when it joins. If a player's version doesn't match the host's (e.g. someone still has 2.0.0 open, or an old app from the store), they see a "please update" message instead of a broken game. A future Android app built from the same code will join the same rooms as the website.

## Troubleshooting

**"Δεν βρέθηκε ενεργό δωμάτιο"**: check the code, and make sure the host still has the app open.

**Some players can't connect on 4G/5G (Wi-Fi works):** a few mobile networks block direct phone-to-phone connections. Quick fix: that player switches to Wi-Fi. Permanent fix: sign up for a **TURN relay** service, put its address and login in `config.js` (the format is shown in the file), and upload the folder again. You can also send the details to Claude and it will add them.

**Nobody can connect at all:** the free PeerJS matchmaking server may be temporarily down. Try again later. If it happens often, you can run your own copy on free hosting (ask Claude for the steps).

## Next steps (ideas)

- Android app for the Play Store (same code, same rooms as the website)
- More questions and word categories, a solo quiz mode
- Ads and a Premium unlock (in the Android app)
