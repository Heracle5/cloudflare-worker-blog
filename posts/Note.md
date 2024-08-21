# Note

> I will paste some important stuff from the paper I read into this article.

## Contrastive estimators for \( I(X_1; X_2) \)
> Source: https://arxiv.org/pdf/2306.05268

**Theorem .** (Contrastive estimators for \( I(X_1; X_2) \)) Defining the NCE estimator and NCE-CLUB estimator as follows,

\[
I_{\text{NCE}}(X_1; X_2) = \mathbb{E}_{x_1,x_2^+ \sim p(x_1,x_2)} \mathbb{E}_{x_2^- \sim p(x_2)} \left[ \log \frac{\exp f(x_1, x_2^+)}{\sum_k \exp f(x_1, x_2^-)} \right]
\tag{53}
\]

\[
I_{\text{NCE-CLUB}}(X_1; X_2) = \mathbb{E}_{x_1,x_2^+ \sim p(x_1,x_2)} \left[ f^*(x_1, x_2^+) \right] - \mathbb{E}_{x_1 \sim p(x_1)}\mathbb{E}_{x_2^- \sim p(x_2)} \left[ f^*(x_1, x_2^-) \right]
\tag{54}
\]

where \( f^*(x_1, x_2) \) is the optimal critic from \( I_{\text{NCE}} \) plugged into the \( I_{\text{CLUB}} \) objective \[16\]. We call the proposed plug-in objective Eq.(\[11\]) NCE-CLUB, and obtain lower and upper bounds on \( I(X_1; X_2) \):

\[
I_{\text{NCE}}(X_1; X_2) \leq I(X_1; X_2) \leq I_{\text{NCE-CLUB}}(X_1; X_2)
\tag{55}
\]

**Proof.** The lower bound \( I_{\text{NCE}}(X_1; X_2) \leq I(X_1; X_2) \) follows from Oord et al. \[57\]: optimizing the objective leads to an optimal critic \( f^* = \log p(x_2|x_1) + c(x_2) \) \[59\] or without loss of generality \( f^* = \log p(x_1|x_2) + c(x_1) \), where \( c(\cdot) \) is an arbitrary deterministic function. Plugging the optimal critic into the \( I_{\text{NCE}}(X_1; X_2) \) gives the result: \( I_{\text{NCE}}(X_1; X_2) + \log N \leq I(X_1; X_2) \) \[57, 59\].

Next, the original \( I_{\text{CLUB}}(X_1; X_2) \) \[16\] is defined as:

\[
I_{\text{CLUB}}(X_1; X_2) := \mathbb{E}_{p(x_1,x_2)} \left[ \log p(x_2|x_1) \right] - \mathbb{E}_{p(x_1)p(x_2)} \left[ \log p(x_2|x_1) \right].
\tag{56}
\]

As mutual information is symmetric w.r.t \( x_1 \) and \( x_2 \): \( I(X_1; X_2) = I(X_2; X_1) \), without loss of generality, we have:

\[
I_{\text{CLUB}}(X_1; X_2) = I_{\text{CLUB}}(X_2; X_1) = \mathbb{E}_{p(x_1,x_2)} \left[ \log p(x_1|x_2) \right] - \mathbb{E}_{p(x_1)p(x_2)} \left[ \log p(x_1|x_2) \right].
\tag{57}
\]

The formulation above assumes \( p(x_1|x_2) \) is known, which is satisfied when we use the optimal critic \( f^* = \log p(x_1|x_2) + c(x_1) \) from \( I_{\text{NCE}}(X_1; X_2) \). Plugging the optimal critic \( f^* \) into \( I_{\text{CLUB}}(X_1; X_2) \), we obtain a desired upper bound \( I_{\text{NCE-CLUB}}(X_1; X_2) \) of \( I(X_1; X_2) \):

\[
I_{\text{NCE-CLUB}}(X_1; X_2) = \mathbb{E}_{p(x_1,x_2)} \left[ \log p(x_1|x_2) + c(x_1) \right] - \mathbb{E}_{p(x_1)p(x_2)} \left[ \log p(x_1|x_2) + c(x_1) \right]
\tag{58}
\]

\[
= \mathbb{E}_{p(x_1,x_2)} \left[ \log p(x_1|x_2) \right] + \mathbb{E}_{p(x_1,x_2)} \left[ c(x_1) \right] - \mathbb{E}_{p(x_1)p(x_2)} \left[ \log p(x_1|x_2) \right] - \mathbb{E}_{p(x_1)p(x_2)} \left[ c(x_1) \right]
\tag{59}
\]

\[
= \mathbb{E}_{p(x_1,x_2)} \left[ \log p(x_1|x_2) \right] - \mathbb{E}_{p(x_1)p(x_2)} \left[ \log p(x_1|x_2) \right]
\tag{60}
\]

\[
\geq I(X_1; X_2).
\tag{61}
\]

Eq.(\[59\]) is from the linearity of expectation, Eq.(\[60\]) is from the fact that \( c(x_1) \) is not a function of \( x_2 \) and therefore \( \mathbb{E}_{p(x_1,x_2)} [c(x_1)] = \mathbb{E}_{p(x_1)p(x_2)} [c(x_1)] = \mathbb{E}_{p(x_1)} [c(x_1)] \), and Eq.(\[61\]) is directly from the original \( I_{\text{CLUB}}(X_1; X_2) \) paper \[16\].

--- 

Let me know if you need further assistance!
