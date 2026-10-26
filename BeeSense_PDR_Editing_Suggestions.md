# BeeSense — PDR editing suggestions

**Students:** Dror Ben-Simon and Dan Cooper  
**Project:** p-2027-165 — IoT-Based Acoustic and Weight Monitoring of Honeybee Colonies  
**Source:** `pdr-2027-165-DanDror.docx`, submitted 25 October 2026  
**Review date:** 26 October 2026

## 1. Overall assessment

BeeSense has a clear use case and substantial electrical-engineering content: sensor interfaces, low-noise acquisition, embedded signal processing, event-driven power management, weighing, wireless communication, and an autonomous field gateway. The proposed collaboration with Zippory Honey gives the project a plausible route to real measurements. The architecture and preliminary battery calculation are more concrete than a generic “AI for agriculture” proposal.

The main correction is to separate a deliverable monitoring system from an experimental biological prediction claim. The document commits to precision and recall above 90% for advance swarm alerts, but proposes only three to five hives during one spring. That experiment may provide too few independent swarm events to substantiate either number. A successful engineering project should remain possible even if no colony swarms, or if a beekeeper intervenes to prevent departure.

I would support the project direction after revising the labels, alert evaluation, sensor feasibility, and acceptance criteria. The first milestone should demonstrate useful signals and measured energy on a real hive, rather than assume a generic piezo disc reproduces research-grade accelerometer measurements.

## 2. Strengthen the need, value, and scope

### Motivation and intended user

Keep the remote-apiary use case, but qualify the statement that hives are inspected “every few weeks to months.” Inspection practice depends on season and management. Ask the collaborating beekeeper to describe actual visits, response time, connectivity, and preventable losses. Record this as local user evidence rather than present one schedule as universal practice.

Explain the decision supported by an alert: which hive needs inspection, within what time, and what action remains feasible. A warning that arrives too late for the beekeeper to reach the apiary has different value from a warning issued a day earlier. Conversely, warnings that persist for weeks can create substantial unnecessary work.

“Low cost” also needs a budget. Add a node bill of materials including the mechanical weighing platform, enclosure, battery, mounting, microphone, analog front end, and radio antenna. Add the shared gateway cost and recurring SIM/cloud costs. Quote the assumed number of hives per gateway. An inexpensive processor does not establish an inexpensive deployed system.

### Suggested replacement objective

> Develop and characterize an autonomous monitoring system for a small group of honeybee hives without mains power or Wi-Fi. Each node will collect scheduled and event-triggered vibration, audio, weight, and temperature measurements, transmit features to a solar-powered cellular gateway, and display data quality and alerts per hive. The field study will investigate whether the measured signals provide useful advance warning of independently confirmed swarming events, and whether sensor fusion and event-triggered acquisition improve detection or energy use relative to simpler baselines.

Commit to reliable acquisition, communication, measured power, and traceable reporting. Treat advance swarm prediction as the research objective. Define any additional “colony anomalies” individually or remove that broad promise from the acceptance specification.

## 3. Correct the biological outcomes and evaluation logic

### Do not equate preparation with departure

Section 3.3 currently defines a swarm by “an observed departure or by capped queen cells.” These must be separate labels. Queen-cell observations describe a biological condition or preparation indicator; an actual departure is a distinct event. If preparation is the target, define its expert annotation protocol and evaluate that endpoint. If departure is the target, require independent confirmation of departure.

Maintain a field log with hive identity, inspection times, queen-cell observations, observed departures, management interventions, feeding, added or removed equipment, and uncertainty. A colony in which the beekeeper prevents departure should not automatically become a false alarm. Define a separate intervened or censored category, and report those cases explicitly.

### Obtain independent timestamps

Weekly inspection cannot usually supply a precise departure time. Use entrance video, direct documented observation, or another independently reviewed record where feasible. If only an interval is known, report interval uncertainty rather than exact minute-level lead time.

The proposed weight-drop rule must not both define a departure and serve as the detector being evaluated. That would reward the algorithm for agreeing with itself. Weight can support adjudication, but the independence and uncertainty of the reference label must be disclosed. Removing known masses tests the weighing chain and response to a weight step; it does not validate pre-swarm prediction or prove that natural departures have the same signature.

