---
name: senior-pm
description: "Senior Project Manager for enterprise software, SaaS, and digital transformation projects. Specializes in portfolio management, quantitative risk analysis, resource optimization, stakeholder alignment, and executive reporting. Uses advanced methodologies including EMV analysis, Monte Carlo simulation, WSJF prioritization, and multi-dimensional health scoring. Use when a user needs help with project plans, project status reports, risk assessments, resource allocation, project roadmaps, milestone tracking, team capacity planning, portfolio health reviews, program management, or executive-level project reporting — especially for enterprise-scale initiatives with multiple workstreams, complex dependencies, or multi-million dollar budgets."
---

# Senior Project Management Expert

## Overview

Strategic project management for enterprise software, SaaS, and digital transformation initiatives. Provides portfolio management capabilities, quantitative analysis tools, and executive-level reporting frameworks for complex, multi-project portfolios.

### Core Expertise Areas

**Portfolio Management & Strategic Alignment**
- Multi-project portfolio optimization using advanced prioritization models (WSJF, RICE, ICE, MoSCoW)
- Strategic roadmap development aligned with business objectives and market conditions
- Resource capacity planning and allocation optimization across portfolio
- Portfolio health monitoring with multi-dimensional scoring frameworks

**Quantitative Risk Management**
- Expected Monetary Value (EMV) analysis for financial risk quantification
- Monte Carlo simulation for schedule risk modeling and confidence intervals
- Risk appetite framework implementation with enterprise-level thresholds
- Portfolio risk correlation analysis and diversification strategies

**Executive Communication & Governance**
- Board-ready executive reports with RAG status and strategic recommendations
- Stakeholder alignment through sophisticated RACI matrices and escalation paths
- Financial performance tracking with risk-adjusted ROI and NPV calculations
- Change management strategies for large-scale digital transformations

## Methodology & Frameworks

### Three-Tier Analysis Approach

**Tier 1: Portfolio Health Assessment**
Uses `project_health_dashboard.py` to provide comprehensive multi-dimensional scoring:

```bash
python3 scripts/project_health_dashboard.py assets/sample_project_data.json
```

**Health Dimensions (Weighted Scoring):**
- **Timeline Performance** (25% weight): Schedule adherence, milestone achievement, critical path analysis
- **Budget Management** (25% weight): Spend variance, forecast accuracy, cost efficiency metrics
- **Scope Delivery** (20% weight): Feature completion rates, requirement satisfaction, change control
- **Quality Metrics** (20% weight): Code coverage, defect density, technical debt, security posture
- **Risk Exposure** (10% weight): Risk score, mitigation effectiveness, exposure trends

**RAG Status Calculation:**
- 🟢 Green: Composite score 80, all dimensions 60
- 🟡 Amber: Composite score 60-80, or any dimension 40-60
- 🔴 Red: Composite score 18): Eliminate through scope/approach changes
- **Mitigate** (12-18): Reduce probability or impact through active intervention
- **Transfer** (8-12): Insurance, contracts, partnerships
- **Accept** (18 (Avoid threshold), STOP and initiate escalation to project sponsor before proceeding.

3. **Capacity Analysis**
   ```bash
   python3 scripts/resource_capacity_planner.py current_portfolio.json
   ```
   ⚠️ If any team utilization 90% or 80% within 10% of planned timeline
- Budget Variance: 85 composite rating
- Risk Mitigation Coverage: 90% risks with active plans
- Resource Utilization: 75-85% average

### Strategic Value
- ROI Achievement: 90% projects meeting projections within 12 months
- Strategic Alignment: 95% investment aligned with business priorities
- Innovation Balance: 70% operational / 20% growth / 10% transformational
- Stakeholder Satisfaction: 8.5/10 executive average
- Time-to-Value: 70% probability assessment accuracy

## Continuous Improvement Framework

### Portfolio Learning Integration
- Capture lessons learned from completed projects
- Update risk probability assessments based on historical data
- Refine estimation accuracy through retrospective analysis
- Share best practices across project teams

### Methodology Evolution
- Regular review of prioritization model effectiveness
- Update risk frameworks based on industry best practices
- Integrate new tools and technologies for analysis efficiency
- Benchmark against industry portfolio performance standards

### Stakeholder Feedback Integration
- Quarterly stakeholder satisfaction surveys
- Executive interview feedback on decision support quality
- Team feedback on process efficiency and effectiveness
- Customer impact assessment of portfolio decisions

## Related Skills

- **Product Strategist** (`product-team/product-strategist/`) — Product OKRs align with portfolio objectives
- **Scrum Master** (`project-management/scrum-master/`) — Sprint velocity data feeds project health dashboards
