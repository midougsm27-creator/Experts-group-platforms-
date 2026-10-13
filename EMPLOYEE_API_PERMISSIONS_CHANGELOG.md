# Employee API permissions patch — 2026-10-13

This patch targets the **employee/worker side** of Experts Group Mobile Service. It is based on source snapshot version 31 and is proposed for review; it has not been applied to or deployed on the live Site.

## Changes
- Added signed-in account and permission checks to operational API routes.
- Scoped repairs, sales, cash, customers, suppliers, purchases, and order requests to the user's assigned shop(s); cross-shop requests require `global.view`.
- Separated repair status changes, repair edits, order management, cash movements, sales discounts, and purchase-price visibility by existing permission codes.
- Restricted product responses so purchase price is omitted without `stock.purchase_price`, and unassigned shop stock is not returned.
- Prevented product edits from changing purchase price when the user lacks `stock.purchase_price`.
- Updated the cash view to request the currently selected shop instead of all shops.

## Verification
- TypeScript: no errors in edited files. Three pre-existing errors remain in `customer-view.tsx`, `settings-view.tsx`, and `supplier-view.tsx`; they also occur in the unmodified snapshot.
- ESLint: the changed customer, purchase, sales, and supplier routes retain existing `no-explicit-any` findings.
- No full build or deployment was run.

## Review
The unified diff is in `patches/employee-api-permissions.patch`. Apply and inspect it against the matching version 31 source before adopting it.
