# PostHog post-wizard report

The wizard has completed a deep integration of PostHog analytics into the DevEvents Next.js App Router project. The following changes were made:

- **`instrumentation-client.ts`** (new): Initializes PostHog client-side using the `instrumentation-client` pattern for Next.js 15.3+. Configured with a reverse proxy (`/ingest`), exception capture, and debug mode in development.
- **`next.config.ts`** (updated): Added reverse proxy rewrites so PostHog requests route through `/ingest`, improving reliability against tracking blockers. Added `skipTrailingSlashRedirect: true`.
- **`components/ExploreBtn.tsx`** (updated): Captures `explore_button_clicked` when the user clicks the "Explore Events" CTA button.
- **`components/EventCard.tsx`** (updated): Converted to a client component; captures `event_card_clicked` with `event_title`, `event_slug`, `event_location`, and `event_date` properties when a user clicks an event card.
- **`.env.local`** (updated): `NEXT_PUBLIC_POSTHOG_PROJECT_TOKEN` and `NEXT_PUBLIC_POSTHOG_HOST` written; `.gitignore` coverage ensured.

| Event name | Description | File |
|---|---|---|
| `explore_button_clicked` | User clicks the 'Explore Events' CTA button on the homepage to browse featured events. | `components/ExploreBtn.tsx` |
| `event_card_clicked` | User clicks an event card to view the details page for a specific event. | `components/EventCard.tsx` |

## Next steps

We've built some insights and a dashboard for you to keep an eye on user behavior, based on the events we just instrumented:

- [Analytics basics (wizard) — Dashboard](https://us.posthog.com/project/478505/dashboard/1738975)
- [Explore button clicks over time](https://us.posthog.com/project/478505/insights/C6tyc37A)
- [Event card clicks over time](https://us.posthog.com/project/478505/insights/KYXEOr2i)
- [Top events by click count](https://us.posthog.com/project/478505/insights/k37Z9XmY)
- [Unique users engaging with events](https://us.posthog.com/project/478505/insights/mrsozB2b)
- [Explore to event click conversion funnel](https://us.posthog.com/project/478505/insights/12JI03wW)

## Verify before merging

- [ ] Run a full production build (the wizard only verified the files it touched) and fix any lint or type errors introduced by the generated code.
- [ ] Run the test suite — call sites that were rewritten or instrumented may need updated mocks or fixtures.
- [ ] Add the exact PostHog env var names (`NEXT_PUBLIC_POSTHOG_PROJECT_TOKEN`, `NEXT_PUBLIC_POSTHOG_HOST`) to `.env.example` and any monorepo/bootstrap scripts so collaborators know what to set.
- [ ] Wire source-map upload (`posthog-cli sourcemap` or your bundler's upload step) into CI so production stack traces de-minify.

### Agent skill

We've left an agent skill folder in your project. You can use this context for further agent development when using Claude Code. This will help ensure the model provides the most up-to-date approaches for integrating PostHog.
