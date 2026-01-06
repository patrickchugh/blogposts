# While Everyone's Building AI Agents, Smart Teams Are Building this

**TL;DR:** Your AI agents, coding copilots, and RAG pipelines are only as good as the knowledge they run on. Most enterprises are building AI on stale documentation, tribal knowledge locked in people's heads, and Confluence pages that haven't been touched since 2023. The smart teams are solving this problem first. They're building Enterprise Intelligence: an always-accurate, automatically-updated knowledge base that compounds over time. The secret? Treating documentation as a build artifact, not a chore.

---

Here's something nobody's talking about in the rush to deploy AI agents: **the intelligence layer underneath.** 

Every enterprise AI initiative whether it's coding copilots, autonomous agents, customer service bots, or internal search depends on one thing: accurate, current knowledge about your systems. Your RAG pipelines are only as good as the documents they retrieve.  Your autonomous agents can only reason about systems they have reliable context for.

And yet, most enterprises are feeding their AI strategies on a diet of poor documentation and architecture diagrams that describe the system as it was three sprints ago.

If this sounds like your company, you're building AI on quicksand.

## The Flywheel that gives you a competitive edge

The teams getting this right aren't just writing better documentation. They're building an ***automatic, self-documenting pipeline*** from their codebase that reenforces AI at every step ; what Jeff Bezos calls "the flywheel effect - where each component accelerates the others. 

If you've read my previous post on [Specification-Driven Development (SDD)](https://patrickchugh.github.io/blogposts/sdd.html), you might spot an apparent contradiction. SDD argues that specifications should generate code; the spec and system document is the source of truth, and code is its expression. Here I'm arguing that code should generate documentation. So which is it? The answer is they're two halves of the same cycle, and you need both.

**SDD works when you're building new systems or features.** You start with precise specifications, AI generates implementations in code, and the spec remains the source of truth. It's the future of greenfield development.

But what about the millions of lines of legacy code that already exist? **What about systems built before SDD was feasible? What about the inevitable drift when production realities don't flow back through the spec? What about the third-party services and inherited codebases you don't control?

**Automated Document Generation (ADG)** works when you're understanding existing systems. It extracts truth from reality; capturing what the code actually does, what the infrastructure actually looks like, what dependencies actually exist.

SDD is how you build the future. ADG is how you understand the present. Together, they're how you bridge the gap.

The process to marry the two approaches follows these steps:

1. **ADG pipelines** capture the current state of your systems with forensic accuracy; architecture, dependencies, code structure, existing commentary are all extracted automatically from source code and infrastructure-as-code in a form both humans and AI can understand and access such as those in your Confluence or Sharepoint sites.

2. **AI-assisted SDD generates new code and features from those documents**,   Specification-Driven Development, powered by LLMs, use those documents from the pipelines output as the context on which to create new features.

3. Once the new features are delivered, **The changes from SDD gets integrated into your documents automatically** by the same pipelines in Step 1.

The result: Each iteration through these steps makes the flywheel spins faster. Knowledge compounds instead of decaying.

## Why Your Current Documentation Is Probably Fiction

I've spent more than two decades helping enterprises modernise their technology architecture and software development practices. When I look back at my career, whether it was developing the the Open Banking stack at HSBC, or devising strategy for a JP Morgan CTO as a Solutions Architect at AWS; —one constant remained: documentation is always outdated. *Always*.

Whenever I would go to an application team and ask them to share their architecture, what I got was a lot of uncomfortable smiles and some outdated diagrams produced by someone who had left the company a year ago.

To be fair, the information I needed did exist *somewhere*. I could eventually piece together the entire picture by studying Confluence pages edited six months ago, combined with updates I got over email, cross-referenced with README files nobody remembered to update, and architecture diagrams that reflected the system as it was in 2023.

Does that sound familiar?

The truth is: **if your documentation isn't generated from your source code, it might as well be fiction.**

And here's the kicker: that fiction is now what you're feeding to your AI.

## Why using LLMs can make the problem worse

The obvious solution seems to be throwing an LLM at the problem. Feed it your codebase, ask it to write documentation. Easy, right? For personal projects or quick prototypes, that works well enough.

But try this in an enterprise context and you'll hit a wall: **non-determinism**.

Run the same LLM documentation pipeline twice. You'll get different output. Different word choices. Different sentence structures. Sometimes different interpretations of what a function actually does. Now imagine this in a regulated environment where documentation is subject to audit and any changes must be tracked and explained.

