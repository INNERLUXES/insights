# Mobile App Development Tips: What We Tell Every Client Before the First Sprint

*By Muhammad Dilawar, Chief Technology Officer, INNERLUXES. First published 6 September 2026 on [innerluxes.dev](https://innerluxes.dev/application/mobile/development/tips). That page is the canonical version; this file is the Markdown source.*

Mobile app development tips from the CTO of a team that has shipped apps for ten years: what to decide before coding, native or cross-platform, design, testing, release and the year after launch.

*Editor’s note: Muhammad Dilawar runs engineering at INNERLUXES. These are the mobile app development tips his team repeats to every new client, collected here so you can read them before the kickoff call instead of learning them in month three. If you already know what you want built, the [mobile app development services](https://innerluxes.dev/application/mobile/development) page explains how we price and deliver it.*

I have sat in the kickoff meeting for more mobile apps than I can count. The ones that went badly did not fail because of a bug. They failed because of a decision that was never made, or was made in the wrong order. Most mobile app development tips you will read online are about code. Most of the trouble I have seen is not.

So this list starts before the code, spends some time in it, and then keeps going into the year after launch, which is where the money is either made or lost.

![Mobile app development tips: the decisions in order, from scoping to the year after launch](https://innerluxes.dev/assets/icons/hero-mobile-app-development-tips-icon.jpg)

## Decide these five things before anyone writes code

A client last spring asked my team to start sprinting in week one because the board wanted to see screens. We refused, politely, and spent that week on the five decisions below instead. He told me later it was the reason the app shipped on the date we gave him.

- **Who opens it and why, in one sentence.** "A field technician opens it to close a job and get paid faster" is a product. "An app for our customers" is a wish. If the sentence has two audiences, you are building two apps; decide which one goes first.

- **What already exists that the app must talk to.** The CRM, the ERP, the payment provider, the identity system. Every one of these is a contract, a rate limit and a sandbox you will need on day one. Get the sandbox credentials before the design phase, not during it.

- **What happens with no signal.** Warehouse, hospital basement, aircraft, rural delivery route. If the honest answer is "it must still work", the architecture changes completely and it is far cheaper to know now.

- **Which platform ships first.** Both at once is possible and we do it often, but a business with sixty percent of customers on iPhone should not delay the iOS release for Android parity.

- **What "done" means for version one.** Write the list of screens and the list of things the first version will not do. The second list protects the budget more than the first.

These five go into a short scope document that the client owns. At INNERLUXES the fixed price is put on that document, and the number does not move afterwards. That is only possible because the document exists.

## Native or cross-platform: how we actually choose

This is the question that fills the most forum threads and deserves the least agonising. My team ships both, and the rule we use fits on a card.

- **Cross-platform (React Native or Flutter)** when the app is mostly screens, forms, lists and network calls, and one team maintaining one codebase matters to the budget. That is most business apps: field service, customer portals, booking, internal tools, most fintech front ends.

- **Native (Swift and Kotlin)** when the app leans hard on the device: camera pipelines, Bluetooth medical devices, background location that must survive the OS killing it, heavy animation, AR, or anything where a platform feature ships on Monday and the client needs it on Tuesday.

- **Do not choose on hiring fashion.** A cross-platform app with a native module for the one hard feature is a normal architecture, not a compromise. We have built barcode scanning, payment terminals and health-kit integrations that way.

Whichever you pick, insist that the decision and the reason are written down. A year from now a new engineer will ask why, and "the vendor liked it" is not an answer you want to give.

## Design tips that decide whether people come back

Retention is decided in the first ninety seconds and in the first week. Our [mobile app design](https://innerluxes.dev/application/mobile/design) team measures both, and these are the things that move the numbers.

- **Let people do the main thing before they sign up.** Browse, calculate, scan, look up. Ask for the account when there is something to save. Apps that open with a registration wall lose a large share of first opens before the product is seen.

- **Design the empty states.** The first screen a new user sees is empty: no orders, no bookings, no data. If it says "No items", the app looks broken. If it shows what to do next, the app looks alive.

- **One hand, thumb reach, big targets.** Field workers wear gloves. Parents hold children. Put the primary action where a thumb lands and make it at least the size of a fingertip.

- **Follow each platform’s conventions** for navigation, back gestures and system dialogs. Users do not read your onboarding; they rely on what every other app taught them.

- **Test the design with five real users before the build.** Not colleagues. Five is enough to find the screen everyone gets stuck on, and fixing a screen in Figma costs an afternoon; fixing it in a shipped app costs a release.

## Engineering tips: architecture, offline, performance

These are the habits my engineers are held to on every project. None of them are exotic. All of them are skipped by teams in a hurry.

- **Put the API behind your own backend.** The app talks to a thin service you control, and that service talks to the CRM, the ERP and the payment provider. When a vendor changes an API, you change one server, not every phone in the field.

- **Treat offline as a feature, not an error.** Queue writes locally, sync when the signal returns, and show the user which items are waiting. A "no connection" dialog that loses the form is the fastest way to a one-star review from a delivery driver.

- **Version the API from day one.** Phones do not update on your schedule. Six months after launch, four versions of your app will be live at once, and the server has to answer all of them.

- **Measure cold start, and keep it under two seconds on a mid-range Android phone.** Not on the newest iPhone in the office. The mid-range phone is what most of the world carries, and it is where performance problems show up first.

- **Feature flags and remote config.** A flag lets you switch off a broken feature at 2 a.m. without a store review. It also lets you release quietly to ten percent of users and watch.

- **Crash reporting and analytics before the first external build.** If you cannot see it, you cannot fix it. The first week of a beta is the most information you will ever get for free.

- **Keep secrets out of the app.** Anything shipped in the binary can be read. Keys live on your backend; the app gets short-lived tokens.

## Testing and release tips

The app store is not your QA department, and a rejected build the week before a launch date is an avoidable kind of pain.

- **Test on a device matrix you chose on purpose.** Pull the device and OS breakdown from your analytics, or from your industry, and test on the top eight. Emulators are for developers; releases are for devices.

- **Automate the boring paths.** Login, the main flow, payment, logout, on every build, on real devices in a device cloud. Humans then test the new thing, not the old things again.

- **Read the store guidelines before the design is final.** Apple’s rules on account deletion, sign-in options and in-app purchases have rejected apps that were technically perfect. Google’s data-safety form has to match what the app actually collects.

- **Beta with real users through TestFlight and Play internal testing for at least two weeks.** Your first hundred users will find what your test plan did not.

- **Release in stages.** Ten percent, then fifty, then everyone, with the crash rate watched at each step. A staged rollout has saved more than one launch I have been part of.

## Security and compliance tips

If the app touches health, payments or personal data, security is not a phase at the end. It is a list of decisions at the start, and a regulator will ask to see them.

- **Decide what data never leaves the device** and what must never be stored on it. Both lists are short and both are usually blank in the brief.

- **Use the platform keychain and keystore** for anything sensitive; never the app’s own files.

- **Pin nothing you cannot rotate.** Certificate pinning done badly bricks the app when the certificate renews. Done well, it has a rotation plan.

- **HIPAA and GDPR are architecture, not a checkbox.** Where data is stored, who can export it, how it is deleted on request, and whether the crash reporter is quietly uploading screenshots with a patient’s name in them. We run a short compliance review before the first external build on every regulated app, and it is inside the fixed price.

- **Get a penetration test before the public launch,** from someone who did not build the app. Our [penetration testing](https://innerluxes.dev/security/penetration-testing) team does this for our own builds as well as for other vendors’.

## Cost and timeline tips, without numbers

You will notice this section has no figures. A price without a scope behind it is a guess, and in my experience the client always ends up paying for the guess. What I can give you are the things that move the cost most, so that you can control them.

- **Integrations, not screens, drive cost.** Ten simple screens are cheaper than one screen that talks to a legacy ERP through a partial API.

- **Every platform doubles the release work,** even with a shared codebase. Store listings, review cycles, device testing and crash triage are per platform.

- **Decisions delayed are the most expensive line item.** A week waiting for a logo, a licence key or a sandbox login is a week the team is paid for and you get nothing.

- **Ask for a fixed price on a written scope,** and ask what happens when the scope changes. At INNERLUXES a change of direction gets its own short written quote, approved first; the original number does not move. If a vendor cannot describe that process, expect the invoice to grow.

- **Budget for the year after launch,** not just the build. Two OS releases, a few store policy changes, and the features your first users ask for will all arrive within twelve months.

## After launch: the tips nobody gives you

Launch day is the middle of the project. Here is what the second half looks like when it goes well.

- **Reply to every store review in the first month,** especially the bad ones. Users update reviews when a real person answers, and future users read the replies.

- **Watch three numbers weekly:** crash-free sessions, day-seven retention, and the completion rate of the main flow. Everything else is noise until those three are healthy.

- **Ship something every two to four weeks.** A quiet app looks abandoned to the store algorithms and to users. Small releases also keep the team’s knowledge warm.

- **Plan the OS upgrade weeks.** Every September and every spring a new OS breaks something. Put the two weeks in the calendar in January.

- **Decide who owns the app.** Accounts, certificates, signing keys, the developer accounts themselves, in your company’s name. We hand all of it over at launch; a vendor who keeps the keys is a vendor you cannot leave. Our [mobile app support and maintenance](https://innerluxes.dev/application/mobile/maintenance-and-support) page describes what the year after launch looks like when you would rather we ran it.

## Questions clients ask us

**How long does it take to build a mobile app?** A first production release of a typical business app goes out in weeks, not quarters, once the five decisions above are made. The scoping phase tells you the dates for your app, and we put them in writing.

**Should we build for iOS or Android first?** The one your paying users carry. Pull the numbers from your website analytics or your customer records before the meeting; the answer is usually obvious once it is on paper.

**Can you take over an app another team built?** Yes, and it is common. The first two weeks are a written audit: what works, what is fragile, what is dangerous. Then a stabilisation sprint, then the roadmap. You keep the audit whether or not you continue with us.

**Do you sign an NDA before we send the idea?** Always, and before the first technical call. Most apps we build are under NDA, which is why the examples in this article are described without company names.

If you would rather talk than read, send the idea and the five decisions you have already made to the [mobile app consulting](https://innerluxes.dev/application/mobile/consulting) team. You will get a written response within one business day. The scoping workbook we use is public on GitHub: [github.com/INNERLUXES/insights](https://github.com/INNERLUXES/insights), alongside the Markdown source of this article.
