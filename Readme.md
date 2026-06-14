Julia Sets — Content Repository

This repo holds the dynamic content for the Julia Sets app: fun facts in English and Arabic, served weekly to students.

Structure

juliasets-content/
  manifest.json              ← version + file paths, read by the app first
  facts/
    facts_en.json            ← 52 weekly fun facts in English
    facts_ar.json            ← 52 weekly fun facts in Arabic
  .github/
    workflows/
      weekly-content-bump.yml  ← auto-opens a PR every Sunday

How it works


The app fetches manifest.json on launch (at most once per week).
If the version has changed, it fetches the updated fact files.
Facts are cached in AsyncStorage — the app works fully offline after first load.
The app shows one fact per session, rotating by funFactIndex stored per profile.
Facts are filtered by grade so younger students see age-appropriate content.


Adding a new fun fact


Open facts/facts_en.json
Add a new object at the end of the array:


json{
  "id": "w053",
  "week": 53,
  "text": "Your fun fact here.",
  "tag": "multiplication",
  "grades": [3, 4, 5, 6]
}


Open facts/facts_ar.json and add the Arabic translation with the same id and week.
Update manifest.json — bump the version (e.g. 1.0.1 → 1.0.2) and update updated_at.
Commit and push — the app will pick it up within 7 days.


Available tags

TagTopicnumber_senseBig numbers, place value, zeroadditionAdding, magic squaressubtractionSubtractingmultiplicationTimes tables, Vedic, area modeldivisionDividing, factorsfractionsFractions of a whole, equivalencedecimalsDecimal place value, metricpercentages% of a number, 10%, 100%integersNegative numbers, number lineratioRatio, proportionroundingRounding, estimationfactorsPrimes, LCM, HCFskip_countingCount by 2s, 3s, 5sodd_evenOdd and even numbersgeometryShapes, symmetry, hexagonspatternsFibonacci, sequencesalgebraLetters for unknownsscientific_notationPowers of 10historyHistory of maths

Weekly automation

Every Sunday at 06:00 UAE time, a GitHub Action opens a PR that bumps the manifest version and date. You can:


Merge to approve the weekly update (and add new facts if you have any)
Close to skip that week


The PR description reminds you how to add new facts each week.

Grades

Each fact has a grades array listing which grades it's appropriate for (1–8). The app uses this to filter facts by the student's grade.
