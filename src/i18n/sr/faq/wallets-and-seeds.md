# <i class="fa fa-money"></i> Новчаници и сјеме

---

#### 1. Да ли некоме да дам своје семе новчаника? 

Не, никада не бисте требали[^8613] поделити своје семе новчаника никоме. То је еквивалентан давањем свих ваших ДЦР-а у том новчанику.

---

#### 2. Како могу да претворим своје хеш семе новчаника у семенске речи? 

Можете користити [dcrseedhextowords](https://github.com/davecgh/dcrseedhextowords)[^8660] услужни програм за претварање семена Децред из хеша на речи семена потребне за увоз у новчанике..

---

#### 3. Могу ли покренути више новчаника са истим семенима? 

Покретање више новчаника истог семена може довести до ситуације у којој новчани неће видети исти баланс. Не би требало да покрећете више новчаница са истим семенима.[^9731]

Проблем је једноставно да се адресе генеришу детерминистички из семена. Дакле, ако имате два новчаника који раде на истом семену, у основи завршите са оваквом ситуацијом:

* Новчаник А: Зна за све адресе до адресе # 15
* Новчаник Б: Зна за све адресе до адресе # 12

Дакле, било који новчићи који су послати на адресе # 13, # 14 и # 15 биће познати Новчанику А, али не и Новчанику Б.

Даље, ако једноставно кажете новчанику Б да добије следећу адресу, неће се видети и новчићи јер је, с његове тачке гледишта, та адреса тек сада постојала и тако неће тражити трансакције пре тренутног тренутка. Ово је оптимизација јер, како можете да замислите, блокчејн завршава постаје изузетно велик током времена и био би невероватно скуп (у смислу коришћења ресурса) да скенира цео ланац сваки пут када се генерише нова адреса.

Постоји један изузетак од овога, а то је за гласање новчаница које немају сопствених средстава. Ако новчаник **only** ради гласања и не купује карте или креира друге трансакције, то је сигурно.[^11319]

---

#### 4. Да ли неко може украсти моје новчиће ако приступи валлет.дб? 

Нико не може украсти твоје новчиће ако добију приступ фајлу валлет.дб[^9803] осим ако не поседују и вашу приватну лозинку. Ако сте изабрали да користите јавну енкрипцију, они такође не могу приступити било којем вашем проширеном јавном кључу или адреси.

---

#### 5. Да ли неко може на силу да насумично нападне новчаник како би узео његове семене речи ? 

Све ријечи семена су директно мапиране из енглеских ријечи у хекс цифре. Семе није ништа друго до 256-битни (32-бајтни) криптографски сигуран случајни број. Сол се овде не примењује. То нема никакве везе са насилним бројевима[^10452].

Другим речима, пошто свака реч може бити 256 могућности и има 32 речи, то даје 256 ^ 32 (или 2 ^ 256 у зависности од тога како желите да га погледате, али то је исти број) могућности. Тај број је већи од укупног броја атома водоника у познатом универзуму. Заправо, то је готово више од броја атома укупно у познатом универзуму.

Да ставимо ово у перспективу, под претпоставком да на планети има 7 милијарди људи, а свака особа поседовала 10 рачунара, а сваки од тих рачунара могао би да тестира милијарде могућности у секунди и да би могли пронаћи решење у просеку након тестирања само 50% Тоталне могућности, ипак би требало да узме 26к10 ^ 48 (то је 26 трилиона трилиона трилиона трилиона милијарди долара) година за бруталну силу једног семена.

---

#### 6. Моје семе не ради. Шта могу да урадим? 

Уверите се да су све речи на једној линији раздвојене размацима[^10657]. Even though they are printed out on multiple lines for readability, they must be entered on a single line. Also double-check your words have no typos by comparing them to the words in the [PGP word list](https://en.wikipedia.org/wiki/PGP_word_list).

---

#### 7. Како да увезем кључ који је у формату увоза новчаника (WIF)? 

Могуће је увести засебан приватни кључ[^10724] v `dcrwallet`. Имајте на уму да је ово само за `--noseed` адресе и не би требало да покренете ово осим ако не знате шта радите!

Откључајте новчаник (игноришите угао заграда):

```no-highlight
dcrctl --wallet walletpassphrase <private encryption passphrase> 60
```

Увезите засебни (`--noseed`) приватни кључ (игноришите угао заграда):

```no-highlight
dcrctl --wallet importprivkey <put WIF private key here>
```

Прегледајте стање увезеног налога (дајте мало времена за скенирање и погледајте дневник у дцрваллет-у како бисте видели напредак за поновно скенирање):

```no-highlight
dcrctl --wallet getbalance "imported" 0 all
```

---

#### 8. Која је разлика између тестнет и меиннет адресе? 

Адреса јавног кључа тестне мреже[^11507] почиње словима `Tk`. Адреса главне мреже почиње словима `Dk`. `T` = Тестнет, `D` = (Деактивиран) Меиннет.

---

#### 9. Које су различите врсте адреса? 

Деактивирана адреса[^14995] је уствари само представљање јавног кључа (који сам може бити хаш сцрипт) заједно са 2-бајтним префиксу који идентификује мрежу и тип и суфикс контролног сума како би открио непрописно уписане адресе.

Сходно томе, увек можете да кажете на коју врсту адресе се заснива на 2-бајтном префиксу.

Први бајт префикса идентификује мрежу. Због тога све адресе мреже почињу са "Д", адресе тестнета почињу са "Т", а симнет адресе почињу са "С". Други бајт префикса идентификује врсту адресе која је.

Најчешће коришћене тренутно адресе су сецп256к1 пубкључ хешеви, које су идентификоване малим словима "с". Она представља један јавни кључ и стога има само један повезани приватни кључ који се може искористити.

Ипак, удио користи пеј ту скрипт хеш адресу, коју други бајт идентификује као мала слова "ц" (опет је приказана у повезаним параметрима). Специфични тип сценарија који се генерише је вишеструки потпис 1-оф-2, који омогућава да гласате ви или база. И ви и удружени базен имате своје приватне кључеве и пошто сценарио захтева само један потпис од могућих двоје, тако да дозвољава пренос гласачких права на базен без потпуног одустајања од вашег гласачког права.

---

## <i class="fa fa-book"></i> Извори 

[^8613]: Decred Forum, [Post 8,613](https://forum.decred.org/threads/576/#post-8613)
[^8660]: Decred Forum, [Post 8,660](https://forum.decred.org/threads/534/page-3#post-8660)
[^9731]: Decred Forum, [Post 9,731](https://forum.decred.org/threads/657/#post-9731)
[^11319]: Decred Forum, [Post 11,319](https://forum.decred.org/threads/531/page-3#post-11319)
[^9803]: Decred Forum, [Post 9,803](https://forum.decred.org/threads/686/#post-9803)
[^10452]: Decred Forum, [Post 10,452](https://forum.decred.org/threads/734/#post-10452)
[^10657]: Decred Forum, [Post 10,657](https://forum.decred.org/threads/483/#post-10657)
[^10724]: Decred Forum, [Post 10,724](https://forum.decred.org/threads/643/page-3#post-10724)
[^11507]: Decred Forum, [Post 11,507](https://forum.decred.org/threads/792/#post-11507)
[^14995]: Decred Forum, [Post 14,995](https://forum.decred.org/threads/1321/page-2#post-14995)