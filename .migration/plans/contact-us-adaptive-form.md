# Contact Us Adaptive Form Plan (Document Authoring)

Build a simple **Contact Us** page for `prakrutikk/eds-chefspage` in Document Authoring, with an Adaptive Form that saves each submission as a row in a sheet in Document Authoring.

> Plan mode is on. To start building, switch to Execute mode.

## Decisions
| Topic | Choice |
|---|---|
| How the form is built | Turn on the Forms add-on and use it to build the form definition |
| Where submissions go | A sheet in Document Authoring, one row per submission |
| Consent | One checkbox covering email and SMS |
| Page location | `https://da.live/#/prakrutikk/eds-chefspage/contact-us` |
| Form definition location | `https://da.live/#/prakrutikk/eds-chefspage/forms/contact-us` |

## Form fields
| # | Label | Field name | Type | Required | Validation |
|---|---|---|---|---|---|
| 1 | First name | `firstName` | Text | Yes | 1–50 characters |
| 2 | Last name | `lastName` | Text | Yes | 1–50 characters |
| 3 | Mobile | `mobile` | Phone | Yes | Digits, optional leading `+`, 8–15 digits |
| 4 | Email | `email` | Email | Yes | Valid email format |
| 5 | I agree to receive communication by email and SMS | `consent` | Checkbox | No | Saved as true/false |
| 6 | Submit | `submit` | Submit button | — | — |

Success message: "Thank you! We'll be in touch soon." Fields that fail validation show an error message next to them.

## Approach
1. **Turn on the Forms add-on.** Enable it in the site's agent settings. Its tools become available on the next message, so this step needs one extra message before building can continue.
2. **Build the form definition.** Use the add-on to create the Adaptive Form definition with the fields above: rules for required fields and formats, the consent checkbox and the submit action.
3. **Add the form block to the site's code.** The site doesn't have a form block yet. Add the Adaptive Forms block, check it in the preview, run the lint, then commit and push to a feature branch. Pushing changes what's online, so I'll confirm with you before pushing.
4. **Create the form definition and submission sheet in Document Authoring.** Upload the definition to `/forms/contact-us`, and set up the sheet that receives submissions, with columns for first name, last name, mobile, email, consent and submission time.
5. **Create the Contact Us page in Document Authoring.** Upload `/contact-us` with a heading, a short intro, a Form block pointing to the form definition, and page details (title "Contact Us" and a description).
6. **Preview and test.** Preview the page and the form definition, fill in a test submission, check that the row lands in the sheet, then try empty and invalid values to check the error messages.
7. **Hand over.** Share the page link, the preview link and the submission sheet link, plus short instructions for editing the form later.

## Risks and open items
- **Content source.** The earlier preview error came from your AEM author instance, which means the site's preview may still read content from AEM rather than Document Authoring. If so, Document Authoring pages, including this one, won't preview until the site's content source points to Document Authoring. I'll check this first and tell you before changing anything.
- **Spam.** A sheet that accepts submissions can collect spam. I can add a simple honeypot field now, and a CAPTCHA later if needed.
- **Privacy.** The consent wording is a placeholder. Please confirm it, or give me your legal team's wording.
- **Access.** Uploading to Document Authoring needs the Adobe credentials option enabled in Settings, which already worked for the chef page fix.

## Checklist
- [ ] Turn on the Forms add-on (`forms-excat`) in the site's agent settings, then wait one message for it to load
- [ ] Check the site's preview content source (AEM author or Document Authoring) and report back before changing anything
- [ ] Build the Contact Us form definition with first name, last name, mobile, email, one consent checkbox and submit
- [ ] Add rules: required first name, last name, mobile and email; phone format; email format
- [ ] Add the success message and field error messages
- [ ] Add the Adaptive Forms block to the code and check it in the local preview
- [ ] Run the lint and fix any issues
- [ ] Confirm with you, then commit and push to a feature branch
- [ ] Upload the form definition to `/forms/contact-us` in Document Authoring
- [ ] Set up the submission sheet with columns firstName, lastName, mobile, email, consent and submission time
- [ ] Create the `/contact-us` page in Document Authoring with a heading, intro, Form block and page details
- [ ] Preview the form definition and the Contact Us page
- [ ] Send a test submission and confirm the row appears in the sheet
- [ ] Test empty and invalid values and confirm the error messages appear
- [ ] Share the page, preview and submission sheet links with editing instructions
