
Fastest:

cov_EmpiricalCovariance (Covariance Measure)
Estimated time: 1 second
Reason: Simple, single-pass calculation.
xcorr_mean_sig-False (Cross-Correlation)
Estimated time: 2-3 seconds

Reason: Slightly more complex than covariance, but still efficient.
mi_gaussian (Mutual Information - Gaussian)
Estimated time: 3-5 seconds

Reason: Involves more calculations than simple correlation, but still has closed-form solution.
cohmag_multitaper_max_fs-1_fmin-0_fmax-0-25 (Spectral Coherence)
Estimated time: 5-10 seconds

Reason: Requires Fourier transforms and additional computations.
pec (Power Envelope Correlation)
Estimated time: 10-15 seconds
Reason: Involves envelope extraction before correlation.



Part 1 (Top of dendrogram):

1. Phase-based Multitaper Spectral Measures
Most efficient: phase_multitaper_mean_fs-1_fmin-0_fmax-0-5
Explanation: Uses mean over full frequency range, generally more efficient than other operations.

2. Causal Inference Measures
Most efficient: anm (Additive Noise Model)
Explanation: Simplest method in the group, requiring less computation.

3. Information Theoretic Measures
Most efficient: di_gaussian (Gaussian Directed Information)
Explanation: Gaussian-based methods often have efficient analytical properties.

4. Transfer Entropy Estimators
Most efficient: te_kraskov_NN-4_k-1_kt-1_l-1_lt-1
Explanation: Simplest parameter set, suggesting fewer computational steps.

5. Granger Causality and Integrated Information Measures
Most efficient: gc_gaussian_k-1_kt-1_l-1_lt-1
Explanation: Gaussian measure with minimal parameters, likely most straightforward to compute.

6. Spectral Granger Causality (SGC) Parametric Estimators
Most efficient: sgc_parametric_mean_fs-1_fmin-0_fmax-0-5_order-None
Explanation: Mean over full frequency range without specified order suggests lower computational complexity.

Part 2 (Middle of dendrogram):

7. Phase Lag Index (PLI) Group
Most efficient: pli_multitaper_max_fs-1_fmin-0_fmax-0-25
Explanation: PLI is generally faster than weighted or debiased versions.

8. Phase Slope Index (PSI) Group
Most efficient: psi_wavelet_max_fs-1_fmin-0_fmax-0-25_max
Explanation: Max operation and smaller frequency range are quicker to compute.

9. Barycenter Group
Most efficient: bary_dtw_mean
Explanation: Standard DTW is typically faster than soft or subgradient versions.

10. Phase Locking Value (PLV) and Phase Group
Most efficient: plv_multitaper_mean_fs-1_fmin-0_fmax-0-25
Explanation: PLV is generally simpler to compute than phase measures.

11. Time Series Distance Measures Group
Most efficient: lcss (Longest Common Subsequence)
Explanation: LCSS is generally faster than DTW or constrained versions.

12. Power Envelope Correlation (PEC) Group
Most efficient: pec
Explanation: Basic PEC without additional transformations is likely the quickest.

Part 3 (Bottom of dendrogram):

13. Spectral Coherence Measures
Most efficient: cohmag_multitaper_max_fs-1_fmin-0_fmax-0-25
Explanation: Coherence magnitude is simpler to compute than phase-based measures.

14. Cointegration Measures
Most efficient: coint_johansen_trace_stat_order-0_ardiff-1
Explanation: Uses simplest order and difference parameters, likely requiring less computation.

15. Cross-Correlation and Covariance Measures
Most efficient: xcorr_mean_sig-False
Explanation: Cross-correlation without significance testing is typically faster.

16. Precision and Covariance Measures
Most efficient: cov_EmpiricalCovariance
Explanation: Straightforward, single-pass calculation, likely faster than complex estimators.

17. Gaussian and Information Theory Measures
Most efficient: mi_gaussian
Explanation: Can be computed efficiently using closed-form expressions.

18. Time Series, Cross-Mapping, and Distance-based Measures
Most efficient: dcorr (distance correlation)
Explanation: Generally faster to compute than cross-mapping or sophisticated information-theoretic measures.

If we only had to calculate 10, I would recommend the following:

phase_multitaper_mean_fs-1_fmin-0_fmax-0-5 (Phase-based Multitaper Spectral Measures)
anm (Additive Noise Model - Causal Inference)
di_gaussian (Gaussian Directed Information - Information Theoretic)
te_kraskov_NN-4_k-1_kt-1_l-1_lt-1 (Transfer Entropy)
gc_gaussian_k-1_kt-1_l-1_lt-1 (Granger Causality)
pli_multitaper_max_fs-1_fmin-0_fmax-0-25 (Phase Lag Index)
bary_dtw_mean (Barycenter - Time Series Distance)
pec (Power Envelope Correlation)
cohmag_multitaper_max_fs-1_fmin-0_fmax-0-25 (Spectral Coherence)
cov_EmpiricalCovariance (Covariance Measure)


Standardization: The authors mention that prior to evaluating each statistic, they standardize (z-score) the multivariate time series along the time axis.
Length constraints: Time series lengths (T) were chosen to be greater than 100 samples and less than 2000 samples.
Number of processes: The number of processes (M) in each multivariate time series was chosen to be between 5 and 40.
Dimensionality check: The authors discarded any multivariate time series that requires less than three principal components to explain 95% of the variance, to ensure sufficient complexity and non-trivial dynamics.
Sampling frequency normalization: For spectral methods, the authors consider the time step between successive measurements to be rescaled by a timescale appropriate for the process of interest, yielding a dimensionless time step. They assume a sampling frequency fs = 1 throughout.
Frequency range selection: For spectral methods, they use 125 uniformly sampled bins across the entire frequency range, with specific ranges defined for different analyses.








