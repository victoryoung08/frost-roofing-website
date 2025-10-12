# GoHighLevel Implementation Brief - Frost Roofing Lead Nurture System

## Project Overview

**Objective:** Build a complete automated lead nurture system in GoHighLevel (GHL) for Frost Roofing's sales pipeline, covering 5 key stages from form opt-in to invoice acceptance.

**Client:** Frost Roofing (Brisbane & Gold Coast Colorbond Roof Specialists)
**Pipeline:** Roofing quote to customer conversion
**Channels:** Email + SMS (multi-channel sequences)
**Timeline:** All campaigns documented in `/campaigns/` folder

---

## 1. Pipeline Setup

### Pipeline Name: "Roofing Sales Pipeline"

### Required Stages:

```
1. New Lead (Opt-In)
   ↓
2. Scheduled Call
   ↓
3. Call Completed - Preliminary Quote Given
   ↓
4. In-Person Quote Scheduled
   ↓
5. Detailed Quote Sent
   ↓
6. Quote Viewed
   ↓
7. Deposit Received / Won
   ↓
8. Lost / Dead Lead
```

### Stage Details:

**Stage 1: New Lead (Opt-In)**
- **Trigger:** Typeform submission (incomplete - didn't schedule or finish)
- **Goal:** Get them to schedule preliminary call
- **Automation:** Start "New Lead Opt-In" sequence
- **Move to next stage:** When they book a call via Calendly

**Stage 2: Scheduled Call**
- **Trigger:** Calendar appointment booked
- **Goal:** Ensure they show up for the call
- **Automation:** Start "Scheduled Call" sequence (confirmation + reminders)
- **Move to next stage:** After call is marked "completed" in calendar

**Stage 3: Call Completed - Preliminary Quote Given**
- **Trigger:** Manual move by Luke/Kirby after completing call
- **Goal:** Get them to agree to in-person detailed quote
- **Automation:** None (manual follow-up during call)
- **Move to next stage:** When in-person quote is scheduled

**Stage 4: In-Person Quote Scheduled**
- **Trigger:** In-person appointment booked
- **Goal:** Complete the site visit and send detailed quote
- **Automation:** Reminder sequence (similar to Scheduled Call)
- **Move to next stage:** When quote/invoice is sent

**Stage 5: Detailed Quote Sent**
- **Trigger:** Quote document sent via email or GHL
- **Goal:** Get deposit/acceptance
- **Automation:** Start "Invoice Sent" sequence
- **Move to next stage:** When quote is opened/viewed

**Stage 6: Quote Viewed**
- **Trigger:** Email tracking shows quote opened
- **Goal:** Immediate engagement to address hesitation
- **Automation:** Start "Invoice Viewed - No Action" micro-sequence
- **Move to next stage:** Deposit received OR back to Stage 5 after 48hrs

**Stage 7: Deposit Received / Won**
- **Trigger:** Deposit payment received
- **Goal:** Customer onboarding
- **Automation:** Welcome sequence (out of scope for this project)
- **Notes:** Final stage for won deals

**Stage 8: Lost / Dead Lead**
- **Trigger:** Manual move OR automated after final sequence message with no response
- **Goal:** Archive and potential re-engagement later
- **Automation:** None (or 90-day re-engagement sequence - optional)
- **Notes:** Track loss reason via tags

---

## 2. Custom Fields Required

### Contact Custom Fields:

**Basic Info:**
- `property_address` (Text) - Full property address
- `property_year_built` (Text) - Approximate year
- `roof_issues` (Text Area) - Known issues, damage, leaks
- `ideal_timeframe` (Dropdown) - Within 1 month, 1-3 months, 3-6 months, 6+ months
- `lead_source` (Dropdown) - Typeform, Phone, Referral, Other
- `roof_type_interest` (Dropdown) - Replacement, New Roof, Cladding, Skylights

**Quote Info:**
- `quote_amount` (Currency) - Total quote value
- `quote_sent_date` (Date) - When quote was sent
- `quote_viewed_date` (Date) - First time quote was opened
- `project_duration` (Text) - Estimated days to complete
- `start_date_option` (Date) - Next available start date offered

**Status Tracking:**
- `preliminary_quote_given` (Yes/No) - Did they get satellite quote?
- `no_show_count` (Number) - Track how many times they no-showed
- `last_contact_date` (Date) - Most recent interaction
- `loss_reason` (Dropdown) - Price, Timing, Competitor, No Response, Other

**Automation Tracking:**
- `opt_in_sequence_sent` (Yes/No)
- `scheduled_call_sequence_sent` (Yes/No)
- `no_show_sequence_sent` (Yes/No)
- `invoice_sequence_sent` (Yes/No)
- `invoice_viewed_sequence_sent` (Yes/No)

---

## 3. Calendar Integration

### Required Calendars:

**1. Preliminary Quote Call (Phone)**
- **Duration:** 15 minutes
- **Buffer:** 5 min before/after
- **Availability:** Mon-Fri 9am-5pm AEST
- **Booking Link:** To embed in emails/SMS
- **Notifications:**
  - Email to lead (confirmation)
  - SMS to lead (reminders)
  - Internal notification to Luke/Kirby

**2. In-Person Detailed Quote**
- **Duration:** 60 minutes
- **Buffer:** 15 min before/after
- **Availability:** Mon-Fri 9am-4pm AEST, Sat 9am-12pm
- **Booking Link:** To share after preliminary call
- **Notifications:** Same as above

### Calendar Automations Needed:

**On Appointment Booked:**
- Move pipeline stage to "Scheduled Call"
- Start "Scheduled Call Confirmation" workflow
- Send calendar invite (ICS file)

**24 Hours Before:**
- Send day-before reminder (Email + SMS)
- Wait for SMS confirmation

**1 Hour Before:**
- Send final reminder (Email + SMS)

**On No-Show:**
- Mark appointment as "no-show"
- Move to "New Lead" stage with tag "No-Show"
- Start "No Show" recovery workflow
- Increment `no_show_count` field

**On Completed:**
- Move to "Call Completed" stage
- Tag with "Preliminary Quote Given"
- Send internal notification to send detailed quote

---

## 4. Email & SMS Templates

### Template Naming Convention:
`[Sequence]-[Message#]-[Channel]`

Example: `OptIn-01-Email`, `OptIn-01-SMS`

### Templates to Create:

#### Sequence 1: New Lead Opt-In (3 emails, 3 SMS)
- `OptIn-01-Email` - Immediate Follow-Up
- `OptIn-01-SMS` - Immediate Follow-Up
- `OptIn-02-Email` - Value Reminder (Day 3)
- `OptIn-02-SMS` - Value Reminder (Day 3)
- `OptIn-03-Email` - Last Outreach (Day 7)
- `OptIn-03-SMS` - Last Outreach (Day 7)

**Source:** `/campaigns/1-new-lead-opt-in.md`

#### Sequence 2: Scheduled Call (3 emails, 3 SMS)
- `ScheduledCall-01-Email` - Booking Confirmation
- `ScheduledCall-01-SMS` - Booking Confirmation
- `ScheduledCall-02-Email` - Day Before Reminder
- `ScheduledCall-02-SMS` - Day Before Reminder (with confirmation request)
- `ScheduledCall-03-Email` - 1 Hour Before
- `ScheduledCall-03-SMS` - 1 Hour Before

**Source:** `/campaigns/2-new-lead-scheduled-call.md`

#### Sequence 3: No Show (4 emails, 4 SMS)
- `NoShow-01-Email` - Immediate Follow-Up
- `NoShow-01-SMS` - Immediate Follow-Up
- `NoShow-02-Email` - Value Reminder (4hrs later)
- `NoShow-02-SMS` - Value Reminder (4hrs later)
- `NoShow-03-Email` - Social Proof (Day 2)
- `NoShow-03-SMS` - Social Proof (Day 2)
- `NoShow-04-Email` - Final Outreach (Day 5)
- `NoShow-04-SMS` - Final Outreach (Day 5)

**Source:** `/campaigns/3-initial-call-no-show.md`

#### Sequence 4: Invoice Sent (4 emails, 4 SMS)
- `Invoice-01-Email` - Invoice Delivery
- `Invoice-01-SMS` - Invoice Delivery
- `Invoice-02-Email` - Value Reinforcement (Day 1)
- `Invoice-02-SMS` - Value Reinforcement (Day 1)
- `Invoice-03-Email` - Social Proof + Urgency (Day 3)
- `Invoice-03-SMS` - Social Proof + Urgency (Day 3)
- `Invoice-04-Email` - Last Outreach (Day 7)
- `Invoice-04-SMS` - Last Outreach (Day 7)

**Source:** `/campaigns/4-invoice-sent.md`

#### Sequence 5: Invoice Viewed - No Action (3 emails, 3 SMS)
- `InvoiceViewed-01-Email` - Immediate Check-In (2hrs)
- `InvoiceViewed-01-SMS` - Immediate Check-In (2hrs)
- `InvoiceViewed-02-Email` - Objection Anticipation (12hrs)
- `InvoiceViewed-02-SMS` - Objection Anticipation (12hrs)
- `InvoiceViewed-03-Email` - Final Push (48hrs)
- `InvoiceViewed-03-SMS` - Final Push (48hrs)

**Source:** `/campaigns/5-invoice-viewed-no-action.md`

### Template Requirements:

**All Email Templates Must Have:**
- Mobile-responsive design
- Unsubscribe link (footer)
- Business address in footer
- From: "Luke from Frost Roofing" <admin@frostroofing.com.au>
- Reply-to: admin@frostroofing.com.au
- Merge fields properly mapped
- Tracking pixel enabled

**All SMS Templates Must Have:**
- Character count under 160 (single message) or clearly segmented
- Business identification in first message
- Opt-out instruction where appropriate
- Short links for URLs
- Merge fields properly mapped

### Personalization/Merge Fields in Templates:

```
{{contact.first_name}}
{{contact.phone}}
{{contact.property_address}}
{{contact.quote_amount}}
{{contact.project_duration}}
{{contact.start_date_option}}
{{appointment.start_time}}
{{appointment.date}}
{{appointment.day}}
{{calendar_link}}
{{reschedule_link}}
{{quote_document_link}}
```

---

## 5. Workflow Automations

### Workflow 1: "New Lead Opt-In Sequence"

**Trigger:** Contact enters pipeline stage "New Lead (Opt-In)"

**Conditions:**
- `opt_in_sequence_sent` = No
- No appointment scheduled

**Actions:**
1. Wait 5 minutes
2. Send `OptIn-01-Email`
3. Wait 2 minutes
4. Send `OptIn-01-SMS`
5. Update `opt_in_sequence_sent` = Yes
6. Update `last_contact_date` = Today
7. Wait 3 days
8. Send `OptIn-02-Email`
9. Wait 2 minutes
10. Send `OptIn-02-SMS`
11. Wait 4 days
12. Send `OptIn-03-Email`
13. Wait 2 minutes
14. Send `OptIn-03-SMS`
15. Wait 1 day
16. If still no response: Tag as "Cold Lead" and move to "Lost/Dead Lead" stage

**Exit Conditions:**
- Appointment booked (move to Workflow 2)
- Contact replies (stop automation, manual follow-up)
- Contact unsubscribes

---

### Workflow 2: "Scheduled Call Confirmation & Reminders"

**Trigger:** Appointment booked (Preliminary Quote Call)

**Conditions:**
- Appointment status = Scheduled
- `scheduled_call_sequence_sent` = No

**Actions:**
1. Immediately send `ScheduledCall-01-Email` with calendar invite
2. Wait 2 minutes
3. Send `ScheduledCall-01-SMS`
4. Update `scheduled_call_sequence_sent` = Yes
5. Move pipeline to "Scheduled Call" stage
6. Wait until [24 hours before appointment]
7. Send `ScheduledCall-02-Email`
8. Wait 2 minutes
9. Send `ScheduledCall-02-SMS` (with confirmation request)
10. Wait until [1 hour before appointment]
11. Send `ScheduledCall-03-Email`
12. Wait 2 minutes
13. Send `ScheduledCall-03-SMS`

**Exit Conditions:**
- Appointment canceled/rescheduled (restart workflow with new time)
- Appointment marked complete
- Appointment marked no-show (trigger Workflow 3)

**Special Handling:**
- If appointment is <24hrs away when booked, skip day-before message
- If appointment is <2hrs away when booked, skip all reminders

---

### Workflow 3: "No Show Recovery"

**Trigger:** Appointment marked as "No Show"

**Conditions:**
- `no_show_count` < 3 (don't spam serial no-shows)

**Actions:**
1. Wait 5 minutes
2. Tag contact "No-Show"
3. Increment `no_show_count` by 1
4. Send `NoShow-01-Email`
5. Wait 2 minutes
6. Send `NoShow-01-SMS`
7. Update `no_show_sequence_sent` = Yes
8. Move to "New Lead (Opt-In)" stage
9. Wait 4 hours
10. Send `NoShow-02-Email`
11. Wait 2 minutes
12. Send `NoShow-02-SMS`
13. Wait 2 days
14. Send `NoShow-03-Email`
15. Wait 2 minutes
16. Send `NoShow-03-SMS`
17. Wait 3 days
18. Send `NoShow-04-Email`
19. Wait 2 minutes
20. Send `NoShow-04-SMS`
21. Wait 1 day
22. If no response: Tag "Dead Lead" and move to "Lost/Dead Lead" stage

**Exit Conditions:**
- Contact reschedules (trigger Workflow 2)
- Contact replies (manual intervention)

---

### Workflow 4: "Invoice Sent Follow-Up"

**Trigger:** Contact moved to "Detailed Quote Sent" stage

**Conditions:**
- `invoice_sequence_sent` = No
- Quote document uploaded/attached

**Actions:**
1. Immediately send `Invoice-01-Email` with quote attachment
2. Wait 2 minutes
3. Send `Invoice-01-SMS`
4. Update `invoice_sequence_sent` = Yes
5. Update `quote_sent_date` = Today
6. Enable email tracking for quote opens
7. Wait 24 hours
8. Send `Invoice-02-Email`
9. Wait 2 minutes
10. Send `Invoice-02-SMS`
11. Wait 2 days
12. Send `Invoice-03-Email`
13. Wait 2 minutes
14. Send `Invoice-03-SMS`
15. Wait 4 days
16. Send `Invoice-04-Email`
17. Wait 2 minutes
18. Send `Invoice-04-SMS`
19. Wait 1 day
20. If no response: Tag "Cold Lead" and consider for 90-day re-engagement

**Exit Conditions:**
- Deposit received (move to "Won" stage)
- Quote opened (trigger Workflow 5 in parallel)
- Contact replies with questions (pause automation)

**Note:** This workflow runs for 7 days total, regardless of whether quote is opened

---

### Workflow 5: "Invoice Viewed - No Action (Micro-Sequence)"

**Trigger:** Email tracking detects quote email opened

**Conditions:**
- `invoice_viewed_sequence_sent` = No
- No reply received
- No deposit received

**Actions:**
1. Update `quote_viewed_date` = Today
2. Move to "Quote Viewed" stage
3. Wait 2 hours
4. Send `InvoiceViewed-01-Email`
5. Wait 2 minutes
6. Send `InvoiceViewed-01-SMS`
7. Update `invoice_viewed_sequence_sent` = Yes
8. Wait 10 hours (12hrs total)
9. Send `InvoiceViewed-02-Email`
10. Wait 2 minutes
11. Send `InvoiceViewed-02-SMS`
12. Wait 36 hours (48hrs total)
13. Send `InvoiceViewed-03-Email`
14. Wait 2 minutes
15. Send `InvoiceViewed-03-SMS`
16. Wait 1 hour
17. Move back to "Detailed Quote Sent" stage (continues Workflow 4)

**Exit Conditions:**
- Deposit received (move to "Won")
- Contact replies (pause both workflows)

**Note:** This runs IN PARALLEL with Workflow 4. Both can be active simultaneously.

---

### Workflow 6: "Deposit Received - Won"

**Trigger:** Payment received OR manually moved to "Won" stage

**Actions:**
1. Tag contact "Customer"
2. Remove all "Lead" tags
3. Stop all active nurture workflows
4. Send internal notification to team
5. [Optional] Start customer onboarding workflow (out of scope)

---

### Workflow 7: "Dead Lead - 90 Day Re-Engagement" (Optional)

**Trigger:** Contact in "Lost/Dead Lead" stage for 90 days

**Conditions:**
- Last contact >90 days ago
- Not unsubscribed
- Tagged "Cold Lead" or "No Response"

**Actions:**
1. Send soft re-engagement email ("Checking in about your roof...")
2. Wait 3 days
3. If no response, wait another 90 days and loop

---

## 6. Tags & Organization

### Lead Source Tags:
- `Source: Typeform`
- `Source: Phone`
- `Source: Referral`
- `Source: Website Chat`

### Behavior Tags:
- `Opt-In - Incomplete`
- `Scheduled - No Show`
- `Quote Opened`
- `Quote Viewed Multiple Times`
- `Responded to Nurture`

### Status Tags:
- `Active Lead`
- `Hot Lead` (multiple engagements)
- `Warm Lead` (some engagement)
- `Cold Lead` (no engagement)
- `Dead Lead` (unresponsive)
- `Customer` (won)

### Campaign Tags:
- `OptIn Sequence Active`
- `ScheduledCall Sequence Active`
- `NoShow Sequence Active`
- `Invoice Sequence Active`
- `InvoiceViewed Sequence Active`

### Loss Reason Tags (when moved to Lost):
- `Lost - Price Too High`
- `Lost - Went with Competitor`
- `Lost - Bad Timing`
- `Lost - No Response`
- `Lost - Other`

---

## 7. Integrations Required

### Essential Integrations:

**1. Calendly / Calendar Tool**
- Two-way sync with GHL calendar
- Webhook to trigger workflows on booking
- Pass contact data to GHL
- Update appointment status back to GHL

**2. Typeform**
- Webhook on form submission
- Map form fields to GHL custom fields
- Trigger "New Lead Opt-In" workflow
- Track incomplete vs complete submissions

**3. Payment Processor (Stripe/Square/PayPal)**
- Deposit payment tracking
- Trigger "Won" workflow on payment
- Update `quote_amount` and payment status

**4. Email Tracking**
- Link click tracking
- Email open tracking (critical for "Invoice Viewed" trigger)
- Document download tracking

**5. SMS Service**
- Two-way SMS (replies come back to GHL inbox)
- Short link generation
- Delivery receipts
- Opt-out handling

### Optional Integrations:
- Zapier (for additional automation bridges)
- Google Drive (for quote document storage)
- DocuSign (for contract e-signatures)

---

## 8. Reporting & Dashboards

### Dashboard 1: Pipeline Performance

**Metrics to Track:**
- Total leads by stage
- Conversion rate between stages
- Average time in each stage
- Overall form-to-customer conversion rate

**Widgets:**
- Pipeline funnel visualization
- Stage-by-stage conversion rates
- Stuck leads (>7 days in stage)
- Won deals this month (count + value)

---

### Dashboard 2: Campaign Performance

**Metrics to Track:**
- Email open rates by sequence
- SMS response rates by sequence
- Click-through rates
- Reply rates
- Unsubscribe rates

**Widgets:**
- Table: Sequence performance comparison
- Chart: Open rates over time
- Chart: Response rates by day of week
- Best performing messages (highest engagement)

---

### Dashboard 3: Calendar & No-Shows

**Metrics to Track:**
- Appointments booked
- Show rate %
- No-show rate %
- Reschedule rate
- Average lead time (booking to appointment)

**Widgets:**
- Calendar utilization
- No-show trend line
- Recovery rate from no-shows
- Day/time with best show rates

---

### Dashboard 4: Quote Performance

**Metrics to Track:**
- Quotes sent
- Quote open rate
- Average time to first open
- Quote-to-deposit conversion rate
- Average quote value
- Lost quote reasons

**Widgets:**
- Quote funnel (Sent → Viewed → Deposit)
- Average days from quote to close
- Loss reason breakdown (pie chart)
- Revenue pipeline (quotes in progress)

---

## 9. Testing Checklist

### Before Launch:

**Pipeline Testing:**
- [ ] All stages created correctly
- [ ] Stage transitions working
- [ ] Manual moves between stages trigger correct workflows
- [ ] Tags applied automatically at stage changes

**Custom Fields:**
- [ ] All custom fields created
- [ ] Correct field types (text, number, date, dropdown)
- [ ] Dropdown options populated
- [ ] Fields visible in contact view
- [ ] Fields update via workflows

**Templates:**
- [ ] All 22 templates created (11 email + 11 SMS)
- [ ] Merge fields working correctly
- [ ] No broken personalization
- [ ] Mobile-responsive emails
- [ ] SMS character counts verified
- [ ] Unsubscribe links present
- [ ] Tracking enabled on emails
- [ ] Test send to internal team

**Workflows:**
- [ ] All 7 workflows built
- [ ] Triggers set correctly
- [ ] Conditions logic verified
- [ ] Wait steps set to correct durations
- [ ] Actions in correct order
- [ ] Exit conditions configured
- [ ] Workflow doesn't restart if already sent

**Calendar:**
- [ ] Both calendars created
- [ ] Availability times correct (AEST timezone)
- [ ] Buffer times set
- [ ] Booking confirmations sending
- [ ] Reminders triggering at correct times
- [ ] No-show detection working
- [ ] Reschedule flow functional

**Integrations:**
- [ ] Typeform webhook connected
- [ ] Calendar sync working
- [ ] Payment processor connected
- [ ] SMS provider integrated
- [ ] Email tracking active

**End-to-End Testing:**
- [ ] Submit test Typeform → Verify enters pipeline
- [ ] Book appointment → Verify reminders send
- [ ] Mark no-show → Verify recovery sequence starts
- [ ] Send test quote → Verify invoice sequence starts
- [ ] Open quote email → Verify viewed sequence triggers
- [ ] Submit payment → Verify moves to Won

**Documentation:**
- [ ] Internal process doc created
- [ ] Team trained on manual steps
- [ ] Response handling protocol documented
- [ ] Escalation process defined

---

## 10. Launch Plan

### Phase 1: Soft Launch (Week 1)
- Enable workflows for NEW leads only
- Monitor daily for issues
- Test with 10-20 leads
- Adjust timing/copy based on feedback
- Team debriefs daily

### Phase 2: Historical Data (Week 2)
- Import existing leads (if applicable)
- Place in appropriate pipeline stages
- Don't trigger retroactive workflows
- Manual outreach to hot leads
- Automated sequences for cold/warm leads

### Phase 3: Full Launch (Week 3+)
- Enable all automations
- Scale to full lead volume
- Weekly performance reviews
- Monthly optimization based on data

---

## 11. Maintenance & Optimization

### Weekly Tasks:
- Review stuck leads (>7 days in stage)
- Check for automation errors
- Respond to replies/questions
- Update calendar availability
- Monitor unsubscribe reasons

### Monthly Tasks:
- Analyze sequence performance
- A/B test one variable per month
- Update copy based on common objections
- Review loss reasons and adjust
- Team training on new processes

### Quarterly Tasks:
- Deep dive analytics review
- Major copy refresh if needed
- Seasonal messaging updates (storm season)
- Competitive analysis
- Strategy adjustment based on learnings

---

## 12. Success Criteria

### Target Metrics (3-Month Benchmark):

**Pipeline Conversion:**
- Form Opt-In → Scheduled Call: 40-50%
- Scheduled Call → Show Rate: 85-90%
- Show → Quote Sent: 70-80%
- Quote Sent → Deposit: 30-40%
- **Overall: Form → Customer: 8-15%**

**Engagement:**
- Email Open Rate: 40-50%
- SMS Response Rate: 10-15%
- Calendar Reminder Confirmation: 70%+
- Quote Open Rate: 80%+

**Recovery:**
- No-Show Recovery (Rescheduled): 40-50%
- Cold Lead Reactivation (90-day): 10-15%

**Efficiency:**
- Average Lead Response Time: <2 hours
- Average Days in Pipeline: <21 days
- Manual Intervention Required: <20% of leads

---

## 13. Training Requirements

### For Sales Team (Luke/Kirby):

**Need to Know:**
1. How to manually move contacts between stages
2. When to pause automations (contact replies)
3. How to send manual quotes from GHL
4. Where to view dashboards and reports
5. How to tag lost leads with reasons
6. How to override or restart workflows
7. Response handling protocols

**Training Materials Needed:**
- Video walkthrough of pipeline usage
- Written SOP for common tasks
- Quick reference guide (cheat sheet)
- Troubleshooting FAQ

### For GHL Specialist (You):

**Deliverables Required:**
1. Fully built pipeline with all stages
2. All 22 email/SMS templates created
3. All 7 workflows active and tested
4. Custom fields populated
5. Tags configured
6. Integrations connected
7. Dashboards created
8. Documentation provided
9. Training conducted
10. 30-day support for issues

---

## 14. Files & Resources

### Campaign Copy:
All email and SMS copy is in the `/campaigns/` folder:
- `1-new-lead-opt-in.md`
- `2-new-lead-scheduled-call.md`
- `3-initial-call-no-show.md`
- `4-invoice-sent.md`
- `5-invoice-viewed-no-action.md`
- `README.md` (overview and strategy)

### Brand Assets:
- Logo: Available on website (frostroofing.com.au)
- Brand colors: From website CSS
- Tone/voice: See campaign files and website

### Contact Info:
- **Business Name:** Frost Roofing
- **Owners:** Luke & Kirby
- **Phone:** 0412 517 411
- **Email:** admin@frostroofing.com.au
- **Website:** frostroofing.com.au (currently in development)
- **Location:** Brisbane & Gold Coast, Queensland

### Compliance:
- **Spam Act:** Australian Spam Act 2003 compliance required
- **SMS Regulations:** Must include opt-out, send 8am-8pm only
- **Email:** Unsubscribe link, physical address, accurate sender info

---

## 15. Support & Questions

### During Build:

**For Campaign Strategy Questions:**
- Reference `/campaigns/README.md`
- Review website for brand voice

**For Technical GHL Questions:**
- Consult GHL documentation
- Use GHL community/support

**For Copy Edits:**
- Minor tweaks OK (formatting, personalization)
- Major changes should be approved by client
- Maintain brand voice (direct, transparent, no-BS)

### Post-Launch:

**Week 1-2:** Daily check-ins
**Week 3-4:** Bi-weekly check-ins
**Month 2+:** Monthly optimization reviews

---

## 16. Budget & Timeline Estimate

### Estimated Implementation Time:

**Setup Phase (Week 1):**
- Pipeline & stages: 2 hours
- Custom fields: 1 hour
- Tags setup: 1 hour
- Calendar integration: 2 hours

**Template Creation (Week 1-2):**
- 11 email templates: 8 hours (design + copy)
- 11 SMS templates: 3 hours (copy only)
- Testing all templates: 2 hours

**Workflow Building (Week 2):**
- 7 workflows: 10-12 hours (complex logic)
- Testing workflows: 4 hours
- Integration connections: 2 hours

**Dashboards & Reporting (Week 2-3):**
- 4 dashboards: 4 hours
- Custom reports: 2 hours

**Documentation & Training (Week 3):**
- SOP creation: 4 hours
- Video training: 2 hours
- Team training session: 2 hours

**Testing & QA (Week 3-4):**
- End-to-end testing: 6 hours
- Bug fixes: 2-4 hours
- Final adjustments: 2 hours

**Total Estimated Hours: 60-70 hours**

### Phased Approach (If Needed):

**Phase 1 (Priority):**
- Scheduled Call sequence (highest ROI)
- Invoice Sent sequence (where money is made)
- Basic pipeline and fields

**Phase 2:**
- Opt-In sequence (top of funnel)
- No Show recovery
- Calendar automation

**Phase 3:**
- Invoice Viewed micro-sequence (advanced)
- Dashboards and reporting
- 90-day re-engagement

---

## Next Steps

1. **GHL Specialist:** Review this brief thoroughly
2. **Questions:** Document any questions or clarifications needed
3. **Timeline:** Confirm build timeline and phasing
4. **Access:** Ensure you have admin access to:
   - GHL account
   - Typeform account
   - Calendar system
   - Email domain (for sending)
   - SMS provider
5. **Kickoff Call:** Schedule to review brief and align on approach
6. **Build:** Begin with Phase 1 (Scheduled Call + Invoice Sent)
7. **Test:** Thoroughly test before launch
8. **Train:** Conduct team training
9. **Launch:** Soft launch → Full launch
10. **Monitor:** Weekly check-ins for first month

---

**Questions or clarifications needed?** Document them and let's review before build begins.

This system will transform Frost Roofing's lead management from manual chaos to automated precision. Let's do this! 🚀
