# QUICK WIN
## Automatic Lead Qualification Over the Weekend

**Step-by-step guide with Make.com + Claude API**

**Save 4.5 hours/week starting Monday**

---

## PROBLEM: Website Leads Are Eating Your Time

If you have a website with a lead form — you know this pain:

- 100+ leads every week
- 70-80% of them are junk (spam, students, "just browsing")
- 5 hours per week spent on manual sorting
- Hot leads get lost in the flow

### Real Example

SaaS product owner receives 150 leads/week:

- 100 leads (67%) — spam or students asking for free access
- 30 leads (20%) — cold "just looking at options"
- 20 leads (13%) — HOT (ready to buy, have budget)

### Cost of Your Time

- 5 hours/week on manual lead sorting
- 5 hours × 4 weeks = 20 hours/month
- Your rate $25/hour (average) = $500/month lost
- Annual cost: **$6,000**

### But the Worst Part Isn't Money

The worst part:

- You get tired of spam → start ignoring ALL leads
- Hot leads get lost among junk
- Lost revenue: each missed lead = $500-5,000

---

## SOLUTION: Automatic Qualification Over the Weekend

### What We Automate

1. **Reading lead** — Claude API analyzes each lead
2. **Scoring** — assigns score: 🔴 Spam / 🟡 Cold / 🟢 Hot
3. **Routing** — only hot 🟢 go to your CRM

### Results After Implementation

| Metric | Before | After | Savings |
|--------|--------|-------|---------|
| Time/week | 5 hours | 30 minutes | 4.5 hours |
| Time/month | 20 hours | 2 hours | 18 hours |
| Cost/month | $500 | $50 | $450 |
| **Annual savings** | | | **$5,400** |

### ROI (Payback)

Tools (almost all free):

- **Make.com** — FREE tier (1,000 operations/month)
- **Claude API** — $5-10/month (for 100 leads/week)
- **Your CRM** — you already have (HubSpot, Pipedrive, Notion, Google Sheets...)

**Total:**
- ✅ Costs: $5-10/month
- ✅ Savings: $450/month
- ✅ ROI: **4,500%** in first month

---

## STEP-BY-STEP INSTRUCTIONS

**Total time:** 2 hours (can do over Saturday-Sunday)

**Result:** Automation works from Monday

---

## STEP 1: Preparation (30 minutes)

### 1.1. Register on Make.com

1. Go to make.com
2. Sign up (free)
3. Choose FREE tier (1,000 operations/month)

### 1.2. Get Claude API key

1. Go to console.anthropic.com
2. Sign up
3. Settings → API Keys → Create Key
4. Copy key (save in safe place)

### 1.3. Define "hot lead" criteria

What for YOU = hot lead? Write 10-15 indicators.

**Examples of HOT lead criteria:**
- ✅ Mentions specific problem/pain
- ✅ Company specified (not personal email @gmail)
- ✅ Budget mentioned or implied
- ✅ Urgency ("need in 2 weeks")
- ✅ Decision maker (CEO, founder, director)

**Examples of COLD lead criteria:**
- ⚠️ "Just browsing"
- ⚠️ Student/studying
- ⚠️ No specifics
- ⚠️ Looking for free solution

**Examples of SPAM criteria:**
- ❌ Service offer (SEO, advertising)
- ❌ Incoherent text
- ❌ Suspicious email

---

## STEP 2: Make.com Setup (1 hour)

### 2.1. Create new scenario

1. Make.com → Create a new scenario
2. Name: Lead Qualification Automation

### 2.2. Module 1: Webhook (form from website)

1. Add module: Webhooks → Custom webhook
2. Create webhook
3. Copy URL
4. In website form: send data to this URL

**Platform-specific:**
- **Tilda:** form settings → webhook URL
- **WordPress:** Contact Form 7 → webhook integration
- **Typeform:** integrations → webhooks
- **Webflow:** form settings → webhook

### 2.3. Module 2: Claude API (scoring)

