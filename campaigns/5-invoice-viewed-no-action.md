# Campaign: Invoice Viewed - No Action After 2 Hours

**Trigger:** Prospect opens/views the quote but doesn't accept or respond within 2 hours

**Objective:** Address hesitation immediately, uncover objections, create urgency to close

**Timeline:** 3 high-intensity touchpoints over 48 hours (then merge back into regular Invoice Sent sequence)

---

## Message 1: Immediate Check-In (2 hours after view)

### EMAIL
**Subject:** Quick question about your quote

Hi [First Name],

I saw you opened your roof quote earlier – thanks for taking a look!

**Quick question:** Was everything clear?

Sometimes prospects have questions but aren't sure what to ask, so here are the most common ones:

❓ **"Can I see examples of similar projects?"**
→ Yes! Check out our [PROJECT_LINK] (Norman Park used same COLORBOND® Surfmist)

❓ **"What's included in the price?"**
→ Everything: materials, labor, old roof removal, cleanup, warranty. No hidden fees.

❓ **"How long will it take?"**
→ [PROJECT_DURATION] days, weather permitting. We protect your home throughout.

❓ **"When can you start?"**
→ Next available slot: [START_DATE_OPTION]

**Not one of these?** Just hit reply and ask me anything. I'm here to help, not pressure you.

Or if you're ready to move forward, just reply "YES" and I'll send the deposit details to lock in your spot.

Cheers,
Luke
0412 517 411

---

### SMS
Hi [First Name], saw you checked out your quote! Questions? I'm around. Call me: 0412 517 411 or reply YES if ready to book - Luke

---

## Message 2: Objection Anticipation (12 hours after view)

### EMAIL
**Subject:** Is one of these holding you back?

Hi [First Name],

Following up on your quote from yesterday.

You opened it, which tells me you're interested... but something's making you hesitate.

**Let me guess what might be going through your head:**

**"I need to get other quotes"**
Smart move. But here's what to ask other contractors:
- Are YOU licensed (not your subcontractors)?
- What's the factory warranty on materials?
- Who's actually on site doing the work?
- Can I see your QBCC license?

We check all those boxes. Some won't.

**"The price seems high"**
Fair. But ask yourself: What's the cost of doing this twice because you went cheap?

We use premium COLORBOND® steel with up to 20-year factory warranty. Our roofs outlast the cheaper stuff by decades.

**"I need to think about it"**
Totally understand. But thinking has a cost too:

→ Every week of Queensland weather is another week of risk
→ Our schedule fills up (especially approaching storm season)
→ Procrastination often leads to emergency repairs (way more expensive)

**"I'm not sure about the timeline"**
We're flexible. If the dates don't work, let's find ones that do.

**Real talk:** If none of these are the issue, what is?

Just reply and tell me what's actually on your mind. Maybe I can help. Maybe I can't. But at least you'll have clarity.

Fair?

Luke
Frost Roofing
0412 517 411

P.S. If you've already accepted another quote, no worries – just let me know so I can close out your file and free up your slot.

---

### SMS
[First Name] - Be honest: What's holding you back? Price? Timeline? Something else? Let's talk it through: 0412 517 411 - Luke

---

## Message 3: Final Push - Scarcity + Empathy (48 hours after view)

### EMAIL
**Subject:** Your spot is slipping away – [Address]

Hi [First Name],

I'll be direct: **I need to know if you're moving forward.**

Here's why:

We have **[X] homeowners** waiting for our next available slots, and I've been holding one for you. But I can't hold it much longer.

**If you're in, let's do this:**
Reply YES and I'll send deposit details today. We lock in [START_DATE], protect your home before storm season, and you get peace of mind.

**If you're out, that's okay:**
Just let me know so I can give your spot to the next family. No hard feelings.

**If you're undecided:**
Call me in the next 24 hours: **0412 517 411**

Let's talk through whatever's making you hesitate. Worst case? You get clarity. Best case? You get a roof that protects your family for 20+ years.

**But I need to hear from you by [DEADLINE - e.g., "5pm tomorrow"].**

After that, I'm releasing your spot to the waitlist.

