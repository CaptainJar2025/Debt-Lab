# Debt Lab model guide

Read **Read before use** for the public-beta limitations. This guide describes what the calculator actually computes. Rates and percentages use numbers such as 6.5, not 0.065. Currency inputs and results are dollars. The same engine and assumptions apply to every compared strategy.

## Opening snapshot and horizon

Each loan starts with current principal, opening unpaid interest, and any opening fee. Historical payments and interest already paid are not reconstructed. Enter only the remaining balance and future required installments. Dates before the simulation start are ignored; they do not reconstruct arrears. The horizon includes the start date and excludes the evaluation date, calculated in calendar months from the start. Monthly anniversaries clamp to the end of short months. The maximum horizon is 600 months.

There is no new spending on a revolving account unless represented by a new opening balance. No loan forgiveness, refinancing, consolidation, subsidies, automatic capitalization, deferments, income-driven payment rules or future credit purchases are inferred.

## Independent modes

**Loans + monthly payments** assumes a monthly amount equal to the sum of the initial regular payment amounts plus your chosen extra is available. It answers what would happen if those funds were available. Income, living expenses, initial emergency savings and mortgage eligibility are excluded. Expense events are excluded and counted in the result. Dated income events are additional assumed funds. A one-time payment event supplies additional assumed funds and requests their allocation; entering both income and payment for the same money double counts it in this mode.

**Full household budget** uses your entered take-home income, essentials and savings. If take-home is after retirement deductions, do not deduct them again. Regular income and expenses post at the start and each monthly anniversary. Dated income is additional income: set regular income to zero for an irregular-only paycheck schedule. Expenses consume cash first, then emergency savings; any unmet amount is reported. A payment event requests an allocation from existing cash and the current allowance; it does not add money in Full budget.

## Cash, payment budget and emergency fund

The initial regular payment amounts plus requested extra create a fixed monthly spending allowance. Released payments remain in that allowance. Additional dated income increases that month's allowance. Unspent allowance expires at the next monthly anniversary; cash remains. Money outside the allowance remains uninvested cash rather than automatically going to investments or emergency savings.

Required debt payments take priority. Future installments before the next monthly cycle reserve both cash and allowance before voluntary uses. Active fixed-payment loans reserve their full installment, even if the current payoff balance is smaller, because interest can accrue before the due date. Large maturity balloons or growing card minimums may exceed the chosen allowance; required amounts can still be paid from available cash and reported separately. The engine does not invent borrowing to resolve a shortfall.

The Full-budget emergency target is six times essential expenses, excluding debt service. Voluntary dollars first fill that target. After a withdrawal, voluntary debt payments and investing pause until it is restored; mandatory debt payments continue. A zero essential-expense input creates a zero target, not a separately estimated living-cost requirement. Savings earn no interest here. Once the target is met, available allowance can go to debt or the hypothetical investment projection.

## Loan controls

**Loan type** is Standard, Student, BNPL or Credit Card. Loan names must be unique; they are used to target dated payments. No account numbers are needed.

**Regular payment** is the contractual installment or an approximate regular amount. It excludes the scenario's extra budget. **Next required payment** is the next actual due date; it can be far in the future when a loan is paid ahead.

**Payments remaining** counts monthly required installments from that date. Zero means unknown: continue regular installments until payoff or horizon, without inventing maturity. For a positive Standard/Student term, the last scheduled installment is a balloon for the remaining balance. It is not merely a descriptive term field.

**Daily simple** interest accrues on principal alone. **Daily compounding** accrues on principal plus unpaid interest. **Monthly** posts APR/12 on principal plus unpaid interest on the due day after the start; partial first months are not prorated and nothing is newly charged on the opening date. Daily accrual precedes same-day payments. Internal calculations use unrounded floating-point amounts; display rounds to cents. Lender rounding can differ.

**Student** always uses daily simple interest with the selected day denominator, such as 365 or 365.25. There are no automatic capitalization events. The generic Interest method field is ignored for this type.

**Credit Card** always uses APR/365 daily compounding on a single revolving bucket without a grace period. The generic Interest method and Days per year fields are ignored. The minimum is capped at balance and uses the greater of the selected dollar floor and either (a) principal × minimum percentage + unpaid interest + fees, or (b) total balance × minimum percentage. Issuer formulas, multiple APRs and statement-close/due-date lag can differ; defaults are illustrative.

