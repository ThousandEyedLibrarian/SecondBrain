## Information

- Paper Title: FASTER: Fully Automated Statistical Thresholding for EEG artifact Rejection
- Author(s): H. Nolan, R. Whelan, and R.B. Reilly
- Year: 2010
- Journal: [[Journal of Neuroscience Methods]]
- DOI: 10.1016/j.jneumeth.2010.07.015

### Abstract

[[Electroencephalography (EEG)]] data are typically contaminated with artifacts such as eye movements. These artifacts can be attenuated through various methods, but many existing approaches require supervision (e.g., training using canonical artifacts) and are time-consuming for high-density EEG. 

This paper introduces FASTER (Fully Automated Statistical Thresholding for EEG artifact Rejection), a method that automatically detects and removes outliers in various aspects of EEG data in both the time series and independent components. FASTER was tested on both simulated (n=47) and real (n=47) EEG data across 128-, 64-, and 32-scalp electrode arrays. 

The method showed high sensitivity and specificity for detecting contaminated channels, eye movement and EMG artifacts, linear trends and white noise compared to supervised expert detection and the Statistical Control for Dense Arrays of Sensors (SCADS) method. FASTER had >90% sensitivity and specificity for detecting most types of artifacts, and generally >60% sensitivity and specificity for contaminated epochs (vs. 0.15% for SCADS). 

The variance in the ERP baseline, a measure of noise, was significantly lower for FASTER than either supervised or SCADS methods, while ERP amplitude did not differ significantly between FASTER and supervised approaches.

### Key Points

- Developed fully automated, unsupervised method for EEG artifact detection and removal
- Uses statistical thresholding to identify outliers in multiple aspects of EEG data
- Combines independent component analysis (ICA) with statistical thresholding
- Automatically detects contaminated channels, epochs, ICs, and subject datasets
- Shows superior performance compared to existing methods across different electrode densities
- Reduces processing time and subjectivity in EEG data cleaning

### Methodology

- Artifacts are detected in five aspects of EEG data:
    1. Channels: Identifies bad channels using mean correlation, variance, and Hurst exponent
    2. Epochs: Detects contaminated epochs using amplitude range, variance, and channel deviation
    3. Independent Components: Identifies artifactual ICs using correlation with EOG channels, spatial kurtosis, spectrum slope, Hurst exponent, and median gradient
    4. Single-channel, single-epoch: Detects remaining artifacts in specific channel-epoch combinations
    5. Aggregated data: Identifies contaminated subject datasets in the grand average
- Uses Z-score of ±3 as the threshold for outlier detection across all parameters
- Contaminated channels are interpolated, contaminated epochs are removed, and artifactual ICs are subtracted
- Tested on both simulated EEG with artificially inserted artifacts and real EEG from 47 subjects
- Compared with supervised artifact detection by experts and a variant of SCADS method
- Evaluated across 128-, 64-, and 32-scalp electrode arrays to assess scalability

### Results

- Channel artifacts: FASTER showed high specificity (>96% across all array sizes) but lower sensitivity than SCADS for 128-channel arrays
- Epoch artifacts: FASTER had significantly higher detection sensitivity (>58%) compared to SCADS (0.15%) across all array sizes
- Eye movement artifacts: FASTER removed >97% of EOG artifacts across all array sizes compared to <19% for SCADS
- Muscle artifacts: Both methods showed high removal rates (>94%) with no significant differences
- Single-channel, single-epoch artifacts: FASTER showed high sensitivity for detecting linear trends and discontinuities
- Baseline variance: FASTER processed data had significantly lower baseline variance than supervised or SCADS methods
- Signal integrity: ERP amplitude was preserved or enhanced (higher amplitude for FASTER vs. supervised processing)
- Contaminated subject detection: FASTER successfully identified poor quality subject datasets, even in smaller sample sizes

### Conclusions

- FASTER provides an effective, fully automated approach to EEG artifact detection and removal
- The method works well across different electrode densities (128, 64, and 32 channels)
- Combining statistical thresholding with ICA produces better results than either approach alone
- FASTER outperforms supervised detection for some metrics, suggesting it can be more consistent than human experts
- Automated approach standardises EEG preprocessing, reducing variability in analysis methods
- Low computational requirements except for the ICA decomposition step
- Applicable to standard ERP research paradigms without requiring signal processing expertise

### Personal Notes

- The fully automated approach could significantly reduce processing time for high-density EEG datasets
- Z-score thresholds of ±3 seem to work well across different types of artifacts
- Performance decreases for channel detection with 32-electrode arrays, suggesting lower limits for electrode density
- The technique of detecting contaminated subjects in the grand average is particularly useful for large studies
- Combining ICA with statistical detection appears to be the key innovation here
- Could be especially valuable for standardising preprocessing across research groups

### Quotations

> "The advantage of testing an artifact rejection method on simulated data is that the sensitivity and specificity of the detection algorithms can be quantified."

> "Given the diversity of signal-processing methods applied to EEG data (e.g., different criteria for artifact rejection), the use of FASTER may help standardize the approach to EEG analysis."

### References to Follow Up

- Junghöfer et al. (2000) - Statistical Control of Artifacts in Dense Array Studies
- Delorme & Makeig (2004) - EEGLAB toolbox for analysis of EEG dynamics
- Bell & Sejnowski (1995) - Information-maximization approach to blind separation
- Jung et al. (2000) - Removing electroencephalographic artifacts by blind source separation

## Literature Review Sections

- Existing Artifact Rejection Methods
    - Simple amplitude thresholding approaches
    - Statistical Control for Dense Arrays of Sensors (SCADS)
    - Independent Component Analysis (ICA) based methods
    - Supervised vs. unsupervised approaches
- Challenges in Current Methods
    - Need for supervision and training with canonical artifacts
    - Time-consuming nature of artifact rejection for high-density arrays
    - Variability in results between human experts

## Research Questions

- How effective are automated methods compared to expert human processing?
- How does electrode density affect artifact detection performance?
- Can statistical thresholding effectively identify artifactual ICs without supervision?
- How robust is the method across different types of artifacts?

## Gaps in the Literature

- Limited testing of fully automated methods on different subject populations (children, older adults, clinical groups)
- Need for standardisation in EEG preprocessing approaches
- Lack of methods that combine statistical detection with ICA in an unsupervised manner
- Limited evaluation of artifact removal methods' impact on actual ERP parameters beyond simple signal-to-noise metrics

## Synthesis

The FASTER method addresses a critical need in EEG research by providing a fully automated approach to artifact rejection. By combining statistical thresholding with ICA, it achieves superior performance to existing methods while requiring no human supervision. This approach could help standardise EEG preprocessing across research groups and significantly reduce processing time for high-density arrays. The comprehensive evaluation across different electrode densities and artifact types demonstrates its robustness and practical utility.

## Ideas for Future Research

- Evaluate FASTER on special populations (clinical groups, children, older adults)
- Test performance on other ERP paradigms with smaller signal amplitudes (e.g., MMN)
- Investigate modifications for very low-density arrays (<32 channels)
- Develop optimisations to reduce ICA decomposition time
- Integrate FASTER with real-time EEG processing systems
- Explore additional artifact types not currently addressed


See also:
- x