# Frost Roofing Email & SMS Campaign Overview

## Campaign Strategy

This nurture campaign system is designed to guide leads through Frost Roofing's sales pipeline with personalized, timely communications that build trust, address objections, and drive conversions.

---

## Campaign Sequences

### 1. [New Lead Opt-In](./1-new-lead-opt-in.md)
**Trigger:** Lead starts Typeform but doesn't schedule or complete
**Duration:** 7 days (3 touchpoints)
**Goal:** Recover abandoned leads, schedule preliminary call
**Tone:** Helpful, low-pressure, value-focused

**Key Tactics:**
- Immediate follow-up (5 min)
- Social proof and differentiation (Day 3)
- Soft close with exit option (Day 7)

---

### 2. [New Lead - Scheduled Call](./2-new-lead-scheduled-call.md)
**Trigger:** Lead books preliminary quote call
**Duration:** Until call time (3 touchpoints)
**Goal:** Reduce no-shows, build anticipation, ensure preparedness
**Tone:** Professional, organized, excitement-building

**Key Tactics:**
- Immediate booking confirmation with calendar invite
- Day-before reminder with prep checklist
- 1-hour reminder to ensure availability

---

### 3. [Initial Call - No Show](./3-initial-call-no-show.md)
**Trigger:** Lead misses scheduled call
**Duration:** 5 days (4 touchpoints)
**Goal:** Reschedule call, recover opportunity
**Tone:** Understanding → Direct → Final outreach

**Key Tactics:**
- Instant follow-up (5 min post-call)
- Urgency and value reminder (4hrs, Day 2)
- Social proof + last chance (Day 2, Day 5)
- Empathetic but firm closing message

---

### 4. [Invoice Sent](./4-invoice-sent.md)
**Trigger:** Detailed quote sent after in-person visit
**Duration:** 7 days (4 touchpoints)
**Goal:** Drive quote acceptance, address concerns, close deal
**Tone:** Consultative → Educational → Urgent

**Key Tactics:**
- Professional quote delivery with clear next steps
- Value reinforcement + FAQ (Day 1)
- Social proof + schedule urgency (Day 3)
- Objection handling + respect close (Day 7)

---

### 5. [Invoice Viewed - No Action](./5-invoice-viewed-no-action.md)
**Trigger:** Quote opened but no response within 2 hours
**Duration:** 48 hours (3 touchpoints)
**Goal:** Address immediate hesitation, create urgency to close
**Tone:** Helpful → Assertive → Urgent

**Key Tactics:**
- Immediate check-in with FAQ (2hrs)
- Objection anticipation and direct ask (12hrs)
- Scarcity + empathy close (48hrs)
- Then merge back to Invoice Sent sequence

**Note:** This is a high-intensity micro-sequence that runs parallel to Invoice Sent for engaged-but-hesitant leads.

---

## Brand Voice & Messaging Guidelines

### Core Brand Attributes (Frost Roofing)
- **Family-owned:** Luke & Kirby, personal touch
- **Transparent:** Clear pricing, no surprises
- **Quality-focused:** Craftsmanship over patch jobs
- **Licensed & Certified:** QBCC, Master Builders QLD
- **Fast turnaround:** Typically 14 days to start
- **Long-term warranty:** Up to 20 years factory warranty
- **Local expertise:** Brisbane & Gold Coast specialists

### Tone Spectrum
- **Early stage (Opt-in, Scheduled):** Friendly, helpful, educational
- **Mid-stage (No-show, Invoice):** More direct, value-driven, professional
- **Late stage (Viewed, Final outreach):** Assertive, urgent, respectful

### Writing Style
- Short sentences and paragraphs
- Active voice
- Direct and honest (anti-salesy)
- Use questions to engage
- Personal pronouns (I, we, you)
- Local Queensland references (weather, storm season)

### What to Avoid
- Corporate jargon
- Over-promising
- Aggressive sales tactics
- Fake urgency or scarcity
- Generic contractor speak

---

## Technical Implementation

### Required CRM/Automation Features
1. **Email tracking** – Open rates, click tracking
2. **SMS integration** – Two-way communication
3. **Calendar integration** – Automated reminders based on appointment time
4. **Conditional logic** – Sequence switching based on actions
5. **Personalization** – Dynamic fields for name, address, amount, dates
6. **Multi-channel** – Coordinated email + SMS delivery

