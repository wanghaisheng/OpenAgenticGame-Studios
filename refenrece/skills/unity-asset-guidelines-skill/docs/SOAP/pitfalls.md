# SOAP Pitfalls

## Development Checklist

Check before writing code:

- [ ] Subscribe in OnEnable, unsubscribe in OnDisable
- [ ] Null check before subscribe/unsubscribe for events
- [ ] Use Variable/Event instead of direct references (Singleton)
- [ ] Create custom class for parameterized Events (`ScriptableEvent<T>`)
- [ ] Control frequency when raising Events in Update
- [ ] Share original ScriptableObjects instead of copying

## Troubleshooting by Symptom

| Symptom | Cause | Solution | Details |
|---------|-------|----------|---------|
| Memory leak / Object not garbage collected | Subscribe without unsubscribe | Use OnEnable/OnDisable pair | [Details](./pitfalls/variable-listener-leak.md) |
| NullReferenceException on event | Event not assigned in Inspector | Add null check before subscribe | [Details](./pitfalls/event-null-check.md) |
| Event not firing | Forgot to call Raise() or wrong event reference | Verify event reference and Raise call | - |
| Multiple listeners triggered unexpectedly | Same SO shared across instances | Intended behavior - use instance data if needed | - |
| Value not updating in UI | Listener not registered or wrong variable | Check OnEnable subscription | [Details](./pitfalls/variable-listener-leak.md) |

## Template for Adding New Pitfalls

When discovering a new pitfall:
1. Add prevention item to checklist
2. Add symptom/cause/solution to troubleshooting table
3. Create detailed file in `./pitfalls/` (if needed)
