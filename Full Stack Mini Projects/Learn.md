The most dangerous salary in the world is ₹5 LPA. It is enough to survive. It is enough to pay rent. So you stop running. You stop learning. You settle.

You stop learning after office hours.
You stop opening LeetCode.
You stop thinking about system design.

And one day you wake up with:

- 4–5 years of experience
- Same tech stack
- Same salary band

Not because you’re bad. For SDEs, growth never comes from comfort.

It comes from intentional discomfort:

- Studying after work
- Building real projects
- Practicing DSA & system design
  Don’t wait for a layoff to wake you up.

In the last month, 

I cracked 3 offers 20L, 22L, and 26LPA.

I was happy. But days later… I wasn’t comfortable, so I started applying again.

Over the last three months, I have applied to over 180 companies. Got rejected. Got ghosted. But also cracked 5 offers.

I interviewed at Oracle → got 20 LPA offer
I interviewed at Deloitte → got 23 LPA offer
I interviewed at Walmart → Lost 28 LPA offer

After giving multiple interviews, one thing became clear: If you want to clear any Software Engineer interviews, the formula is simple: System Design and DSA

Got rejected in 8 straight interviews

But by the 17th, I had 5 offers in hand

First time: I froze, lost 21LPA offer
Second time: I smiled, got 26LPA offer

In one interview, I was asked: 

- Why does WhatsApp instantly show ‘typing…’ even if your friend is on the other side of the world?

I froze. I didn’t know the answer. And yes, I got rejected. But instead of moving on, I went deeper into the questions and learned.

In another interview, two weeks later, I faced the same question. I smiled and explained:

- As soon as a user presses a key, WhatsApp sends a tiny “typing” signal (not the text).
- That signal travels over a WebSocket to the nearest WhatsApp server.
- Using Redis Pub/Sub, the event is broadcast to the server where the other person’s connection is active.
- That server pushes the event instantly, so within ~200ms, the “typing…” status appears.

These events(packets) are extremely lightweight, which is why even on 2G networks, WhatsApp still feels real-time.

No matter if you have 1, 2, or 5 years of experience.

Truth is:

If you are giving an interview at any good product-based company or MNCs, 3-5 rounds are just:

- DSA, Development (2 to 3 rounds), and 
- System Design (1 to 2 rounds)
