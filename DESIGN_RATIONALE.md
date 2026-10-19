# Sprout 2.0: Design Rationale

Scope: homepage (mobile and desktop) and the first five app-onboarding screens, designed as one continuous story with one mascot, **Ankur**.

## 1. The story in one line
"You do not need to understand markets today. You need three things in your hand, and Ankur will walk you through the rest." The website promises a calm, plain first step. The app keeps that promise screen by screen, and the progress indicator is Ankur growing from seed to bud, so the website's metaphor and the app's progress are the same object.

## 2. Stakeholder conflicts and how each was resolved

| Conflict | Resolution | Cost accepted |
|---|---|---|
| CEO wants a bold, playful mascot. Marketing wants it everywhere. Compliance wants a serious tone. | One restrained mascot. It guides, never sells, never appears next to a return figure or a risk message. Max one per screen. | Less "viral" character energy. |
| Compliance needs a 12px+ risk disclaimer visible without scrolling. | 13px risk band is inside the first 844px on the homepage hero and on onboarding screens 1, 2 and 5 (mobile and desktop). Hero height is fixed so it cannot be pushed below the fold. | The hero is shorter than Marketing would like. |
| Marketing wants video, a live ticker, referral and three pop-ups. | Video: yes, but tap to load (poster only on first paint). Referral: yes, a quiet strip. Pop-ups: none on first visit. Live ticker: deferred to phase 2 (needs a data feed, adds weight, and a moving number near risk copy is a compliance question). | Marketing gets 3 of 5 asks now. |
| Support sees "stuck at KYC" tickets. | Screen 2 is a checklist (PAN, Aadhaar-linked mobile, bank) before anything is asked. Screen 5 is an honest wait state: what is done, what is in progress, "you can close the app". | Adds one screen before the first input. |
| Engineering: 3 weeks, one front-end dev, 1.5 MB page weight. | Inline SVG, one font family (Hind), no hero photo, CSS-only motion. Video loads on tap. | No illustration-heavy hero. |
| Hindi later, without redesign. | One font covers Latin and Devanagari. Layouts tested with a Hindi draft (screen 2). Line heights and button widths have slack. | Hindi copy still needs professional review. |

## 3. Data caveats (what the brief gives us, and what we do not know)
- Funnel from the brief: 40,000 visits to 9,000 app-install clicks is 22.5%. 9,000 to 3,000 KYC starts is 33%. Overall visit-to-KYC-start is 7.5%.
- The 78% bounce figure is flagged as unreliable. I treat it as a symptom to investigate, not a target, and I do not design to a number I cannot trust.
- The cause of the 62% KYC drop is unknown. Every KYC decision here is a **hypothesis**: people arrive without the documents, the Aadhaar OTP phone is not at hand, and they get no feedback during the wait.
- The survey is biased toward people who already finished or complained, so it informs wording, not priorities.
- "Many" Hindi users is not a number. Hindi is designed in, but not launched until we measure it.

## 4. Three-week plan, one front-end developer
- **Week 1:** tokens, mascot SVGs, homepage mobile, risk band and CTA tracking. Ship behind a flag. Add analytics events (below).
- **Week 2:** onboarding screens 1 to 5, checklist, wait state. Desktop homepage ("text me the link" phone input).
- **Week 3:** accessibility pass, performance pass, A/B setup, compliance sign-off, Hindi copy review (not launched).
- **Cut if late, in this order:** desktop phone preview, referral strip, FAQ accordions. Never cut: risk warning, checklist screen, wait state.

## 5. Performance budget (estimate, not measured)
Page limit 1.5 MB. Design target under 300 KB on first load. Estimated: HTML+CSS about 25 KB, inline SVG about 15 KB, Hind subset about 60 to 90 KB, video poster as a compressed SVG or small WebP under 40 KB, video itself 0 KB until tapped. These are estimates from the choices above and must be confirmed with a real build.

## 6. A/B and instrumentation plan
Events: `home_cta_tap`, `onb_step_view(n)`, `onb_step_exit(n)`, `kyc_doc_missing_tap`, `kyc_wait_close`, `lang_toggle`. Measure the real bounce rate first (fix the tracking), then test: (A) current vs (B) new homepage on visit to install click, and (C) with vs without the screen-2 checklist on KYC start to completion. Success is a relative lift with a pre-agreed minimum sample, not a hit on the 78% figure.

## 7. Compliance notes
- Banned words (guaranteed, safe, risk-free and Hindi equivalents) are checked by script on every board.
- The risk warning appears on screens 1, 2 and 5. Screens 3 (OTP) and 4 (PAN) carry no investing claims, so I omitted it for space. **Open question for Compliance:** whether every onboarding screen needs it. The layouts have room to add it if required.
- Aadhaar and PAN screens say why the data is asked and warn that Sprout never asks for an OTP or password on a call or chat.

## 8. Accessibility
Text contrast is AA or better (computed on the Mascot and System board). All tap targets are at least 44px, with 8px gaps. Progress is shown by shape, not colour. Motion is a slow leaf sway and stops under reduced-motion. Form fields have visible labels. Checked by script (text under 12px, targets, contrast, overflow, clipping) and by eye.

## 9. What I would do next
Test the screen-2 checklist with five real users. Get the Hindi copy reviewed by a native fintech writer. Measure real page weight. Revisit the live ticker once a compliance rule for moving numbers exists.
