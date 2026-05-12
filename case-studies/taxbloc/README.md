# TaxBloc

Project link: [taxbloc.ai](https://taxbloc.ai)

## Project Summary

TaxBloc is a financial export platform built around a demanding mix of concerns: external financial integrations, sensitive data handling, subscription logic, asynchronous export workflows, and a deployment model that needed to feel credible in production without becoming too heavy for the stage of the product.

At a business level, the platform supports financial and reporting workflows that would otherwise be much more manual, fragmented, and error-prone. The value was not only in generating exports, but in making sensitive financial data easier to access, process, and deliver through a more structured product experience.

The platform uses a modern web frontend, a NestJS API, Redis-backed background processing, AWS containerized backend infrastructure, and a separate compute path for heavier CSV generation. My work centered on shaping the backend and infrastructure so the system could be easier to deploy, safer to operate, and more resilient as export traffic and operational complexity increased.

## My Role

I worked as a backend and infrastructure-focused engineer across both the application layer and the AWS platform layer.

That included improving deployment workflows, organizing infrastructure into reusable Terraform layers and modules, tightening the security model around GitHub-to-AWS deployments, and redesigning the export path so heavier CSV generation did not stay tightly coupled to the main API runtime.

The work was not only about getting features live. It was about making the system easier to reason about in production: how it would fail, how it would be rolled back, how it would scale, and how sensitive data would be handled under normal and degraded conditions.

## Technical Architecture

TaxBloc is split into a web application and an API, with the frontend and backend deployed separately. The frontend handles the user flow around company search, account connection, and export requests. The API remains the control point for authentication, authorization, subscription-aware export rules, and orchestration of downstream work.

The backend integrates with external company-data, financial-data, billing, authentication, email, and background-processing services. That allows the platform to support both user-facing export flows and the background work needed to deliver them reliably.

One of the more important architectural decisions was moving CSV generation into a separate compute path. Both direct downloads and queued email exports could then use the same core export logic without forcing the main API runtime to absorb all of the heavier processing work. That created a cleaner separation between request handling and export execution.

The infrastructure itself is organized through Terraform using reusable modules and clear ownership boundaries. Shared platform concerns, application runtime concerns, and observability are separated so the system can evolve without turning every change into a broad infrastructure event.

## Key Engineering Decisions

The first major decision was to structure the infrastructure as layers rather than a flat Terraform project. That matters because network concerns, deployment identity, application runtime resources, and observability do not evolve at the same speed. Separating them reduced the chance that a routine application change would carry unnecessary infrastructure risk, and it created a cleaner path for future environments and services.

The second was improving the deployment security model so releases could run with short-lived credentials and tighter permissions. It was a meaningful maturity step because deployment security stopped being a side concern and became part of the platform design itself.

The third was offloading CSV generation from the main API runtime. Export generation is exactly the kind of workload that can create latency, memory pressure, and noisy failure modes if it sits in the same runtime that serves normal application traffic. A concrete example is long-running exports affecting normal API responsiveness during busy periods. Separating that work made the system more predictable under load and gave the export path a better runtime boundary.

Another important decision was deliberately not persisting direct-download export artifacts longer than necessary. That reduced storage complexity and limited the footprint of sensitive financial data. The tradeoff is that large payloads need explicit limits and fallback behavior, but that is a reasonable exchange when data minimization is part of the design goal.

## Problems Solved

A major problem this work addressed was the gap between a working application and an operable production system. The product already had useful application capabilities, but the surrounding delivery and infrastructure model needed to be easier to scale responsibly.

The deployment path became more disciplined through automated releases, consistent image versioning, and a clearer rollback story. That matters because production issues are easier to handle when the release process is repeatable and known-good revisions are easy to restore.

The export path also became more robust. Instead of treating CSV generation as just another synchronous backend responsibility, the system treats it as a heavier workload with dedicated handling. Direct downloads and queued email exports can share the same export logic while using a runtime better suited to that workload.

The infrastructure code solved a different class of problem: future change risk. By using reusable modules, isolated environments, validation, and clearer layer ownership, the platform is easier to extend without repeatedly rethinking its foundation.

## Business Impact

The strongest business impact here is improved production readiness.

This work made the platform easier to deploy, easier to recover, and easier to evolve without carrying as much delivery ambiguity. It improved the security posture of deployments by removing the need for long-lived cloud credentials in CI. It also reduced the risk that expensive export workloads would degrade the main API experience for users.

There is also a clear cost-awareness story. Non-production environments intentionally used simpler infrastructure choices while the product was still evolving. Supporting services were kept lean so the team could preserve flexibility without carrying unnecessary spend too early. Those are not flashy optimizations, but they reflect practical engineering judgment: spend where it matters, keep the rest lean until the system earns more complexity.

## Infrastructure And Scalability Thinking

The project shows good scalability thinking not because it uses a long list of cloud services, but because it is selective about where complexity belongs.

The API remains the stable control plane. Heavier export work is pushed into a separate compute path. Background workflows use asynchronous processing instead of stretching request-response paths. Infrastructure is laid out so shared platform concerns do not get mixed into every application change. Observability is lean, but it is present in the areas that matter most for release confidence and runtime health.

The environment model is also practical. The same infrastructure approach can be reused across environments without duplicating the entire setup, while still leaving room for more separation as the platform grows. That is the kind of decision that looks minor early on but prevents painful reshaping later.

## Challenges And Tradeoffs

The system makes several intentional tradeoffs.

Non-production environments intentionally used simpler networking and runtime boundaries to keep cost and maintenance overhead in proportion to the maturity of the product. That was a pragmatic compromise, not a permanent statement about what every environment should look like.

The current workload model also favors system simplicity over early separation. That is often the right choice while traffic and background processing volume are still manageable, even though the architecture should eventually evolve toward more independent scaling boundaries.

The decision not to persist export files long-term reduces data exposure and storage complexity, but it means export size limits and delivery behavior need to be handled carefully. In other words, the system trades some flexibility for a tighter production and data-handling model.

## What I Would Improve Next

As workload volume grows, the architecture naturally supports separating background execution into its own scaling boundary. That would allow different processing profiles to evolve independently without overcomplicating the system too early.

I would also continue tightening environment-specific infrastructure choices as the platform matures, especially where stronger isolation becomes worth the extra operational cost.

The broader theme is continued maturation without unnecessary complexity. The platform already shows the right direction. The next step is to keep the same discipline while deepening resilience, deployment confidence, and long-term scalability where the product actually demands it.

The project reinforced the importance of building systems that remain understandable and maintainable as both product requirements and runtime demands evolve.
