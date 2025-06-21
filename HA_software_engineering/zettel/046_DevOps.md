# DevOps
- **Level**: L5
- **Definition**: The marriage of development and operations
- **Korean**: 데브옵스
- **Context**: When developers are forced to feel the pain they cause

## Core Understanding
DevOps is what happens when you make developers responsible for their code at 3 AM. It's the radical idea that the people who break production should also fix it. Like making arsonists join the fire department, it creates a beautiful feedback loop of suffering and enlightenment.

## Deeper Insights
- **CI/CD**: Continuous Integration, Continuous Disappointment
- **Infrastructure as Code**: Because nothing says "reliable" like executable documentation
- **Monitoring**: Watching systems fail in real-time with pretty graphs
- **On-Call Rotation**: Distributed suffering for distributed systems

## Technical Details
```yaml
# The DevOps Pipeline of Broken Dreams
name: CI/CD Pipeline
on:
  push:
    branches: [main, develop, hotfix/*, prayer/*]
  pull_request:
    types: [opened, closed, panicked]
  schedule:
    - cron: '0 3 * * *'  # Daily failure at 3 AM

jobs:
  test:
    runs-on: ubuntu-latest-with-issues
    steps:
      - name: Checkout code
        uses: actions/checkout@v2
        with:
          fetch-depth: 0  # Get all history to blame properly
          
      - name: Run tests
        run: |
          echo "Running tests..."
          npm test || echo "Tests failed but deploying anyway"
          
      - name: Security scan
        run: |
          echo "Scanning for vulnerabilities..."
          npm audit || echo "Security is overrated"
          
  deploy:
    needs: [test]  # "needs" is a strong word
    if: always()   # YOLO deployment strategy
    runs-on: self-hosted-prayer-circle
    steps:
      - name: Deploy to production
        run: |
          # No staging environment because we live dangerously
          kubectl set image deployment/app app=$IMAGE_TAG
          kubectl rollout status deployment/app || \
            kubectl rollout undo deployment/app
          
      - name: Notify on-call
        if: failure()
        run: |
          curl -X POST $SLACK_WEBHOOK \
            -d '{"text":"🔥 Production is on fire. Again. 🔥"}'
            
      - name: Update status page
        if: always()
        run: |
          # Always say everything is fine
          curl -X POST https://status.company.com/api \
            -d '{"status":"operational","lie":true}'

# Post-deployment regret
on-call:
  schedule:
    - name: "Poor soul #1"
      days: ["Mon", "Tue", "Wed"]
      phone: "+1-555-HELP-ME"
    - name: "Poor soul #2"  
      days: ["Thu", "Fri", "Sat", "Sun"]
      phone: "+1-555-SAVE-ME"
```

## Connection to Truth
DevOps embodies the Buddhist principle that suffering leads to enlightenment. By making developers experience the consequences of their actions, we create a karmic loop of cause and effect. It's applied philosophy: you shall reap what you deploy.

## When It Matters
- **Deployment Velocity**: Ship bugs faster than ever
- **System Reliability**: Someone's always watching (and crying)
- **Automation**: Because humans make mistakes, let's automate them
- **Culture Change**: From "not my problem" to "everything is my problem"

## Human Element
DevOps engineers are the Swiss Army knives of tech—equally bad at development and operations, but somehow responsible for both. They speak in pipelines and think in containers. They've automated themselves into permanent on-call duty and convinced themselves this is progress. They're the digital janitors with admin access.

## Related Concepts
- [[045_cloud_computing]] - Where DevOps engineers live
- [[039_version_control]] - The source of truth
- [[023_testing]] - What we pretend to do
- [[051_technical_debt]] - What we actually create

## Metadata
- **Created**: 2024-01-20
- **Modified**: 2024-01-20
- **Zettel ID**: 046
- **Abstraction Level**: L5
- **Domain**: Operations