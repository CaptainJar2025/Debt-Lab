# Debt Lab 0.8.0 — Public beta

A local desktop calculator for comparing debt payoff, emergency savings and hypothetical investment scenarios. **Planning estimates only.** It is not financial, investment, tax or legal advice, a lender statement, a quote, a guarantee or an investment forecast. Read [Read before use](READ-BEFORE-USE.md) and [Model guide](ASSUMPTIONS.md).

## Open the Mac beta

Unzip the public-beta download and double-click **Debt Lab.app**. The app bundles Python and Qt; users do not need Python installed. This build targets Apple Silicon Macs, macOS 14 or newer. It has been tested locally, is locally signed, and is **not Apple-notarized**. No Windows executable or Intel Mac build is included.

The public build starts with an empty loan list and zero household inputs. It contains no personal scenario. **Load fictional example** is an optional illustration with clearly labeled sample loans. The empty-start investment settings use 7% before and after payoff as editable illustrations, not predictions. Existing scenarios retain their saved return assumptions.

## Start with only what you want to model

1. **Loans:** Add loan. Choose its type from a dropdown; enter principal, unpaid interest, current effective APR, regular payment and next required date. Use the calendar for dates. Unknown remaining term is 0. Click a column heading for its explanation.
2. **More loan settings:** choose interest and minimum-payment rules from dropdowns. Edit installments and future APR changes in date/amount dialogs. Custom numbers remain editable. Student/card types override the generic accrual field as described in the guide.
3. **Loans + monthly payments:** enter the monthly extra in Payments & budget and Run comparisons. No income is required; this mode assumes payment funds are available and excludes household affordability.
4. **Full household budget:** optionally enter take-home income, essentials, savings and dated cash flows. Voluntary funds fill the six-month emergency target first. Cash outside the selected payment allowance remains uninvested.
5. **Results:** view payoff estimates and debt graphs. **Compare investing too** enables a separate hypothetical return comparison. Before/after-payoff assumptions are editable; each strategy switches after its own payoff date. The fixed-7% reference remains available.
6. **Dated cash flows:** enter events or inspect the read-only amortization/cash-flow ledger. Select a strategy/loan and export the ledger if needed.
7. **Save scenario file:** save current loans, budget and events in one standard ZIP. It contains unencrypted CSVs; keep it private. **Open scenario file** restores it. **Import old CSV folder** and individual table CSV options remain supported.

There is no autosave. The app marks unsaved edits and asks before discarding them on close or scenario replacement. Edited inputs mark previous results stale; calculated exports require a new run. Scenario saves preserve current inputs even before recalculation.

## What the results do not establish

- Exact lender billing, including capitalization, grace periods, fees, rounding, paid-ahead rules or issuer-specific minimums.
- Lifetime interest already paid, unless independently calculated from historical records outside this app.
- An investment advantage caused by debt freedom. A higher post-payoff return is only a chosen scenario; taxes, fees, inflation, market volatility and forced sales are absent.
- Mortgage preapproval or the value of unentered retirement accounts and other assets.
- A globally optimal repayment plan. Avalanche is an APR-priority heuristic.

Amounts and dates are conditional on the chosen inputs and horizon. Test against statements before acting.

## Source development

Requires Python 3.10 or newer and a graphical desktop:

```sh
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python -m debt_app
```

Windows: use `py -m venv .venv` and `.venv\Scripts\activate` for the first two steps. Source portability is not a claim that a Windows binary was tested.

```sh
python -m unittest discover -s tests -v
```

The engine tests verify important identities and edge cases; UI tests also need PySide6 and use its offscreen platform. Tests do not certify agreement with every contract. Source: `debt_app/engine.py` for simulation; `app.py` and `ui_fields.py` for controls; `report.py` for reporting; `scenario.py` for ZIP/CSV persistence.

## Build and distribution status

Install PyInstaller in the local environment, collect upstream license notices with `packaging/collect_notices.py` (network required), then build:

```sh
python -m pip install 'pyinstaller>=6.11,<7'
python packaging/collect_notices.py
PYINSTALLER_CONFIG_DIR="$PWD/build/pyinstaller-cache" python -m PyInstaller --noconfirm packaging/DebtLab.spec
```

Output on macOS: `dist/Debt Lab.app`. Its `--smoke-test` argument loads the fictional example and verifies packaged startup. Build each operating system on that operating system and test separately.

This is a **reviewable public-beta candidate**, not an uploaded production release. [Release readiness](PUBLIC-RELEASE.md) records remaining publisher work, including distribution terms/license review and Developer ID signing/notarization. [Third-party notices](THIRD-PARTY-NOTICES.md) accompany the runtime. No synced project reference files were modified.

## License and origins

Original Debt Lab code: [MIT License](LICENSE.txt). Built with AI tools from the musings of a chemical engineer in capital projects—an afternoon project that survived its creator’s testing, not an independently audited financial model. [Origins, limitations and the link-back request](ORIGIN.md). If you find it useful, please credit Debt Lab and link to the original repository once published.

## Alchemy-shop theme

Version 0.6 uses the supplied alchemy logo, brass accents, deep green controls and parchment reports. The fantasy presentation is decorative: financial field names, assumptions and warnings remain explicit. Debt Lab is a planning simulator, not a bank or lender.

## Planning tools in 0.7

- Minimum, avalanche, snowball and custom/Selected comparisons use the same budget and dates.
- Leave a regular payment blank to estimate it; enter remaining term for Standard/Student loans. Explicit 0 is not estimated. The Payment calculator explains estimates before running.
- Results show principal-weighted APR, daily interest equivalent, payoff milestones, payment sources, warnings and first-month allocations.
- Explore payments / bonuses compares extra $25/$50/$100 monthly and a funded one-time payment without changing your scenario.
- Reset to saved inputs restores the most recent save/open snapshot.
- Export readable report saves HTML; Print / save PDF uses the system print dialog. Reports contain private scenario details.
- Unused table headers follow the dark theme; ledger and timeline CSV money displays to cents.

### 0.8.0 simplification

Only Minimum, Avalanche and Snowball are shown. Main summaries and experiments use Avalanche. Selected/custom is removed; legacy lock fields are ignored with a notice. Each loan payoff gets a labeled chart flag, tooltip and date-table entry.

## New explanation tools in 0.8

- Compare saved plans: select two ZIPs, see changed fields and side-by-side outcomes; export the comparison as HTML.
- Break-even constant investment return: an explicitly bounded search using actual contribution dates, with fixed-return assumptions throughout.
- Cash-flow freedom: dated changes in required monthly payment proxies, plus a new chart option.
- Funding breakdown and reconciliation: monthly funds, dated additions, starting savings, spending and ending assets.
- Click payoff flags to jump to the exact final-payment row.

These tools appear in the continuously scrolling Results page and exported detailed report. Scenario comparison is also available before running a current plan.
