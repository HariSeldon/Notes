Preliminary info to remember:

sigmoid = 1 / (1 + e-x)  ->  sigmoid(-inf) = 0, sigmoid (inf) = 1 

tanh(-inf) = -1, tanh(inf) = 1

First, decide how to update the cell state.

1. Decide what to forget (remove from the cell state) and what to remember (add to the cell state).

```
forget_t = sigma(Weights_forget * [h_t-1, x_t] + bias_f)

// Decide what elements we are going to remember.
i_t = sigma(W_i * [h_t-1, x_t] + b_i)

// Decide what values we are going to remember.
candidate_cell_state_t = tanh(Weights_c * [h_t-1, x_t] + bias_c) 

// This is the value of the new state if we where to forget everything from the past and replace all the memory with the information gathered in the current state.
to_remember_t = i_t * candidate_cell_state_t

// Update the cell state.
cell_state_t = forget_t * cell_state_t-1 + to_remember_t 
```

2. Decide what we are going to output.

```
output_t = sigma(Weights_output * [h_t-1, x_t] + bias_output)

// The next hidden state is the current output modulated by the cell state.
hidden_t = output_t * tanh(cell_state_t) 
```

Notice that the cell state does not influence the output at the same time step, but it influences the next hidden state.

References:

[1] http://colah.github.io/posts/2015-08-Understanding-LSTMs/
