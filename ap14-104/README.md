# AP-14: fourteen primes in arithmetic progression, 104 digits

```
(541343583659 + 2878343921·n)·229# + 1,   n = 0, 1, ..., 13
```

Fourteen primes in arithmetic progression, each with 104 digits. Here 229# is the product of all primes up to 229
(the primorial). The common difference is 2878343921·229#.

- **Found:** 14 November 2026
- **Discoverer:** Arnav Garg ([arnavgarg.in](https://arnavgarg.in))
- **Proof:** all fourteen terms are proven prime. Each has an ECPP certificate in the format of [CM](https://www.multiprecision.org/cm/) by
  Andreas Enge, checked with its `ecpp-check` verifier, and an N−1 certificate.
- The terms for n = −1 and n = 14 are composite, so the progression has exactly fourteen terms.

On 14 November 2026, the largest AP-14 on Norman Luhn's
[list of records for primes in arithmetic progression](https://www.pzktupel.de/PAP/aprecords.php) (page updated 10 November 2026) was
a 103-digit AP-14 (Norman Luhn, 27 December 2019).

## The terms

| n | term |
|---|---|
| 0 | 10327897368008186014735330367918260811378659486761790970966442462455134787679568124071243371820599555211 |
| 1 | 10382811181533024747294725885555314935854178806131801032675287575874859351418886750300557818954395440201 |
| 2 | 10437724995057863479854121403192369060329698125501811094384132689294583915158205376529872266088191325191 |
| 3 | 10492638808582702212413516920829423184805217444871821156092977802714308478897524002759186713221987210181 |
| 4 | 10547552622107540944972912438466477309280736764241831217801822916134033042636842628988501160355783095171 |
| 5 | 10602466435632379677532307956103531433756256083611841279510668029553757606376161255217815607489578980161 |
| 6 | 10657380249157218410091703473740585558231775402981851341219513142973482170115479881447130054623374865151 |
| 7 | 10712294062682057142651098991377639682707294722351861402928358256393206733854798507676444501757170750141 |
| 8 | 10767207876206895875210494509014693807182814041721871464637203369812931297594117133905758948890966635131 |
| 9 | 10822121689731734607769890026651747931658333361091881526346048483232655861333435760135073396024762520121 |
| 10 | 10877035503256573340329285544288802056133852680461891588054893596652380425072754386364387843158558405111 |
| 11 | 10931949316781412072888681061925856180609371999831901649763738710072104988812073012593702290292354290101 |
| 12 | 10986863130306250805448076579562910305084891319201911711472583823491829552551391638823016737426150175091 |
| 13 | 11041776943831089538007472097199964429560410638571921773181428936911554116290710265052331184559946060081 |

The same list is in [`terms.txt`](terms.txt).

## Files

| file | what it is |
|---|---|
| `terms.txt` | all fourteen terms in decimal |
| `certificates/t<n>.ecpp.cert` | ECPP certificate of term n (CM format) |
| `certificates/t<n>.nminus1.txt` | N−1 certificate of term n: N, the factored part of N−1 and the witnesses |
| `certificates.zip` | the same 28 certificate files in one archive |
| `record.json` | the numbers above, for scripts |

## Checking it yourself

Probable-prime check of all terms, and that they form the progression (Python with gmpy2):

```python
import gmpy2
a, d, p = 541343583659, 2878343921, gmpy2.primorial(229)
terms = [(a + d * n) * p + 1 for n in range(14)]
assert all(gmpy2.is_prime(t) for t in terms)
assert all(len(str(t)) == 104 for t in terms)
assert not gmpy2.is_prime((a - d) * p + 1) and not gmpy2.is_prime((a + 14 * d) * p + 1)
print("14 terms, 104 digits each, probable primes")
```

Proofs, with CM installed:

```
for n in $(seq 0 13); do ecpp-check -f certificates/t$n.ecpp.cert; done
```

Each run should print that the file contains a valid ECPP certificate in the CM format. The first number in each
certificate is the term it proves.
