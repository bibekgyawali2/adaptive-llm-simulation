# LLM Request Routing Simulator

Live demo: https://bibekgyawali2.github.io/adaptive-llm-simulation/

An interactive simulation for the paper *When Is Prediction Worth Its Cost? Adaptive
Request Routing for Large Language Model Inference*. Five routers handle the same
stream of LLM requests on a simulated GPU cluster:

| Router | How it picks a GPU |
|---|---|
| LC | Fewest requests in progress |
| WLC | Fewest requests per unit of GPU speed |
| ECT | Shortest finish time from a formula |
| Always-predictive | Asks a latency model for every request |
| Adaptive | Uses WLC; asks the model only when the expected gain is larger than the delay it causes |

Four scenarios from the paper are built in: mixed GPUs, high load, GPU slowdown and a
slow predictor. You can also change the load, the time per prediction, the GPUs, and
slow down two GPUs while it runs.

## What is simulated

- GPU step times fitted to the Vidur simulator for Llama-2-7B (A100, H100, A40)
- Continuous batching: up to 128 requests and 4096 prompt tokens per step, KV memory limit
- Real prompt and output lengths sampled from the Azure LLM inference trace (2023)
- Deadlines of 2 s plus 5 times the ideal service time
- One router that handles requests in order, with monitoring data that is 0.5 s old

The trained prediction model from the paper is replaced by a simple stand-in that knows
each GPU's speed and slowdown. Numbers come from one live run in the browser, so they
differ from the paper's results over 20 runs.

## Run locally

Open `index.html` in a browser. It is a single file with no build step.
