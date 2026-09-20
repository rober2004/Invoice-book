# Invoice Book

Quoting and invoicing for construction and fabrication work. A Windows desktop
app that keeps your records in a folder on your own computer — no account, no
subscription, no cloud.

It was written to replace a folder of Word documents, and it is deliberately
small: quotes, invoices, progress claims, and the PDFs that go with them.

**[Download the latest version](../../releases/latest)**

<!-- Add a screenshot here before sharing this widely. A desktop app without
     one is a hard sell. Check it for real client names first. -->

---

## Installing

1. Download `Invoice Book Setup <version>.exe` from the
   [releases page](../../releases/latest).
2. Run it. **Windows will warn you** — see below.
3. On first launch it asks where to keep your records. Pick a folder you know
   how to find and back up.

### "Windows protected your PC"

You will see this, and it is expected:

> **Windows protected your PC**
> Microsoft Defender SmartScreen prevented an unrecognised app from starting.

Click **More info**, then **Run anyway**.

This appears because the installer is not code-signed. A signing certificate
costs money every year, and this is a small free app. SmartScreen is telling you
it has not seen this file often enough to vouch for it — not that it found
anything wrong. If that is not good enough for you, that is a reasonable
position: the app reads and writes your business records, and installing
software you cannot verify is a real decision.

---

## What it does

- **Quotes** — itemised, or priced as a whole with a written scope. Issue,
  mark sent, accept or decline.
- **Invoices** — including **progress claims** against a job, which carry
  "less previously claimed" arithmetic so the totals across a contract add up.
- **A quote becomes an invoice** without retyping it.
- **PDFs** named after the document: `INV-0047.pdf`. Three templates, with
  sections you can switch off.
- **Payments** recorded against invoices; paid, part paid and overdue are
  worked out rather than stored, so they cannot drift.
- **Clients, jobs and a saved-items list** that fills in prices you use often.
- **Australian tax invoices** — ABN, GST, and the wording that goes with them.

### What it does not do

It is **not accounting software** and does not try to be. No ledger, no BAS,
no payroll, no bank feeds, no Xero or MYOB sync. It produces the documents you
send to a client and keeps a record of what was sent and what was paid.

---

## Where your records live

In a folder **you choose**, not hidden in an application directory:

```
<your folder>\
  invoicebook.db      your records
  pdfs\               every PDF you have issued
  backups\            automatic copies
```

Back up that folder and you have backed up everything. There is no export step
and nothing held anywhere else.

**Nothing leaves your computer.** The app makes no network calls of any kind:
no telemetry, no update check, no account, no licence server. If you unplug the
network it behaves exactly the same.

### A note on Dropbox, OneDrive and Synology Drive

You can keep your records in a synced folder, and the app is built to survive
it — but it is worth knowing why that needs building at all.

A sync client keeps folders matching by **replacing files**. It has no way to
know when a database is open, and replacing a database file mid-write corrupts
it. That is not damage an app can prevent from the inside, and it is how this
app's own records were destroyed twice in forty minutes the day it first went
into real use.

So Invoice Book does not hold the synced file open. The live database sits on
your local disk, and the copy in your chosen folder is only ever written
**whole** — when you issue a document, after a pause, and when you close the
app. A sync client can copy, replace or roll that copy back as often as it
likes; the worst it can leave is an out-of-date file rather than a broken one.

The app tells you which folder it thinks is synced, and says so once when you
choose it.

---

## Two computers

Two people can use the same records folder, **one at a time**.

The second computer to open a workspace gets it **read-only**, and is told who
holds it. When both have written — because the sync service was offline, or a
machine was closed before its work was saved back — the app **detects that and
asks**, naming the other computer and when it wrote.

**Nothing is merged.** Two sets of records cannot be combined, by this app or
any other. One of the two continues and the other is kept as a file, and you
choose which. Whichever you pick, nothing is deleted.

This is honest rather than clever, and you should size it accordingly: it is
fine for two people who take turns. It is not a multi-user system.

---

## Backups

- A copy is taken **once on the first launch each day**, into `backups\`.
- A copy is taken **before any database upgrade**, separately.
- Nothing is ever deleted to make room, and the uninstaller never touches your
  records folder.

If the database is ever damaged — by a sync client, a power cut, a failing
disk — the app says so on startup rather than failing later in the middle of
your work, and offers to rebuild it from the parts that survived or to restore
a backup. The damaged file is always kept, never deleted.

---

## Requirements

- **Windows 10 or 11, 64-bit.** No macOS or Linux build.
- About 300 MB of disk for the app.
- No internet connection needed, ever.

## Updating

Download the newer installer and run it. It replaces the installed version and
leaves your records alone; the database is upgraded automatically on first
launch, with a backup taken first.

**Uninstall an older version rather than leaving it beside the new one.** Once
the new version has written to your records folder, the older one can no longer
open it — it will say so clearly and change nothing, but it is a confusing
minute you can avoid.

## Known limits in 0.1.1

- Windows only, 64-bit only.
- **Australian GST assumptions** throughout — the wording, the ABN field and
  the tax handling. It will not produce correct documents for other countries.
- Two-computer use detects conflicts and reports them; it does not merge, and
  it has not yet been tested on two physical machines over a real sync service.
- The installer is unsigned, so SmartScreen warns.
- Updates are manual. There is no update check, by design.

---

## Licence

MIT — see [LICENSE](LICENSE). Use it, change it, ship it.

It comes with **no warranty**, and that is worth reading rather than skipping:
this software produces documents you send to clients and asks for money with.
Check what it produces before you send it. Nobody is liable if it gets
something wrong.

## Bugs

Open an issue. Include what you did, what appeared on screen, and the version
from **Settings**. Please do not attach your database or any PDF with a real
client's details in it.