Payments go to fees, then unpaid interest, then principal, capped at the balance. An extra principal payment does not advance future required dates. Opening unpaid interest is not historical interest already paid. Opening fees are charged once and do not earn interest. A configured late fee is charged on each due date when available cash cannot cover required installments, without contractual grace periods or fee caps. Arrears carry forward and are paid when cash is available. Use only fees supported by the actual agreement.

**Installment dates** specifies a BNPL remaining schedule of dates and total amounts required. It replaces monthly installments for that loan. A schedule that does not cover principal, interest and fees can leave residual debt. The pay-in-4 button creates a generic editable zero-interest example with four equal installments 14 days apart, starting at the simulation start. It is not a provider offer, contract, or promise of eligibility.

**Future APR changes** are dated replacements of the effective APR, not additional discounts. They apply before that day's accrual and payment ranking. Earlier changes apply when the simulation starts after them. Dates must be unique. The app does not determine future rate policy or discount eligibility.

**Paid-ahead voluntary payment** optionally requests monthly payments before the next required date. Set it to zero to disable. The first voluntary date must be earlier than the required date. Requests stop when required installments resume, do not create arrears, and expire if unfunded that day. In accelerated strategies they use the existing regular-plus-extra allowance, after emergency funding and before general extra allocation. The minimum strategy skips them. This models a fixed paid-ahead snapshot, not a complete servicer billing system.

**Locked extra** requests monthly dollars before the remaining avalanche allocation. It does not create additional funds or mandatory obligations. Unaffordable requests are processed in table order. Locks remain subject to cash and emergency rules.

## Strategies and fair comparison

Minimum pays required installments and invests unused available allowance. Avalanche pays available extra to the highest current effective APR, with table order breaking ties. Selected honors monthly locks before allocating the remainder by avalanche. Both accelerated strategies honor dated payment requests and paid-ahead voluntary requests; their difference isolates locks.

Every strategy receives the same input cash flows or assumed Loan-only funding and runs to the same date, including after payoff. A payoff later than the horizon is unknown, not never. Time saved is shown only when both compared strategies pay off within the horizon. Interest savings and override cost compare interest accrued inside the horizon; fees are shown separately. This is a rate-priority heuristic rather than a guaranteed global optimum.

## Investment projections and return switch

The independent fixed-return references are 7%, 3.3% and 1% annually effective. A fourth optional projection uses the editable before-payoff and after-payoff returns. These are alternative projections of the same deposits, not simultaneously funded accounts. The public empty-start setup uses 7% before and after; changing a return is a modeling assumption. A higher rate after debt freedom is not caused or guaranteed by the debt being repaid.

Growth is daily, before that day's deposits, using annual factor raised to 1/365.25. If the last debt is paid on a date, the new return applies the following day. If there is no opening debt, it applies from the start. Each strategy switches independently at its own payoff; one still in debt keeps the before-payoff return. The switch applies to the entire invested portfolio and future contributions.

The full original payment budget, including extra, continues after payoff. The unused part of the final payment month is invested, including same-day release of final payment reserves. Full-budget cash availability and emergency rules still apply. Investment returns are not withdrawn to pay loans or living costs; they never change the debt calculation. Taxes, fees, inflation, volatility, forced sales and account restrictions are excluded.

Net worth is modeled cash + emergency savings + one selected investment projection − remaining modeled debt. Assets or liabilities absent from the inputs are excluded. The report shows both strategies' uninvested cash and savings. Differences versus the 7%-throughout reference measure the effect of the return assumptions, not a verified price of flexibility or an expected investment advantage. Negative returns greater than -100% are accepted; the numeric upper limit is 1000%, which is a software bound, not a plausible forecast.

## Mortgage illustration

Monthly P&I room is max(0, gross monthly income × selected total-DTI fraction − modeled monthly debt obligation − taxes/insurance/HOA/PMI). Borrowing amount is the present value of that P&I at the hypothetical mortgage rate and term. It is not approval, a quote or an estimate of property value. Gross income is separate from take-home; the report marks the illustration uncalculated when no gross income is entered.

The debt-obligation proxy uses current modeled balances and minimum rules, and excludes a loan whose first required date is at least a month away. BNPL uses its regular payment field as a monthly proxy even if an explicit schedule is biweekly. Underwriters may treat these debts differently. Credit history, down payment, lender-specific policies and other qualification limits are absent.

## Ledgers, exports and saving

The amortization ledger records payment dates and monthly checkpoints. For each loan, opening balance + accrued interest + added fees − payment = closing balance. Its period starts after the previous row. The APR column is the effective rate on the row date; accrual uses actual changes within the period. Opening interest and fees are already in opening balance. Payment components reconcile to the payment total.

