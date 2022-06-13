# CSOB certification of payment terminal integration test cases
CSOB certifikace testovací scénáře

```lua
=>          = automatic step
then        = manual step
and         = simultaneous step
+           = automatic simultaneous step
PA          = partial approval
Rxxx        = response code from terminal
reopen app  = close and open the app in the browser


## A - NORMAL PURCHASE
PASS A00 -  66 CZK approved          then finish payment
PASS A01 -  77 CZK approved          then manual reversal  77 CZK then cancel purchase
PASS A02 - 200 CZK approved          then manual reversal 200 CZK then cancel purchase
PASS A03 - 550 CZK approved with PIN then manual reversal 550 CZK then cancel purchase

PASS A04 -  88 CZK manual decline R-01 then redo card payment
PASS A05 - 200 CZK manual decline R-01 then redo card payment
PASS A06 - 550 CZK manual decline R-01 then redo card payment

PASS A07 - 100 CZK auto declined R076 nekryta castka
PASS A08 - 101 CZK auto declined R105 volejte AC
PASS A09 - 102 CZK auto declined R909 zadrzte kartu
PASS A10 - 103 CZK auto declined R050 zamitnuto
PASS A11 - 104 CZK auto declined R055 chybna data
PASS A12 - 105 CZK auto declined R205 neplatna castka
PASS A13 - 106 CZK auto declined R107 prekrocen limit
PASS A14 - 107 CZK auto declined R900 prekrocen pocet PIN
PASS A15 - 108 CZK auto declined R057 kradena karta
PASS A16 - 109 CZK auto declined R096 je pozadovan PIN >> R-01
PASS A17 - 110 CZK auto declined R201 nespravny PIN >> R-01


## B - PARTIAL APPROVAL
PASS B01 - 103 CZK 1x PA auto declined R050 then redo card payment with different card then manual reversal 103 CZK

PASS B02 - 150 CZK 1x PA + 1x CASH REST approved then manual reversal 1x 111 CZK
PASS B03 - 200 CZK 1x PA + 1x card rest approved then manual reversal 1x 111 CZK + 89 CZK (use a different card for the last PA)
PASS B04 - 210 CZK 1x PA + 1x card rest with manual declined R-01 => continue PA from 1x 111 CZK
PASS B05 - 211 CZK 1x PA + 1x card rest =>   auto declined R076 => continue PA from 1x 111 CZK
PASS B06 - 212 CZK 1x PA + 1x card rest =>   auto declined R105 => continue PA from 1x 111 CZK
PASS B07 - 213 CZK 1x PA + 1x card rest =>   auto declined R909 => continue PA from 1x 111 CZK
PASS B08 - 214 CZK 2x PA + 1x card rest =>   auto declined R050 => continue PA from 1x 111 CZK

PASS B09 - 250 CZK 2x PA + 1x CASH REST approved then manual reversal 2x 111 CZK
PASS B10 - 300 CZK 2x PA + 1x card rest approved then manual reversal 2x 111 CZK + 78 CZK (use a different card for the last PA)
PASS B11 - 310 CZK 2x PA + 1x card rest with manual declined R-01 => continue PA from 2x 111 CZK
PASS B12 - 326 CZK 2x PA + 1x card rest =>   auto declined R055 => continue PA from 2x 111 CZK
PASS B13 - 327 CZK 2x PA + 1x card rest =>   auto declined R205 => continue PA from 2x 111 CZK
PASS B14 - 328 CZK 2x PA + 1x card rest =>   auto declined R107 => continue PA from 2x 111 CZK
PASS B15 - 329 CZK 2x PA + 1x card rest =>   auto declined R900 => continue PA from 2x 111 CZK

PASS B16 - 350 CZK 3x PA + 1x CASH REST approved then manual reversal 3x 111 CZK
PASS B17 - 400 CZK 3x PA + 1x card rest approved then manual reversal 3x 111 CZK + 67 CZK (use a different card for the last PA)
PASS B18 - 410 CZK 3x PA + 1x card rest with manual declined R-01      => continue PA from 3x 111 CZK
PASS B19 - 441 CZK 3x PA + 1x card rest =>     auto declined R057      => continue PA from 3x 111 CZK
PASS B20 - 442 CZK 3x PA + 1x card rest =>     auto declined R096/R-01 => continue PA from 3x 111 CZK
PASS B21 - 443 CZK 3x PA + 1x card rest =>     auto declined R201/R-01 => continue PA from 3x 111 CZK

PASS B22 - 160 CZK 1x PA then manual reversal 1x 111 CZK
PASS B23 - 260 CZK 2x PA then manual reversal 2x 111 CZK


## C - SIGNATURE CHECK
PASS C01 - 66 CZK approved, signature check required then signature incorrect =>          reversal 66 CZK then cancel purchase
PASS C02 - 76 CZK approved, signature check required then signature   correct then manual reversal 76 CZK then cancel purchase

PASS C03 - 436 CZK then signature incorrect after 1st PA => reversal 1x 111 CZK then continue PA
PASS C04 - 437 CZK then signature incorrect after 2nd PA => reversal 1x 111 CZK then continue PA
PASS C05 - 438 CZK then signature incorrect after 3rd PA => reversal 1x 111 CZK then continue PA
PASS C06 - 439 CZK 3x PA + 1x card rest => auto declined R107 then continue PA from 3x PA

PASS C07 - 450 CZK 4x PA + 1x card rest => approved then manual reversal 4x 111 CZK + 6 CZK then cancel purchase

PASS C08 - 350 CZK combi 20 cash 310 card 20 cheque then signature incorrect after 3rd PA => reversal 1x 88 CZK then continue PA

PASS C09 - 250 CZK combi 20 cash 210 card 20 cheque then signature incorrect after 2nd PA => reversal 1x 88 CZK then reopen app 
    then continue PA


## D - NON STANDARD SITUATIONS - RECONNECT INTERNET, POS CRASH RECOVERY
PASS D01 - disconnect net then 500 CZK => cannot connect then connect net then check last trans => inapplicable
    then redo card payment => approved then manual reversal 500 CZK
PASS D02 - 210 CZK wait => terminal respond with timeout => R-18 then redo card payment => approved then manual reversal 210 CZK

PASS D03 -  60 CZK disconnect net then swipe PA then reconnect within 60sec => approved then manual reversal 60 CZK
PASS D04 - 100 CZK disconnect net then swipe PA then reconnect within 60sec => auto declined R076
PASS D05 -  70 CZK disconnect net               then reconnect within 60sec then swipe => approved then manual reversal 70 CZK
PASS D06 - 101 CZK disconnect net               then reconnect within 60sec then swipe => auto declined R105

PASS D06 -  80 CZK disconnect net then      swipe PA then reconnect after 60sec then check last trans => approved 
    then manual reversal 80 CZK
PASS D07 - 102 CZK disconnect net then dont swipe PA then reconnect after 60sec then check last trans => auto declined R-18

PASS D08 - 203 CZK      swipe PA and reopen app then restore => passivate last trans => card rest then approved 
    then manual reversal 1x 111 CZK + 92 CZK
PASS D09 - 103 CZK dont swipe PA and reopen app then restore => passivate => declined R-01
PASS D10 -  90 CZK      swipe PA and reopen app then dont restore then reopen app then restore => approved

PASS D11 - 203 CZK      swipe PA then card rest PA 92 CZK then dont swipe and reopen app 
     then restore => passivate last trans => declined R-01 => continue PA from 111 CZK

PASS D12 - 200 CZK      swipe PA and reopen app then restore => passivate last trans => partially approved 
     then continue and finish PA then manual reversal 1x 111 CZK + 89 CZK


PASS D13 - 200 CZK and reopen app then swipe PA then restore then CASH rest PA  89 CZK then manual reversal 1x 111 CZK
PASS D14 - 200 CZK and reopen app then swipe PA then restore then card rest PA  89 CZK then manual reversal 1x 111 CZK + 89 CZK
PASS D15 - 211 CZK and reopen app then swipe PA then restore then card rest PA 100 CZK => auto declined R076 => continue PA from 1x 111 CZK
PASS D16 - 326 CZK and reopen app then swipe PA then restore then 2x card rest PA 215 + 104 => auto declined R076 => continue PA from 2x 111 CZK

PASS D17 - 326 CZK and reopen app then dont swipe then restore => passivate => declined R-01 then redo card payment 326 CZK

PASS D18 -                326 CZK and reopen app then      swipe PA then restore => passivate => approved PA 111 CZK 
    then continue card PA 215 CZK and reopen app then dont swipe PA then restore => passivate => auto declined R-01 => continue PA from 1x 111 CZK

PASS D19 -                200 CZK and reopen app then      swipe PA then restore => passivate => approved PA 111 CZK 
    then continue card PA  89 CZK and reopen app then      swipe PA then restore => passivate => approved 89 CZK then manual reversal 1x 111 CZK + 89 CZK
        
PASS D20 -                326 CZK and reopen app then      swipe PA then restore => passivate => approved PA 111 CZK 
    then continue card PA 215 CZK and reopen app then      swipe PA then restore => passivate => approved PA 111 CZK 
    then continue card PA 104 CZK and reopen app then      swipe PA then restore => passivate => auto declined R055 => continue PA from 2x 111 CZK
        
PASS D21 326 CZK and reopen app then swipe PA then dont restore PA (cannot ignore restore)

PASS D22 restore passivate last trans with different amount (change amount of last trans) - this can be simulated by turning off the payment terminal after swiping

PASS D23 payment terminal unavailable before reversal

PASS D24 1st partial approval approved then 2nd partial approval timeout then reopen app then restore


## E - CLOSE TOTAL
PASS E01 - close total after transaction
PASS E02 - close total without any transaction after last close total
PASS F03 - refund feature only avalable for manager or admin, or seller with specific privilege


## F - REFUND
PASS F01 - refund with reference number 12345678901, amount 100 CZK => auto declined R076
PASS F01 - refund with reference number 12345678901, amount 150 CZK => approved R000
PASS F02 - refund with reference number 12345678901, amount 200 CZK then manual decline => R-01
PASS F03 - refund feature only avalable for manager or admin, or seller with specific privilege


## G - Combined payments cash + card before sending to terminal
- repeat all test cases above for combined payments
```
