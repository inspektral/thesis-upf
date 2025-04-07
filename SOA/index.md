# State of the Art

This chapter illustrates the current state of the art of the various topics pertinent to the work. It is divided into two groups of sections. The first group reviews the concept of groove from a more theoretical point of view, covering the psychoacoustic and cognitive aspects ([Groove](#groove)) and proceeds to go over past and current technical approaches for onset detection ([Onset Detection](#onset-detection)), which is the most relevant MIR topic related to groove. 

The second group is an overview of the idea of sonic trajectories ([Trajectories](#trajectories)), which is one of the scopes used for music analysis, especially for the more experimental genres where most of the structures are built on timbral aspects of sound, and proceeds presenting various more technical representations and algorithms ([Representations](#representations)) used to analyze sound and music, especially from a timbral perspective, that can be useful for a trajectory-based interpretation of sound.

## Groove

In the musicology discourse, groove is an important concept, yet elusive and multifaceted, depending on genres, eras, and contexts. It is closely related to the idea of rhythm, musical gesture, dance, immersion, and is deeply correlated with motor areas of the brain, as explained by Etani [@etani]. 

Defining groove is not a simple task. Several definitions have been proposed. An interesting general one that should be taken into account was proposed by Duman et al. in 2024 [@duman_groove_2024]:

> “Groove is a participatory experience (related to immersion, movement, positive affect, and social connection) resulting from subtle interaction of specific music- (such as time- and pitch-related features), performance-, and/or individual-related factors.”

It is thus clear that groove is an incredibly wide term. For our purposes, it has been narrowed down to computable rhythmic audio features, in the literature [@stupacher_audio_2016] mainly related to percussive elements and more generally events that provide a perceptual quantization of time. In the field of MIR, those events are mainly treated with various onset detection techniques.

## Onset Detection

Onset detection refers to the process of locating the beginning of a musical note or sound, often associated with the transient phase where the signal exhibits rapid changes. It is essential for applications such as automatic music transcription, beat tracking, and synchronization in music production. The task is particularly challenging in polyphonic music, where multiple instruments play simultaneously, leading to overlapping signals.

### Traditional Approaches

Traditional digital signal processing methods for onset detection rely on analyzing various signal properties to detect abrupt changes indicative of onsets [@muller_fundamentals_2015]. These can be categorized into several sub-approaches depending on the audio representation used:

#### Time Domain

A common technique is energy-based detection, where the signal's energy is calculated over short windows, and onsets are identified when energy exceeds a predefined threshold [@muller_fundamentals_2015]. For example, detecting sudden increases in amplitude is straightforward but can lead to false positives in noisy or amplitude-modulated signals.

#### Frequency Domain

These involve the transformation of the signal into the frequency domain using techniques such as the Fast Fourier Transform (FFT). Metrics such as spectral flux [@muller_fundamentals_2015], which measures the rate of change in spectral energy between consecutive frames, are widely used. Other metrics include spectral centroid, which tracks the center of mass of the spectrum and can highlight frequency shifts at onsets. 

These methods are more robust than time-domain approaches but require more computational resources due to FFT processing. **Superflux** is in this category of onset detection algorithms and is the most widely used, as it is the standard go-to for Librosa and Essentia, the most widespread MIR toolkits. Other advanced methods in this category also take into account phase changes of the components, detecting onsets when simultaneous changes in phase occur.

### Deep Learning Approaches

Deep learning methods, particularly Convolutional Neural Networks (CNNs), have gained prominence in onset detection by leveraging neural networks to learn patterns directly from data, often represented as spectrograms or other transforms (wavelet, CQT). They learn spatial patterns that correspond to onsets, such as sudden changes in frequency content.

A notable early example is the work by Schlüter and Böck [@schulter], which showed CNNs outperforming traditional methods on a dataset with 26,000 annotated onsets. RNNs, particularly LSTMs, are also able to outperform traditional methods, as shown by Marchi et al. [@Marchi]. 

Nowadays, most advanced models use a combination of the two, as shown by one of the most advanced models for polyphonic strings onset detection developed in 2023 [@tomczak_onset_2023].

Although these models outperform traditional methods, the costs to develop them are very high, both from a computational and data sourcing point of view. Running them is also expensive; GPU acceleration might be needed and not all of them can run in real time on a common laptop.

In the vast panorama of onset detection models, **Dance Dance Convolution** is the one used as of today by the system. It is based on a convolutional architecture trained on Dance Dance Revolution annotations and shows outstanding real-time performance for transient-like onset detection. This is ideal for detecting percussive sounds but falls short when onsets are softer or happen in the pitch or timbre domain.

## Trajectories

Sound gestures and trajectories in sound art and electroacoustic music refer to how sounds move and evolve, capturing both performer actions and spatial dynamics. Smalley's *spectromorphology* [@SMALLEY_1997], introduced in 1986, describes the temporal shaping of sound spectra, providing a tool to analyze these aspects.

While Smalley describes them from an analytical point of view, composers have been using similar concepts, representing them with graphic notation. This notation uses visual symbols to represent music, offering flexibility beyond traditional notation. Xenakis's **UPIC** system translates drawings into sound, while Cardew's *Treatise* (1967) leaves interpretation open, both influencing sound gestures.

MIR techniques model and generate music by computational representations that collide with the ones used by musicologists and composers. Though direct research is sparse, the integration of those representations could lead to interesting results.

## Representations

Sound representations are methods used to transform raw audio signals into structured formats that emphasize specific characteristics, making it easier to analyze, process, or interpret the audio data. They are essential in fields like audio processing, speech recognition, music analysis, and machine learning for audio-related tasks. Each representation highlights different aspects of sound—such as amplitude, frequency, or abstract features—depending on the intended application.

### Traditional Representations

Traditional representations focus on decomposing audio signals into interpretable components, often based on frequency or perceptual scales.

#### Fourier Transform

The Fourier Transform decomposes a signal into its frequency components. For audio, the Short-Time Fourier Transform (STFT) is commonly used to capture how these frequencies evolve over time [@muller_fundamentals_2015]. It divides the audio into short segments and computes the Fourier Transform for each, resulting in a time-frequency representation.

#### Constant Q Transform

The Constant Q Transform is a time-frequency representation where each frequency bin has a constant Q factor, meaning the bandwidth is proportional to the frequency. This results in a logarithmic frequency scale, aligning with human perception of pitch. Unlike STFT, which uses linear frequency spacing, CQT uses logarithmic spacing [@CONSTANTQTT].

#### Nonnegative Matrix Factorization (NMF)

NMF is a matrix decomposition technique that factors a non-negative matrix (e.g., a spectrogram) into two non-negative matrices: a dictionary matrix (basis spectra) and an activation matrix (how these bases are activated over time). This representation is widely used in the MIR field, especially for source separation.

### Latent Spaces

Latent space representations leverage machine learning, particularly neural networks, to create abstract, high-level representations of data [@mikolov2013efficientestimationwordrepresentations]. These are often used for tasks requiring similarity measurements, semantic understanding, generation, or compression.

#### CLAP and Semantics

Using contrastive learning, it is possible to map audio clips and textual descriptions into a shared embedding space. This allows related concepts, like the sound of rain and the phrase "rain falling", to be close together. 

CLAP [@clap] is the most widespread model trained this way and enables tasks like:
- Text-to-audio retrieval
- Audio-to-text annotation
- Zero-shot classification

While it builds semantically rich embeddings, it requires long samples and lacks frame-level temporal resolution.

#### RAVE and Live Use

Some models focus on real-time audio synthesis and manipulation via latent spaces. They usually leverage variational autoencoders (VAEs), which compress and reconstruct audio. A known example is **RAVE** [@rave], which is optimized for live performance. It enables sound generation, morphing, and style transfer with low latency, making it ideal for music production and interactive applications.

#### SoundStream and Compression

Neural codecs like **SoundStream** [@soundstream] use latent spaces for efficient compression and high-quality reconstruction. It's trained end-to-end to balance compression and perceptual quality. SoundStream supports real-time encoding/decoding and variable bitrates, making it suitable for streaming applications, though its latent space is optimized for compression rather than interpretability.