Which version goes into your compliance records? Which version do you diff against to see what actually changed? How do you trust documentation when every iteration could have been derived from a different LLM and from a different set of files?

This isn't a hypothetical problem. I've watched teams abandon LLM documentation experiments specifically because they couldn't achieve the reproducibility their governance required.

And it gets worse. If your AI agents are reasoning based on LLM-generated documentation that's non-deterministic, you've now got **compounding unreliability**. Hallucinations feeding hallucinations. Good luck explaining that to your auditor.

## The Breakthrough: Deterministic First, LLM Second

The difference in what I am advocating comes from flipping the mental model. Instead of asking "how can we make LLM output more consistent?", ask: **"what can we extract without an LLM at all?"**

The answer is: far more than you'd think.

Consider what's already present in your codebase, waiting to be extracted deterministically:

- Your **project structure** is a tree of directories and files. That's pure data.
- Your **function signatures**; method names, parameter types, return type; —are available through Abstract Syntax Tree parsing.
- Existing **docstrings and comments** can be extracted verbatim.
- Your **architecture** can be inferred from Infrastructure as Code.
- Your **tech stack** is declared in package.json, requirements.txt, go.mod, and similar dependency files.
- Your **API contracts** are defined in OpenAPI specs, GraphQL schemas, and protobuf definitions.
- Your **database schemas** are documented in migrations and ORM models.
- Your **infrastructure dependencies** are explicit in Terraform, CloudFormation, or Kubernetes manifests.

You have a goldmine of information. None of this requires an LLM. It requires parsers. And parsers are deterministic.

The result: documentation that's **80% deterministic, 20% LLM-enhanced, and 100% auditable**. Run it twice, get identical output. That's the foundation Enterprise Intelligence needs.

## The Toolchain

Making this work requires orchestrating several tools, each handling what it does best.

