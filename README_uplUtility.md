## uplUtility

Utility helper module for per-axis motor enable/disable commands.

### Integration Example

```txt
// Enable motor on A axis before running motion
uplMotorOn(A_AXIS)
```

### Notes

- APIs are axis-scoped through `AChooseAxis[AProgThread]`.
- `MOTOR_ON` / `MOTOR_OFF` constants are defined in `uplUtility.puh2`.