### Personalization Variables

**Universal:**
- `[First Name]`
- `[Phone Number]`
- `[Property Address]` / `[Address]`

**Sequence-Specific:**
- `[Time]` – Appointment time
- `[Date]` / `[Day]` – Appointment date
- `[QUOTE_AMOUNT]` – Quote dollar amount
- `[KEY_INCLUSIONS]` – Quote scope summary
- `[START_DATE_OPTION]` – Next available start date
- `[PROJECT_DURATION]` – Estimated job duration
- `[Month 1]`, `[Month 2]` – Schedule availability
- `[CALENDAR_LINK]` – Booking URL
- `[SHORT_LINK]` – Shortened URLs for SMS
- `[PROJECT_LINK]` – Similar project examples
- `[DEADLINE]` – Response deadline with specific time

### Sequence Flow Logic

```
FORM START
    ↓
Did they schedule?
    ├─ NO → [1. New Lead Opt-In]
    │         ↓
    │       Scheduled? → [2. Scheduled Call]
    └─ YES → [2. Scheduled Call]
                ↓
            Attended call?
                ├─ NO → [3. No Show]
                │         ↓
                │       Rescheduled? → [2. Scheduled Call]
                └─ YES → Call completed
                            ↓
                        Quote sent? → [4. Invoice Sent]
                            ↓
                        Quote opened?
                            ├─ YES (no action) → [5. Viewed - No Action]
                            │                      ↓
                            │                    48hrs → Back to [4. Invoice Sent]
                            └─ NO → Continue [4. Invoice Sent]
                                      ↓
                                  Deposit paid? → CUSTOMER (onboarding)
```

### Timing Best Practices

**Immediate triggers:**
- Form abandonment: 5 minutes
- Booking confirmation: 1 minute
- Missed call: 5 minutes
- Quote sent: Immediate
- Quote viewed: 2 hours

**Optimal send times (Brisbane/Gold Coast):**
- **Email:** 8-9am, 12-1pm, 5-6pm (AEST)
- **SMS:** 9-10am, 1-2pm (avoid dinner time 5-7pm)
- **Never:** Before 8am or after 8pm

**Day-of-week performance:**
- **Best:** Tuesday, Wednesday, Thursday
- **Good:** Monday, Friday morning
- **Avoid:** Friday afternoon, weekends (unless scheduled reminders)

---

## Success Metrics

### Sequence-Level KPIs

**1. New Lead Opt-In**
- Target: 25-35% reschedule rate
- Open rate: 40-50%
- Response rate: 15-20%

**2. Scheduled Call**
- Target: 85-90% show rate
- Confirmation rate: 90%+
- Day-before SMS response: 70%+

**3. No Show**
- Target: 40-50% recovery rate
- Re-book rate: 30-40%
- Dead lead rate: <50%

**4. Invoice Sent**
- Target: 30-40% close rate
- Quote-to-deposit time: <7 days avg
- Response rate: 60%+

**5. Invoice Viewed - No Action**
- Target: 50-60% conversion boost vs control
- Response within 48hrs: 40%+
- Close rate lift: +15-20%

### Overall Campaign Health
- **Lead-to-appointment:** 40-50%
- **Appointment-to-quote:** 70-80%
- **Quote-to-close:** 30-40%
- **Overall conversion:** 8-15% (form start to customer)

---

## A/B Testing Roadmap

### Phase 1: Subject Lines
- Urgency vs. Value
- Questions vs. Statements
- Personal (Luke) vs. Company name

### Phase 2: Message Length
- Short (100-150 words) vs. Long (300-400 words)
- Bullet lists vs. Paragraphs

### Phase 3: Sender Identity
- "Luke from Frost Roofing"
- "Frost Roofing"
- "Luke & Kirby"

### Phase 4: CTA Style
- Calendar link vs. "Reply YES"
- Phone-first vs. Email-first
- Single CTA vs. Multiple options

### Phase 5: Content Variations
- Social proof placement
- Objection handling approach
- Urgency framing (schedule vs. weather vs. price)

---

## Integration Checklist

