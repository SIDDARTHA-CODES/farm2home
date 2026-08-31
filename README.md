# Farm2Home — Standalone React Project

A farmer-to-consumer marketplace prototype for Telangana, built with React + Vite + Tailwind CSS.
This is the exact same app you saw as a Claude artifact, exported into a runnable local project.

## Run it

```bash
npm install
npm run dev
```

Then open the URL Vite prints (usually `http://localhost:5173`). No API keys, backend, or
database needed — everything runs on in-memory React state with demo data.

```bash
npm run build     # production build to /dist
npm run preview   # preview the production build locally
```

## Project structure

```
farm2home/
├── index.html                # HTML shell Vite serves; loads src/main.jsx
├── package.json               # dependencies + npm scripts
├── vite.config.js             # Vite + React plugin config
├── tailwind.config.js         # Tailwind content paths
├── postcss.config.js          # Tailwind/Autoprefixer wiring
├── .gitignore
├── README.md
└── src/
    ├── main.jsx                # React entry point — mounts <App /> into #root
    ├── index.css                # Tailwind directives (@tailwind base/components/utilities)
    └── App.jsx                  # THE ENTIRE APPLICATION (all pages + components)
```

## Where everything lives

The app was originally built as a single self-contained React artifact, and to avoid
any risk of breaking working functionality while splitting it up, **all components and
pages live in `src/App.jsx`**, in this order:

| Section in `App.jsx`              | What it is |
|---|---|
| Design tokens (`const C`, `fontImport`) | Color palette, Google Fonts import, custom CSS animations |
| Sample data (`INITIAL_FARMERS`, `INITIAL_PRODUCTS`, `CATEGORIES`, `LOCATIONS`) | Demo dataset — 5 Telangana farmers, 8 products |
| UI primitives (`Btn`, `Card`, `Badge`, `Eyebrow`, `SectionHeading`, `EmptyState`, `StatusPill`) | Reusable building blocks used across every page |
| `SupplyChainDiagram` | The traditional-vs-Farm2Home supply chain visual, reused on Landing, About, Impact & Price Transparency, and Impact Dashboard |
| `ProductCard` | Marketplace product tile |
| `NavBar`, `Footer` | Site navigation and footer, shared across all pages |
| `Landing` | Home page (hero, how it works, featured products, testimonial, impact stats, CTA) |
| `FarmerLogin`, `ConsumerLogin`, `Field`, `Select` | Login pages and shared form inputs |
| `FarmerDashboard` | Farmer's home page after login |
| `AddProduct` | Form for farmers to list a new product |
| `MyProducts` | Farmer's product listing management (edit/delete) |
| `Marketplace` | Consumer browsing page with search/category/location filters |
| `ProductDetails` | Single product page with add-to-cart |
| `CartPage` | Shopping cart with quantity controls |
| `Checkout` | Delivery details + order placement |
| `OrderTracking` | Consumer's order status page |
| `FarmerOrders` | Farmer's incoming orders + status updates |
| `FarmerEarnings` | Farmer's earnings breakdown and charts |
| `PriceComparison` | **Impact & Price Transparency** page (interactive per-product breakdown, supply chain diagram, comparison table, charts) |
| `advisorHash`, `getAdvisorRecommendation`, `AIAdvisor` | **AI Price Advisor** page and its deterministic demo recommendation logic |
| `ImpactDashboard` | **Impact Dashboard** page (KPIs, supply chain visuals, farmer earnings, consumer savings, product categories, recent activity) |
| `About` | About page |
| `Root` | Top-level app state (products, cart, orders, farmers, consumer session) and page router |
| `RedirectNotice` | Shown when a farmer-only page is opened without a farmer logged in |
| `export default function Farm2Home()` | The component `main.jsx` renders |

All state (products, cart, orders, farmer/consumer sessions) lives in `Root` via React
`useState`/`useMemo` and is passed down as props — there is no external state library,
router library, or backend call anywhere in the app.

## Dependencies (all declared in `package.json`)

**Runtime:**
- `react`, `react-dom` — the UI library
- `lucide-react` — icon set used throughout the nav, cards, and buttons
- `recharts` — the bar/line/pie charts on Farmer Earnings, Price Transparency, and Impact Dashboard

**Build tooling:**
- `vite`, `@vitejs/plugin-react` — dev server and bundler
- `tailwindcss`, `postcss`, `autoprefixer` — utility CSS

Fonts (Fraunces, Space Grotesk) are loaded via a `@import` inside a `<style>` tag rendered
by the app itself (see the `fontImport` constant near the top of `App.jsx`) — no separate
font files or `<link>` tags are needed; this requires an internet connection to fetch from
Google Fonts at runtime, exactly as it did inside the artifact.

## Notes

- All data is in-memory demo data. Refreshing the page resets products/cart/orders back to
  the seeded starting state — this matches the artifact's original behavior.
- No environment variables, API keys, or backend services are required.
