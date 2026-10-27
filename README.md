# resume-tailoring-codex

`resume-tailoring-codex` is a lightweight resume and application workflow for Codex. It uses project instructions and connected plugins to assess a job posting, prepare a tailored copy of a resume in Google Docs, update an existing Google Sheets application tracker, and draft a cover letter in Google Drive. It is inspired by the workflow in [AI Job Search](https://github.com/ai-job-search-dev/ai-job-search).

This repository is an instruction-driven project, not a standalone application. It has no web interface, server, package installation, or LaTeX workflow.

## What you need

- **Codex** with this repository opened as a project so it can follow [`AGENTS.md`](AGENTS.md).
- **Google Drive plugin** connected to the Google account that owns or can access your resume, tracker, and cover-letter folder. The workflow uses Drive for native Google Docs, Google Sheets, and folders.
- **A browsing plugin** that can retrieve the job-posting URLs you use. Firecrawl is one supported option. If the page is blocked or unavailable, you can paste the complete job description in chat.
- An existing **Google Docs master resume**, **Google Sheets application tracker**, and **Google Drive parent folder** for cover letters. The project will not create a new tracker.

Plugin names and capabilities can vary by Codex environment. Google Drive must allow the relevant read and write operations for the workflow; `/setup` checks access without making test edits or copies. The workflow reports capabilities that it cannot verify.

## Set up

1. Clone or download this repository. In GitHub, choose **Code** and then **Download ZIP**, or clone it with Git.
2. Open the project folder in Codex. Confirm that `AGENTS.md` is present; it contains the project-specific workflow rules.
3. Connect the Google Drive and browsing plugins in your Codex environment. Grant the Google account access to the specific files and folder you intend to use.
4. In the project chat, send `/setup` as a regular message.
5. Provide the links to your master Google Docs resume, existing Google Sheets tracker, and Drive parent folder when asked. If the tracker has multiple tabs, choose the tab to use. Answer profile questions when you can; it is fine to say you do not know.
6. Review the setup report for accessibility, remaining questions, and capabilities that could not be confirmed.

Run `/setup` again when your resume, experience, tracker, or folder changes. The local candidate profile is updated with confirmed details rather than replaced from scratch.

## Use the workflows

Send these requests as ordinary chat messages; they do not need to be registered as Codex slash commands:

- `/setup` — configure or refresh your links, candidate profile, and access checks.
- `/apply https://example.com/job` — read a posting, compare its requirements with your evidence, score job fit, prepare a tailored Google Docs resume copy, and update the configured tracker when safe.
- `/coverletter https://example.com/job` — prepare a tailored Google Doc in a `Cover Letters` subfolder of the configured Drive parent folder. You can omit the URL to use the most recent usable application record.

Replace the example URL with the actual job-posting URL. If the browsing plugin cannot read the posting, paste the full description when asked. Review all generated content before using it. Job-fit and resume-quality scores are estimates, not predictions of an employer's decision. The project does not submit applications or send cover letters.

## Local files and privacy

The project stores user-specific information under `private/`:

- `private/config.json` — links to your master resume, tracker, selected tracker tab, and cover-letter parent folder.
- `private/profile.md` — evidence-backed candidate facts, their sources, and open questions.
- `private/applications/` — saved job details, assessments, and links to generated documents.

The repository's `.gitignore` excludes `private/` by default. Before committing or uploading, check the file list and make sure no personal data is staged. GitHub's website upload does not apply `.gitignore` automatically; omit `private/` manually if you upload files there. If sensitive content has already been committed, adding it to `.gitignore` will not erase it from the repository history.

Local files are not encrypted. Protect your computer and backups. Do not save OAuth tokens, passwords, or other secrets in this project. Connected services process information under their own account permissions and policies. Review the repository files before making a public fork or publishing your own copy.

## Scope and limitations

- The master resume is treated as the source of truth and is not edited unless you explicitly request it. Tailored resumes are copies.
- The tracker must be an existing Google Sheet. The workflow uses its current columns and preserves existing data and formatting; it does not add columns or submit applications.
- Posting access, Google Drive permissions, document copying/editing, Sheets updates, folder operations, and PDF/layout inspection depend on the connected tools. The workflow reports failures and checks it could not complete rather than claiming success.
- A resume's layout and page count can only be verified when the connected tools provide a suitable export or inspection capability.
- No resume can be guaranteed to pass an applicant tracking system or secure an interview.

