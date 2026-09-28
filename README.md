# Fashion Brand Claude Skills

The [Claude Code](https://claude.com/claude-code) skills I use for my fashion brand, [Fenclaw & Faund](https://www.fenclawandfaund.com/).

Fenclaw & Faund is pirate and fantasy fashion where every piece belongs to a story. Each item ships with a storybook about its lore, and the collections follow the Cat Captain, Felix Fenclaw, and the Enchantress, Fiona Faund. That makes the copy harder than usual: it has to stay in the world *and* tell you what the thing is made of. These skills are how I keep AI on-brand for that.

## What I've learned about AI and brand voice

- **Approved lines beat generated ones.** Campaign copy pulls brand lines word for word from a bank I wrote. When a story has no lines yet, the skill asks instead of making some up.
- **Never let it invent a material.** If it's not in the spec, it's not in the copy. In the [product samples](examples/product-descriptions.md), the skill turns down the title "Tiger Silk Shirt" because the fabric is poly-silk.
- **Humans approve everything that goes out.** Nothing gets published or sent without a person saying yes. The trend scout can run on a schedule, but it shows me the digest before posting unless I switch that off.

## The skills

| Skill | What it does |
|---|---|
| `brand-guardrails` | The brand guide the copy and design skills read from: stories, voice, approved lines, colors, fonts |
| `product-descriptions` | Titles and descriptions from a product and its specs. Character limits, no invented materials, duplicate-title check |
| `campaign-copy` | Storyline, brand lines, copy block and content ideas for a collection |
| `moodboard-queries` | Search queries for a campaign moodboard, frozen per story so it stays consistent |
| `design-brief` | Colors, fonts and art direction, turned into a brief a designer can work from |
| `social-trend-scout` | Finds TikTok and Instagram trends that fit the brand, with a warning on audio rights |
| `skill-builder` | Interviews me about a task I keep repeating and turns it into a new skill |
| `rate-and-improve` | Scores any draft 1-10 with three critics and lists what would make it a 10 |

## See them run

The `examples/` folder has real output from these skills on real products:

- [`product-descriptions.md`](examples/product-descriptions.md): five products, from the Captain's overcoat to the Jeweler's Guild ring
- [`campaign-copy.md`](examples/campaign-copy.md): a feature for The Cat Captain's Coffers
- [`moodboard.md`](examples/moodboard.md) and [`design-brief.md`](examples/design-brief.md): the same campaign, handed to design

The brand guide the skills read from is [`brand/brand-reference.md`](brand/brand-reference.md). It's a working document with blanks. Colors aren't confirmed yet, so the samples show the skills stopping to ask instead of guessing. Fonts are a best read from the site, so the skills use them and flag them for me to confirm.

The skill files themselves use a made-up brand, Northwind Apparel, in their built-in examples so they stay reusable for anyone.

## Use them yourself

1. Copy a skill folder into `~/.claude/skills/`
2. Fill in `brand-guardrails` with your own brand first, since the others read from it
3. Ask Claude for the skill by name