### Define an alert-matching protocol

“An alert is a true positive if it precedes the swarm” is incomplete. Define a minimum actionable lead time, a maximum prediction horizon, and one-to-one event matching. An alert one second before departure and an alert weeks before departure should not automatically receive the same credit.

For illustration, the team could explore a warning interval from 30 minutes to 48 hours before departure, but these are reviewer-proposed values, not established biological thresholds. Agree on the interval with the beekeeper and freeze it before final testing. If several horizons are explored, label the primary one and report the others as exploratory.

Group repeated notifications into alert episodes using a declared reset/cooldown rule. Count an episode as a true positive only under the frozen matching policy. An unmatched eligible episode is a false positive; an independently confirmed eligible departure without a valid warning is a false negative. Define how outages and incomplete ground-truth periods affect eligibility, and also report total monitoring coverage so exclusions cannot hide failures.

### Recognize the sample-size constraint

Report the number of hives, confirmed events, alert episodes, and monitored hive-days alongside precision and recall. Samples from adjacent ten-second recordings are not independent swarm events. As an illustration, even detecting all five independent departures leaves a one-sided exact 95% lower confidence bound of approximately 55% for recall. That is a promising pilot, not evidence establishing recall above 90%.

The final result should be allowed to state that too few events occurred for reliable prediction estimates. Keep an engineering acceptance track and a biological research track. Public or archived data can support algorithm development if their labels and acquisition are suitable, but cannot substitute for validation of the custom sensor in this apiary.

## 4. Improve the acquisition and detection design

### Establish piezo sensitivity experimentally

The feasibility argument moves from published accelerometer measurements to a generic 27-mm piezo disc without establishing equivalent sensitivity or frequency response. A piezo disc responds through its mounting, mechanical loading, capacitance, and analog input impedance. Quoting the research signal amplitude alone does not show that the proposed circuit can measure it.

Specify the disc, preamplifier, biasing, input protection, gain, filtering, ADC settings, and mounting method. Measure circuit noise, saturation, transfer response over the intended band, and reproducibility after remounting. Where possible, compare against a reference vibration sensor or controlled excitation. The real-hive nighttime recording is an important early gate: document whether the measured spectrum is distinguishable from the electronics noise under the actual mounting conditions.

Positioning a sensor in the comb also creates practical requirements. Explain how the frame remains inspectable, how wires are routed, how the sensor tolerates wax/propolis and humidity, and whether installation affects colony management. These are engineering questions to settle with the beekeeper.

### Do not assume an amplitude trigger captures a spectral precursor

The wake circuit reacts to amplitude excursions; the biological hypothesis concerns spectral changes and their evolution. Gradual redistribution of spectral energy may not cause a burst. Keep scheduled recordings as the baseline and evaluate the extra information provided by event-triggered acquisition.

Define the threshold estimator, hysteresis, trigger duration, and event hold-off. Specify whether the 20-minute hold-off suppresses only additional event wakes or also periodic recordings. Test false triggers caused by wind, rain, handling, and other disturbances. Count missed useful events as well as false wakes. A low false-wake count obtained by an insensitive trigger is not sufficient.

The abstract says the sensor “listens at nanoampere current,” whereas the design assigns approximately 2 µA to the wake circuit. A passive piezo and its powered detection circuit are different things. State the total always-on current consistently and distinguish component datasheet estimates from measured board current.

### Correct the feature and threshold statements

Replace `|z| > 3` with `z > 3` wherever the intended condition is an increase above baseline. If both increases and decreases are meaningful, define separate interpretations. Specify how long the condition must persist, how many observations are required, and what happens when baseline variance is close to zero.

Normalizing each band by total power removes a common multiplicative gain in an idealized model. It does not generally cancel frequency-dependent coupling, placement differences, resonance, or changes in the noise contribution. It also removes overall amplitude information. Keep both absolute and normalized features and compare their stability and predictive value. Reject or mark low-signal recordings before normalizing near-zero total power.

Twenty-four equal bands over 50–800 Hz are approximately 31 Hz wide. Explain why that resolution preserves the candidate indicators. State sampling rates, anti-alias filtering, FFT length, analysis window, averaging method, and quantization. Fixed-point FFT is a reasonable implementation choice, but validate its numerical error against an offline reference. No floating-point unit does not make floating-point software impossible; justify the chosen implementation by measured runtime and energy.

