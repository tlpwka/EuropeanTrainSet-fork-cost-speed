25.09.2026
----
updating grf id for bananas

06.11.2024
----
tlpwka fork
 # 1\. Configurable vehicle purchase and running costs

 The central change of the fork is the introduction of **user-adjustable purchase and running-cost multipliers**.

 Two new parameters were added:

- **Purchase cost multiplier**
- **Running cost multiplier**

 Each has nine selectable levels:

 | Setting | Multiplier |
| --- | --- |
| 1/16 | ÷16 |
| 1/8 | ÷8 |
| 1/4 | ÷4 |
| 1/2 | ÷2 |
| Normal | ×1 |
| 2 | ×2 |
| 4 | ×4 |
| 8 | ×8 |
| 16 | ×16 |

The default is the **Normal / ×1** setting. The parameters are applied directly to vehicle `cost_factor` and `running_cost_factor` values throughout the set.


 This allows the speed parameters to cover essentially the full range used by the fork rather than being restricted to the original narrower ranges.  GitHub+1



 # 2\. Large-scale economic rebalance

 The initial `fork` commit replaces the original economic values on a large portion of the train roster.

 The affected vehicles include:

- AGV
- BB15000
- Eurostar E300
- Eurostar E320
- ICE 1
- ICE 2
- ICE 3
- ICE 3V
- ICE 4
- Renfe S-100
- Renfe S-102
- Renfe S-103
- Renfe S-130
- TGV Atlantique/AR
- TGV Duplex
- TGV La Poste
- TGV M
- TGV POS
- TGV Réseau Duplex
- TGV Sud-Est

 The fork generally replaces the original fixed cost values with expressions such as:

```
cost_factor:         <base>*param_purchase_cost;
running_cost_factor: <base>*param_running_cost;
```
So players can change costs globally rather than editing individual vehicle definitions. The same treatment extends to passenger and postal wagon definitions (standard passenger car, special passenger wagon, TGV Poste wagon).

Several electric trains and the TGV Poste wagon had their `running_cost_base` changed from `RUNNING_COST_DIESEL` to `RUNNING_COST_ELECTRIC`. This affects TGV AR, TGV Duplex, TGV La Poste, TGV POS, TGV Réseau Duplex, TGV Sud-Est, and several Renfe units. 


 # 3\. Broad speed rebalance

 Substantial changes to the nominal speeds of the high-speed fleet.

 Examples include:

 - **AGV:** 300 → 390 km/h
- **ICE 1:** 280 → 300 km/h
- **ICE 2:** 280 → 300 km/h

 Adding new liveries for lategame, including:
- **ICE 4:** 265 → 365 km/h
- **TGV M:** 362 → 502 km/h


 The intent is to provide better QoL for large network, where adaptive speed presented issues to run thoses trains and to have gihg speed trains later in game (still, slower then top maglev units) -  The train's graphics speed was changed from a fixed value to this callback:



 ### TGV Duplex

 A new callback determines its speed from the current year:

```
0..2025: return 329;
return 349;
```



 ### TGV La Poste

 A similar year-dependent speed callback was introduced:

```
0..2029: return 329;
return 503;
```



 ### TGV M

 TGV M receives another adaptive-speed callback:

```
0..2029: return 388;
return 502;
```

 Also increases its specified power from **8,000 kW to 12,000 kW** and its tractive-effort coefficient from **0.3 to 0.4** 




 # 4\. Speed unification and specification cleanup

 It changes specifications for:

 - AGV
- Eurostar E320
- ICE 4
- Renfe S-103
- TGV Duplex
- TGV M
- TGV POS
- TGV Réseau Duplex
- Special passenger wagon
- Passenger wagon

 Examples:

- AGV introduction date: **2012 → 2016**
- Eurostar E320 introduction date: **2014 → 2011**
- TGV POS introduction date: **2006 → 2010**

 The passenger wagon definitions were simultaneously expanded to support additional cargo types.



 # 6\. Expanded cargo/refit functionality

 A notable gameplay change is the expansion of cargo compatibility.

 Previously, many passenger vehicles had:

```
cargo_allow_refit: [PASS];
```

 The fork changes this to:

```
cargo_allow_refit: [PASS, MAIL, VALU];
```

 This is applied to multiple vehicles, including:

 - AGV
- Eurostar E320
- ICE 4
- TGV M
- TGV POS
- Special passenger wagon
- Standard passenger wagon

 Thus these vehicles can be refitted for **passengers, mail, and valuables**, rather than passengers alone. 

 The Eurostar E320 also receives an additional consist-attachment rule allowing another **Eurostar E320** to be attached.



 # 7\. TGV M consist compatibility

 The original TGV M attachment switch is extended to allow:

```
TGV_Poste_wagon
```

 in addition to the existing compatible vehicles.

 This makes the TGV M capable of attaching a TGV postal wagon through its vehicle callback.



 # 8\. Speed-wise compatiblity with JP set fork
https://github.com/tlpwka/JPplusShinkansen-speed-cost-fork



 # 9\. Build-system and path portability fixes

 ### Build tool

 The Makefile changes:

```
NMLC ?= nml/nmlc.exe
```

 to:

```
NMLC ?= nmlc
```

 This removes the hard-coded Windows executable path and instead expects `nmlc` to be available through the environment/path.

 ### Graphic path normalization

 A number of `.pnml` graphic files change Windows-style paths such as:

```
src\locomotive\...
```

 to forward-slash paths:

```
src/locomotive/...
```


2022.09.30 (릴리즈 미공개)
-----
* TGV Pos (리뉴얼)
* TGV Pos Lyair (리뉴얼)
* TGV Pos Thalys (리뉴얼)
* TGV Duplex (객차 리뉴얼)
* TGV Duplex TGV DUPLEX Lyria / Carmillon (객차 리뉴얼)
* TGV DUPLEX Ouigo (객차 리뉴얼)
* TGV Pos Carmillon (도색추가)
* TGV M (리뉴얼)
* BB15000 (신규)
* 객차형 승객 차량 (신규)

2022.08.28
-----
* ICE 1 (신규)
* ICE 2 (신규)
* ICE 3 (리뉴얼)
* ICE 3 Velaro D (신규)
* ICE 4 (신규)
* TGV 쉬드-에스트 (리뉴얼)
* TGV 아틀랑티크 레조 (리뉴얼)

2022.05.28
일부 열차는 YST에서 분리되는 과정에서 열차 명칭이 변경되었습니다.
-----
* AGV
* 유로스타 E300
* 유로스타 E320
* ICE3
* 렌페 AVE S-100
* 렌페 AVE S-102
* 렌페 AVE S-103
* 렌페 Alvia S-130
* TGV 쉬드-에스트
* TGV 아틀랑티크 레조
* TGV 레조 듀플렉스
* TGV 듀플렉스
* TGV 포스
* TGV M
* TGV 라포스트
