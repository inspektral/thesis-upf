# Introduction

This work aims to extract a groove, inteded as a stream of impulses, from an audio signal. For some kind of features that are mostly associated with notation like pitch and transients this is a well studied problem, but for more timbral features this is not the case. The purpose of this work is to extract a groove from an audio signal with a system that is sensitve to timbral features.
The intended final use of this system is to be used in a live performance setting, where the system can be used as an encoder form audio to groove in real time.

## Context

## The idea

The basic idea is to project the sound in a multidimensional space, which is supposed to represent also timbral features. A simple version of this could be the MFCC space that we plan to use as a baseline. A more interesting rapresentation would be a learned latent space, like the one of a neural encoder, preferably with sematic meaning of some sort. The project will consider some of the available models and try to adapt them to the task.

Once the sound is represented by a trajectory in the latent space the idea is to track those movements and associate onsets with big changes in direction or speed. 

![Diagram](/images/basic-overview-diagram.png)