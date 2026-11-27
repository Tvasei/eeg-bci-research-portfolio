[← Research portfolio](../../README.md)

# Brain responses to electroacupuncture, read through saliency maps

**Tahereh Vasei, Harshil Gediya, Maryam Ravan, Anand Santhanakrishnan, David Mayor, and Tony Steffert** · *Algorithms*, 2024 · [Open paper](https://doi.org/10.3390/a17110477)

For this published study, I classified EEG recorded while 48 participants received transcutaneous electroacupuncture stimulation (TEAS) at 2.5, 10, or 80 pulses per second, or a sham condition at 160. The question I focus on here is not only whether a network can decode the stimulation, but where on the scalp its decision comes from.

## The decoding result

A customized EEGNet separated the pre-stimulation, during-stimulation, and post-stimulation phases with accuracies consistently above 92% at every stimulation frequency, and total classification accuracies across recording slots ranged from 95.65% to 97.66%. Gamma-band (30–50 Hz) activity carried the strongest response to stimulation.

## Saliency maps: which electrodes the model uses

To interpret the network, I computed gradient-based saliency maps for each class, averaged them across samples, and summed each electrode's saliency over time to obtain a single importance score per electrode. The topographic maps below aggregate the saliency for each TEAS frequency.

[![Topographic saliency maps for the four TEAS frequencies, with the frontal electrodes Fp1 and Fp2 showing the highest importance.](../../assets/figures/teas-saliency.png)](../../assets/figures/teas-saliency.png)

*Figure 5 from the published paper. Warmer colors indicate higher saliency. In all four conditions the importance concentrates at the front of the scalp.*

Across all four frequencies, the same seven electrodes carried the highest scores: **Fp1 and Fp2** (prefrontal), **Fz** (frontal midline), **F7 and F8** (dorsolateral prefrontal), and **T3 and T4** (temporal).

## Fewer electrodes, nearly the same accuracy

I then retrained the classifier on electrode subsets ordered by their saliency scores:

| Combination | Electrodes |
| :--- | :--- |
| comb1 | Fp1, Fp2 |
| comb2 | Fp1, Fp2, Fz |
| comb3 | Fp1, Fp2, Fz, F8, F7 |
| comb4 | Fp1, Fp2, Fz, F8, F7, T3, T4 |
| Full montage | All 19 electrodes |

The two prefrontal electrodes alone reached only about 48–52% pre-stimulation accuracy, but accuracy climbed steeply as the frontal and temporal sites were added. The seven-electrode combination (comb4) performed close to the full 19-electrode montage — the remaining twelve electrodes added little. For clinical and wearable EEG, that means a much smaller setup can carry this classification, with shorter preparation and more comfortable recordings.

[Figure credits](../../assets/FIGURES.md) · [Back to the portfolio](../../README.md)
