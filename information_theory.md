


# Information Entropy

The entropy of a set of messages `S` is calculated by the following equation

$H(S)=\sum p(s)*log_{2}(1/p(s))$ 

Where `s` is an element of `S`, meaning a message from the set with probability `p(s)`.

$i(s)=log_{2}(1/p(s))$ is called the `Self Information`.

## Example

The following is a set of probabilities of 4 messages

$p(S)={0.25, 0.25, 0.5, 0}$

$H(S)=0.25*2*log_{2}(1/0.25*2) + 0.5*1*log_{2}(1/0.5*1) + 0*1*log_{2}(1/0*1)$

$H(S)=0.5*log_{2}(4) + 0.5*log_{2}(2)$

$H(S)=1+0.5$

$H(S)=1.5$

