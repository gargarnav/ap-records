# AP-18: eighteen primes in arithmetic progression, 41 digits

```
(301916538450 + 1029495088·n)·73# + 1,   n = 0, 1, ..., 17
```

Eighteen primes in arithmetic progression, each with 41 digits. Here 73# is the product of all primes up to 73
(the primorial). The common difference is 1029495088·73#.

- **Found:** 28 November 2026
- **Discoverer:** Arnav Garg ([arnavgarg.in](https://arnavgarg.in))
- **Proof:** all eighteen terms are proven prime. Each has an ECPP certificate in the format of [CM](https://www.multiprecision.org/cm/) by
  Andreas Enge, checked with its `ecpp-check` verifier, and an N−1 certificate.
- The terms for n = −1 and n = 18 are composite, so the progression has exactly eighteen terms.

On 28 November 2026, the largest AP-18 on Norman Luhn's
[list of records for primes in arithmetic progression](https://www.pzktupel.de/PAP/aprecords.php) (page updated 27 November 2026) was
a 40-digit AP-18 (Norman Luhn, 24 January 2026).

## Acknowledgements

Special thanks to **[Dr. Anirudh Singh Rana](https://www.bits-pilani.ac.in/pilani/anirudh-singh-rana/)** (Department of Mathematics, Birla Institute of Technology and Science, Pilani Campus, Pilani, Rajasthan, India, 333031), who made this possible by arranging computing time on **Sharanga**, the high-performance computing facility of the Birla Institute of Technology and Science, Pilani, Hyderabad Campus ([sharanga.hpc.bits-hyderabad.ac.in](https://sharanga.hpc.bits-hyderabad.ac.in/)). The search ran on one NVIDIA A100 GPU there, and the eighteen proofs on the same node.

I gratefully acknowledge the computing time provided on the high performance computing facility, Sharanga, at the Birla Institute of Technology and Science - Pilani, Hyderabad Campus.

## The terms

| n | term |
|---|---|
| 0 | 12296964178699387041096041398820142421501 |
| 1 | 12338895184812122807947899423480566536861 |
| 2 | 12380826190924858574799757448140990652221 |
| 3 | 12422757197037594341651615472801414767581 |
| 4 | 12464688203150330108503473497461838882941 |
| 5 | 12506619209263065875355331522122262998301 |
| 6 | 12548550215375801642207189546782687113661 |
| 7 | 12590481221488537409059047571443111229021 |
| 8 | 12632412227601273175910905596103535344381 |
| 9 | 12674343233714008942762763620763959459741 |
| 10 | 12716274239826744709614621645424383575101 |
| 11 | 12758205245939480476466479670084807690461 |
| 12 | 12800136252052216243318337694745231805821 |
| 13 | 12842067258164952010170195719405655921181 |
| 14 | 12883998264277687777022053744066080036541 |
| 15 | 12925929270390423543873911768726504151901 |
| 16 | 12967860276503159310725769793386928267261 |
| 17 | 13009791282615895077577627818047352382621 |

The same list is in [`terms.txt`](terms.txt).

## Files

| file | what it is |
|---|---|
| `terms.txt` | all eighteen terms in decimal |
| `certificates/t<n>.ecpp.cert` | ECPP certificate of term n (CM format) |
| `certificates/t<n>.nminus1.txt` | N−1 certificate of term n: N, the factored part of N−1 and the witnesses |
| `certificates.zip` | the same 36 certificate files in one archive |
| `record.json` | the numbers above, for scripts |

## Checking it yourself

Probable-prime check of all terms, and that they form the progression (Python with gmpy2):

```python
import gmpy2
a, d, p = 301916538450, 1029495088, gmpy2.primorial(73)
terms = [(a + d * n) * p + 1 for n in range(18)]
assert all(gmpy2.is_prime(t) for t in terms)
assert all(len(str(t)) == 41 for t in terms)
assert not gmpy2.is_prime((a - d) * p + 1) and not gmpy2.is_prime((a + 18 * d) * p + 1)
print("18 terms, 41 digits each, probable primes")
```

Proofs, with CM installed:

```
for n in $(seq 0 17); do ecpp-check -f certificates/t$n.ecpp.cert; done
```

Each run should print that the file contains a valid ECPP certificate in the CM format. The first number in each
certificate is the term it proves.
