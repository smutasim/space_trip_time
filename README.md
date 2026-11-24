# space_trip_time

Single-file Deep Space Trip Time Estimator. Open `index.html` in a browser.

Order-of-magnitude straight-line travel times between Solar System bodies, nearby stars, or one custom object (distance to the Sun). Gravity and orbital mechanics are ignored.

## Model

- **Acceleration mode:** constant proper acceleration, accelerate over half the distance then decelerate symmetrically (start and arrive at rest). Uses the exact hyperbolic-motion solution (`x = (c²/a)(γ−1)`, `t = (c/a) sinh η`, `τ = (c/a) η`), which reduces to `t = √(2x/a)` at low speed. It replaces the earlier 101-segment numerical integrator, which drifted by about 0.5% near 0.95c and clamped speed at 0.999999c.
- **Impulse mode:** two burns summing to total Δv; cruise at Δv/2. Burn time is ignored and Δv is added classically (not by rapidity). Δv/2 must be below c.
- **Range:** if the two objects are within 10 AU of each other, a conjunction (|r1−r2|) / opposition (r1+r2) range is shown.
- **Relativity:** traveler (proper) time is shown when peak speed is at least 1% of c. Stars are placed collinear with the Sun, so star-to-star distance is a lower bound.
- Light-year is 9,460,730,472,580.8 km (the earlier 9.4607e12 was rounded).

## Input handling

- Empty, non-numeric, negative, zero, or overflowing inputs show an inline message and mark the field `aria-invalid`.
- Same start and destination (including Custom to Custom) gives distance 0 and duration 0.
- Results that overflow double precision report an error instead of printing NaN or Infinity.
- Durations scale from µs through years; beyond 10^9 years they use scientific notation. Speeds near c show `(1 − ε) c` and γ is listed in Details.
- Enter submits the form. After the first Calculate, results update as inputs change.
