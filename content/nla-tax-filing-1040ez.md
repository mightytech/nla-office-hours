# NLA Tax Filing: The Hybrid Model

---

## The Idea

An NLA that helps users file a simple federal tax return. The user provides raw financial information in whatever format they have — PDF W-2s, spreadsheets, typed descriptions, photos of documents. The AI reads and categorizes the inputs, the human reviews and approves the categorization, and traditional code runs the deterministic tax calculations. The result is a completed return ready for filing.

This is a white paper illustration, not a product plan. The point is to demonstrate the hybrid model — flexible human interface on top, deterministic computation underneath, AI as the bridge between them.

---

## Why This Example Works

Everyone understands taxes. The pain points are universal. And the architecture makes the NLA advantage viscerally obvious:

**The input problem is a judgment problem.** W-2s come in different formats. People describe income differently. Receipts are messy. Freelance income might be "about 3k from two clients" or a spreadsheet or a stack of 1099s. Traditional tax software forces the user to translate their reality into the software's categories ("enter the amount from Box 12a"). The NLA inverts this: give me what you have, I'll figure out what it means.

**The calculation problem is a determinism problem.** Tax math must be exactly right. It's auditable, regulated, and has real consequences. You'd never want an LLM doing arithmetic on your tax return. Traditional code handles this perfectly — the same way the penny post calls shell scripts for mechanical tasks.

**The middle is where the NLA shines.** Mapping messy human inputs to clean tax categories is a judgment call that traditional software can't make and humans shouldn't have to make unaided. The AI proposes categorizations. The human confirms or corrects. Each confirmation teaches the system about this user's financial situation. By the time the numbers reach the calculation engine, they're clean and correct — not because the user cleaned them, but because the AI and human collaborated on the translation.

**The interface is conversational.** TurboTax has help pages. The NLA has a conversation. "Wait, what's the standard deduction?" "Should I itemize?" "What happens if I don't report that freelance income?" These aren't FAQ lookups — they're contextual answers from an AI that already knows your specific financial situation. The difference between searching a help database and asking a colleague who's been reviewing your return with you.

---

## The Hybrid Model in Action

Three layers, each doing what it's best at:

### Layer 1: Flexible Input (AI + Human)

Accept anything:
- PDF W-2s, 1099s (AI reads via code tools)
- Spreadsheets (AI parses and interprets)
- Photos of documents (AI extracts with vision)
- Natural language ("I made $45k at my main job and about $3k freelancing")
- Prior year returns (AI extracts relevant carryforward items)

The AI categorizes each input into tax-relevant buckets: wages, interest, freelance income, deductions, etc. For each categorization, it explains its reasoning. The human approves, corrects, or asks questions.

This is the humanist UI. The software adapts to the person — not the other way around.

### Layer 2: Deterministic Calculation (Traditional Code)

Once inputs are categorized and approved, traditional code takes over:
- Compute adjusted gross income
- Apply standard deduction
- Calculate tax owed using the tax tables
- Determine refund or amount due
- Validate against IRS rules and constraints

No LLM involvement in the math. Auditable, reproducible, exact. The code is called by the NLA the same way any NLA calls traditional tools — judgment decides what to calculate, code does the calculating.

### Layer 3: Review and Filing (AI + Human)

The AI presents the completed return with explanations:
- "Here's your completed 1040. Your refund is $1,247."
- "I categorized your freelance income as self-employment income on Schedule SE. Here's why..."
- "One thing to flag: your charitable donations are close to the threshold where itemizing might save you money. Want me to check?"

And unlike traditional tax software, the conversation continues. "Why did you categorize that payment as self-employment?" "What would my refund be if I contributed to an IRA before the deadline?" The AI answers with your actual numbers, not generic guidance.

The human reviews. The human decides whether to file. Filing is irreversible — an NLA that prepares everything and says "here's what I'd file, and why — ready?" is the right design. The human bears the consequences, so the human holds the authority.

---

## What This Demonstrates

### Discipline collapse
Traditional tax software is an entire engineering discipline: OCR pipelines for document reading, rule engines for categorization, form-filling logic, validation systems. In the NLA model, most of this collapses into instructions the AI follows. "Read this W-2 and extract the relevant amounts" is a sentence, not a pipeline.

### Appropriate trust boundaries
- Input categorization: AI proposes, human approves (judgment + consequences)
- Calculations: traditional code, no AI involvement (determinism required)
- Filing: human decides (irreversible, real-world consequences)

Each boundary is drawn where the nature of the task demands it. Not "AI does everything" or "AI does nothing" — the right tool for each part.

### Progressive trust
A first-time user might review every categorization carefully. A returning user whose financial situation hasn't changed might approve most categorizations quickly and focus on what's new. The system supports both without changing — the same explanations are available, the same approval points exist, the user decides how much scrutiny to apply.

---

## Open Questions

- **Scope:** A simple return is simple by design. How far does this extend? Itemized deductions? Business returns? The architecture should scale, but the complexity of the tax code is a real challenge for the categorization layer.
- **Liability:** Who's responsible for errors? The NLA recommends, the human approves — but the approval is based on the AI's explanations. This is a real question for any high-stakes NLA.
- **Multi-document reconciliation:** What happens when a W-2 and a pay stub disagree? The AI flags it, explains the discrepancy, and asks the human to resolve. This is a judgment call that traditional software handles poorly.

---

## The Bigger Point

This isn't really about taxes. It's about a pattern: any domain where humans have messy inputs, the process requires deterministic calculations, and the stakes are high enough that human oversight matters.

But there's a sharper version of the argument. Most developed countries pre-fill simple returns for their citizens — the UK, Japan, Denmark, much of the EU. The US doesn't, not because it's technically hard, but because the tax preparation industry has spent decades preventing return-free filing. The people most harmed pay $50–100+ for software to navigate complexity that doesn't need to exist. It's the boots theory of tax preparation — the people with the simplest returns, who can least afford professional help, end up paying the most per dollar of actual complexity.

An NLA routes around the obstacle entirely. You don't need legislation. You don't need Intuit's permission. You build the thing that dissolves the complexity gap with judgment. And the pattern applies anywhere incumbents profit from that kind of gap: insurance claims, benefits applications, legal filings, immigration paperwork. "Give me what you have, I'll figure out what it means" is an equity proposition as much as a technology one.

The simple tax return is just the clearest example because everyone has filed taxes, everyone has felt the pain of translating their life into little boxes, and everyone understands why the math needs to be right. The NLA doesn't make taxes easier by simplifying the tax code. It makes taxes easier by meeting people where they are.