I started Frost Roofing because I was sick of seeing homeowners get burned by cowboys and patch-job contractors.

**You seem like someone who values quality** (you're still reading this email, after all).

Don't let indecision cost you the protection your home deserves.

Ball's in your court,
Luke
Frost Roofing
0412 517 411

---

P.S. Here's what Adam said after his roof was done:
*"Luke and his team were very professional. Takes pride in his work and will go above and beyond with anything asked. My new roof looks awesome."*

He almost went with a cheaper contractor. I'm glad he didn't.

---

### SMS
[First Name] - Need answer by [TIME] today: Are you in? Reply YES to lock your spot or call 0412 517 411. After that, giving your slot to waitlist - Luke

---

## Implementation Notes

**Timing:**
- Message 1: 2 hours after quote first viewed
- Message 2: 12 hours after quote first viewed
- Message 3: 48 hours after quote first viewed

**Critical Requirements:**

**View Tracking:**
- Must have email tracking or proposal software that logs "opens"
- Only trigger if opened but no response/action taken
- Don't trigger if they've replied with questions (they're engaged)

**Personalization Variables:**
- [First Name]
- [Address] / [Property Address]
- [PROJECT_LINK] – Similar completed project
- [PROJECT_DURATION] – Estimated days for completion
- [START_DATE_OPTION] – Next available start date
- [X] – Actual number of waitlist prospects (be truthful)
- [DEADLINE] – Specific time to respond
- [TIME] – Today's deadline

**Tone Calibration:**
- Message 1: Helpful, consultative
- Message 2: More direct, objection-focused
- Message 3: Urgent but not desperate, scarcity-driven

**Response Handling:**

**"YES" / Ready to proceed:**
- Immediate response with deposit invoice
- Remove from this sequence
- Move to deposit/onboarding flow

**Objection/Question:**
- Immediately call (don't just email back)
- This is hot lead moment – phone >>> email
- Address concern, close on call if possible

**"Need more time":**
- Ask specific date to follow up
- Exit this sequence
- Re-enter regular Invoice Sent sequence at Message 3

**"Too expensive":**
- Phone call required
- Explore budget concerns
- Payment plan option if applicable
- Don't discount unless genuinely necessary

**No response to all 3:**
- Exit to regular Invoice Sent sequence (continue at Message 4)
- They've seen the quote, so don't start from scratch

**Exit Criteria:**
- Deposit paid → Customer onboarding
- Explicit "not interested" → Tag as lost, ask for feedback
- After Message 3 no response → Back to Invoice Sent sequence Day 7 message
- Lost to competitor → Request to understand why

**Special Scenarios:**

**Multiple Views (They keep opening it):**
- Sign of interest but uncertainty
- Could mean they're showing family/spouse
- Adjust Message 2 to acknowledge: "I noticed you've looked at the quote a few times..."

**Viewed on mobile vs desktop:**
- Mobile = might be quick glance, lower intent
- Desktop = more serious review
- Consider sending Message 1 later if only mobile view

**Viewed but not downloaded:**
- May indicate technical issues
- Include direct link to download in Message 1

**Critical Success Factors:**
1. **Real urgency** – Don't fake scarcity, use actual schedule
2. **Phone prioritization** – Any engaged response should trigger call
3. **Empathy with firmness** – You care about their decision but need answer
4. **Respect the timeline** – This is compressed sequence, don't drag it out

**A/B Test Ideas:**
- Message 3 deadline (24hr vs 48hr)
- Scarcity frame (schedule vs waitlist vs material availability)
- Luke's signature vs "Luke & Team"
- Video message vs text-only in Message 2

**Metrics to Track:**
- View-to-response rate by message
- Most effective objection handling in Message 2
- Conversion rate from "viewed" to "deposited"
- Time between view and deposit (compressed timeline = good)

**Pro Tips:**
- This sequence is more aggressive than others – that's intentional
- They've already invested time (site visit, quote review) – capitalize on it
- Some prospects need push to overcome inertia
- Balance: Assertive ≠ Desperate
- After Message 3, ease off or you risk burning goodwill
