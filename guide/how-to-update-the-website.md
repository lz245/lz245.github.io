# How to update the Zhang Lab website

A guide for keeping **https://lz245.github.io** up to date.

You do not need to install anything, and you do not need to know how to code.
Everything in this guide is done in a normal web browser.

---

## How it works, in one paragraph

The website is built from a set of plain text files. When you change one of
those files and click **Commit changes**, GitHub notices, rebuilds the website
for you, and publishes it. Your change appears online about two to four minutes
later. You are only ever editing text — the design, layout, and colors take
care of themselves.

**Everything you do is reversible, and you cannot take the site down.** If a
change has a mistake in it, the website simply keeps showing the previous
version until the mistake is fixed. Nothing you type into a file can break the
live site for visitors.

---

## One-time setup

1. Create a free GitHub account at https://github.com (if you don't have one).
2. Ask **Dr. Zhang** to add your account to the website repository. He is the
   only person who can do this. You need "Write" access.
3. Accept the email invitation GitHub sends you.
4. Bookmark these two links:
   - **The files:** https://github.com/lz245/lz245.github.io
   - **The live website:** https://lz245.github.io

That's it. Setup is done forever.

---

## The four rules

Almost nothing you type can cause a problem. These four things can:

1. **Keep the two `---` lines.** Every news post starts and ends its
   information block with a line containing only three dashes. Don't delete
   them.

2. **Type quotes directly into GitHub — don't paste them from Word.** Word
   turns straight quotes into curly ones, and curly quotes stop the page from
   building. If you draft in Word, paste your text into GitHub and then retype
   any quotation marks.

3. **Dates are always year-month-day.** March 4, 2027 is written `2027-03-04`.
   Not `03/04/2027`.

4. **File names use dashes, never spaces.** `2027-03-04-new-grant.qmd`, not
   `March 4 new grant.qmd`.

---

## Add a news post

This is the most common task — new papers, awards, new lab members, events.

**The easiest approach is to copy a post that already exists.**

1. Go to https://github.com/lz245/lz245.github.io and click the **news**
   folder.
2. Open any existing post to see how it's written, for example
   `2026-07-12-psa-early-achievement-award.qmd`.
3. Go back to the **news** folder. Click **Add file** → **Create new file**.
4. In the file name box, type a name in this pattern — the date first, then a
   few words with dashes, then `.qmd`:

       2027-03-04-short-description.qmd

5. Paste in the template below and change the parts that need changing:

```
---
title: "Sunita receives a travel award"
date: 2027-03-04
author: "Zhang Lab"
description: >
  One or two sentences. This is the preview text people see on the news
  page and on the homepage.
categories: [Awards]
---

Write the post here in normal sentences. You can use as many paragraphs as
you like.

To make text bold, put two stars around it, like **this**. To add a link,
write it like [this](https://www.example.com).
```

6. For `categories`, pick whichever fits: `[Awards]`, `[Publications]`,
   `[Media]`, or `[Announcements]`.
7. Scroll down and click the green **Commit changes** button, then **Commit
   changes** again in the box that appears.

Your post automatically appears on the News page and in the "What's growing in
the lab" section of the homepage. You don't have to add it anywhere else.

---

## Add or update a lab member

The People page is built from six small files in the **data/people** folder,
one for each group:

| File | Who it holds |
|---|---|
| `faculty.yml` | Research faculty |
| `postdocs.yml` | Postdoctoral researchers |
| `staff.yml` | Research staff |
| `phd.yml` | Ph.D. students |
| `ms.yml` | M.S. students |
| `undergrad.yml` | Undergraduate researchers |

1. Open the right file and click the **pencil icon** (top right) to edit it.
2. Copy an existing person's block and change the details. A full entry looks
   like this:

```
- name: Jane Doe
  role: Ph.D. Student, Poultry Science
  photo: assets/images/team/jane-doe.jpg
  blurb: >
    One or two sentences about what they work on.
  award: Best Poster, IPSF 2027
  email: jd123@msstate.edu
```

3. The dash at the start of `- name:` marks the beginning of a person. Keep the
   spacing of the lines below it exactly as shown.
4. `photo`, `award`, and `email` are optional. **If you leave out the photo,
   the card shows the person's initials instead** — which looks perfectly fine,
   so don't hold up an update waiting for a picture.
   You can also add `scholar:` (a Google Scholar link) or `profile:` (an MSU
   profile link) on their own lines if you have them.
5. Click **Commit changes**.

**To remove someone**, delete their whole block — from their `- name:` line
down to the line just before the next `- name:`. To move them to Alumni, add
them to the alumni list in the `people.qmd` file instead.

