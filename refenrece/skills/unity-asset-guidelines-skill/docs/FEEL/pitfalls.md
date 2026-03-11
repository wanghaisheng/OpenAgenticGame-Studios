# FEEL Pitfalls

## Development Checklist

Check before writing code:

- [ ] Verify Initialization timing before using RestoreInitialValues
- [ ] Be cautious with feedback manipulation in OnEnable (may run before MMF_Player initializes)
- [ ] Test on Android/iOS builds (may behave differently from Editor)
- [ ] Cache initial values manually when using Transform manipulation feedbacks
- [ ] Check `IsPlaying` before calling StopFeedbacks if needed

## Troubleshooting by Symptom

| Symptom | Cause | Solution | Details |
|---------|-------|----------|---------|
| Transform resets to (0,0,0) instead of Inspector values | RestoreInitialValues called before Initialization | Manual caching in Awake | [Details](./pitfalls/restore-initial-values.md) |
| Different behavior on Android/iOS vs Editor | Script execution order difference | Set InitializationMode or manual init | [Details](./pitfalls/restore-initial-values.md) |
| First instance behaves differently | Initialization timing race condition | Explicit Initialization() call in Start | [Details](./pitfalls/restore-initial-values.md) |
| Feedback not playing | IsPlaying still true from previous play | Call StopFeedbacks first | - |
| Feedback plays but no visible effect | Target not assigned or wrong target | Check Inspector assignments | - |

## Template for Adding New Pitfalls

When discovering a new pitfall:
1. Add prevention item to checklist
2. Add symptom/cause/solution to troubleshooting table
3. Create detailed file in `./pitfalls/` (if needed)
