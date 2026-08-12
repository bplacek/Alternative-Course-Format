# Alternate Training Formats

This repository contains learner-facing HTML alternate formats for selected training courses, along with the script used to generate them from exported course JSON.

The generated pages are intended to provide a simpler, more accessible reading experience for keyboard users and screen-reader users. They preserve course structure and core learning content, but they do not reproduce the full behavior of the original training platform.

## What is in this repo

 published alternate-format HTML pages

## Viewing the alternate formats

If this repository is published with GitHub Pages, start from `generated/index.html`.

If you are browsing the repo locally, open `generated/index.html` in a browser and use that page to navigate to individual courses.

Current generated examples include:

- MATLAB Onramp
- Simulink Onramp

## Accessibility approach

The generated pages are designed to:

- use semantic headings and landmarks
- keep primary lesson content expanded by default
- present course, module, and lesson structure in a single page
- include readable video summaries and transcripts when available
- convert interactive practice into read-only guided steps
- support keyboard navigation and screen-reader review more directly than the source platform

## Important limitations

- These pages are alternate formats, not full replacements for the original course platform.
- MATLAB execution, grading, progress tracking, and other platform-specific interactions are not reproduced.
- Practice activities are rewritten as guided, read-only content.
- Quiz blocks may appear only when the generator can produce a conservative, high-confidence question from the source material.

## Regenerating the HTML

The generator is a standalone Node.js script with no external package install step.

Generate one course:

```powershell
node scripts/generate-accessible-course.js "course examples\MATLAB\MATLAB Onramp.json" "generated\MATLAB Onramp.html"
```

Generate all supported courses in the sample tree:

```powershell
node scripts/generate-accessible-course.js "course examples" "generated"
```

Generate one course with explicit Brightcove settings:

```powershell
node scripts/generate-accessible-course.js "course examples\MATLAB\MATLAB Onramp.json" "generated\MATLAB Onramp.html" --brightcove-account 123456789001 --brightcove-player default
```

## Generator behavior

The generator currently supports:

- MATLAB-style exported course JSON
- Simulink manifest-style course JSON
- directory mode that recursively discovers supported course inputs
- automatic creation of `generated/index.html` when generating a directory
- default Brightcove embeds for MathWorks-hosted course videos
- optional Brightcove account and player overrides

## Notes for maintainers

- Update generated HTML by rerunning the generator rather than editing the output files by hand.
- If a Simulink manifest references missing concept content, generation fails with the missing paths called out explicitly.
- Optional course header imagery is resolved from files in `images/` when matching assets are available.
