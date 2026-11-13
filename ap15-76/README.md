# AP-15: fifteen primes in arithmetic progression, 76 digits

```
(198301127768 + 848309427·n)·163# + 1,   n = 0, 1, ..., 14
```

Fifteen primes in arithmetic progression, each with 76 digits. Here 163# is the product of all primes up to 163
(the primorial). The common difference is 848309427·163#.

- **Found:** 13 November 2026
- **Discoverer:** Arnav Garg ([arnavgarg.in](https://arnavgarg.in))
- **Proof:** all fifteen terms are proven prime. Each has an ECPP certificate in the format of [CM](https://www.multiprecision.org/cm/) by
  Andreas Enge, checked with its `ecpp-check` verifier, and an N−1 certificate.
- The terms for n = −1 and n = 15 are composite, so the progression has exactly fifteen terms.

On 13 November 2026, the largest AP-15 on Norman Luhn's
[list of records for primes in arithmetic progression](https://www.pzktupel.de/PAP/aprecords.php) (page updated 10 November 2026) was
a 75-digit AP-15 (Norman Luhn, 23 December 2025).

## The terms

| n | term |
|---|---|
| 0 | 1143434488103188031823436429768353123953430296924683463249659856462009716081 |
| 1 | 1148325969388910609329082464743089109799427820176997204427180956916693387951 |
| 2 | 1153217450674633186834728499717825095645425343429310945604702057371377059821 |
| 3 | 1158108931960355764340374534692561081491422866681624686782223157826060731691 |
| 4 | 1163000413246078341846020569667297067337420389933938427959744258280744403561 |
| 5 | 1167891894531800919351666604642033053183417913186252169137265358735428075431 |
| 6 | 1172783375817523496857312639616769039029415436438565910314786459190111747301 |
| 7 | 1177674857103246074362958674591505024875412959690879651492307559644795419171 |
| 8 | 1182566338388968651868604709566241010721410482943193392669828660099479091041 |
| 9 | 1187457819674691229374250744540976996567408006195507133847349760554162762911 |
| 10 | 1192349300960413806879896779515712982413405529447820875024870861008846434781 |
| 11 | 1197240782246136384385542814490448968259403052700134616202391961463530106651 |
| 12 | 1202132263531858961891188849465184954105400575952448357379913061918213778521 |
| 13 | 1207023744817581539396834884439920939951398099204762098557434162372897450391 |
| 14 | 1211915226103304116902480919414656925797395622457075839734955262827581122261 |

The same list is in [`terms.txt`](terms.txt).

## Files

| file | what it is |
|---|---|
| `terms.txt` | all fifteen terms in decimal |
| `certificates/t<n>.ecpp.cert` | ECPP certificate of term n (CM format) |
| `certificates/t<n>.nminus1.txt` | N−1 certificate of term n: N, the factored part of N−1 and the witnesses |
| `certificates.zip` | the same 30 certificate files in one archive |
| `record.json` | the numbers above, for scripts |

## Checking it yourself

Probable-prime check of all terms, and that they form the progression (Python with gmpy2):

```python
import gmpy2
a, d, p = 198301127768, 848309427, gmpy2.primorial(163)
terms = [(a + d * n) * p + 1 for n in range(15)]
assert all(gmpy2.is_prime(t) for t in terms)
assert all(len(str(t)) == 76 for t in terms)
assert not gmpy2.is_prime((a - d) * p + 1) and not gmpy2.is_prime((a + 15 * d) * p + 1)
print("15 terms, 76 digits each, probable primes")
```

Proofs, with CM installed:

```
for n in $(seq 0 14); do ecpp-check -f certificates/t$n.ecpp.cert; done
```

Each run should print that the file contains a valid ECPP certificate in the CM format. The first number in each
certificate is the term it proves.
