# How to Request a Feature

This guide helps you submit feature requests that we can act on.

## Before You Request

- **Check existing requests** - Search [GitHub Issues](https://github.com/your-org/SharKNX/issues) to see if your idea has already been suggested
- **Read the roadmap** - See our [Roadmap](../docs/roadmap.md) to learn what we're already planning
- **Review the app** - Make sure the feature doesn't already exist

## How to Submit

### Via GitHub Issues

1. Click **"New Issue"** on the [GitHub Issues page](https://github.com/your-org/SharKNX/issues)
2. Fill out the feature request template below
3. Submit

### Via Email (General Feedback)

Send your idea to **info@owl-automata.com** with the subject line: `SharKNX | Feature Request | Your idea title`

---

## Feature Request Template

Use this template when suggesting new features. Clear explanations help us understand your need!

```
## Problem Description
[Explain the problem or use case.]

## Proposed Solution
[Describe how this feature would solve the problem]

## Importance Level
- [ ] **Nice-to-have** - Would be good but not urgent
- [ ] **Important** - Would improve workflow significantly
- [ ] **Critical** - Essential for your use case

## Additional Context
[Any other information that might help, screenshots, examples, etc.]
```

---

## Example Feature Request

```
## Problem Description
When monitoring KNX bus traffic, there's no way to filter telegrams by a specific group address or device. With large KNX installations (200+ devices), the telegram log becomes overwhelming and it's hard to find relevant traffic.

## Proposed Solution
Add filtering options to the Bus Traffic Monitor:
1. Filter by source address (e.g., 1.1.1)
2. Filter by destination group address (e.g., 5/5/10)
3. Filter by DPT type (e.g., show only temperature values)
4. Save custom filter profiles for quick switching

## Importance Level
- [ ] Nice-to-have
- [x] **Important** - Filtering makes diagnostics 10x faster on large projects
- [ ] Critical

## Additional Context
Most professional KNX tools (ETS, other diagnostic apps) have this feature. On-site integrators depend on this for troubleshooting.
```

---

## What Happens Next?

1. **Review** - We'll evaluate your request within 1 week
2. **Discussion** - We may ask questions or suggest modifications
3. **Roadmap Update** - If approved, we'll consider it for future releases
4. **Implementation** - Features are prioritized based on impact and community interest

---

## Need Help?

Questions about feature requests? Email **info@owl-automata.com**

