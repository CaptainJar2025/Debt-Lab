# Debt Lab — read before use

**Public beta. Planning estimates only.** Debt Lab is a calculator for exploring assumptions. It does not provide financial, investment, tax, legal or lending advice. It does not establish the best action for your circumstances, guarantee a payoff date, predict market performance, or approve borrowing.

## An afternoon project, with tests

Built with AI tools from the musings of a chemical engineer working in capital projects. It has survived the creator’s testing, but has not been independently audited. If this afternoon project is the entire basis of your financial modeling, you might be cooked. Check the workings and verify results independently. The software is provided as is, without warranty; see the MIT license in About / licenses.

## Check the inputs before relying on a result

Use current lender statements and distinguish principal, unpaid interest, fees, next required payments and optional payments. Use income after deductions when entering take-home pay. Do not deduct retirement contributions twice. Debts and assets you have not entered are outside this model. Historical interest already paid is not reconstructed from today's balance. The simulation starts at the date you choose; it does not establish lifetime borrowing cost.

A positive remaining-term value creates an assumed final balloon for a Standard or Student loan. Choose **0 / Unknown** if you do not know the remaining contractual term. Confirm dates and actual minimum-payment requirements with the lender. Paid-ahead billing can differ from the simplified fixed-date model.

## The two calculation modes answer different questions

**Loans + monthly payments** assumes your entered regular payments plus extra are available. It does not test affordability, emergency savings or mortgage eligibility. Expense events are excluded and reported as such. Income events are additional assumed funds. A one-time payment event brings additional assumed funds; do not also enter that same money as an income event.

**Full household budget** uses entered income, expenses and savings. Voluntary funds first fill six months of essential expenses. Required debt payments take priority; cash shortages and arrears are reported. Monthly timing is simplified, so irregular income and bill timing can change feasibility. Money outside the payment budget stays in uninvested cash; it is not automatically invested.

## Lender calculations can differ

Interest, compounding, payment allocation, minimums, fees, rounding, grace periods, statement cycles, subsidies, capitalization, variable rates, contract terms and legal requirements can differ from this model. Credit cards use one APR bucket without a grace period. Federal student loans use daily simple interest without automatic capitalization, deferments, forgiveness or income-driven repayment rules. BNPL templates are editable examples, not verified offers or a complete provider contract. Enter only fees your agreement authorizes. Future APR changes must be entered; the app does not determine future eligibility or discounts.

The avalanche comparison follows effective APR priority. It is not a proof of a globally optimal strategy when fees, liquidity or contractual rules differ. Interest savings cover the selected simulation horizon. When a payoff date lies beyond that horizon, the app does not know the complete time savings.

## Investment returns are assumptions, not expected outcomes

The app compounds chosen annual-effective returns daily on a smooth path. Real markets fluctuate and losses can be severe. A higher post-payoff return does **not** follow automatically from eliminating debt; it represents a scenario you choose. It is not evidence of investing skill, an expected risk premium, or a probability estimate. Taxes, investment fees, inflation, volatility, forced sales, sequence risk and account restrictions are not modeled.

Each strategy can switch returns after its own debt payoff and can reinvest its freed payment budget. The comparison uses the same horizon. Net worth includes cash, emergency savings, the selected hypothetical portfolio and remaining modeled debt; it excludes other assets and liabilities. Independent return scenarios are alternatives, not simultaneous investment accounts. A positive result is conditional on the entered assumptions, not a recommendation.

The public beta starts with the same 7% illustration before and after payoff. Neither value is a forecast or recommendation. You can edit either assumption, including a negative return, to explore sensitivity. Existing saved scenarios retain their own return settings.

## Mortgage illustrations are incomplete

Borrowing capacity uses a simplified total-DTI calculation and hypothetical mortgage terms. It omits lender-specific underwriting, credit history, down payment, front-end limits, property eligibility and other qualification rules. It is not a preapproval or quote. Enter gross income separately from take-home income; without gross income, the app does not calculate the illustration.

## Privacy, saving and beta status

Calculations and scenario files are local. The app has no account, bank connection, telemetry, trading or payment capability. External reference links open websites only when clicked. A scenario ZIP contains readable, **unencrypted** CSVs with your financial inputs. Treat exports as private and remove identifiers before sharing. The app does not autosave; use Save scenario file and keep backups. It asks before closing unsaved edits, but a crash can still lose changes.

This beta has automated tests and local desktop checks, but these do not establish correctness for every contract or operating system. Validate projections against statements and independent calculations before making financial commitments. Software can contain errors. Versions before 0.4.1 contained a Full-budget reservation bug; recalculate those results in the current release.

For exact simulation conventions, see **Model guide**. No personal scenario is included in the public build. The optional example is fictional.

## Informal comparison

One informal comparison of modeled total interest with the creator’s independent estimate differed by approximately 2.5%, using similar but unmatched inputs. This was a plausibility check, not a controlled historical backtest, an independently verified error bound, or a guarantee of accuracy for other scenarios.
