# AP-16: sixteen primes in arithmetic progression, 61 digits

```
(289822162743 + 153276754·n)·127# + 1,   n = 0, 1, ..., 15
```

Sixteen primes in arithmetic progression, each with 61 digits. Here 127# is the product of all primes up to 127
(the primorial). The common difference is 153276754·127#.

- **Found:** 27 November 2026
- **Discoverer:** Arnav Garg ([arnavgarg.in](https://arnavgarg.in))
- **Proof:** all sixteen terms are proven prime. Each has an ECPP certificate in the format of [CM](https://www.multiprecision.org/cm/) by
  Andreas Enge, checked with its `ecpp-check` verifier, and an N−1 certificate.
- The terms for n = −1 and n = 16 are composite, so the progression has exactly sixteen terms.

On 27 November 2026, the largest AP-16 on Norman Luhn's
[list of records for primes in arithmetic progression](https://www.pzktupel.de/PAP/aprecords.php) (page updated 14 November 2026) was
a 60-digit AP-16 (Norman Luhn, 9 January 2026).

## Acknowledgements

Special thanks to **[Dr. Anirudh Singh Rana](https://www.bits-pilani.ac.in/pilani/anirudh-singh-rana/)** (Department of Mathematics, Birla Institute of Technology and Science, Pilani Campus, Pilani, Rajasthan, India, 333031), who made this possible by arranging computing time on **Sharanga**, the high-performance computing facility of the Birla Institute of Technology and Science, Pilani, Hyderabad Campus ([sharanga.hpc.bits-hyderabad.ac.in](https://sharanga.hpc.bits-hyderabad.ac.in/)). The search ran on one NVIDIA A100 GPU there, and the sixteen proofs on the same node.

I gratefully acknowledge the computing time provided on the high performance computing facility, Sharanga, at the Birla Institute of Technology and Science - Pilani, Hyderabad Campus.

## The terms

| n | term |
|---|---|
| 0 | 1163484388839399752272037658980770506688647427428906931323391 |
| 1 | 1164099714833668574984066585127201086848649995167135471591811 |
| 2 | 1164715040827937397696095511273631667008652562905364011860231 |
| 3 | 1165330366822206220408124437420062247168655130643592552128651 |
| 4 | 1165945692816475043120153363566492827328657698381821092397071 |
| 5 | 1166561018810743865832182289712923407488660266120049632665491 |
| 6 | 1167176344805012688544211215859353987648662833858278172933911 |
| 7 | 1167791670799281511256240142005784567808665401596506713202331 |
| 8 | 1168406996793550333968269068152215147968667969334735253470751 |
| 9 | 1169022322787819156680297994298645728128670537072963793739171 |
| 10 | 1169637648782087979392326920445076308288673104811192334007591 |
| 11 | 1170252974776356802104355846591506888448675672549420874276011 |
| 12 | 1170868300770625624816384772737937468608678240287649414544431 |
| 13 | 1171483626764894447528413698884368048768680808025877954812851 |
| 14 | 1172098952759163270240442625030798628928683375764106495081271 |
| 15 | 1172714278753432092952471551177229209088685943502335035349691 |

The same list is in [`terms.txt`](terms.txt).

## Files

| file | what it is |
|---|---|
| `terms.txt` | all sixteen terms in decimal |
| `certificates/t<n>.ecpp.cert` | ECPP certificate of term n (CM format) |
| `certificates/t<n>.nminus1.txt` | N−1 certificate of term n: N, the factored part of N−1 and the witnesses |
| `certificates.zip` | the same 32 certificate files in one archive |
| `record.json` | the numbers above, for scripts |

## Checking it yourself

Probable-prime check of all terms, and that they form the progression (Python with gmpy2):

```python
import gmpy2
a, d, p = 289822162743, 153276754, gmpy2.primorial(127)
terms = [(a + d * n) * p + 1 for n in range(16)]
assert all(gmpy2.is_prime(t) for t in terms)
assert all(len(str(t)) == 61 for t in terms)
assert not gmpy2.is_prime((a - d) * p + 1) and not gmpy2.is_prime((a + 16 * d) * p + 1)
print("16 terms, 61 digits each, probable primes")
```

Proofs, with CM installed:

```
for n in $(seq 0 15); do ecpp-check -f certificates/t$n.ecpp.cert; done
```

Each run should print that the file contains a valid ECPP certificate in the CM format. The first number in each
certificate is the term it proves.
