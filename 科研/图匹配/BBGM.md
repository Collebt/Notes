# BBGM



```python
@staticmethod
    def forward(ctx, weights, lambda_val, num_vertices, edges):
        ctx.weights = weights.detach().cpu().numpy() #move to CPU
        ctx.lambda_val = lambda_val #record lambda
        ctx.solver = partial(min_cost_perfect_matching, edges=edges, num_vertices=num_vertices) #define solver
        ctx.perfect_matchings = np.array(maybe_parallelize(ctx.solver, list(ctx.weights))) #output solve
        return torch.from_numpy(ctx.perfect_matchings).float().to(weights.device) #move to GPU
```

```python
@staticmethod
    def backward(ctx, grad_output):
        assert grad_output.shape == ctx.perfect_matchings.shape
        device = grad_output.device
        grad_output = grad_output.cpu().numpy() #move to cpu

        weights_prime = np.maximum(ctx.weights + ctx.lambda_val * grad_output, 0.0) #calculate perturbed weight
        better_matchings = np.array(maybe_parallelize(ctx.solver, list(weights_prime))) #solve

        gradient = -(ctx.perfect_matchings - better_matchings) / ctx.lambda_val 
        return torch.from_numpy(gradient).to(device), None # move to GPU

```

