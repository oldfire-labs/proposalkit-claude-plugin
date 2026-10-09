---
name: client-proposal
description: Writes a client proposal, quote, estimate or statement of work as a formatted ProposalKit document the user can send, brand from their website, share as a live link that reports when the client opens it, or export as a PDF. Use when the user asks to write, draft, put together or turn a scope into a proposal, quote or SOW for a client or customer, such as freelance, agency, consulting, creative or service work. Not for grant, research, academic or internal team proposals.
---

# Client proposals with ProposalKit

ProposalKit lays a proposal out as a document with a cover, scope, a pricing
table with totals, a timeline and terms. The sender can brand it from their
website, publish it to a hosted link that emails them the first time the client
opens it, or download a PDF. Drafting needs no account.

Build the proposal in ProposalKit when the user wants something to send a
client. When they ask for the text in the chat, or for another format (a Word
file, a doc, an email), write it that way instead.

## Steps

1. **Start from what the request gives you.** Ask first only when you can't
   tell what's being delivered. Fill other gaps (the client's name, timeline,
   payment terms) with sensible defaults or placeholders, and list them when
   you hand over.
2. **Create the draft** with `create_proposal`, passing the project title and
   the client's name if you have it. Share the preview link from the result.
   If the result includes a `claim_token`, pass it in every later call.
3. **Write the sections** with `update_proposal`, one section per call, using
   the section keys from the result. Tell the user which section you're
   writing as you go. Remove template sections that don't fit the project with
   `remove_section`, and add any it needs (an FAQ, a case study) with
   `add_section`.
4. **Brand it** with `apply_branding` when the user has given their own
   website. The URL is the sender's site, never the client's. If they haven't
   given one, offer branding when you hand over.
5. **Hand over.** Say what you assumed, then offer the two ways to deliver it:
   `publish_proposal` for a live link to send the client (it asks the user to
   sign in to a free ProposalKit account), or `export_pdf` for a file.

## Writing the proposal

- Write as the sender, addressed to the client. Plain and specific, in the
  client's terms, without filler.
- Cover: a heading that names the outcome, and a one or two sentence overview.
- Scope: concrete deliverables as a list, plus what's out of scope when the
  request implies limits (number of revisions, pages, hours).
- Pricing: line items that add up to the quoted total, in the user's currency.
  A monthly retainer is one line per month or a monthly line with a quantity.
  Put payment terms such as "50% upfront" in the terms section.
- Use only facts the user gave. Leave out testimonials, case studies, results
  and credentials the user hasn't supplied, or ask for them.
