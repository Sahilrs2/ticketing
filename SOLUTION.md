# Agentic Ticket Triage

## Design

The triage agent investigates each support ticket using tools to inspect ticket details, resolve accounts, retrieve account context, find related tickets, and search the knowledge base. It uses the gathered evidence to determine category, priority, routing, escalation, TAM notification, duplicate status, clarification needs, and draft responses.

The agent follows a tool-driven reasoning loop: it observes results, chooses relevant next actions, and stops when it has enough evidence or reaches its iteration limit. Ticket content is treated as untrusted input, and security incidents receive priority handling. Retrieval favors relevant current knowledge-base guidance over deprecated articles.

## Evaluation Plan

- Run the provided data validation script.
- Execute the required review set of 10 tickets.
- Run the output checker and confirm schema validity.
- Verify security incident classification and escalation.
- Verify active incident matching and Premium account TAM notification.
- Verify account resolution when the account ID is missing.
- Test prompt-injection resistance and deprecated knowledge-base filtering.
- Review reasoning traces and fallback behavior for failed model calls.

## Scaling

For 10x ticket volume, use bounded concurrent processing, request timeouts, retry limits, caching for account context and knowledge-base retrieval, and structured logs. Monitor model latency, failure rates, decision accuracy, and escalation quality.

## Limitations

Model output and retrieval quality can vary. Fallback decisions may be less accurate than evidence-rich agent decisions. Production deployment requires stronger evaluation, secret management, monitoring, and human review for high-impact security decisions.

## Run

```bash
python scripts/validate_data.py
python run.py --set review
python scripts/check_outputs.py
```
