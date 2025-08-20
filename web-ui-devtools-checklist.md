# Web UI + DevTools Checklist (SauceDemo)

| Step | What to Verify | Artifacts (Logs, Screenshots, Reports) |
|------|----------------|-----------------------------------------|
| **0. Setup** | Open DevTools (F12), disable cache, preserve log. Select **XHR/Fetch** filter. | No artifacts, just DevTools prepared |
| **1. Login Page – Positive** | Standard login (`standard_user` / `secret_sauce`) → redirect to Products. Check Network (200/302), Storage, Cookies. | HAR: `login-success.har`, Screenshot: Products page, Storage (local/session) screenshot |
| **1. Login Page – Negative** | Empty/invalid password → red error text. `locked_out_user` → specific error message. | HAR: `login-fail.har`, Screenshot: error message |
| **1. DevTools Checks** | Input fields, button attributes, console has no errors. | Screenshot: Console logs |
| **2. Products – Display** | Product cards load, no broken images, titles, prices, buttons visible. | Screenshot: Products page |
| **2. Products – Sorting** | Sort A–Z, Z–A, Price ↑/↓ works. Verify via Network if sorting is XHR or client-side. | HAR: `sorting.har`, Screenshot: Products after sorting |
| **2. Products – Add to Cart** | Add → badge updates, button changes to Remove. Reload → cart persists. | HAR: `add-to-cart.har`, Screenshot: Cart badge, Storage screenshot |
| **3. Product Details** | Clicking a product → details page loads. Back returns with preserved state. | Screenshot: Product details page |
| **4. Cart** | Cart shows correct items, prices. Continue/Checkout buttons work. | Screenshot: Cart page |
| **4. Checkout – Validation** | Empty fields → validation error. Filled fields → proceed. | Screenshot: error message, Screenshot: successful step |
| **4. Checkout – Finish** | Totals visible. Finish → “Thank you” confirmation. Back Home → Products. | Screenshot: Order complete page |
| **5. Logout & Session** | Logout → back to Login. Storage/cookies cleared. Products blocked without login. | HAR: `logout.har`, Storage screenshot |
| **6. Responsive View** | Mobile mode (iPhone 12). Layout correct, no overlaps. | Screenshot: Mobile Login, Screenshot: Mobile Products |
| **6. Throttling** | Slow 3G: Login/Products load with visible feedback. No broken UI. | Screenshot: Timing panel, Screenshot: Products load |
| **7. Accessibility** | Tab navigation works. Images have `alt`. Good color contrast. | Lighthouse accessibility report, Screenshot: highlighted accessibility checks |
