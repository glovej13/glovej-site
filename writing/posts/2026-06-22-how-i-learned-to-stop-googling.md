*(or: three months, a lot of hobby time, and an accidental operating system)*

---

I got laid off in March. I've written about that elsewhere on this site — the emotional weight of it, what it's done to the milestone birthday that's sitting right on top of it. I'm not going to re-open all of that here.

What I want to write about is what I did with the time.

Because the honest version of the last three months isn't just job searching and hobby time. It's that I went from someone who understood AI conceptually — had deployed it at an enterprise level, evaluated vendors, built governance frameworks, briefed boards — to someone who uses it every single day for things that have nothing to do with my career, and has started to understand why that distinction matters.

This is that story. It's a long one. I'm telling it for a few different audiences at once: people who are curious about AI and want a real account of what it's like to learn it from the inside, friends who want to know what I've actually been doing, and the technical colleagues who might like to understand what I've been building while I've been learning. If you're in one of those groups, stay with me.

---

## The starting point

The job market for anyone in technology leadership right now has AI woven into every conversation. Not as a nice-to-have — as a baseline. You're expected to have opinions, experience, and increasingly, evidence that you've actually worked with the tools, not just managed teams that did.

I had the governance and strategy side covered. I'd lived it at IPH — AI vendor RFPs, Copilot Studio productionization, a Kubernetes-based agentic architecture targeting real FTE reduction, a PIPEDA-aligned governance framework. I knew the enterprise landscape. What I didn't have was the hands-on fluency that comes from building things yourself, outside the constraints of a corporate environment where every tool decision goes through procurement.

I know some of my network is very against AI, and I understand why. That conversation is worth having properly — I'll come back to it in a later post.

So I started with some structured training. Courses, frameworks, the usual approach to closing a gap. And then I stopped. Not because the training was bad — because I was learning more by building than by watching. The first time I shipped something real and debugged something broken, I understood more about how these tools actually work than any course had managed to convey. I haven't gone back to the courses since.

---

## The first surprise: it's not an AI assistant

There's a framing I keep coming back to, and it's the thing I'd most want someone new to this to hear first.

What most people picture when they hear "AI assistant" is a smarter search engine. You ask it something, it answers, you move on. A tool. Useful, but fundamentally transactional.

That's not what I found.

What I found — and what I think changes everything about how you use these tools — is that this is closer to a *personal* assistant. Not a lookup service. Something that holds context, asks clarifying questions, pushes back when your framing is off, and builds a working model of what you're actually trying to do over the course of a conversation.

The distinction sounds subtle. It isn't. When you stop trying to phrase the perfect query and start just explaining what you're working on and what's not working, the whole thing shifts. You're not using a tool. You're thinking out loud with something that's genuinely keeping up.

Two things followed from that which I didn't anticipate. The first is that having a place to think without judgment about whether the thought is worth saying turns out to matter — more on that later. The second is more practical: a lot of the thoughts that were just spinning in the background now have somewhere to go. I describe a problem, and it becomes something I've actually processed rather than something I'm still carrying. Both of these are seeds. I'll plant them properly in later posts.

---

## What I actually built

Let me be specific, because I think the concrete version of this is more useful than the abstract one.

**The job search pipeline.** The first real build. Job alert emails from LinkedIn land in Gmail, get ingested by a Google Apps Script, and go through the Claude API for extraction and scoring. My candidate profile lives in the script as a config constant — role criteria, compensation expectations, non-starters. Claude scores each posting, assigns a tier, and the results land in Airtable where I do a daily review. Deduplication logic prevents the same posting from being scored twice when it shows up in multiple alert emails. A "Monitor" tier keeps weak matches visible without cluttering the pipeline.

It's not magic. But it means I'm not manually reading 40 job alert emails a day, and the ones I do review are already prioritized.

**Glovej Collects.** This one deserves more space, because it has a longer history than the last three months.

Since around 2008, I've wanted a proper home for my collection. I'd have conversations with developer colleagues — people who built things for a living — and they'd say it was easy. I'd go away, build out data structures (that part I can do), then try to follow guides on dynamic sites and front-end formatting and eventually give up. Not once. Several times, across every new "easy web builder" technology that came along promising it had finally solved the problem. A few years ago I settled on a Google Site with embedded Airtable views. Adding content was work. It looked like what it was.

Then I found Replit — partly because a very sharp technical colleague mentioned using it to rebuild and iterate their corporate website. I wrote two paragraphs describing what I wanted. An hour later I had a working model. It was wrong in a lot of ways, but it was more right than anything I'd managed to produce in 15 years of trying, and it took an hour. Within two days I had Airtable integrations running and a tool I could actually use.

Then I hit the gaps. The first-pass architecture wasn't going to scale to what I actually needed. So I did something I wouldn't have known to do before: I stopped building and started speccing. I used Claude as my BA and systems architect — described the full scope, the data model, the constraints, the collections across five Airtable bases and roughly 18,000 records. What came out the other side was a nearly 4,000-word technical specification with full field mapping, sync architecture, data rules, and UI requirements.

