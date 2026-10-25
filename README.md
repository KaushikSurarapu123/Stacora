# Stacora

Stacora is a free web app that guides a 15-minute standing heart rate test at home and turns the readings into a one-page summary a family can bring to a doctor. It was built for the 2026 Congressional App Challenge (TX-31).

**Live app:** https://stacora.vercel.app

## The problem

Postural orthostatic tachycardia syndrome (POTS) makes the heart rate jump when a person stands up. It often starts in the teen years and is easy to miss, and most health apps ignore it. Doctors look for a sustained heart rate rise of at least 30 bpm after standing (at least 40 bpm for ages 12 to 19). Stacora helps people record that test carefully and share the result.

## What it does

- **Guided test:** a 5-minute lying-down timer, then a 10-minute standing timer, with prompts at 1, 3, 5, and 10 minutes. Optional spoken instructions.
- **Heart rate log:** the user enters their pulse at each mark (from a smartwatch or counted by hand). Blood pressure from the user's own cuff can be entered too, and the summary flags a drop of 20/10 or more after standing.
- **Results page:** a chart, a readings table, and a plain-language note on whether the rise reached the 30 or 40 bpm mark. It never diagnoses.
- **Context and symptoms:** the user can note things that affect the test (caffeine, sleep, fluids, illness) and symptoms during it. These appear on the summary.
- **Doctor summary:** print or save the page as a PDF. It includes a list of questions to ask the doctor, tailored to the result and symptoms.
- **Find care near you:** opens Google Maps searches for the right kind of doctor, using a ZIP code or the device location. Stacora never sees or stores the location.
- **Chart feedback (AI):** the user uploads a screenshot of a heart rate chart, and an AI model explains it and suggests next steps.
- **Safety:** an "I feel unwell" button stops the test at any time and shows what to do.
- **Saved results (optional):** results are stored only on the user's own device, and only if they choose to save them. A small chart shows the rise across saved tests.
- **Install as an app:** on a phone, "Add to Home Screen" gives Stacora its own icon and full-screen view.

## How it works

- `index.html` is the whole app: HTML, CSS, and JavaScript, with no frameworks.
- The timer uses the clock time instead of counting ticks, so it stays accurate if the screen sleeps.
- The rise in heart rate is each standing reading minus the resting reading. It is compared to 40 bpm for ages 12 to 19, and 30 bpm for ages 20 and older.
- The chart is drawn as an SVG by the app's own code.
- `api/analyze.js` is a small server function on Vercel. It keeps the OpenAI API key on the server, accepts only JPG and PNG images, limits each visitor to 5 requests a minute, and uses a fixed prompt.

## Privacy

- Nothing is saved unless the user taps "Save this result on this device."
- A chart image is sent to OpenAI only when the user uses Chart feedback. The page warns users to crop out names and personal details.
- The app does not use accounts and does not collect personal information.

## Limits

- Stacora is a student project. It has not been clinically validated.
- It is educational only and does not diagnose POTS or any condition.
- It does not measure blood pressure. It only records readings the user takes with their own cuff.
- A single home test can be affected by caffeine, hydration, illness, sleep, and how the pulse was measured.
- Find care opens search results. It does not recommend or verify any doctor.

## AI disclosure

Parts of this project were built with help from AI tools. The chart feedback feature uses an OpenAI model.

## What I would build next

- A hand-checked directory of clinics that treat POTS.
- Spanish language support for families in our district.
- Testing with doctors and patient groups.
