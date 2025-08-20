\# Web UI + DevTools Checklist (SauceDemo)



| Step | What to Verify | Artifacts |

|------|----------------|-----------|

| \*\*0. Setup\*\* | Open DevTools (F12), disable cache, preserve log. Select \*\*XHR/Fetch\*\* filter. | — |

| \*\*1. Login Page – Positive\*\* | Standard login (`standard\_user / secret\_sauce`) → redirect to Products. Check Network (200/302), Storage, Cookies. | HAR: `login-success.har`, screenshot Products |

| \*\*1. Login Page – Negative\*\* | Empty/invalid password → red error text. `locked\_out\_user` → specific error message. | HAR: `login-fail.har`, screenshot error |

| \*\*1. DevTools Checks\*\* | Elements: fields and button attributes. Console: no errors on submit. | Console log screenshot |

| \*\*2. Products – Display\*\* | Product cards load, no broken images, titles, prices, buttons visible. | Screenshot Products |

| \*\*2. Products – Sorting\*\* | Sort A→Z, Z→A, Price ↑/↓ works. Network: check if XHR or client-side. | HAR (sorting), screenshot |

| \*\*2. Products – Add to Cart\*\* | Add → badge updates, button changes to Remove. Reload → cart persists. | HAR: `add-to-cart.har`, Storage screenshot |

| \*\*3. Product Details\*\* | Click product → details page loads, Back returns with preserved state. | Screenshot product details |

| \*\*4. Cart\*\* | Cart shows correct items/prices, Continue/Checkout buttons functional. | Screenshot cart |

| \*\*4. Checkout – Validation\*\* | Empty fields → validation errors. Filled fields → Continue. | Screenshot error \& success |

| \*\*4. Checkout – Finish\*\* | Totals visible, Finish → “Thank you” confirmation, Back Home → Products. | Screenshot order complete |

| \*\*5. Logout \& Session\*\* | Logout → back to Login. Storage/cookies cleared. Products blocked without login. | HAR logout, Storage screenshot |

| \*\*6. Responsive View\*\* | Mobile mode (iPhone 12): layout correct, no overlaps. | Screenshot mobile Login/Products |

| \*\*6. Throttling\*\* | Slow 3G: Login/Products load with proper UI feedback, no broken flows. | Timing panel screenshot |

| \*\*7. Accessibility\*\* | Tab navigation works, images have `alt`, good contrast. Lighthouse Accessibility audit. | Lighthouse report, screenshot |

| \*\*8. Error Handling\*\* | Invalid login → UI error \& 4xx. Offline mode during Add to cart → UI handles error. Slow checkout → no duplicate submits. | HAR + screenshot |

| \*\*9. Bug Report Example\*\* | Document bugs in template (Title, Env, Steps, Actual, Expected, Artifacts). | Example bug report file |



---



\### Notes

\- Always export \*\*HAR\*\* via Network → right-click → “Save all as HAR”.

\- Attach screenshots + HAR to bug reports.

\- Use \*\*Application tab\*\* for storage/cookies checks.



