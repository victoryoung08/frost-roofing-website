# Campaign: New Lead - Scheduled Call

**Trigger:** Lead schedules their preliminary quote call

**Objective:** Confirm appointment, reduce no-shows, build excitement and trust before the call

**Timeline:** 3 touchpoints (Immediate, Day Before, 1 Hour Before)

---

## Message 1: Booking Confirmation (Immediate)

### EMAIL
**Subject:** Your Frost Roofing Call is Confirmed – [Date] at [Time]

Hi [First Name],

Great news – your preliminary quote call is locked in!

**Call Details:**
📅 **Date:** [Day], [Date]
⏰ **Time:** [Time] AEST
📞 **We'll call you on:** [Phone Number]
⏱️ **Duration:** 10-15 minutes

**What to expect on the call:**

1. I'll ask about your current roof (age, material, any issues)
2. We'll discuss your goals and timeline
3. I'll use satellite imagery to provide a ballpark quote
4. If it makes sense, we'll schedule an in-person detailed quote

**To make the most of our time, please have ready:**
- Your address (for satellite view)
- Approx. year your home was built
- Any known roof issues (leaks, damage, etc.)
- Your ideal timeframe

**Need to reschedule?** No worries – just click here: [RESCHEDULE LINK]

Looking forward to chatting soon!

Cheers,
Luke
Frost Roofing
0412 517 411

---

P.S. While you wait, check out our recent Norman Park project: [WEBSITE PROJECT LINK]

---

### SMS
Hi [First Name]! Your Frost Roofing call is set for [Date] at [Time]. We'll call [Phone]. Have your address handy. See you then! - Luke 0412 517 411

---

## Message 2: Day Before Reminder

### EMAIL
**Subject:** Tomorrow: Your Frost Roofing Quote Call at [Time]

Hi [First Name],

Just a quick reminder – we're chatting tomorrow!

**Call Time:** [Day] at [Time] AEST
**I'll call:** [Phone Number]

To prepare, I've already pulled up your property on our satellite imaging system. All I need from you is:
- Confirmation of your property address
- Any specific concerns or goals
- Your rough timeline

**Why homeowners choose Frost Roofing:**
✓ Transparent pricing (no hidden costs)
✓ QBCC Licensed professionals
✓ Factory warranty up to 20 years
✓ Fast turnaround (typically start within 14 days)

Still good for tomorrow?

If you need to reschedule, just hit reply or use this link: [RESCHEDULE LINK]

See you tomorrow!

Luke
Frost Roofing

---

### SMS
Hi [First Name], reminder: I'll call you tomorrow at [Time] for your roof quote. Still good to chat? Reply YES to confirm or call me to reschedule: 0412 517 411 - Luke

---

## Message 3: 1 Hour Before Call

### EMAIL
**Subject:** Calling you in 1 hour – [Time] today

Hi [First Name],

This is it – I'll be calling you in about an hour at [Time].

I've got your details ready and looking forward to discussing your roofing project.

**Quick checklist:**
- ✓ Have your phone handy
- ✓ Find a quiet spot for our chat
- ✓ Have your address ready to confirm
- ✓ Any questions you want to ask

If something's come up and you can't make it, give me a quick call: 0412 517 411

Otherwise, talk to you at [Time]!

Luke
Frost Roofing

---

### SMS
[First Name], calling you in 1 hour at [Time]! Make sure you're near your phone. See you soon - Luke from Frost Roofing

---

## Implementation Notes

**Timing:**
- Message 1: Immediate (within 1 minute of booking)
- Message 2: 24 hours before call (e.g., if call is Tuesday 2pm, send Monday 2pm)
- Message 3: 1 hour before call

**Personalization Variables:**
- [First Name]
- [Date] / [Day] / [Time]
- [Phone Number]
- [RESCHEDULE LINK]
- [WEBSITE PROJECT LINK]

**Special Considerations:**
- If call is within 24 hours of booking, skip Message 2
- If call is within 2 hours of booking, skip Messages 2 & 3
- Use local time (AEST/AEDT) for all times

**Response Handling:**
- "YES" reply to SMS = Send thank you + "Looking forward to it!"
- Reschedule request = Update calendar and trigger this sequence again with new time
- No response = Proceed to call as scheduled

**After Call Actions:**
- If attended → Move to appropriate sequence based on outcome
- If no-show → Trigger "No Show" sequence
- If rescheduled on call → Update and restart this sequence

**Pro Tips:**
- Include calendar invite (ICS file) in Message 1 email
- Add 2-click reschedule option (don't make them work hard)
- Keep SMS character count under 160 for single message
