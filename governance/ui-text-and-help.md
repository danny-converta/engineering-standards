# UI Text: Labels, Helper Text and Tooltips

> Authoritative standard for the words that explain an interface: field labels, helper text, tooltips, option descriptions and empty states, across all web, desktop and mobile apps.

## Purpose

Most support questions about a working feature are really questions about its words. A setting called "Match opportunities by" with options named after database relationships is correct and useless: the person filling it in cannot tell what will happen or what to do next. Clear help text is cheaper than a guide, a training call or a bug report that turns out to be a misunderstanding.

This standard defines who we write for, which kind of text goes where, and the rules every piece of explanatory text follows. It is mandatory for all user-facing screens.

## The Reader

Write for **someone who has never seen this app and does not know its internal words**. They are a capable adult in a hurry, not a child: keep the tone plain and respectful, and never talk down.

Assume they do not know:

- what any of our internal terms mean (record types, statuses, "sources", "pipelines", "categories" as we use them);
- how one screen affects another;
- what happens if they leave a field empty;
- where else in the app they need to go to make the setting do anything.

If a new member of staff could read the text and still need to ask a colleague what to do, the text is not finished.

## Where Each Kind of Text Goes

| Text | Where it shows | What it is for | Rule |
| ---- | -------------- | -------------- | ---- |
| **Label** | Always, on the control | Names the thing in the reader's words | 1 to 4 words, sentence case, no internal names |
| **Helper text** | Always, under the control | What to enter, or what the setting does, and what happens if it is left empty | 1 to 3 short sentences. Anything the reader **needs** to fill the field in correctly goes here |
| **Option description** | Under each choice in a select, radio group or toggle group | What choosing this option means, in one line | Required when the options are not self-explanatory |
| **Selected-option explanation** | Under the control, once a choice is made | How to make the chosen option work, including where to go next | Use it when an option depends on something done on another screen |
| **Tooltip / info icon** | On hover, focus or tap | Extra detail and background: the "why" | Never the only place required information lives (see Accessibility) |
| **Section intro** | Under a section heading | What this group of settings is for | One sentence |
| **Empty state** | Where data would be | Why it is empty and the one action that fills it | A sentence and a button or link |
| **Placeholder** | Inside an empty input | An example of the format | Never a substitute for a label or helper text; it disappears when typing starts |

Errors, toasts and confirmations follow [Notifications & Confirmations](/standards/governance/notifications-and-confirmations).

## The Rules

1. **Say what it does, in the reader's words.** Describe the outcome they will see, not the mechanism. No table, column, enum or code names ("membership source", "FormCategories", "Money13"), and no acronym without spelling it out the first time.
2. **Say where to click.** When a setting only works together with something on another screen, name that screen and the steps, using the exact button and field labels: "Open the deal, click **Edit** and choose the stage under **Pipeline stage**."
3. **Say what happens when it is left empty.** Every optional field explains its blank behaviour: "Leave it empty and Orbit works one out from where the stage sits."
4. **Give an example for every number, percentage, date or format.** "Out of 100, how likely a deal in this stage is to be won (50 means half of them). A £10,000 deal at 50% counts as £5,000."
5. **Describe every option that is not self-evident.** A select whose choices need thought gets a one-line description under each option. Put the recommended option first and label it "(recommended)". Do not label an option "(default)" unless the reader can act on that fact; say what an untouched setting does in the helper text instead.
6. **One idea per sentence.** Aim for sentences under 20 words. Helper text is at most three sentences; a tooltip is at most about 50 words. If it needs more, the feature needs a guide link, not a longer tooltip.
7. **Use the same word for the same thing everywhere.** If the dashboard says "deal", the form, the tooltip and the guide say "deal" too (or define the pair once: "a deal (an opportunity)"). Refer to on-screen labels exactly as they appear, in bold in docs.
8. **Explain consequences that are hard to undo or easy to miss.** "Every deal they have moves together." "This stage's value is left out of every money total."
9. **Keep it true.** Help text is part of the feature. When behaviour changes, the text changes in the same pull request, and a reviewer checks the words against the code. Text that promises behaviour the code does not have is a bug.
10. **Plain, friendly, adult tone.** No jargon, no blame ("you entered an invalid..."), no filler ("simply", "just", "easily", "please note"). Address the reader as "you".
11. **UK English, never an em dash.** Follow the [Documentation Standards](/standards/governance/documentation-standards) punctuation rules: sentence case, UK spelling, and the mark the sentence calls for (colon, semicolon, comma or parentheses) instead of a dash.
12. **Do not explain the obvious.** "Name" needs no helper text. Spend words where people actually get stuck: settings that affect other screens, numbers, and choices between similar-sounding options.

