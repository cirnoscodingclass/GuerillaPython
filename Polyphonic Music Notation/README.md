# Polyphonic Music Notation

We're re-creating Andrea Cogliati’s method for pitch prediction and onset detection of polyphonic piano music, as described in their paper. The process involves four main stages: training, convolutional sparse coding, post-processing, and binarization.

We compile a training set consisting of 88 individual piano notes played forte, sourced from the MAPS database a collection of piano notes recorded by Telecom ParisTech. Each note serves an entry in the scripts dictionary for the sparse coding algorithm.

Convolutional Basis Pursuit DeNoising (CBPDN) aims to approximate a polyphonic signal comparing of individual note from the dictionary to waveform of the pieces also aranged by Telecom ParisTech. We utilize SPORCO, a Python implementation of CBPDN, to solve this optimization problem efficiently. Our polyphonic piano performance signal is downsampled to 11,025Hz for alignment with the training set. The algorithm returns activation estimations for all notes. We set lambda to 0.005 and 500 as the maximum iterations, following the paper's recommendations.

Post-processing and Binarization: From the raw activation vectors, we conduct peak picking of local maxima at each timestamp to infer note onset. However, our observed local maxima were noisy. Therefore, we revised the original approach. Instead of considering the earliest local maxima in each 50ms window, we sorted all local maxima and calculated the Interquartile Range (IQR). By analyzing transcription accuracy (F-measure) across various thresholds, we determined "Q3 + 8 * IQR" as the optimal threshold. Binarization of peaks is then performed based on this threshold.

Precision, recall, and F-measure are computed for transcription evaluation. Precision measures the percentage of notes in the transcription that align with the ground truth, while recall indicates the percentage of ground truth notes overlapping with the transcription. A tolerance of 50ms is applied for both recall and precision calculations, considering the practicality of piano music onset intervals.

This implementation ensures fidelity to Cogliati's method while addressing nuances and optimizing parameters for accurate transcription and onset detection of polyphonic piano performances.
