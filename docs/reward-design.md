# Case study: dense feedback versus checkpoint progress

## Observation

The HW3-2 report describes circling, local oscillation, and uneven behavior across maps during early experiments with a strongly weighted distance-difference term. These are qualitative observations from the report, not measurements reconstructed from a video or experiment rerun.

## Original distance signal

`previous_distance - current_distance` supplied dense feedback about the magnitude of local progress. The report explains that prioritizing this signal did not reliably align the agent's behavior with checkpoint completion.

## Revision

The submitted `RewardManager.calculate_distance_reward()` compares the norms of successive `target_position` observations and returns +1, -1, or 0. `calculate_reward()` combines this with checkpoint-index progress weighted by 50 and the survival/death term.

The first observation returns zero total reward because there is no previous observation to compare. Reward history resets between episodes.

## What the evidence supports

The source confirms the submitted reward formula. The report supports the stated failure behavior and design motivation. It does not establish a numerical improvement, a best choice of weights, or generalization to unseen maps. The separate HW3-1 return log and plots must not be used as evidence of this change's effect.

## Source pointers

- `archive/HW3-2/rl_play.py`: `RewardManager`, `MLPlay.config`, PPO integration.
- Original HW3-2 report, pp. 1–2: reward variants, behavior observations and rationale.