A previous-week, same-hour baseline needs a cold-start policy, enough samples per hour, and a treatment for missing data. Avoid incorporating the current sample into its own baseline. Discuss whether progressive pre-swarm changes could be absorbed into an adaptive baseline. Record external temperature and management activity as potential confounders rather than assume every temperature rise is swarm-specific.

The proposed three-sigma fusion rule is a hypothesis inspired by prior observations, not a validated implementation of the published predictors. Ramsey et al. used learned spectral discrimination and spectral-history analysis [1]; Ferrari et al. reported acoustic and temperature observations [2]. Neither directly validates this particular rule.

## 5. Make weighing, power, and communications claims reviewable

### Weighing

HX711 noise is only one contributor to the complete scale error. Add load-cell sensitivity/tolerance, creep, temperature effects, corner loading, platform stiffness, calibration, and ADC settling after power-up. Clarify whether ±20 g means absolute accuracy over 0–200 kg, repeatability, or accuracy of a short-term weight difference. These are different requirements.

For detecting a nominal 0.8-kg drop, a stable change measurement may matter more than ±20-g absolute accuracy across full scale. Set the requirement from the intended decision. Test reference masses at several loads, off-center placement, temperature variation, and multi-day drift. Do not infer field accuracy from nominal ADC resolution.

### Node and gateway energy

The preliminary calculation is useful: 96 acquisitions/day at 0.3 A·s each plus 22 µA standby gives approximately 0.355 mA average and 282 days from 2400 mAh usable capacity. That broadly matches the stated estimate, but depends on the acquisition charge being correct.

Measure the complete cycle: sensor startup, recording, FFT, radio association/channel handling, transmit, acknowledgment/retry, and shutdown. Include board regulator losses, powered sensor bridges, indicator LEDs, and any sensors that remain active. Show expected and adverse event/retry scenarios. Six months should be a projection supported by measured profiles and a stated usable-capacity margin, unless a full-duration test is available.

The hub's 0.5 W is 12 Wh/day. A nominal 15-W panel does not guarantee 45 Wh/day in every installation. Specify the assumed solar resource, charging/conversion losses, shading, cellular connection behavior, battery capacity, and required days of low-sun autonomy. “Thirty days unattended” should mean no maintenance intervention under declared conditions; distinguish it from thirty days without solar input.

Replace “thousands of times less power” with an explicitly estimated comparison. The referenced research system continuously acquired data, while BeeSense records intermittently. Compare energy and retained detection performance at the same time; different duty cycles alone do not prove a better sensing method. Include gateway consumption amortized over the declared hive count when describing deployed-system power.

### Communication and availability

Define packet delivery at the receiving application, not merely the transmitter's success callback. Espressif distinguishes MAC-layer delivery from application receipt and recommends application acknowledgments, retry handling, and sequence numbers where required [5]. Add hive ID, acquisition timestamp, sequence number, firmware version, and data-quality flags.

Define buffering during cellular outages, stale-data indication, hub reboot recovery, and the maximum acceptable delay for an alert. Test simultaneous periodic reports from several nodes and disturbances at the actual hive placement. “Fallback: LoRa” is a separate hardware/protocol change; give it an early decision date or remove it as an assumed effortless fallback.

## 6. Revised KPI and acceptance table

These are proposed edits to the project requirements. Additional numerical thresholds below are examples for agreement after the pilot, not literature-established guarantees.

