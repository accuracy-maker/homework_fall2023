# Theory Analysis in Imitation Learning

## Traditional Imitation Learning: Behavior Cloning

`Behavior Cloning` refers to an agent to mimic the expert's behavior in one task. However, there are few recover actions that refers that the expert correct his/her mistake, which means that the agent will continue to make mistakes when the agent firstly execute an action not belong to the training data. Therefore, this problem will cause to distribution shift and make a bad result.

### Analysis

We train the policy under $p_{data}(O_t))$, and want to maxium $max_\theta E_{o_t\sim p_{data}(o_t)}[log\pi_\theta(a_t|o_t))]$.

But we test the policy under $P_{\pi_\theta}(O_t))$. And

$$
P_{data}(O_t) \neq P_{\pi_\theta(O_t)}
$$

We have several assumptions:

$$
c(s_t, a_t) = 
\begin{cases} 
0 & \text{if } a_t = \pi^*(s_t) \\
1 & \text{otherwise}
\end{cases}
$$

that means you will get cost 1 if you make a mistake.

Our goal is to minimize:

$$
E_{s_t\sim P_{\pi_\theta}(s_t)}[c(s_t,a_t))]
$$

And we assum that the probability of agent makes a mistake is bound by $\epsilon$ :

$$
\pi_\theta(a \neq \pi^*(s)|s) \leq \epsilon
$$

for all $s \sim P_{train}(s)$.

We can show that:

$$
E[\sum_tc(s_t,a_t)] \leq \epsilon T + (1-\epsilon)(\epsilon(T-1) + (1-\epsilon)(...))
$$

So the expression $E \sim O(\epsilon T^2)$, that means the mistakes will increase quadratically and lead to bad results.

So look at the homework1:

![analysis](hw1/docs/images/analysis.png)
