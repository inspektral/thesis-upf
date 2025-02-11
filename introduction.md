# Introduction

This work aims to extract a groove, inteded as a stream of impulses, from an audio signal. For some kind of features that are mostly associated with notation like pitch and transients this is a well studied problem, but for more timbral features this is not the case. The purpose of this work is to extract a groove from an audio signal with a system that is sensitve to timbral features.
The intended final use of this system is to be used in a live performance setting, where the system can be used as an encoder form audio to groove in real time.

## Context

## The idea

```mermaid
graph LR
    A[Audio Input] --> B[Neural Encoder]
    A --> O[Onset Detection]
    B --> C[Latent Space]
    C --> D[Change Detection]

    O --> G[Groove Output]
    D --> G
```