1. Add module: HTTP → Make a request
2. Settings:

**URL:** `https://api.anthropic.com/v1/messages`

**Method:** POST

**Headers:**
```
x-api-key: [your Claude API key]
anthropic-version: 2023-06-01
content-type: application/json
```

**Body** (prompt for Claude):

```json
{
  "model": "claude-sonnet-4-20250514",
  "max_tokens": 1024,
  "messages": [{
    "role": "user",
    "content": "Analyze lead and assign score.\n\nLead:\nName: {{name}}\nEmail: {{email}}\nCompany: {{company}}\nMessage: {{message}}\n\nCriteria:\nHOT (score='hot'): mentions specific problem, has budget, decision maker, urgency\nCOLD (score='warm'): just browsing, no specifics, no budget mentioned\nSPAM (score='spam'): service offer, incoherent text, suspicious\n\nRespond ONLY with JSON:\n{\"score\": \"hot/warm/spam\", \"reason\": \"brief explanation\"}"
  }]
}
```

**Important:** Replace `{{name}}`, `{{email}}`, `{{company}}`, `{{message}}` with actual fields from your webhook

### 2.4. Module 3: Router (branching)

1. Add module: Router
2. Create 3 paths:

- **Path 1:** If score = "hot" → create Lead in CRM
- **Path 2:** If score = "warm" → to Google Sheet (follow-up later)
- **Path 3:** If score = "spam" → to archive (or ignore)

---

## STEP 3: CRM Integration (30 minutes)

### 3.1. Choose your CRM

Add module for your CRM:

- **HubSpot:** HubSpot → Create a contact
- **Pipedrive:** Pipedrive → Create a deal
- **Notion:** Notion → Create a database item
- **Google Sheets:** Google Sheets → Add a row

### 3.2. Configure fields

Data mapping from webhook to CRM:

```
Name: {{name}}
Email: {{email}}
Company: {{company}}
Message: {{message}}
Score: {{score}} (hot/warm/spam)
Reason: {{reason}} (justification from Claude)
```

---

## STEP 4: Testing (30 minutes)

### 4.1. Send 5 test leads

**Test 1: Hot lead**
```
Name: John Smith
Email: john@company.com
Company: ABC Corp
Message: "Need CRM automation. Budget $5k. Urgent, starting in 2 weeks."
```
Expected result: score = "hot"

**Test 2: Cold lead**
```
Name: Maria
Email: maria@gmail.com
Company: -
Message: "Interested in your services. Can I get pricing?"
```
Expected result: score = "warm"

**Test 3: Spam**
```
Name: SEO Expert
Email: seo@spam.com
Company: SEO Agency
Message: "We'll boost your site in Google for $99. Top-10 guaranteed."
```
Expected result: score = "spam"

### 4.2. Check results

1. In Make.com: check History → should be 5 runs
2. In CRM: hot lead should appear in CRM
3. In Google Sheet: cold lead should appear in table
4. Spam: should be in archive (or ignored)

### 4.3. If not working

Check:
- ✅ Claude API key copied correctly?
- ✅ Webhook URL inserted in form?
- ✅ Prompt contains all criteria?
- ✅ Fields `{{name}}`, `{{email}}` mapped correctly?

---

## STEP 5: Launch (10 minutes)

### 5.1. Enable scenario

1. Make.com → Toggle ON
2. Scheduling: Instant (each lead processed immediately)

### 5.2. Monitor first 24 hours

- Check History every 2-3 hours
- Ensure scoring works correctly
- Verify hot leads reach CRM

### 5.3. Tuning (if needed)

- If Claude too strict → loosen criteria
- If missing spam → add filters
- If wrong categorization → refine prompt

---

## WHAT'S NEXT?

You automated lead qualification! 🎉

**Savings:** 4.5 hours/week = $450/month

But this is just the beginning. Lead qualification is one of 20-30 processes that can be automated in your business.

---

## WHY LEAD QUALIFICATION?

