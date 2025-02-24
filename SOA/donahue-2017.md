# Donahue (2017) - Dance Dance Convolution

## Summary

The paper present a model based on Dance Dance Revolution, a popular video game, to generate music. The model is an CNN + RNN + LSTM that based on sound generates a choreography. This approach is based on onset detection, and this is the aspect that is most relevant to us. The dataset available for the game is 100k songs, and this is the secret ingredient of the model. On the side the issue is that the music doesn't span across all possible genres and styles and not all the onsets are also steps in the game.

## What's good
- Good onset detection
- More transienty sounds are very well detected
- Since it's old, it is quite fast and not too computationally expensive

## What's bad
- frame based onset detection, 10ms
- 40ms window for onset detection accepted error


## Reference

Donahue, Chris, Zachary C. Lipton, and Julian McAuley. “Dance Dance Convolution.” arXiv, June 21, 2017. https://doi.org/10.48550/arXiv.1703.06891.
