# Public-beta candidate — release notes

## Prepared in 0.5.0

- Empty first launch, zero household inputs, neutral equal-return example settings, separate fictional example button.
- Friendly field labels and click-to-read help. Persistent dropdowns for loan type, accrual and credit-card rules; event-type and target-loan menus. Dates use calendars; numbers use validated controls. Installment and APR schedules use date/amount dialogs.
- Advanced loan settings can be expanded without requiring typed calculation codes. Saved CSV fields retain their existing stable values.
- Persistent beta/planning notice, notices embedded in reports, and a complete Read before use page. Explicit exclusions for lender accuracy, historical interest, advice, investment assumptions, taxes/risk, mortgage approval and data privacy.
- Unsaved-change protection; stale reports visibly marked and calculated exports blocked until recalculation. Current input scenario saves remain available independently.
- Existing scenario ZIPs and old CSV folders supported. No personal scenarios included in the public artifact. App payload and source bundle are built from selected generic files, not the workspace or Downloads directories.
- Collected upstream runtime license texts, exact version inventory and source locations.

## Scope of testing

Automated calculation/CSV/scenario tests and offscreen desktop interaction tests run locally. The packaged Mac startup check loads fictional data. These checks do not establish correctness for every lender, transaction history or operating system. Public claims should describe it as a beta calculator, not an audited financial advisor or a guaranteed optimizer.

## Remaining publisher decisions before a production launch

1. Original Debt Lab code now uses the MIT License, credited to Debt Lab contributors. Set the public repository URL, confirm copyright attribution and choose the distribution channel before publication. Linking back is requested as a courtesy, not an added license restriction.
2. Review actual bundled dependency licenses and notices, Qt/PySide distribution/source and replacement/relinking obligations, and any commercial license choice. Collected texts and links alone do not certify compliance.
3. Sign and notarize the Mac build using the publisher's Apple Developer credentials. This candidate uses local signing and is not notarized. No credentials or signing identities were invented.
4. Test installation, saving, imports and calculations on independent target Macs. A Windows executable requires a Windows build and separate tests; it is not included here.
5. Verify representative real lender statements independently before making accuracy claims. Gather beta feedback and keep the known-limitation guide visible.

No site, store listing or public release has been published by this task. No financial data has been uploaded. These notes distinguish a completed local beta-preparation package from a production publication decision.
