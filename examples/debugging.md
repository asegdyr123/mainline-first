# Example: Debugging

## User goal

A motor is oscillating at high frequency and needs to be made stable.

## Expected Mainline First behavior

Use:

symptom -> likely failure layer -> discriminating test -> result -> fix

Start with the measurements or tests that can distinguish controller instability, sensor noise, mechanical resonance, or command jitter.

Do not dump a large generic list of every possible motor problem before using the available evidence.
