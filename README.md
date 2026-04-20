# Israel Handgun License — AI-Assisted Application

> **Hebrew supported** — If you speak Hebrew, Claude will respond in Hebrew. See also: [README בעברית](README.he.md)

An agentic Claude Code workspace that guides you through applying for an Israeli handgun license (רישיון לנשיאת אקדח). Claude checks your eligibility, collects the required information, and navigates the gov.il portal to submit your application on your behalf using Playwright.

## How It Works

1. Clone this repo and open it in Claude Code
2. Tell Claude: "Help me apply for a gun license"
3. Claude checks your eligibility under Israeli firearms law
4. Claude collects your personal and application details
5. A Playwright MCP server controls a real browser session
6. Claude navigates the gov.il portal, fills the application form, and submits it on your behalf
7. Claude guides you through the next steps (medical exam, status tracking)

No coding required.

## Prerequisites

| Requirement | Details |
|-------------|---------|
| [Claude Code](https://claude.ai/code) | Desktop app, VS Code extension, or CLI (`npm i -g @anthropic-ai/claude-code`) |
| [Playwright MCP](https://github.com/microsoft/playwright-mcp) | `npm install -g @playwright/mcp` |
| Node.js 18+ | Required by Playwright MCP |
| Israeli ID (ת.ז.) | Required to authenticate on gov.il |
| gov.il account | Register at [https://www.gov.il](https://www.gov.il) if you don't have one |

## Setup

### 1. Clone the repo

```bash
git clone https://github.com/tupe12334/israel-gun-license.git
cd israel-gun-license
```

### 2. Install Playwright MCP

```bash
npm install -g @playwright/mcp
```

### 3. Open Claude Code in this directory

```bash
claude .
```

The `.mcp.json` in this repo pre-configures the Playwright MCP server automatically.

## Usage

Once inside Claude Code, tell Claude:

> "Help me apply for a gun license"

Claude will:

- Ask about your eligibility category (settlement resident, security role, etc.)
- Collect your personal details, address, and supporting information
- Open a browser via Playwright and log in to gov.il
- Fill and submit the application form
- Guide you through scheduling a medical examination
- Track your application status

## Eligibility Categories

Under Israeli firearms law (חוק כלי ירייה, תשי"ט-1949), a personal handgun license requires one of:

| Category | Description |
|----------|-------------|
| תושב יישוב מוגדר | Resident of a defined security settlement |
| תפקיד ביטחוני | Security role (licensed security guard, etc.) |
| הסעת ערכים | Transporter of valuables (cash, jewelry) |
| ניצול שואה | Holocaust survivor |
| איום מוכח | Documented credible threat |
| אחר | Other exceptional circumstances (requires special approval) |

## What You'll Need to Have Ready

- Israeli ID number (מספר זהות)
- gov.il username and password
- Proof of eligibility (e.g., confirmation of residence in defined settlement, employment certificate for security roles)
- Recent passport photo
- Access to your phone for OTP verification during login

## What Claude Cannot Do

- **Medical examination** — Must be done in person at an authorized clinic
- **Background check** — Performed automatically by the Ministry; no action needed
- **Weapons training** — If required for your category, must be done at an approved range
- **Final licensing decision** — Made by the Israel Police Firearms Licensing Division

## Process Timeline

1. **Application submitted** → reference number issued (Claude handles this)
2. **Background check** → 7–21 days (automatic)
3. **Medical exam** → Schedule and attend in person
4. **Approval / rejection notice** → 30–90 days from submission
5. **If approved** → Purchase and register weapon within 6 months

## Privacy & Security

- Your personal data is stored only in `./data/` on your local machine and is gitignored
- The browser session runs locally via Playwright — no external proxies
- No credentials or personal data are sent to any third-party service
- Claude interacts with official government portals directly through your local browser

## Troubleshooting

**Playwright MCP not connecting**
Check that the MCP server shows green status under `/mcp` in Claude Code. Restart Claude Code after any changes to `.mcp.json`.

**gov.il OTP not arriving**
The portal sends OTP to the phone number registered with your Israeli ID. Ensure your details are current at [gov.il](https://www.gov.il).

**Application rejected**
The Israel Police Firearms Licensing Division will state the reason. Common reasons: insufficient proof of eligibility, medical fitness issues, criminal record.

## Contributing

Improvements to skills, portal automation, or eligibility logic are welcome. Open a PR or issue on [tupe12334/israel-gun-license](https://github.com/tupe12334/israel-gun-license).

## Disclaimer

This tool automates interaction with publicly accessible government web portals on your behalf. You are responsible for the accuracy of the information you provide. Misrepresenting information on a firearms license application is a criminal offense under Israeli law. This is not legal advice.

## License

Released under the [PolyForm Noncommercial License 1.0.0](LICENSE). Personal and noncommercial use only. Commercial use requires a separate written license from the author.
