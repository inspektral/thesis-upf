# Introduction

This work aims to extract a groove, inteded as a stream of impulses, from an audio signal. For some kind of features that are mostly associated with notation like pitch and transients this is a well studied problem, but for more timbral features this is not the case. The purpose of this work is to extract a groove from an audio signal with a system that is sensitve to timbral features and less transient like changes.
The intended final use of this system is to be used in a live performance setting, where the system can be used as an encoder form audio to groove in real time.

## Context

This work is an iteration over Bezhad Haki's performance-oriented real-time drum generation systems, that currently focus on detecting very rhythmic onsets and generate correlated drum patterns. This iteration aims to be more sensitive to less percussive features of the sound focusing on softer and subtle gestures possibly working on continuous envelopes instead of discrete onsets.

## The idea

The basic idea is to project the sound in a multidimensional space, which is supposed to represent also timbral features. A simple version of this could be the MFCC space that we plan to use as a baseline. A more interesting rapresentation would be a learned latent space, like the one of a neural encoder, preferably with sematic meaning of some sort. The project will consider some of the available models and try to adapt them to the task.

Once the sound is represented by a trajectory in the latent space the idea is to track those movements and associate onsets with big changes in direction or speed. 

![Diagram](/images/basic-overview-diagram.png)

## The plan

We will test a few different neural codecs with synthetic data for which we know the ground truth (various f(t) functions that modulate parameters). Then the sound will be encoded and we will look for matches between latent space movements and ground truth trajectories. To map the latent trajectory to the ground truth one different strategies can be used, and we will try a few of them.