Cash flows show deposits, expenses, debt payments, emergency changes, investment contributions and growth, and closing cash. In Loan-only mode the income column represents assumed funding. Contribution columns are deposits, not portfolio growth. Growth-only dates appear for the switched-return projection so its value can be audited.

Scenario ZIPs contain ordinary unencrypted loans.csv, budget.csv and events.csv. Current editable inputs are saved even if results are stale; calculation results are regenerated on open. Display toggles and ledger filters are not saved. Older CSV folders remain importable. There is no autosave; keep backups and remove identifiers before sharing.

The persistent public-beta notice and report notice summarize limitations; they are not a certification of software correctness or a guarantee of legal protection for a publisher. Automated tests cover important identities and edge cases, not every lender contract. Versions before 0.4.1 had a Full-budget reserve error; recalculate those results.

## Payment estimates and snowball

Blank payment cells are saved as blank CSV values and automatically estimated; explicit zero remains zero. Standard/Student estimates use the monthly amortization formula on principal plus opening interest/fees, current entered APR and remaining term, rounded upward to cents. This is an approximation, including for daily-simple loans; future APR changes and irregular periods are not priced into the estimate. A missing remaining term requires correction, not an assumed new ten-year term. Card blanks use their minimum rules; BNPL blanks require an installment schedule. Enter the lender amount to override. Existing CSVs that omit the entire payment column retain the legacy zero default.

Snowball maintains required payments, then targets the smallest current total balance. It ignores custom locks; Selected honors them and otherwise uses avalanche. Table order breaks ties. Unassigned one-time payments use the strategy priority. Targeted payments retain their selected target. All comparisons share funds and horizon.

Milestones are modeled dates; the half-debt milestone is the first recorded snapshot at or below half the opening balance. Average APR weights starting principal, excluding opening interest and fees. The daily cost is a principal-interest equivalent; compound/monthly accrual can differ. Payment allocation previews sum actual simulated payments during the first simulation month.

Payment experiments are independent runs and never change current inputs. Additional monthly amounts increase the payment allowance; full-budget cash and emergency-fund rules still constrain spending. A one-time preview adds funded cash once on simulation start, plus the matching payment request; it is not a payment history reconstruction. Reset restores the most recently saved or opened input snapshot, subject to discarding unsaved edits. Reports may be exported as HTML or printed to PDF using the system print dialog. Money in ledger/timeline CSV exports is rounded to cents only for display; internal calculations retain precision.

## Three-strategy comparison in 0.7.2

The desktop now shows only Minimum, Avalanche and Snowball. Main payoff, milestone and investment summaries use Avalanche versus Minimum; Snowball remains in the comparison table and graph. The former Selected/custom comparison is removed. Legacy locked-extra CSV values remain readable for compatibility, but are hidden in the editor and ignored by these three strategies; imported nonzero values trigger a report notice. Payment experiments now use Avalanche. Payoff flags M1/A1/S1 identify individual loan payoffs, with names and dates on hover and a report table. Only active opening debts paid off within the horizon receive flags.

## Explanation tools in 0.8

Compare saved plans opens exactly two scenario ZIP files without replacing current inputs. The change table compares loan fields by name, budget fields, loan order and event rows. Each plan is simulated using its own saved assumptions; different dates or horizons are explicitly flagged. Outcomes are not a controlled strategy comparison when other inputs differ.

The break-even constant investment return reprices actual dated investment contributions for Avalanche and Minimum using the same annual-effective return throughout, with growth before each day’s contribution. Ending cash, emergency savings and debt are included. It searches sign changes on a one-percentage-point grid from -90% through +100% and bisects crossings. It can miss tangent crossings or several crossings inside one interval; it does not prove a unique global break-even or price the return-switch scenario.

Cash-flow freedom shows changes in the existing required-monthly-payment proxy at recorded snapshots, including increases when paid-ahead obligations resume. Dates need not be exact lender obligation-release dates. The Required monthly payments chart compares this proxy for all strategies. Freed obligations do not reduce the fixed contribution budget.

Funding tables distinguish assumed monthly payment funds (Loan-only) from actual entered household income (Full budget), dated income, additionally funded Loan-only payments and starting savings. They exclude events outside the simulation. Full-budget payment events allocate existing cash. The reconciliation excludes market growth and compares opening savings plus income with funded expenses, debt payments, investment contributions and ending cash/savings.

Clicking a payoff flag opens that strategy and loan in the amortization ledger and selects the final-payment row. Stale results require recalculation before navigating.
