## Effect of PID Components

### P

The `p` component of the algorithm heavily influences the reactivity of the algorithm to small pertubations away from the ground truth. This means that a higher `p` will make the vehicle more reactive when addressing natural curves in the roadway. Lowering the `p` component will help the vehicle more smoothly tackle turns, but can also harm the algorithm's ability to react appropriately when a turn is sharp.

### I

The `i` component of the algorithm does not need to be tuned as much as the other components in this project. This component represents a kind of "working memory" of the overall errors created by the vehicle's inaccurate sterring over the past cycles of processing. It will naturally adjust the vehicle's motion to reduce noise once the algorithm believes the vehicle has converged onto the ground truth, smoothing out the steering errors present in the vehicle itself.

### D

The `d` component of the algorithm modulates the overall effects of the `p` component. If no `d` component were used, the vehicle would vary its steering angle wildly around the ground truth, never really converging. The `d` component needs to be relatively low, while still accounting for any possible overreactions made by the vehicle as a result of its `p` component.

## Tuning Hyperparameters

I tuned the hyperparameters manually.

My methodology was trial and error. I first adjusted the `p` component to see how reactive the vehicle would be with different initial `p` values. I noticed a lot of varying movement around the ground truth in my trials, and began increasing the `d` value to accomodate for that noise. Once the vehicle was driving fairly smoothly, I noticed that the algorithm did not seem to be reactive enough to the curves in the track. At this point I began increasing the `p` value, which had the obvious effect of increasing the noise of steering back and forth around the ground truth. For each increas in `p`, I made a proportional increase in `d` to accomodate for the likelihood of more variation in steering.

Within about 15-20 trials, I found that the values `-0.1` for `p` and `-2.75` for `d` were a good fit for the vehicle successfully driving this track without leaving the drivable portion of the road or being too "wobbly" around the ground truth.