| Requirement | Recommended revision | Acceptance evidence |
| --- | --- | --- |
| Pre-swarm precision/recall >90% | Research targets; define event unit, warning interval, eligibility, and minimum evidence needed for a claim | Independently confirmed events; counts, uncertainty, lead-time distribution, and hive-days |
| No missed departure | Separate departure detection from advance prediction; avoid an unconditional guarantee | Recall on observed eligible departures; report outage-period events separately |
| ≤1 false alert/hive-week | Retain as a provisional user-facing target with a fixed episode policy | False episodes divided by eligible hive-weeks, plus total alert burden and coverage |
| ±20 g weighing | State range, temperature, settling, absolute/change error, and calibration | Full-system reference-mass tests, corner loads, drift, and field conditions |
| Valid vibration/audio | Add explicit signal-quality acceptance and mounting repeatability | Noise/signal comparisons, controlled excitation, clipping and invalid-recording rate |
| ≤20 false wakes/hive-day | Evaluate together with useful-event capture and energy | Annotated trigger trials and comparison with scheduled reference recordings |
| ≥95% packet delivery | Define application receipt, retry budget, node count, range, and deadline | Sequence-based sent/received counts and latency at the apiary |
| ≥6-month node life | Project from measured complete operating cycles with margins | Power-analyzer profiles, usable battery capacity, and event/retry scenarios |
| ≥30 days unattended | Define maintenance and availability expectations | Field uptime log, missing-data periods, resets, interventions, and solar/battery history |
| Low cost | Add node, gateway, installation, and recurring costs | Bill of materials and cost per hive at a specified deployment size |
| Useful sensor fusion | Add comparison against simpler sensing | Weight-only, acoustic/vibration-only, and fused results on the same eligible events |

Alert precision and false alerts per week are complementary. With few real events, even an apparently modest false-alert rate can produce poor precision. Report both; do not treat one threshold as guaranteeing the other.

## 7. Evaluation plan and scope protection

Run three evaluation stages. First characterize sensors, mechanics, timing, packet delivery, and power on the bench. Second perform a short real-hive feasibility pilot to fix mounting, feature extraction, thresholds, and field logging. Third freeze the evaluated system and collect untouched prospective data.

Use held-out hives where possible, alongside a later time period. Report same-hive future performance separately from transfer to another hive. Thresholds, persistence rules, fusion choices, and alarm matching must not be repeatedly adjusted after seeing the final swarm outcomes.

Compare weight-only detection, acoustic/vibration-only detection, and the fused rule. Separately compare scheduled-only acquisition with scheduled-plus-event acquisition, measuring both information retained and energy. An empty platform helps reveal environmental/mechanical disturbance but is not a substitute for a healthy nonswarming colony control.

Retain a limited raw audio/vibration reference set during development, through local storage or an explicit retrieval procedure. Sending only 24 band energies permanently discards information needed to diagnose aliasing, coupling, unexpected noise, and feature-selection errors. The reference recording plan must be included in its own storage and energy budget.

If too few natural swarms occur, complete the measured monitoring platform, publish the uncertainty honestly, and report exploratory biological results. Controlled mass changes validate weight-step detection, and replay validates software operation; neither should be relabeled as successful biological prediction. Avoid expanding into general colony-health diagnosis to compensate for scarce swarm labels.

## 8. Literature and supporting evidence

The sources below support the design rationale and the limits of the claims. They do not establish BeeSense's numerical acceptance targets. Publisher, university, and official documentation records were checked; this review is not an exhaustive novelty survey. AlphaXiv-targeted searches did not locate a suitably matched primary paper to add, so no unrelated AlphaXiv citation is supplied merely to fill the bibliography.

