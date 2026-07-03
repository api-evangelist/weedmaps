# Weedmaps (weedmaps)

Weedmaps is a cannabis discovery and ordering marketplace connecting consumers with dispensaries, delivery services, and brands. For its business customers it publishes a partner integration API suite documented at [developer.weedmaps.com](https://developer.weedmaps.com/docs): a **Menu API** for keeping a retailer's product menu, pricing, and availability in sync with their point-of-sale; a **Brand Catalog API** for mapping and enriching menu items against the Weedmaps brand and product catalog; a **Taxonomy API** for categories, cannabinoids, strains, terpenes, and discovery tags; and an **Orders API** for receiving and updating online orders directly in a partner POS.

**Access model (important):** The developer documentation is fully public, but production access is **partner-gated**. Integrators apply by email; on approval they receive OAuth2 client-credentials and a test listing, and a Listing Owner must select the partner as their POS provider before production access is granted. The onboarding documentation notes that **new integrations are not currently being onboarded**. Because a live partner account could not be exercised, the endpoints below are documented but **modeled** from the public reference — the brand and orders paths are confirmed from the reference pages, while the exact menu-item CRUD/upsert paths are inferred from the documented endpoint categories.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/weedmaps/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/weedmaps/refs/heads/main/apis.yml)

## Authentication

OAuth2 **ClientCredentials** flow. Retrieve an access token from the `/auth/token` endpoint (limited to 1 request/minute) and send it as a Bearer token on all partner requests. Access must be granted by a Listing Owner.

## Base URLs

- Menu / Brand Catalog / Taxonomy: `https://api-g.weedmaps.com/wm/2025-07/partners`
- Orders: `https://api-g.weedmaps.com/oos/2026-01`

Weedmaps uses date-based versioning (`YYYY-MM`) with two releases per year (January and July) and roughly two-year support windows per version.

## Tags

- Cannabis
- Dispensary
- Marketplace
- Menu Sync
- Point of Sale
- Orders
- Brands
- Partner API

## Timestamps

- **Created:** 2026-07-03
- **Modified:** 2026-07-03

## APIs

### Weedmaps Menu API

Keep a retailer's Weedmaps menu in sync with their point-of-sale. Retrieve menus and menu items, and create, retrieve, update, delete, and upsert-by-external-ID menu items to publish real-time product availability and dynamic pricing across single or multiple (e.g. medical vs. recreational) menus.

- **Human URL:** [https://developer.weedmaps.com/docs/wm-menu-api-getting-started](https://developer.weedmaps.com/docs/wm-menu-api-getting-started)
- **Base URL:** `https://api-g.weedmaps.com/wm/2025-07/partners`

#### Tags

- Menu Sync
- Menu Items
- Point of Sale
- Inventory

#### Properties

- [Documentation](https://developer.weedmaps.com/docs/wm-menus)
- [API Reference](https://developer.weedmaps.com/reference/get_menus)

### Weedmaps Brand Catalog API

Sync or map the Weedmaps catalog of Brands and Brand Products to an internal catalog to improve menu-item search relevance and discoverability. Retrieve all brands, a single brand, the brand product catalog, an individual brand product, and brand product reviews.

- **Human URL:** [https://developer.weedmaps.com/reference/get_brands](https://developer.weedmaps.com/reference/get_brands)
- **Base URL:** `https://api-g.weedmaps.com/wm/2025-07/partners`

#### Tags

- Brands
- Products
- Reviews
- Enrichment

#### Properties

- [Documentation](https://developer.weedmaps.com/docs/overview)
- [API Reference](https://developer.weedmaps.com/reference/get_brands)

### Weedmaps Taxonomy API

Read-only reference taxonomy used to enrich menu items — retrieve cannabinoids, categories (flat and tree), strains, terpenes, and discovery tags. Linking menu items to these taxonomy entries increases the quality and discoverability of a retailer's Weedmaps menu.

- **Human URL:** [https://developer.weedmaps.com/docs/core-concepts-and-structure](https://developer.weedmaps.com/docs/core-concepts-and-structure)
- **Base URL:** `https://api-g.weedmaps.com/wm/2025-07/partners`

#### Tags

- Taxonomy
- Categories
- Cannabinoids
- Strains
- Terpenes

#### Properties

- [Documentation](https://developer.weedmaps.com/docs/core-concepts-and-structure)
- [API Reference](https://developer.weedmaps.com/reference/get_menus)

### Weedmaps Orders API

Receive and manage online Weedmaps orders directly in a partner POS. Update order status, retrieve applicable discounts, retrieve order schedule time windows, and retrieve document URLs, removing manual re-entry between Weedmaps and the retailer's system.

- **Human URL:** [https://developer.weedmaps.com/reference/update_order_status](https://developer.weedmaps.com/reference/update_order_status)
- **Base URL:** `https://api-g.weedmaps.com/oos/2026-01`

#### Tags

- Orders
- Discounts
- Fulfillment
- Documents

#### Properties

- [Documentation](https://developer.weedmaps.com/docs/overview)
- [API Reference](https://developer.weedmaps.com/reference/update_order_status)

## Common Properties

- [Website](https://weedmaps.com)
- [Business](https://weedmaps.com/business)
- [Documentation](https://developer.weedmaps.com/docs)
- [Authentication](https://developer.weedmaps.com/docs/oauth)
- [Onboarding](https://developer.weedmaps.com/docs/onboarding-process)
- [LinkedIn](https://www.linkedin.com/company/weedmaps)
- [Plans](plans/weedmaps-plans-pricing.yml)
- [Rate Limits](rate-limits/weedmaps-rate-limits.yml)
- [Fin Ops](finops/weedmaps-finops.yml)

## Rate Limits

- **Global:** 2,500 requests/minute per integrator (enforced as 420 requests / 10 seconds across all endpoints)
- **Token endpoint (`/auth/token`):** 1 request/minute — cache and reuse the token
- **Overage:** HTTP 429 Too Many Requests; use exponential backoff

## Pricing

The partner API carries no separate per-call fee; the cost driver is the **Weedmaps for Business** listing subscription that the APIs keep in sync — a monthly, market-dependent charge sold via Weedmaps sales (reported retailer base ~$495/mo, delivery ~$395/mo, national brand programs substantially higher). See [plans/weedmaps-plans-pricing.yml](plans/weedmaps-plans-pricing.yml).

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