---

## Add a publication

1. Open the **publications.qmd** file and click the **pencil icon**.
2. Find the right year heading, for example `## 2027`.
3. Add the new paper as number 1 at the top of that year's list, and renumber
   the ones below it.
4. Match the style of the papers already there:

```
1. Author, A., Author, B., & **Zhang, L.\*** (2027). Title of the paper.
   *Journal Name*, 12(3), 100456. [DOI](https://doi.org/10.xxxx/xxxxx)
```

   - Two stars around **Zhang, L.** makes his name bold.
   - The `\*` right after his name marks him as corresponding author. Leave it
     off if he isn't.
   - Single stars around the journal name make it italic.
5. Click **Commit changes**.

If the total count near the top of the page (currently "67+") has fallen behind,
you can update that number in the same edit.

---

## Fix a typo anywhere

1. Find the page on the website, then open the matching file on GitHub:

| Website page | File to edit |
|---|---|
| Home | `index.qmd` |
| People | `people.qmd` |
| Research | `research.qmd` |
| Publications | `publications.qmd` |
| Teaching | `teaching.qmd` |
| Join Us | `join.qmd` |
| A news post | the matching file in the `news` folder |

2. Click the **pencil icon**, fix the text, click **Commit changes**.

You'll see some markers that look like `::: {.something}` or
`[text]{.something}`. Those control the layout. Change the words around them,
not the markers themselves.

---

## Adding photos

1. Go to the **assets/images/team** folder.
2. Click **Add file** → **Upload files** and drag your picture in.
3. Name the file in lowercase with dashes: `jane-doe.jpg`.
4. Click **Commit changes**.
5. Point to it in a person's entry as
   `photo: assets/images/team/jane-doe.jpg`.

**One important rule: shrink the picture first.** Photos straight from a phone
or camera are very large and will make the website slow to load. Before
uploading, resize the image so the file is **under about 500 KB**. On Windows,
open it in Photos and choose Resize. On a Mac, open it in Preview and choose
Tools → Adjust Size.

---

## How to check your change worked

1. After you click **Commit changes**, go to the **Actions** tab at the top of
   the GitHub page.
2. Your change appears there with a spinning yellow dot while the site
   rebuilds. It becomes a **green check** when it's finished — usually about a
   minute.
3. Wait one more minute, then open https://lz245.github.io and press
   **Ctrl+Shift+R** (Windows) or **Cmd+Shift+R** (Mac) to force the page to
   load fresh rather than from memory.

Your change should be there.

---

## If something looks wrong

**First, don't worry.** The live website is fine. It keeps showing the last
good version until the problem is sorted out.

**If you see a red X in the Actions tab**, your change had a small formatting
error and was not published. Nine times out of ten it is one of these:

- A curly quote pasted in from Word (see rule 2)
- A missing `---` line
- A date written in the wrong format
- The spacing changed in one of the `data/people` files

Go back to the file, click the pencil, and fix it. Saving again starts a fresh
attempt automatically.

**To undo a change completely:**

1. Open the file on GitHub and click **History** (top right).
2. Click the version from before your change.
3. Use the **...** menu → **View file**, copy what's there, and paste it back
   into the current file.

Or just ask for help — nothing is ever lost, and every past version is saved
permanently.

---

## What not to change on your own

These control how the site looks and how it's organized. Changing them can make
the site look broken, so please ask before touching:

- `styles/` — colors, fonts, spacing
- `_quarto.yml` — the navigation menu and site settings
- `_partials/` and `_templates/` — page framework
- `.github/` — the automatic publishing setup
- **`docs/`** — this folder is generated automatically. Never edit anything
  inside it; your changes there will be overwritten the next time the site
  rebuilds.

Adding new pages, changing the menu, or altering the design are all perfectly
possible — they just need someone comfortable with the setup.

---

## Who to ask

- **Access problems** (can't log in, can't edit): Dr. Zhang.
- **Something looks broken and you're not sure why:** take a screenshot of the
  red X in the Actions tab. It names the exact file with the problem, which
  makes it quick for anyone to help.

---

## Quick reference

| I want to... | Edit this |
|---|---|
| Post news, an award, a paper announcement | a new file in `news/` |
| Add or remove a lab member | a file in `data/people/` |
| Move someone to alumni | `people.qmd` |
| Add a publication | `publications.qmd` |
| Fix wording on a page | that page's `.qmd` file |
| Add a photo | upload to `assets/images/team/` |

**Remember:** save → wait 2–4 minutes → hard refresh the website.