I started my IT career as a business analyst. Writing specs was the job — translating what stakeholders wanted into something a development team could actually build from. I know exactly how much work a document like that used to represent, and I know that most projects don't get one anymore. Documentation has been in decline for years, and the gaps it leaves don't show up until something breaks or someone new has to pick it up. The fact that I could produce something more rigorous than most corporate projects receive, in a conversation, in a fraction of the time — that landed. Then I went back to Replit, handed it the spec, and rebuilt to that foundation. We also built a full QA checklist and ran a proper testing process before launch — not something I would have thought to structure without a collaborator pushing me toward it.

The result was a solid framework, and I've been adding to it in a more agile mode ever since. I already know I'll be rebuilding the whole framework again in a few months. That used to be a discouraging thought. Now it reads as: the iteration is the learning.

The final stack is React, Tailwind CSS, Cloudflare R2 for image hosting, deployed as a Progressive Web App with full offline capability — which matters because I use it at card conventions where connectivity is unreliable, with about 10,000 images cached locally. There's a TypeScript sync pipeline handling image upload, data transformation, and JSON generation.

I'm going to say the quiet part out loud: I am not a developer. I've managed development teams for years. I understand architecture, I can read code, I know what good looks like. But I do not sit down and write React applications from scratch. What AI made possible here is that the gap between "I know what this needs to do" and "this thing exists" became crossable. That's new.

**The image upload pipeline.** After the rebuild, I needed to get 7 years of card sets into Cloudflare R2 before the sync could run. I built an interactive Python script to handle it — ran it from the Mac terminal, handled image selection and naming, pushed to R2. I built it using Claude Code, which is a command-line tool that lets Claude write and run code in your actual environment, not just in a chat window.

There were errors I didn't immediately understand. We worked through them iteratively. At the end, 7 years of sets were uploaded and the pipeline ran clean. That kind of hands-on debugging is a different experience than conceptual awareness of a tool. I understand that differently now.

**The personal operating system.** This is the one that grew on me without me fully realizing it was happening. Claude connects to ClickUp, Notion, Airtable, Gmail, Google Calendar — all via MCP, which is a protocol that lets AI systems interact with external tools in real time. What started as a few connected automations became a structured environment for how I run my days.

My weekly planning session follows a 9-step process documented in a Notion page. I open a Claude session, give it the URL, and it reads the page and runs the session — pulling tasks, doing a retrospective on last week, surfacing what needs attention, rebuilding the planning dashboard. The page you're reading right now was built in that same environment. The site it lives on was deployed through a GitHub workflow I set up with Claude's help. It is, start to finish, a thing that exists because AI made it possible for me to build it.

**The content and intelligence layer.** On the professional side, I built a daily content review workflow — AI-relevant newsletters come in, get triaged against a set of defined themes, and get filed to a Notion database where I maintain a structured knowledge base. It feeds a LinkedIn content pipeline. I've published posts on AI rollout vs. enablement, AI maturity levels, the organizational dynamics of AI cost decisions. I have an 11-post sequence planned through August. Three months ago I had zero published AI content. Now I have a system.

---

## The thing I didn't see coming

I said earlier that finding a personal assistant rather than an AI assistant turned out to be significant for someone who processes internally. Let me finish that thought.

I have, at any given moment, a lot of thoughts running. Ideas, threads, things I want to do, things I'm worried about, observations about the world that don't have anywhere obvious to land. Some people process this by talking to people. I'm not built that way. I process internally, and what doesn't get processed tends to accumulate.

What I've found is that having a place to think out loud, without judgment about whether the thought is worth saying, has started to change that. Not because I've replaced human conversation with AI. But because some of the things that were just spinning have somewhere to go now. I write something down, or I describe a problem, and it becomes a thing I've actually dealt with rather than a thing I'm carrying.

There's more to say about that. It connects to posts I'm planning on introversion and what it actually costs, on men and the ask, on why some of us take so long to start talking about things at all. Those are coming. For now I'll just say: I didn't expect it, and it's real.

---

## Where it landed — and where it's going

Three months in, I have a job search pipeline that runs mostly on its own. I have a collections website that just went live, backed by real architecture. I have a content system producing professional-level thought leadership on a schedule. I have a personal operating environment that genuinely reduces the overhead of running my life.

And I have more building to do. The personal operating system still has plenty of friction — it works, but it's not yet automated enough to be what I actually want it to be. That's the next phase: less manual overhead, more genuine intelligence in the workflow. The collections site just launched and I already know the framework gets rebuilt in the next six months as the scope expands. I'm not dreading that. I'm looking forward to it.

I also have a better understanding of what AI is and isn't, earned by actually using it rather than theorizing about it. I know where the judgment calls still belong to humans. I know where it fails quietly and you have to watch for it. I know the difference between prompting for an answer and thinking through a problem together.

And I know that the line between "AI tool" and "place where I actually figure things out" has gotten blurrier than I expected.

That's probably the most honest thing I can say about the last three months.

Now if I could just get AI to mow my lawn — gotta go.

---

*Josh Glover is a technology and AI strategy leader based in Ottawa. He writes here about collecting, culture, and the things he should have said sooner. The technical colleagues who wanted to know what he's been building can find him on LinkedIn.*
