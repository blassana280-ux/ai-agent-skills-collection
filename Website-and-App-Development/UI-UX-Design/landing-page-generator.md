---
name: landing-page-generator
description: "Generates high-converting landing pages as complete Next.js/React (TSX) components with Tailwind CSS. Creates hero sections, feature grids, pricing tables, FAQ accordions, testimonial blocks, and CTA sections using proven copy frameworks (PAS, AIDA, BAB). Outputs SEO meta tags, structured data, and performance-optimised code targeting Core Web Vitals (LCP **Bold Startup** headings: add font-black tracking-tight to all / elements."
---

# Landing Page Generator

## Copy Frameworks

**PAS (Problem → Agitate → Solution)**
- H1: Painful state they're in
- Sub: What happens if they don't fix it
- CTA: What you offer
- *Example — H1:* "Your team wastes 3 hours a day on manual reporting" / *Sub:* "Every hour spent on spreadsheets is an hour not closing deals. Your competitors are already automated." / *CTA:* "Automate your reports in 10 minutes →"

**AIDA (Attention → Interest → Desire → Action)**
- H1: Bold attention-grabbing statement → Sub: Interesting fact or benefit → Features: Desire-building proof points → CTA: Clear action

**BAB (Before → After → Bridge)**
- H1: "[Before state] → [After state]" → Sub: "Here's how [product] bridges the gap" → Features: How it works (the bridge)

---

## Representative Component: Hero (Centered Gradient — Dark SaaS)

Use this as the structural template for all hero variants. Swap layout classes, gradient direction, and image placement for split, video-bg, and minimal variants.

```tsx
export function HeroCentered() {
  return (
    
      
      
      
        
          
          Now in public beta
        
        
          Ship faster.
          
            Break less.
          
        
        
          The deployment platform that catches errors before your users do.
          Zero config. Instant rollbacks. Real-time monitoring.
        
        
          
            Start free trial
          
          
            See how it works →
          
        
        No credit card required · 14-day free trial
      
    
  )
}
```

---

## Other Section Patterns

### Feature Section (Alternating)

Map over a `features` array with `{ title, description, image, badge }`. Toggle layout direction with `i % 2 === 1 ? "lg:flex-row-reverse" : ""`. Use `` with explicit `width`/`height` and `rounded-2xl shadow-xl`. Wrap in `` with `max-w-6xl` container.

### Pricing Table

Map over a `plans` array with `{ name, price, description, features[], cta, highlighted }`. Highlighted plan gets `border-2 border-violet-500 bg-violet-950/50 ring-4 ring-violet-500/20`; others get `border border-gray-800 bg-gray-900`. Render `null` price as "Custom". Use `` icon per feature row. Layout: `grid gap-8 lg:grid-cols-3`.

### FAQ with Schema Markup

Inject `FAQPage` JSON-LD via `` inside the section. Map FAQs with `{ q, a }` into shadcn `` with `type="single" collapsible`. Container: `max-w-3xl`.

### Testimonials, CTA, Footer

- **Testimonials:** Grid (`grid-cols-1 md:grid-cols-3`) or single-quote hero block with avatar, name, role, and quote text.
- **CTA Banner:** Full-width section with headline, subhead, and two buttons (primary + ghost). Add trust signals (money-back guarantee, logo strip) immediately below.
- **Footer:** Logo + nav columns + social links + legal. Use `border-t border-gray-800` separator.

---

## SEO Checklist

- [ ] `` tag: primary keyword + brand (50–60 chars)
- [ ] Meta description: benefit + CTA (150–160 chars)
- [ ] OG image: 1200×630px with product name and tagline
- [ ] H1: one per page, includes primary keyword
- [ ] Structured data: FAQPage, Product, or Organization schema
- [ ] Canonical URL set
- [ ] Image alt text on all `` components
- [ ] robots.txt and sitemap.xml configured
- [ ] Core Web Vitals: LCP  **Validation step:** Before outputting final code, verify every checklist item above is satisfied. Fix any gaps inline — do not skip items.

---

## Performance Targets

| Metric | Target | Technique |
|---|---|---|
| LCP |  1s | Preload hero image, use `priority` on Next/Image |
| CLS |  0.1 | Set explicit width/height on all images |
| FID/INP |  100ms | Defer non-critical JS, use `loading="lazy"` |
| TTFB |  200ms | Use ISR or static generation for landing pages |
| Bundle |  100KB JS | Audit with `@next/bundle-analyzer` |

---

## Common Pitfalls

- Hero image not preloaded — add `priority` prop to first ``
- Missing mobile breakpoints — always design mobile-first with `sm:` prefixes
- CTA copy too vague — "Get started" beats "Learn more"; "Start free trial" beats "Sign up"
- Pricing page missing trust signals — add money-back guarantee and testimonials near CTA
- No above-the-fold CTA on mobile — ensure button is visible without scrolling on 375px viewport

---

## Related Skills

- **Brand Voice Analyzer** (`marketing-skill/skills/content-production/scripts/brand_voice_analyzer.py`) — Run before generation to establish voice profile and ensure copy consistency
- **UI Design System** (`product-team/ui-design-system/`) — Generate design tokens from brand color before building the page
- **Competitive Teardown** (`product-team/competitive-teardown/`) — Competitive positioning informs landing page messaging and differentiation