This process chosen by Decision Framework from AI Automation Decision System.

### 5 Automation Criteria:

**1. Frequency**
- ✅ 100 leads/week = 400/month
- Rule: >50 times/month = automate

**2. Standardization**
- ✅ Process always same (read → analyze → score)
- Rule: If process NOT standardized = DON'T automate

**3. Creative Core?**
- ✅ Scoring = applying criteria (not creative)
- ✅ Human checks final (20% involvement)
- Rule: Creative core = maximum 70/30 (AI/Human)

**4. ROI (Payback)**
- ✅ Costs: $5-10/month
- ✅ Savings: $450/month
- ✅ Break-even: 1 month
- Rule: Break-even <12 months = automate

**5. Complexity**
- ✅ No-code tools (Make.com)
- ✅ 2 hours implementation
- Rule: High complexity = postpone

### Verdict: 🟢 AUTOMATE NOW

All 5 criteria met → lead qualification = perfect candidate.

---

## WANT TO APPLY SAME CRITERIA TO YOUR PROCESSES?

### 1. FREE AI Automation Decision System
**→ https://aimethodology.gumroad.com/l/free**

- Decision Framework for any process
- 5 automation criteria
- Anti-patterns (what NOT to automate)
- Basic concepts

### 2. Business Owner Edition ($147)
**→ https://aimethodology.gumroad.com/l/business**

**For whom:** E-commerce, service companies, business owners $30k-500k/month

**What's inside:**
- ROI calculator (calculate payback BEFORE investment)
- 7 ready-made prompts for other processes
- Implementation checklist (50 items)
- Anti-patterns ($35k failures)

🎁 **BONUS:** 30-min consultation (first 10 buyers)

### 3. Professional Edition ($297)
**→ https://aimethodology.gumroad.com/l/professional**

**For whom:** Enterprise ($500k+/month), Regulated industries (GDPR), Automation agencies

**What's inside:**
- Everything from Business Owner Edition +
- GDPR Compliance Checklist (40 items)
- Self-hosted deployment guide
- Multi-agent architecture prompts
- Enterprise decision framework

🎁 **BONUS:** 30-min consultation (first 10 buyers)

---

## TROUBLESHOOTING

### Q: Claude categorizes incorrectly?

**Cause:** Criteria in prompt not specific enough for your niche.

**Solution:**
- Add more examples in criteria (15-20 indicators)
- Refine wording for your niche
- In prompt add: "If unsure — score = warm"

### Q: How much per month?

**Make.com FREE tier:** 1,000 operations/month
- 100 leads/week × 4 weeks = 400 operations
- FREE tier sufficient (if <250 leads/week)
- If more → CORE plan: $9/month (10,000 operations)

**Claude API:**
- 100 leads/week × 300 tokens/lead = 30k tokens/week
- 120k tokens/month = ~$5-10/month

**Total:** $5-10/month vs $450/month savings = **ROI 4,500%**

### Q: Can use for other process?

**YES!** Same scheme works for:

- ✅ Customer support tickets — ticket classification
- ✅ Job applications — resume screening
- ✅ Partnership requests — partnership spam filtering
- ✅ Survey responses — feedback categorization

**Principle:**
1. Incoming stream (leads, tickets, resumes)
2. Claude reads + categorizes
3. Automatic routing by category

### Q: Works with my form?

**YES!** Works with any form that can send webhook:

- ✅ Tilda: form settings → webhook URL
- ✅ WordPress (Contact Form 7): webhook integration
- ✅ Typeform: integrations → webhooks
- ✅ Google Forms: via Apps Script → webhook
- ✅ Webflow: form settings → webhook
- ✅ Any custom form: send POST request to webhook URL

---

## SUMMARY

- **Implementation time:** 2 hours
- **Costs:** $5-10/month
- **Savings:** $450/month
- **ROI:** 4,500%

Start this weekend. Works automatically from Monday.

---

© AI Automation Decision System
