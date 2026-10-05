# An Agent Skill for Generating Multiple Customized CVs with a Single Prompt

Turn one Codex prompt and multiple job descriptions into one truthful, tailored LaTeX CV and PDF for each role.

This starter repository is for developers and IT students who want a repeatable CV-tailoring workspace. It ships with a reusable Codex skill, a safe input structure, and synthetic samples. Your candidate data, real JDs, generated CVs, and LaTeX build files stay local by default.

## What it does

1. Read every real JD in `input/target-JD/`.
2. Match each JD only against evidence in your local candidate materials.
3. Produce a focused, ATS-readable CV source, PDF, and short submission note per role.
4. Keep applications isolated so content from one company is not reused for another.

The skill does not invent experience, metrics, skills, or project details.

## Quick start

1. Clone this repository.
2. Keep the sample files as format references, or replace them locally.
3. Add your private materials directly under the appropriate `input/` subfolders:
   - `current-CV/`: your current CV PDFs or source files.
   - `CV-feedback/`: recruiter feedback and writing guidance.
   - `personal-information/`: facts used to complete a CV.
   - `Prism-data/`: approved LaTeX CV templates.
   - `projects-information/`: project evidence and neutral summaries.
   - `target-JD/`: one `.txt` file per job description.
4. Leave `input/target-JD/sample.txt` untouched; it is a format reference, not an application.
5. Run the prompt in [PROMPT.md](PROMPT.md) with Codex.
6. Find the generated files in `output/<company>_<role>/`.

The root `.gitignore` uses an allowlist. New files under `input/` and all generated `output/` files are ignored until you deliberately add a new public sample rule. Never use `git add -f` for candidate data.

## Input and output

Put private material directly in `input/current-CV/`, `input/CV-feedback/`, `input/personal-information/`, `input/Prism-data/`, `input/projects-information/`, and `input/target-JD/`. Add one real `.txt` JD per role to `target-JD/`; leave `sample.txt` as the format reference.

The project examples under `input/projects-information/` are based on real public work and show the evidence-plus-summary structure expected by the skill. Replace them locally with your own evidence. `input/Prism-data/` and every generated application directory under `output/` are entirely ignored by Git.

## Skill setup

The repository-local skill is at `.agents/skills/write-cv-by-jd/`. Use it directly when your Codex environment discovers project-local skills. Otherwise install or copy that folder to your Codex skills directory, then invoke `$write-cv-by-jd`.

The skill expects a LaTeX engine such as MiKTeX or TeX Live to build PDFs. It uses `latexmk` when available and can fall back to `pdflatex` for supported templates.

## Public samples

The two PDFs and `sample-ai-engineer-cv.tex` in `input/current-CV/` are real CV examples published by the repository owner. Their phone number and email address have been redacted; the name, professional history, public GitHub profile, and Hanoi location are intentionally public. `input/Prism-data/` remains local and is entirely ignored.

Do not put real contact details, government identifiers, private addresses, application notes, or unpublished project evidence in a public repository unless you intentionally want to disclose them.

The samples and all candidate-facing CV text are in English because that is the skill's output language. Review the staged diff before each push and never use `git add -f` for candidate data.

## Repository layout

```text
.agents/skills/write-cv-by-jd/  reusable Codex skill
input/                          local candidate evidence and JDs
output/                         generated application artifacts (ignored)
PROMPT.md                       one prompt for a multi-JD run
```

## Contributing

Keep contributed examples synthetic and remove personal, employer-confidential, and application-specific data. Improvements to the skill should preserve truthful, evidence-first CV writing and one-JD-per-output isolation.

## License

This project is available under the [MIT License](LICENSE).
