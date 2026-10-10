# Search & Matching Specification

Pack 1 puts "Complex AI matching" out of scope for MVP. MVP search is rule-based and transparent. This doc defines it and prepares for later ranking.

## 1. Search Surfaces
1. Job search/feed (providers find jobs)
2. Provider search/browse (customers find providers)
3. Category browse
4. Global search box (keywords → jobs/providers/categories)

## 2. Job Search
Filters: category/subcategory, keywords, budget range, location/distance, posted date, schedule/date needed, type (digital/physical/both), remote vs on-site.
Sort: newest (default), nearest (for physical), highest budget, closing soon.
Hide: draft, cancelled, filled/in-progress jobs, jobs from suspended customers, jobs a provider already applied to (or mark clearly).

## 3. Provider Search
Filters: category, skills, location/service area, rating minimum, verification level, price range, availability, completed-jobs minimum.
Sort: best match (default), rating, nearest, most completed jobs.
Show: only active, non-suspended providers with completed profiles and at least L1 verification.

## 4. Location Handling (Pack 1 requirement)
- Store normalised address: country, state, LGA/city, area/neighbourhood, optional geo point (lat/lng).
- Use a MongoDB `2dsphere` index on geo points; distance queries run on the server only.
- Providers define a service area: radius from a point and/or list of LGAs/areas.
- Customers' exact address is never public. Show approximate area/distance band (e.g., "within 5 km") until hire.
- Geolocation consent: explain first, then ask for foreground permission through the OS prompt; allow manual area selection if denied. Never require GPS. Do not track location in the background. On iOS, offer approximate location as acceptable.
- Digital jobs ignore distance.
- Abstract the maps/geocoding provider behind a `LocationService` (OD-12). Cache geocoding results.
- Nigerian address realities: informal addresses and landmarks; support free-text "landmark/nearby" field plus area/LGA selection.

## 5. Matching Logic (rule-based, MVP)
When a job is published, compute eligible providers:
1. Provider category matches job category.
2. Provider active, verified at required level, not suspended.
3. Physical jobs: job within provider service area; digital: no distance rule.
4. Provider available (if availability set).
5. Budget fit (soft): flag if job budget is far below provider's stated pricing.
Notify eligible providers (doc 12) with limits per provider per day.

**Relevance score (for "best match" ordering)** — weights are configurable and should be tuned later:
`score = categoryMatch*40 + skillOverlap*15 + distanceScore*20 + ratingScore*10 + verificationScore*10 + responsivenessScore*5`
Transparency: never rank by paid promotion at MVP. If sponsored placement is added later, label it "Sponsored".

## 6. Text Search
Start with MongoDB text indexes (or Atlas Search if available) on job title/description and provider bio/skills/categories. Support partial matches and common Nigerian terms (e.g., "generator mechanic", "AC repair"). Maintain a small synonym list (admin-editable later): "plumber/pipe fitter", "AC/air conditioner", "gen/generator".
Sanitize inputs; limit query length; rate-limit search endpoints.

## 7. Performance Targets (starting)
First page of results < 1.5 s on a typical mobile network; payloads kept small (list responses return only fields the card needs); infinite scroll with cursor pagination, page size 10–20; cache recent results in the app for offline viewing; indexes on category, status, createdAt, geo point, providers' rating/verification; avoid unbounded queries.

## 8. API Notes
`GET /jobs?category=&q=&minBudget=&maxBudget=&lat=&lng=&radiusKm=&type=&sort=&page=&limit=`
`GET /providers?category=&q=&minRating=&verified=&lat=&lng=&radiusKm=&sort=&page=&limit=`
Server validates and bounds all parameters (e.g., radius max 100 km). Responses are paginated with total counts or cursors.

## 9. Anti-gaming
Keyword stuffing penalties (post-MVP), suspended/duplicate profile exclusion, rate limits, reviews required to be on-platform and verified by job completion.

## 10. Future (doc 20)
AI semantic search, recommendations, learning-to-rank from hire/application data, saved searches, job alerts, "similar providers".

## 11. Acceptance Criteria
- Filters combine correctly (category + distance + budget).
- Draft/cancelled/filled jobs never appear in the feed.
- Exact customer address never appears in any search response.
- Distance results are correct within reasonable tolerance and use indexes.
- Suspended or unverified (below L1) providers do not appear.

## 12. Mobile Search UX
- Search bar always visible on Home; recent searches and suggested categories shown before typing.
- Debounce typing and cancel in-flight requests.
- Map toggle on the job feed (cluster markers; respect approximate locations).
- Filter sheet (bottom sheet) with clear/apply, showing active filter count.
- Skeleton loading, empty states with suggestions, and offline cached results labelled as such.
- Blocked users and their content are excluded from results for the blocker.
