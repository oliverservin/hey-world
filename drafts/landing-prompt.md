# Preparation

## Why am I writing this?

I'm writing it because marketing is a challenge for me. As a developer, I struggle to sell anything to anyone. However, since I'm starting a portfolio of SaaS products, I need to learn how to sell my products. A crucial part of any marketing strategy for selling SaaS products is writing a compelling landing page. This document outlines my process for creating a landing page for one of my SaaS products.

## What audience is it for?

This writing is for developers who share my struggle with writing effective marketing copy. By the end of this guide, you'll have a repeatable process for writing landing pages as a developer.

## How it's distinctive?

It's distinctive because most copywriting material found on the internet is not created for developers. We typically have a different perspective on how to do things, often utilizing tools that assist us in this process.

# Draft

## Developer Struggles with Marketing

Now that I'm working on a portfolio of products, building them is not my main struggle since I'm a web developer. Instead, I find it challenging to act as a salesperson, trying to sell a product and write marketing copy.

## Seeking Help: The Stripe Guide

The first thing I considered was getting some help. After a quick search, I found an article on Stripe that provides a guide on writing landing pages ([Stripe Atlas Landing Page Copy Guide](https://stripe.com/guides/atlas/landing-page-copy)). I read the entire article, and it made sense to me.

## Using Language Models to Assist

The first step I took was to use a language model (I used GPT-4.1, but you can use any modern model like Claude or Gemini) to create a prompt based on the guide to help me write a landing page. This approach is similar to how I use language models to assist me in writing code for building products, but this time, I aimed to create effective landing page copy.

I provided a language model with the URL to read and asked it to generate a prompt for writing landing pages based on the article.

```md
# Landing Page Copywriting Prompt (Based on Stripe Atlas Guide)

You are an expert conversion copywriter. Write compelling, high-converting copy for a landing page. Follow these guidelines:

1. **Focus on the Customer:**
   - Address the visitor directly using “you” language or start sentences with verbs.
   - Avoid “we” or “our” language unless absolutely necessary.

2. **Pattern, Texture, and Shine:**
   - Vary sentence length and structure for a conversational, engaging feel.
   - Replace bland words with vivid, memorable synonyms.

3. **Defang Objections:**
   - Anticipate and address common objections using “even if” clauses.

4. **One Idea Per Sentence:**
   - Keep sentences focused and easy to digest.

5. **Landing Page Purpose:**
   - Write for a specific audience and offer, with a clear, relevant call to action (CTA).
   - Do not write a generic homepage.

6. **Three Foundational Elements:**
   - Make a direct, specific, and professional first impression.
   - Tailor copy length and detail to the market’s maturity (educate if new, differentiate if mature).
   - Match the copy to the visitor’s stage of awareness (unaware, problem aware, solution aware, product aware, most aware).

7. **Frameworks:**
   - Use AIDA (Attention, Interest, Desire, Action) or PAS (Problem, Agitation, Solution) to structure the copy.
   - Apply the Rule of One: one reader, one big idea, one promise, one offer.

8. **Be Specific and Visual:**
   - Use concrete, specific language and data.
   - Visualize numbers or achievements to make them relatable.

9. **Clarify Who It’s For:**
   - Include an “ideal for” statement near the top to help visitors self-identify.

10. **Iterate and Test:**
    - Write copy that is easy to test and refine.

**Input:**
- Product/service name
- What it does
- Target audience
- Main benefit(s)
- Objections or hesitations customers might have
- Market maturity (new/emerging or established/mature)
- Stage of customer awareness
- Any proof, data, or testimonials

**Output:**
- Headline
- Subheadline
- Body copy (including features, benefits, and (optional) social proof)
- Clear, specific CTA
- “Ideal for” statement
- Objection-handling statements
- Visual or data-driven proof points (optional)

Write in a clear, persuasive, and customer-focused style. Make the copy specific, memorable, and actionable.
```

## Required Inputs for the Prompt

However, using this prompt requires me to provide eight things, as it's based on the Stripe guide:

```md
- Product/service name
- What it does
- Target audience
- Main benefit(s)
- Objections or hesitations customers might have
- Market maturity (new/emerging or established/mature)
- Stage of customer awareness
- Any proof, data, or testimonials (optional—skip if you don’t have these yet)
```

Besides the product name and what it does, I didn't have anything else at first. This is normal for early-stage founders who are focused on building.

## Writing the Initial Draft

So, I wrote a draft outlining the purpose of the product, the problem it solves, and how it works. I didn’t have any testimonials or social proof yet, so I focused on making the product’s value clear and actionable.

```md
Terrific Poll is a service that allows you to create polls easily embedded in newsletters using any email newsletter service.

Even if your newsletter service doesn't support polls, it may require a plan upgrade or a paid add-on.

First, you create a poll by assigning it an internal name, writing the question, and adding up to 10 response options.

You can then copy the poll for easy embedding in services like Beehiiv, Brevo, EmailOctopus, Ghost, HubSpot, Kit, Loops, MailerLite, and Sendy.

The copied poll includes your question and links to the response options. When your recipient clicks on a response option, it opens a page to confirm their selection. It pre-fills the contact email using your newsletter service's merge tags and submits their response.

Once you start collecting responses, your poll dashboard will display the number of responses received and a percentage indicator for each response option. You can also access a detailed table showing the responses for each option, along with the date of the response and the contact email (if provided) of the person who submitted it.
```

## Filling in the Gaps with Language Models

Now that my draft is written, I could use language models again to help me address the missing parts required for the prompt to write my landing page copy. After generating the draft, I reviewed it for clarity and specificity. Editing the AI output is crucial.

### What the Product Does

The first task was to ask the language model to identify, in its own words, what the product does.

It did a great job summarizing what my product does with minimal refinement.

```md
Terrific Poll is a service that allows users to easily create and embed polls in email of which newsletters, regardless of which newsletter service they use.

- Create Polls: Users can create a poll by giving it an internal name, writing a question, and adding up to 10 response options.
- Embed in Newsletters: The service generates poll content that can be embedded in popular newsletter plattorms (e.g., Beenliv, Brevo, Emailoctopus, Ghost, Hubspot, Kit, Loops, MallerLite, sendy), even if those platforms don't natively support polls.
- Easy Response Collection: Each poll option is a link. When a recipient clicks a response, they're taken to a confirmation page where their selection is pre-filled (using the newsletter service's merge tags for contact email) and submitted.
- Dashboard & Analytics: After responses are collected, users can view a dashboard showing:
    - The number of responses for each option
    - Percentage indicators for each response
    - A detailed table with each response, the date, and the contact email (if provided)

Terrific Poll lets you create, embed, and track polls in any email newsletter, with easy response collection and analytics—even if your newsletter service doesn’t support polls natively.
```

### Identifying the Target Audience

Next, I asked it to think about the target audience. It effectively identified the main target audience as newsletter creators and publishers.

```md
1. Newsletter Creators & Publishers
   - Independent writers, bloggers, and content creators who send regular newsletters and want to engage their audience with polls.
   - Small businesses and startups using email newsletters for marketing, feedback, or customer engagement.

1. Marketing Teams
   - Email marketers looking to add interactive elements (like polls) to their campaigns without upgrading to expensive plans or add-ons.
   - Agencies managing newsletters for multiple clients across different platforms.

2. Organizations Using Diverse Email Platforms
   - Companies or groups using platforms that don’t natively support polls (eg., Beehiiv, Brevo, EmailOctopus, Ghost, HubSpot, Kit, Loops, MailerLite, Sendy).
   - Nonprofits, clubs, or educational institutions wanting to gather feedback or opinions from their mailing lists.

3. Anyone Wanting Polls in Email Without Technical Hassle
   - Users who want a no-code, copy-paste solution for adding polls to emails.
   - People who want analytics (response counts, percentages, respondent emails) without building their own system.

Terrific Poll is ideal for anyone who sends email newsletters and wants to easily add polls—especially if their platform doesn’t support polls natively or requires a paid upgrade to do so.
```

### Summarizing Main Benefits

The next step was to describe the main benefits of my product. The model summarized my product's benefits like a salesperson, highlighting eight key advantages.

```
1. Universal Compatibility
   - Works with any email newsletter service-even those that don't natively support polls.
   - No need to switch platforms or pay for expensive add-ons.

2. Easy Poll Creation
   - Simple interface to create polls: just name your poll, write a question, and add up to 10 response options.
   - No coding or technical skills required.

3. Seamless Embedding
   - Generates poll content that can be copy-pasted into any newsletter platform.
   - Supports popular services like Beehiiv, Brevo, EmailOctopus, Ghost, Hubspot, Kit, Loops, MailerLite, and Sendy.

4. Frictionless Response Collection
    - Recipients click a link in the email to vote-no forms or extra steps.
    - Contact email is pre-filled using newsletter service merge tags, making it easy for users to respond.

5. Real-Time Analytics & Dashboard
   - Instantly see how many responses each option received.
   - View percentage breakdowns for each response.
   - Access a detailed table with response data, including date and (if available) contact email.

6. No Platform Lock-In
    - You're not tied to a specific email provider or forced to upgrade plans just to use polls.

8. Improved Engagement
   - Polls increase interactivity and engagement in newsletters, helping you better understand your audience.

Terrific Poll makes it easy to add interactive polls to any newsletter, collect responses with a single click, and view detailed analytics—all without technical hassle or platform limitations.
```

### Handling Objections

Next, I focused on objection-handling statements, which are legitimate doubts that potential customers might have. The language model generated ten main objection-handling statement topics.

```md
1. Deliverability & Spam Concerns
   - "Will adding poll links affect my email deliverability or increase the chance of my emails being marked as spam?"

2. Privacy & Data Security
   - "How is my audience's data (especially email addresses) handled and protected?"
   - "Is Terrific Poll GDPR/compliance-friendly?"

3. Branding & Customization
   - "Can I customize the look and feel of the poll and confirmation page to match my brand?"
   - "Will my subscribers see Terrific Poll branding instead of my own?"

4. User Experience
   - "Will my subscribers find it confusing to click a link and be taken to a separate confirmation page?"
   - "Is the process seamless, or does it add friction?"

5. Integration Limitations
   - "Does it work with my specific newsletter platform and merge tags?"
   - "What if my platform doesn't support merge tags or has limited support?"

6. Response Tracking Accuracy
   - "How accurate is the response tracking, especially if people forward emails or click links multiple times?"
   - "Can people vote more than once?"

7. Cost & Value
   - "Is it worth paying for this service when some platforms offer basic polls for free or as a paid add-on?"
   - "Are there hidden costs or limitations?"

8. Technical Support & Reliability
   - "What if something goes wrong-how quickly can I get support?"
   - "Is the service reliable and always available?"

9. Data Ownership & Export
   - "Can I export my poll results and data easily?"
   - "Do I retain ownership of my data?"

10. Accessibility
    - “Are the poll links and confirmation pages accessible to all users, including those using assistive technologies?”
```

Since I was still hesitant to address those statements, I asked the language model to generate responses to each objection.

```md
1. Deliverability & Spam Concerns
   - "Will adding poll links affect my email deliverability or increase the chance of my emails being marked as spam?"

**Response:** Terrific Poll uses standard, reputable link formats that are compatible with all major email providers. Our links are designed to avoid common spam triggers, and we never include attachments or suspicious redirects. As with any email, following best practices—such as using a verified sending domain and avoiding excessive links—will help maintain high deliverability.

2. Privacy & Data Security
   - "How is my audience's data (especially email addresses) handled and protected?"
   - "Is Terrific Poll GDPR/compliance-friendly?"

**Response:** We take privacy and data security seriously. All data, including email addresses, is encrypted in transit and at rest. We never sell or share your audience’s information with third parties. Terrific Poll is designed with GDPR and other privacy regulations in mind, and we provide tools to help you manage, export, or delete data as needed.

3. Branding & Customization
   - "Can I customize the look and feel of the poll and confirmation page to match my brand?"
   - "Will my subscribers see Terrific Poll branding instead of my own?"

**Response:** At this time, the confirmation page cannot be customized with your brand’s colors, logo, or messaging. However, Terrific Poll does not display any visible Terrific Poll branding to your subscribers—the only reference is the domain name in the web browser’s address bar. The
experience is kept clean and neutral, so your audience’s focus remains on your poll question and options.

4. User Experience
   - "Will my subscribers find it confusing to click a link and be taken to a separate confirmation page?"
   - "Is the process seamless, or does it add friction?"

**Response:** The process is designed to be as simple as possible: one click takes the subscriber to a clear confirmation page where their choice is pre-filled. This extra step helps votes and gives users a chance to confirm their selection, improving data quality without adding confusion.

5. Integration Limitations
   - "Does it work with my specific newsletter platform and merge tags?"
   - "What if my platform doesn't support merge tags or has limited support?"

**Response:** Terrific Poll is compatible with all major newsletter platforms and supports a wide range of merge tags for pre-filling subscriber information. If your platform has limited merge tag support, the poll will still function—recipients can manually enter their email if needed. We provide detailed guides for the most popular platforms and are happy to help with custom
setups.

6. Response Tracking Accuracy
   - "How accurate is the response tracking, especially if people forward emails or click links multiple times?"
   - "Can people vote more than once?"

**Response:** Each response is tracked individually, and we use email addresses (when available) to help prevent duplicate votes. While forwarding emails can allow multiple responses from the same link, our dashboard highlights potential duplicates so you can review them. For most use cases, this provides a reliable and accurate picture of your audience’s preferences.

7. Cost & Value
   - "Is it worth paying for this service when some platforms offer basic polls for free or as a paid add-on?"
   - "Are there hidden costs or limitations?"

**Response:** Terrific Poll offers universal compatibility, advanced analytics, and customization that most built-in or add-on poll features can’t match. There are no hidden fees—our pricing is transparent, and you get full access to all features. For many users, the time saved and increased engagement more than justify the investment.

8. Technical Support & Reliability
   - "What if something goes wrong-how quickly can I get support?"
   - "Is the service reliable and always available?"

**Response:** We offer responsive customer support via email and chat, with most issues resolved within one business day. Our infrastructure is built for reliability, with high uptime and regular monitoring to ensure your polls are always available.

9. Data Ownership & Export
   - "Can I export my poll results and data easily?"
   - "Do I retain ownership of my data?"

**Response:** Absolutely. You can export your poll results at any time in CSV format. You always retain full ownership of your data, and we never use it for any purpose other than providing the service to you.

10. Accessibility
    - “Are the poll links and confirmation pages accessible to all users, including those using assistive technologies?”

**Response:** Accessibility is a priority for us. Our poll links and confirmation pages are designed to meet modern accessibility standards (such as WCAG), ensuring that all users—including those using screen readers or other assistive technologies—can participate without barriers.
```

### Assessing Market Maturity

The next task was to determine the market maturity, meaning whether the product market is new or emerging. Personally, I didn't know how to assess this; it's probably something a good marketer would do. Market maturity affects how much you need to educate your audience. If your product is in a new category, explain more. If it’s established, focus on differentiation. To assess, look for competitors, read reviews, and see how much your target audience already knows. I should learn more about how to evaluate it.

Asking the language model to determine the market maturity provided a quick fix for my lack of knowledge for now.

```md
The overall email marketing market is mature, but the specific niche of universal, embeddable, no-code polling for newsletters is new and emerging. There is clear demand, but the space is not yet crowded or saturated.

**Customer Awareness Stage: Problem-Aware to Solution-Aware**

- Problem-Aware:
    Most potential customers (newsletter creators, marketers, etc.) are aware that:
    - They want to engage their audience more.
    - Their current newsletter platform doesn’t support polls, or only does so with limitations or extra cost.
    - They may have tried workarounds (like Google Forms) but found them clunky or not well-integrated.
- Solution-Aware:
    Some customers may know that “email poll” tools exist, but:
    - They may not know a universal, easy, no-code solution is available.
    - They may not be aware of Terrific Poll specifically.
    - They may not realize how seamless and platform-agnostic a solution can be.
- Not Yet Product-Aware:
    Most of the target audience likely does not know Terrific Poll by name or its unique benefits, unless they’ve specifically searched for this kind of tool.

Terrific Poll’s audience is mostly problem-aware and solution-aware—they know they want to add polls to emails and may know some solutions exist, but are not yet familiar with Terrific Poll as the best or easiest option.
```

## Generating the Final Landing Page Copy

That was the last point. Now I could use my prompt to ask the language model to generate my landing page copy with all the input for my product.

Here’s the final landing page copy I ended up with (after some manual tweaks). Note: Since I didn’t have any testimonials or social proof yet, I focused on the product’s benefits and a clear call to action.

---

# Terrific Poll: Add Interactive Polls to Any Newsletter

**Easily create and embed polls in your email newsletters—no coding, no platform lock-in.**

Terrific Poll lets you engage your audience with interactive polls, even if your newsletter service doesn’t support polls natively. Just create your poll, copy-paste the content, and start collecting responses instantly.

- Works with Beehiiv, Brevo, EmailOctopus, Ghost, HubSpot, Kit, Loops, MailerLite, Sendy, and more
- No need to upgrade plans or pay for add-ons
- One-click response collection with pre-filled contact emails
- Real-time analytics and exportable results

**Ideal for:**
- Newsletter creators, marketers, agencies, and organizations using any email platform

**Objection-handling:**
- “Will this affect deliverability?” No—our links are designed to avoid spam triggers.
- “Is my data safe?” Yes—your data is encrypted and never shared.
- “Can I customize the look?” The experience is clean and neutral, with no visible Terrific Poll branding.

**Ready to boost engagement?**
[Start your first poll now]

---

If you don’t have testimonials or social proof yet, that’s perfectly fine. Focus on making your product’s value clear, and invite visitors to try it or join your early access list. As you get feedback from users, you can update your landing page with quotes or data points that show your product’s impact.

I made a few manual changes to adjust it to my taste, but overall, the changes were minimal.

## Reflections on the Process

The language model really helped me gain a better understanding of the market my product is entering and the possible target audiences. The prompt was effective in generating a draft for a landing page that I later used to design a landing page for my product.

It's astonishing that language models can assist us with this work. I would have needed to invest a significant amount of time in market research or hire a professional landing page copywriter.

Using language models as a tool, just like I do to help write code, for areas outside my expertise has really helped me cover my knowledge gaps in those areas, and it might help you too.

**Next steps:** Test your landing page with real users, iterate based on feedback, and keep learning. If you don’t have testimonials yet, consider inviting friends, colleagues, or early users to try your product and share their thoughts. For more, see [Copyhackers](https://copyhackers.com/) and the [Stripe Atlas guide](https://stripe.com/guides/atlas/landing-page-copy).
