# Scenario Naming Conventions

This document describes the naming conventions and parameter configurations used for vaccination scenario files in the COVID-19 Mesa model.

## Naming Format

Scenario files follow the naming pattern:
```
cu-vaccination-test-{scenario}-{num_agents}-{model_type}.json
```

Where:
- **`cu`**: Champaign-Urbana location identifier
- **`vaccination-test`**: Test type identifier
- **`{scenario}`**: Scenario description (e.g., `rapid-effective`, `slow-effective`, `no-vaccination`)
- **`{num_agents}`**: Number of agents in the simulation (e.g., `10`, `200`, `1000`, `2000`)
- **`{model_type}`**: Model parameter set (`stdM` for Standard Model, `heavyM` for Heavy Model)

## Model Parameter Sets

The model supports two predefined parameter sets that represent different epidemiological conditions:

### Standard Model (`stdM`)

The Standard Model represents baseline epidemiological conditions with moderate transmission rates:

```json
{
  "rate_inbound": 0.0002,
  "prop_initial_infected": 0.004,
  "avg_incubation_time": 3,
  "avg_recovery_time": 11,
  "proportion_asymptomatic": 0.35,
  "proportion_severe": 0.08,
  "prob_contagion": 0.009,
  "proportion_beds_pop": 0.001
}
```

### Heavy Model (`heavyM`)

The Heavy Model represents more severe epidemiological conditions with higher transmission and severity rates:

```json
{
  "rate_inbound": 0.0004,
  "prop_initial_infected": 0.006,
  "avg_incubation_time": 3,
  "avg_recovery_time": 11,
  "proportion_asymptomatic": 0.25,
  "proportion_severe": 0.12,
  "prob_contagion": 0.0130,
  "proportion_beds_pop": 0.001
}
```

**Key Differences:**
- Higher inbound rate and initial infection proportion in Heavy Model
- Lower proportion of asymptomatic cases in Heavy Model (25% vs 35%)
- Higher proportion of severe cases in Heavy Model (12% vs 8%)
- Higher contagion probability in Heavy Model (0.0130 vs 0.009)

## Testing Implementation

All models implement testing starting on **Day 14** of the simulation.

## Vaccination Scenarios

Each scenario is designed to test different vaccination rollout strategies. All scenarios are run with both Standard Model (`stdM`) and Heavy Model (`heavyM`) parameter sets.

### Scenario A: Rapid and Effective Vaccination

Vaccination rollout begins early and achieves high effectiveness:

```json
{
  "day_vaccination_begin": 60,
  "day_vaccination_end": 700,
  "effective_period": 10,
  "effectiveness": 0.95,
  "distribution_rate": 8,
  "cost_per_vaccine": 400
}
```

**Characteristics:**
- Early start (Day 60)
- High effectiveness (95%)
- High distribution rate (8)
- Higher cost per vaccine ($400)

### Scenario B: Rapid but Low-Effectiveness Vaccination

Vaccination rollout begins early but with reduced effectiveness:

```json
{
  "day_vaccination_begin": 60,
  "day_vaccination_end": 700,
  "effective_period": 10,
  "effectiveness": 0.55,
  "distribution_rate": 8,
  "cost_per_vaccine": 200
}
```

**Characteristics:**
- Early start (Day 60)
- Moderate effectiveness (55%)
- High distribution rate (8)
- Lower cost per vaccine ($200)

### Scenario C: Slow but Effective Vaccination

Vaccination rollout begins later but maintains high effectiveness:

```json
{
  "day_vaccination_begin": 300,
  "day_vaccination_end": 700,
  "effective_period": 10,
  "effectiveness": 0.95,
  "distribution_rate": 8,
  "cost_per_vaccine": 200
}
```

**Characteristics:**
- Delayed start (Day 300)
- High effectiveness (95%)
- High distribution rate (8)
- Lower cost per vaccine ($200)

### Scenario D: No Vaccination

Control scenario with no vaccination rollout:

```json
{
  "day_vaccination_begin": 700,
  "day_vaccination_end": 700,
  "effective_period": 10,
  "effectiveness": 0.00,
  "distribution_rate": 0,
  "cost_per_vaccine": 0
}
```

**Characteristics:**
- No effective vaccination (begin and end on same day)
- Zero effectiveness
- Zero distribution rate
- Zero cost

### Scenario E: Slow and Limited Supply Vaccination

Vaccination rollout begins late with limited availability:

```json
{
  "day_vaccination_begin": 300,
  "day_vaccination_end": 700,
  "effective_period": 2,
  "effectiveness": 0.95,
  "distribution_rate": 5,
  "cost_per_vaccine": 200
}
```

**Characteristics:**
- Delayed start (Day 300)
- High effectiveness (95%)
- Reduced distribution rate (5)
- Shorter effective period (2)
- Lower cost per vaccine ($200)

## Future Considerations

Potential extensions to the model could include:
- Variable cost analysis for vaccination and testing
- Budget-constrained optimization scenarios (e.g., "Given a budget of $1,000,000, how should a town allocate funds between vaccination and testing to minimize deaths?")