**For architecture diagrams**, tools like [Terravision](https://github.com/patrickchugh/terravision) (shameless plug, I wrote that) parse your Terraform code and generate accurate infrastructure diagrams. No guessing about which services connect to which and whether it matches production or not. The IaC scripts are the source of truth.

**For codebase analysis**, [Repomix](https://repomix.com/) packs your entire repository into a structured format optimised for analysis. But here's the key: you don't send this directly to an LLM for interpretation. You extract the deterministic metadata first, and only send the gaps.

**For tech stack detection**, dependency scanning tools like [Syft](https://github.com/anchore/syft) generate a software bill of materials, and AST parsers identify every framework, library, and language version in use. This forms the foundation of your technical documentation.

**For the template**, [Jinja2](https://pypi.org/project/Jinja2/) provides deterministic structure. Your documentation always has the same sections, the same headings, the same format. The LLM fills slots within this structure; it doesn't create the structure.

**For publishing**, CI/CD pipelines using Jenkins or GitHub Actions push the generated documentation directly to Confluence, SharePoint, or your internal developer portal. Documentation updates become part of your deployment process, not an afterthought.

**For the LLM layer**, constrain it ruthlessly. Temperature set to zero. Specific, bounded prompts for each gap. Explicit instructions to say "no description available" rather than guess. Validate outputs against schemas. This isn't creative writing; it's gap-filling.

## The Pipeline Architecture

The pipeline follows a specific sequence:

![pipeline](ADP.png)

**Stage 1: Deterministic Extraction (100% reproducible)**

- AST parsing → function/class metadata
- Terravision → architecture diagrams
- Syft → software bill of materials
- Repomix → structured codebase representation
- Dependency files → tech stack
- Existing docstrings → verbatim extraction

**Stage 2: Template Rendering (100% reproducible)**

- Jinja2 templates with fixed structure
- All metadata slots filled deterministically
- Placeholder markers for LLM sections: `{{SUMMARY}}`

**Stage 3: Constrained LLM Fill (bounded variance)**

- Only fills marked placeholders
- Each prompt is specific and constrained
- Temperature=0 for consistency
- Fallback to "No description available" if uncertain

**Output: Version-controlled documentation artifact**
→ Confluence / SharePoint / GitHub Pages / Developer Portal

If you want to see sample code of how this works in practice, check out my example script on [GitHub](http://www.github.com/patrickchugh/ucd). It's an MVP, but in production you'd expand the LLM stage with proper API calls and validation. The structure remains: extract first, template second, LLM last.

## The Governance Angle

For enterprises subject to regulatory requirements, this approach offers something valuable: **an audit trail**.

Your documentation is generated from code. The generation process is deterministic (or near-deterministic). The output is version-controlled. You can prove that documentation version X was generated from code version Y on date Z.

This matters for compliance frameworks like SOX, MiFID II, and DORA that require demonstrable traceability between systems and their documentation. When the auditors come knocking, you can point to a pipeline; not a wiki page last edited by someone who left the company.

This isn't possible with manually-maintained documentation. It's barely possible with unconstrained LLM generation. But a deterministic-first pipeline provides the traceability that compliance teams will love you for.

## Practical Considerations

There are genuine challenges with this approach that deserve acknowledgment.

**AST parsing across polyglot repositories** requires investment. You'll need parsers for each language, and they need to produce a common metadata format. This is engineering work, not magic. The good news: most mainstream languages have mature AST libraries.

**Template design matters enormously.** A poor template produces poor documentation regardless of how accurate your extraction is. Budget time for iteration. Start with a minimal template and expand based on what your teams actually need.

**LLM costs can accumulate** even with a minimised LLM layer. If you're using OpenAI's GPT or Claude via AWS Bedrock, you could burn through tokens quickly. Batch your gaps efficiently. Consider running a local LLM via Ollama so your costs are fixed, and keep documentation generation to pull requests to main only; not every commit.

**The privacy angle:** Some security teams may feel uncomfortable with the company's source code being sent to a third-party model or cloud provider. Hardware costs are falling and GPUs are now common even in laptops. Running a local LLM via Ollama on your own hardware may not be as crazy as it sounds.

**The "80% deterministic" figure will vary** by codebase. Well-documented codebases might hit 95%. Poorly-documented legacy systems might struggle to reach 60%. The approach scales, but your mileage will vary.

**Start with one service.** Don't try to boil the ocean. Pick a well-understood service, build the pipeline, prove it works, then expand. The tooling is modular; you can add languages and frameworks incrementally.

## The Payoff: What Changes When Your Knowledge Base is always Accurate

Think about what happens when documentation is always accurate and always current:

**Your AI tools actually work.** Coding copilots stop hallucinating about your codebase. RAG pipelines return relevant results. Autonomous agents can reason about your systems without you babysitting them.

**New engineers onboard faster.** The documentation they read matches the code they're debugging. No more "oh, ignore that doc, it's outdated."

**Knowledge survives attrition.** When senior developers leave, their understanding of the system doesn't leave with them. It's captured in the pipeline outputs.

**Cross-team dependencies become visible.** The documentation reveals integration points automatically. No more surprise breaking changes.

**Technical debt becomes measurable.** You can see which services have sparse documentation, which have missing docstrings, which have drifted from their architecture diagrams.

**Audits become trivial.** Point to the pipeline. Show the version history. Demonstrate traceability.

This isn't just about keeping documentation current. It's about building an organisational memory that compounds over time rather than decays. Documentation becomes infrastructure; the foundation on which your AI strategy either succeeds or fails.

Without a pipeline in place your AI investments are built on a weak foundation that's actively rotting, making fast paced innovation at your company a struggle.

## Where This Is Heading

The tooling for deterministic extraction is already here and maturing rapidly. AST parsers exist for every major language. Infrastructure-as-Code can now be easily documented as diagrams. Dependency scanning is a solved problem.

What's emerging is a best practice: **treating documentation as a build artifact with the same reverence as your code**. It should be generated, versioned, and published through the same pipelines as your application code. LLMs accelerate this by filling gaps, but the foundation must be deterministic.

The end state is documentation that's never more than one deployment behind reality. Not because someone remembered to update a wiki page, but because the pipeline **ensures it**.

While everyone else is chasing the latest AI agent framework, the smart teams are building the intelligence layer underneath. They know that agents are commoditising fast; but a rich, accurate, continuously-updated knowledge base about your own systems? That's the asset that keeps compounding.

I hope you take away from this that you should start treating documentation like it is critical; because in the age of AI, it finally is.

---

*Patrick Chugh is an AWS cloud architect specialising in financial enterprise systems and has held senior leadership roles at HSBC, AWS, and Credit Suisse. As a consultant, he has advised C-level leadership at JP Morgan, Santander, and Barclays. He's the creator of [Terravision](https://github.com/patrickchugh/terravision), an open-source tool for generating architecture diagrams from Terraform code.*
