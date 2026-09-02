# HR Onboarding Automation — Workflow Template

> **Price:** $79 · **Build time:** ~8–12 hours · **Difficulty:** Advanced

End-to-end new hire onboarding. Fires welcome emails, assigns Planner tasks, hands off to onboarding + HR policy agents, automates 30/60/90-day check-ins.

---

## What It Does

### Triggers
- **New hire row added** to SharePoint list or Microsoft Forms submission
- **Scheduled trigger** — runs X days before start date

### Logic Flow

```
New hire record created → Welcome email (Outlook)
                          ↓
               Planner tasks created:
               - IT: equipment provisioning
               - Facilities: badge + desk
               - Buddy: welcome plan
                          ↓
               Onboarding Buddy Agent handoff
               (conversational welcome + FAQ)
                          ↓
               Benefits Q&A via HR Policy Agent
                          ↓
               30/60/90-day scheduled check-ins
                          ↓
               Completion dashboard → HR SharePoint
```

Personalized welcome, structured onboarding path, automated check-ins.

---

*Pairs with: `onboarding-buddy-agent.yaml` + `hr-policy-agent.yaml`*
