# myTreep

Project link: [mytreep.com](https://mytreep.com)

## Project Summary

myTreep is an AI-powered travel planning platform designed to help users move from broad travel intent to structured trip plans, itineraries, and shareable outputs.

At a business level, the goal was to reduce the friction and fragmentation that usually come with travel planning. Instead of forcing users to piece together destinations, budgets, timing, and itinerary ideas across multiple tools, the application brings those decisions into a guided planning experience.

As a cofounder, I was involved not only in building the system, but in shaping the decisions behind it: how to structure the planning flow, how to make AI-generated value feel usable rather than gimmicky, how to design monetization without locking the business into an early assumption, and how to keep the application maintainable while the company was still evolving quickly.

## My Role

I worked across strategy, architecture, and implementation.

That meant making founder-level decisions about user experience, monetization strategy, administrative control, and system design, while also helping turn those decisions into working software. My role sat at the intersection of business thinking and engineering execution: deciding what the application needed to become, then building the systems that made that direction viable.

A big part of the work was making sure the product was not just impressive in demos, but credible as a long-term travel planning system. That required balancing AI capability with usability, pricing, control, and reliability.

## Technical Architecture

myTreep is built as a full-stack Next.js application using the App Router, TypeScript, PostgreSQL, and Prisma. The codebase includes the customer-facing experience, backend route handlers, admin tooling, authentication logic, and operational workflows in one place.

That structure was intentional. In an early-stage company, user flows, AI behavior, pricing rules, and backend logic tend to evolve together. Keeping them close reduced iteration overhead and made it easier to move quickly without constantly coordinating changes across separate services.

The platform supports OTP, Google OAuth, and Apple OAuth, but authentication is still controlled by the application rather than being fully outsourced to a vendor auth layer. Trips, wallet transactions, sharing, usage tracking, reminders, and system configuration all live in a structured relational model, which gave the system a stronger operational foundation than a thin prototype would normally have.

On the AI side, the system integrates multiple model providers for planning and itinerary generation. Around that core flow, analytics, error monitoring, email delivery, and monetization are handled through supporting services and a wallet model with pluggable payment providers.

## Key Engineering Decisions

One of the most important decisions was keeping business logic and backend behavior inside the same application boundary. For this stage of the company, that created a tighter feedback loop between user experience decisions and implementation. It meant the team could evolve onboarding, generation flows, payment behavior, and admin tooling together rather than spending early effort on service separation before the overall workflow was stable.

Another important decision was owning authentication at the application level instead of treating a database platform as the system of truth for auth behavior. That gave the system more control over provider choices, authorization rules, and long-term vendor independence. It added responsibility on the engineering side, but it aligned better with the level of flexibility the business needed.

The monetization model was also a meaningful engineering decision. Rather than hard-coding a single payment flow, the platform uses a configurable wallet and pricing system. That matters in AI applications because pricing strategy often changes as usage patterns, cost models, and willingness to pay become clearer. Building flexibility into the payment layer made it easier to evolve the business model without rebuilding the application around it later.

A further decision was investing in admin controls and system configuration early. That gave the team a way to manage credits, pricing, users, and operations without turning routine business adjustments into manual database work or constant engineering intervention. It also enabled faster experimentation around onboarding, pricing, and rollout decisions because many adjustments no longer depended on shipping a code change first.

## Problems Solved

One of the main problems this project solved was turning AI output into a usable planning workflow.

Many AI applications look compelling in isolation but become weak when users need continuity, structure, or repeatable value. myTreep addressed that by connecting onboarding, trip generation, itinerary creation, wallet logic, sharing, and user management into a more cohesive system.

It also solved a business problem that many AI-first platforms struggle with early on: how to introduce monetization without freezing the experience into a pricing model too early. The wallet system, feature flags, and configurable pricing controls made it easier to test and evolve commercial strategy without rewriting the core application.

A concrete example of this was separating pricing and wallet behavior from the trip-planning flow itself. That allowed the platform to change how credits, bundles, and payment modes worked without forcing a redesign of the main planning experience every time the business model shifted.

There was also a concrete technical challenge around AI-heavy flows: generation is only useful if it feels coherent and dependable to the user. That meant adding controls around rate limiting, usage tracking, and cached enhancement paths so the system could manage latency and cost pressure without letting the planning experience become erratic.

## Business Impact

The strongest business impact here is that the platform became more than a concept or a one-shot AI demo.

It gained the foundations of a usable product: structured user onboarding, persistent trip management, public sharing, administrative controls, payment flexibility, analytics visibility, and a clearer path to monetization. That matters because real user value comes from repeatability and internal control, not just from generating a good first impression.

From a founder perspective, the engineering work also created leverage. Pricing rules, wallet behavior, rollout decisions, and certain administrative actions could be adjusted without treating every experiment as a full engineering rebuild. That made the system better suited to the realities of early-stage iteration, reduced dependency on engineering for routine pricing changes, and supported faster experimentation around onboarding and monetization.

## Infrastructure And Scalability Thinking

The platform shows scalability thinking less through infrastructure sprawl and more through business-aware architecture.

AI-assisted systems do not only need runtime scale. They need cost control, user instrumentation, and the ability to change monetization and rollout behavior without destabilizing the rest of the application. myTreep addresses that by combining feature flags, rate limiting, monitoring, configurable pricing, and structured usage tracking.

The system also leaves room for future separation. The current architecture favors iteration speed and cohesion, but the underlying boundaries around services, data models, payments, analytics, and admin operations create a workable path for deeper decomposition as growth demands it.

## Challenges And Tradeoffs

The biggest tradeoff was choosing speed of iteration and system cohesion over premature service separation.

That was the right call for this stage, but it required discipline. When business logic, backend routes, admin operations, and AI workflows live close together, the architecture has to be intentionally organized or complexity grows quickly.

There was also a deliberate tradeoff in building monetization flexibility early. A configurable wallet and payment abstraction take more thought than a simple single-checkout flow, but that extra design work pays off when the business model is still being shaped.

As a founder-led company, another constant tradeoff was balancing ambition with implementation realism. It was important to build enough capability for the experience to feel differentiated, while resisting the urge to overengineer before real usage patterns justified it.

## What I Would Improve Next

As the product grows, the architecture naturally supports separating some responsibilities into more independent execution boundaries, especially around the heaviest AI and payment-adjacent workflows.

I would also continue investing in the parts of the system that improve decision quality rather than only feature count: better instrumentation around planning completion, stronger visibility into AI cost and conversion behavior, and clearer operating signals around where users get stuck or drop out.

The broader lesson from myTreep is that strong product engineering is not only about shipping features. It is about building enough flexibility, control, and structure that the platform can keep evolving without losing coherence as both user expectations and business demands change.