1. **Ramsey et al. (2020), “The prediction of swarming in honeybee colonies using vibrational spectra.”** [Primary paper](https://doi.org/10.1038/s41598-020-66115-5) · [Open full text](https://pmc.ncbi.nlm.nih.gov/articles/PMC7298004/). Supports the plausibility of vibrational predictors. The methods use learned spectral discrimination, including a history-based approach, and report accuracy above 90%. This is not evidence that a generic piezo plus a fixed three-sigma rule achieves the same precision, recall, or warning horizon.

2. **Ferrari et al. (2008), “Monitoring of swarming sounds in bee hives for early detection of the swarming period.”** [Publisher](https://www.sciencedirect.com/science/article/pii/S0168169908001385) · [University record](https://air.unimi.it/handle/2434/61221). Reports acoustic and temperature observations from three hives over 270 hours with nine swarming activities, including spectral changes near 110–300 Hz. Useful for candidate features; the observations do not validate the proposed alarm threshold or all-site generalization.

3. **Bencsik et al. (2015), “Honeybee Colony Vibrational Measurements to Highlight the Brood Cycle.”** [Primary paper](https://doi.org/10.1371/journal.pone.0141926). Uses calibrated accelerometers in central comb locations, with temporal averaging and nighttime analysis. Supports sensitivity to placement and biological context. Brood-related vibration is also a reason not to assume that every acoustic change uniquely identifies swarm preparation. Its sensor setup does not establish sensitivity of the proposed piezo circuit.

4. **Cecchi et al. (2020), “A Smart Sensor-Based Measurement System for Advanced Bee Hive Monitoring.”** [Primary paper](https://doi.org/10.3390/s20092726) · [Publisher PDF](https://mdpi-res.com/d_attachment/sensors/sensors-20-02726/article_deploy/sensors-20-02726-v2.pdf). Describes a modular multisensor installation, Raspberry Pi-based hive units, four load sensors, and approximately 4.2 W per hive unit. Supports an architectural comparator, but power comparisons must account for continuous versus intermittent acquisition and the shared gateway.

5. **Espressif, ESP-NOW programming guide.** [Official ESP32-C3 documentation, project-cited version](https://docs.espressif.com/projects/esp-idf/en/v5.3.2/esp32c3/api-reference/network/esp_now.html) · [Official documented delivery semantics](https://docs.espressif.com/projects/esp-idf/en/v5.5/esp32/api-reference/network/esp_now.html). Supports direct radio communication and the distinction between MAC success and application receipt. Freeze the actual target/version and verify payload size, peer limits, retries, and channel settings against that version.

6. **“Empirical Analysis of Honeybees Acoustics as Biosensors Signals for Swarm Prediction in Beehives,” IEEE Access (2024).** [Publisher record](https://ieeexplore.ieee.org/abstract/document/10701518) · [DOI](https://doi.org/10.1109/ACCESS.2024.3471895). Evaluates acoustic classification approaches on NU-hive data. Useful as a lead for an offline feature/model baseline. Before reuse, inspect the labels, event timing, split unit, and data access; high clip-level accuracy is not automatically prospective early-warning performance on new hives.

For component feasibility, replace generic datasheet references with exact load-cell, HX711 module, piezo, microphone, regulator, battery, and wake-circuit parts and operating conditions. Commercial capability comparisons should also carry a dated official source; they cannot establish an independent head-to-head performance result.

## 9. Suggested replacement abstract

> BeeSense is an autonomous monitoring prototype for honeybee colonies at apiaries without mains power or Wi-Fi. Battery-powered hive nodes collect scheduled and event-triggered vibration and acoustic measurements together with weight and temperature. Embedded processing extracts spectral features, which are transmitted to a solar-powered cellular gateway and displayed on a per-hive dashboard. The engineering evaluation will characterize signal quality, weighing performance, application-level packet delivery, energy consumption, and field availability. A prospective study on three to five hives will investigate whether the measured features provide actionable advance warning of independently confirmed swarming events. Prediction performance will be reported using a predefined alert-matching policy, false alerts per hive-week, event-level precision and recall, and warning lead time, subject to the number of observed events. Comparisons with simpler sensing and scheduled-only acquisition will assess the value of sensor fusion and event-driven operation. Six-month node autonomy is an initial target to be supported by measured operating profiles.

## 10. Prioritized editing checklist

- Separate preparation, actual departure, departure detection, and advance prediction throughout the document.
- Replace the committed >90% biological performance claim with a research target and an explicit evidence requirement.
- Define independent ground truth, alert episodes, prediction horizon, actionable lead time, interventions, and outages.
- Validate the piezo acquisition and wake circuit before treating sensitivity as established.
- Correct the sign of the z-score threshold and qualify the normalization claim.
- Complete acquisition settings and retain development reference recordings.
- Distinguish scale resolution, repeatability, absolute accuracy, and short-term change accuracy.
- Measure complete node energy and provide a gateway battery/solar budget.
- Define application-level delivery, buffering, stale data, and alert latency.
- Add simpler baselines and a frozen prospective evaluation protocol.
- Include a realistic cost breakdown and qualify the power-comparison claim.
- Give the first real-hive signal/power demonstration a dated milestone before full field deployment.

The strongest final project would deliver a characterized, reliable monitoring platform and a defensible answer about which signals helped, how much energy they required, and what the available field events actually support.
