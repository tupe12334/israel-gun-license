# data/

This directory stores applicant data files generated during the gun license flow.

```text
data/
├── .gitkeep              # Keeps this folder tracked in git
├── README.md             # This file — canonical schema reference
├── example/              # Git-tracked reference showing the full schema
│   └── applicant.md
└── <id>/                 # One directory per applicant, named after their 9-digit Israeli ID
    ├── applicant.md      # All application data
    ├── session.md        # Login session state (written by login skill)
    ├── submission.md     # Application submission state (written by apply skill)
    └── *.pdf             # Supporting documents (residency cert, security license, etc.)
```

**Applicant subdirectories are gitignored** — contents are private and never committed.

---

## Schema — `<id>/applicant.md`

````markdown
# Gun License Application — <name>

```application-data
PERSONAL:
  id: <9-digit Israeli ID>
  name_he: <full name in Hebrew, as on ID card>
  name_en: <full name in English>
  date_of_birth: <DD/MM/YYYY>
  gender: <male|female>
  phone: <05X-XXXXXXX>
  email: <email address>
  address:
    street: <street name and number>
    city: <city or settlement name>
    zip: <7-digit ZIP>
    council: <regional council name, or "none">

ELIGIBILITY:
  category: <SETTLEMENT|SECURITY_ROLE|VALUE_TRANSPORT|HOLOCAUST_SURVIVOR|DOCUMENTED_THREAT|OTHER>
  category_description: <free text — supporting justification>
  existing_license: <true|false>
  license_number: <license number if existing, or "none">
  license_expiry: <MM/YYYY if existing, or "none">
  previous_refusals: <true|false>
  refusal_details: <details if previous_refusals is true, or "none">

IDF_SERVICE:
  served: <true|false>
  discharge_rank: <rank if served, or "none">
  discharge_year: <YYYY if served, or "none">
  specialty: <specialty or role if relevant, or "none">

WEAPON:
  type: handgun
  caliber: <9mm|.22|other|undecided>
  storage_location: <home|business|both>
  purpose: <free text — reason for personal carry>

APPLICATION:
  reference_number: <filled after submission, or "">
  submission_date: <ISO date after submission, or "">
  status: <draft|submitted|medical_exam_pending|under_review|approved|rejected>
  medical_exam_date: <ISO date if scheduled, or "">
  medical_exam_clinic: <clinic name if scheduled, or "">
  notes: <free text>
```
````

### Rules for skills

1. **Read `./data/README.md` first** before reading or writing any applicant file.
2. Use `mkdir -p ./data/<id>/` before writing for the first time.
3. Before writing, read the existing file (if any) to avoid overwriting data already collected.
4. `APPLICATION.reference_number` and `APPLICATION.submission_date` are written by `apply` after successful submission — do not set them before that.
5. Supporting documents live in `./<id>/`. Reference them by filename only.