**Before Launch:**
- [ ] CRM sequences built and tested
- [ ] Personalization variables mapped correctly
- [ ] Email templates mobile-responsive
- [ ] SMS character counts verified (<160 per message)
- [ ] Calendar integration working
- [ ] Tracking pixels/links functional
- [ ] Unsubscribe links present (emails)
- [ ] SPAM compliance (CAN-SPAM, Australian Spam Act)
- [ ] Phone numbers formatted correctly for SMS
- [ ] Response handling workflows defined
- [ ] Team trained on manual intervention points
- [ ] Fallback process for automation failures

**Weekly Monitoring:**
- [ ] Open/click rates by sequence
- [ ] Response rates and sentiment
- [ ] Conversion rates at each stage
- [ ] Bounce/unsubscribe rates
- [ ] Manual intervention frequency
- [ ] Average time-to-convert

---

## Response Handling Protocols

### Positive Responses
- **"YES" / "Ready"** → Send deposit invoice within 15 minutes
- **"Interested"** → Schedule call within 24 hours
- **Question** → Respond within 2 hours (business hours)

### Neutral Responses
- **"Need time"** → Ask specific follow-up date, set reminder
- **"Checking with spouse"** → Follow up in 48 hours
- **"Getting other quotes"** → Provide comparison checklist, follow up in 5 days

### Negative Responses
- **"Not interested"** → Ask why (feedback), tag as lost, pause sequences
- **"Too expensive"** → Phone call required, explore budget concerns
- **"Went elsewhere"** → Request feedback, wish them well
- **"Unsubscribe"** → Immediate removal, note reason if provided

### No Response
- **After final message** → Pause 90 days, then gentle re-engagement
- **Between messages** → Continue sequence as planned
- **Multiple sequences** → Don't stack – pause one

---

## Compliance & Best Practices

### Australian Spam Act 2003
- ✓ All emails include unsubscribe mechanism
- ✓ Identify sender clearly
- ✓ Include physical business address
- ✓ Accurate "From" information

### SMS Marketing Rules
- ✓ Only send to those who provided phone number
- ✓ Include business name in first message
- ✓ Provide opt-out method ("Reply STOP")
- ✓ Don't send outside 8am-8pm
- ✓ Keep messages relevant and infrequent

### CRM Data Handling
- ✓ Secure storage of personal information
- ✓ Clear privacy policy
- ✓ Data retention policy (delete after X months if no activity)
- ✓ Consent captured at form submission

---

## Continuous Improvement

### Monthly Review Process
1. **Pull metrics** for all sequences
2. **Identify drop-off points** in funnel
3. **Review response feedback** (categorize objections)
4. **Test one variable** per sequence
5. **Update copy** based on common questions
6. **Adjust timing** if needed
7. **Document learnings** for team

### Quarterly Deep Dive
- Customer interviews (why they chose Frost)
- Lost opportunity post-mortems (why they didn't)
- Competitive analysis (what others are doing)
- Seasonal adjustments (storm season messaging)
- Major copy refresh if needed

---

## Quick Start Guide

**To implement these campaigns:**

1. **Choose your platform** (HubSpot, ActiveCampaign, Mailchimp + Twilio, etc.)

2. **Set up sequences** in this order:
   - Start with Scheduled Call (easiest, highest ROI)
   - Then Invoice Sent (where money is made)
   - Then Opt-In (top of funnel)
   - Then No Show (recovery)
   - Finally Viewed (advanced)

3. **Map your triggers:**
   - Form abandonment webhook
   - Calendar booking confirmation
   - Quote sent timestamp
   - Quote opened tracking
   - Missed call log

4. **Test with internal team** before going live

5. **Launch with 10-20 leads** to validate flow

6. **Monitor daily** for first week

7. **Adjust based on feedback**, then scale

---

## Support & Questions

**Campaign Strategy:** Based on brief from `email-sms-lead-nurture-brief.md`
**Brand Voice:** Derived from Frost Roofing website (index.html, apply.html)
**Created:** Claude Code AI
**Last Updated:** [Current Date]

**For updates or questions about these campaigns:**
- Review website copy for any brand voice changes
- Monitor customer feedback and common objections
- Update sequences quarterly or when major business changes occur

---

**Remember:** These are templates. Personalize, test, and iterate based on your actual results. What works for one audience might not work for another. The goal is to start with best practices and refine based on data.