## Accessibility

- **Required information is never tooltip-only.** Tooltips are invisible on touch screens until tapped, are missed by many keyboard and screen reader users, and disappear while the reader acts. If someone needs it to fill the field in correctly, it is helper text.
- **Info icons are reachable and named.** An info icon is focusable, has an accessible name ("More about Deal value"), and shows its tooltip on focus as well as hover. In MUI, set `enterTouchDelay={0}` so a single tap opens it on touch screens.
- **Helper text is linked to its control** (`aria-describedby`; MUI's `helperText` does this) so screen readers announce it with the field.
- **Contrast**: helper and caption text meets WCAG 2.1 AA contrast like any other text (see [Accessibility Standards](/standards/governance/accessibility-standards)). Never below 12 px.

## Examples

These come from a sales pipeline stage's settings. The "before" text was accurate; it just assumed the reader already understood the system.

| Setting | Before | After |
| ------- | ------ | ----- |
| Option: The opportunity itself | "Each opportunity is put into this stage on its own, from the opportunity itself." | Menu line: "You pick the stage on each deal." Under the box once chosen: "Choose the stage under **Pipeline stage** when you create the deal, or later by opening the deal, clicking **Edit** and changing **Pipeline stage**. One company can have deals in different stages at the same time." |
| Option: Their contact or organisation | "An opportunity appears here when its contact or its organisation is tagged with this category." | "A deal shows here when the contact or the organisation it belongs to is in this category. To move deals here, open that contact or organisation, click **Edit** and add this category under **Categories**. Every deal they have moves together." |
| Win probability | "How likely an opportunity at this stage is to close. Used to weight the forecast." | "Out of 100, how likely a deal in this stage is to be won (50 means half of them). The weighted forecast uses it: a £10,000 deal at 50% counts as £5,000. Leave it empty and it is worked out from the stage's position." |
| Deal value | "Which monetary fields on the form add up to an opportunity's value." | "Which money boxes on the form add up to a deal's value in this stage. A deal only counts here when at least one of them is filled in. Leave this empty to use every money box." |
| A dependent picker | "Which stage of the pipeline this opportunity is currently in." | "The stage this deal is in now. Only stages set to match 'The opportunity itself' are listed. Choose **No stage** to take the deal out of the pipeline." |

## Implementation Notes

- **MUI text fields**: use `helperText` for always-visible help; it is wired to `aria-describedby`.
- **Selects with described options**: render each `MenuItem` as two lines (label, then a `caption` description) and set `renderValue` so the closed control shows only the label.
- **Info icons**: one shared component per app (for example `InfoTip`), not ad hoc `Tooltip` + icon pairs, so focus, touch and naming behave the same everywhere.
- **Keep option text with its options**: define each option's label, one-line description and "how to" text in one constant, so the menu, the caption and any guide stay in step.
- **Localised apps**: help text lives in the locale files like every other string; the rules apply to every language.

## Review Checklist

- [ ] Could someone who has never used the app fill this in correctly without asking anyone?
- [ ] No internal names, codes or unexplained acronyms
- [ ] Every setting that depends on another screen says where to go and what to click
- [ ] Every optional field says what happens when it is left empty
- [ ] Every number, percentage or format has an example
- [ ] Every non-obvious option has a one-line description; recommended option first
- [ ] Nothing the reader needs is only in a tooltip; info icons work by tap and keyboard
- [ ] Same word for the same thing as the rest of the app
- [ ] Text matches the code's actual behaviour, changed in the same PR as the behaviour
- [ ] UK English, sentence case, no em dashes, no "simply" or "just"
