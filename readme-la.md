# kenlm

Exemplar linguae illatio in codice Kenneth Heafield (kenlm at kheafield.com)

Pagina "<https://kheafield.com/code/kenlm/>plura habet documenta. Si elit decoder es, recentiorem versionem inde excipe loco exemplaris alterius decoder.

## Compiling

Utere cmake, vide[AEDIFICATIO](BUILDING)for ediderat clientelas et planius.

```bash
mkdir -p build
cd build
cmake ..
make -j 4
```

## Componendis cum suis constructum ratio

Si vis cum tuo aedificandi systemate ordinare (Makefile etc) vel uti in bibliotheca, sunt plures macros quos in linea imperandi vel in util/have.hh pones.

-   `KENLM_MAX_ORDER`est maximus ut possit oneratus. Hoc factum est ut POD potius quam vector rem efficiat.
-   `HAVE_ICU`Si codice tuo nexus contra ICU, hoc definias ut inactivare StringPiece internum et repone cum exemplari StringPiece ICU, pugnas nominandi vitando.

ARPA files legi possunt in forma compressa cum his optionibus:

-   `HAVE_ZLIB`Sustinet, gzip. Link cum -lz.
-   `HAVE_BZLIB`Sustinet bzip2. Vinculum cum -lbz2.
-   `HAVE_XZLIB`Adstipulatur, xz. Vinculum cum -llzma.

Nota quod isti tantum incursum`read_compressed.cc`et`read_compressed_test.cc`. Ratio aedificandi bjam auto- deprehendes bzip2 et subsidium xz erit.

## Aestimatio

lmplz aestimat exempla linguae inputata cum Kneser-Ney delenimentis mutatis. Componendis cum bjam, curre

```bash
bin/lmplz -o 5 <text >text.arpa
```

Algorithmus in orbe est, utens quantitatem memoriae quam denotas. Vide<https://kheafield.com/code/kenlm/estimation/>quia plus.

MT Marathon 2012 iugis sodalium Ivan Pouzyrevsky et Mohammed Mediani ad consilium computationis et primae exsecutionis operam dederunt. Jon Clark consilium contulit, puncta declaravit de levando, et colligationem addidit.

## Filtering

colum sumit ARPA vel tabellam numeratam et entries removet quae numquam queried possunt. colum criterium potest esse vocabularium corpus-gradum, vocabularium sententia-planum, phrases sententia-grada. Curre

```bash
bin/filter
```

et vide<https://kheafield.com/code/kenlm/filter/>pro maiori documento.

## Querying

Duae notitiae structurae sustentantur: perspiciendi et experiendi. Perscrutatio mensae detrahendae est perscrutatio cum clavibus quae sunt 64-frenum hashes n-iiiim et innatat ut valores. Tria est satis vexillum triticum, sed gradatim sarcina sic utitur ut minimus numerus frenorum ad verborum indices et indices congreget. Viscus tri nodi ordinantur indice verbo. Perscrutatio est quam celerrime et memoria maxime utitur. Tria minimo utitur memoria et aliquanto tardius est.

Ut mos est in lingua modelendi, omnia probabilia 10 turpia sunt.

Cum trie, memoria incola est 58% of IRST versionis minimae et 21% versionis pacti SRI. Simul, probate CPU usus est 81% of IRST versionis velocissimae et 84% versionis celeritatis SRI. KenLM scrutans tabulam Nullam massam exsecutionem accedit etiam citius sumptu maiore utendi memoria. Vide<https://kheafield.com/code/kenlm/benchmark/>.

Forma binaria per mmap sustentatur. Curre`./build_binary`ut unum efficiat deinde lima nomen binarium ad congruum exemplar constructoris transeundum.

## Platforms

`murmur_hash.cc`et`bit_packing.hh`praestare unaligned legit et scribit quae codicem architecturae-dependens efficit.  
Bene probatum est in x86_64, x86, et PPC64.  
ARM subsidium parem laborat, saltem in iphone.

Percurrit Linux, OS X, Cygwin et MinGW.

Hideo Okuma et Tomoyuki Yoshimura e NICT portus ad ARM et MinGW contribuerunt.

## Decoder developers

-   Commendo codicem exscribendo et cum decodo tuo distribuendo. Sed commodo flumine mitte emendationes.

-   Possibile est investigatum solum codicem sine Boost ordinare, sed utilia sicut exempla aestimanda require Boost.

-   Macras quas vis elige, in sectione superiore recensita.

-   Sunt duo systemata construendi: compile.sh et cmake. Pulchra simplicia sunt et in systemate aedificando reimpleri volunt.

-   Utere aut interface in`lm/model.hh`or \*`lm/virtual_interface.hh`. Interface documentum in comment of`lm/virtual_interface.hh`et`lm/model.hh`.

-   Plures sunt possibilia notitia structurae in`model.hh`. Usus`RecognizeBinary`in`binary_format.hh`uter quis usor providit. Tu probabiliter iam plumas efficiendi functiones sicut virtualis basis classis abstractae cum pluribus pueris. Moneo tibi hanc virtualem celeritatem existentem cooptare per exemplum linguae pluma exsecutionis in KenLM exemplar, quod a notatur.`RecognizeBinary`. Hoc consilium in Mose & cdec.

-   Vide`lm/config.hh`ad currere-tempus tuning optiones.

## Contributors

Conlationes KenLM grata sunt. Quaeso te confers in fundamus<https://github.com/kpu/kenlm>ac mitto petitiones collige (or me accessum det tibi committo). Exemplar amni in Moyse et cdec conservantur scribendo ita non mutando ibi.

## Python modulus

Collata a Victore Chahuneau.

### Institutionem

```bash
pip install https://github.com/kpu/kenlm/archive/master.zip
```

Cum insertis pituitam, the`MAX_ORDER`environment variabilis ordinem vulgare quo KenLM aedificabatur.

### Basic Ritus

```python
import kenlm
model = kenlm.Model('lm/test.arpa')
print(model.score('this is a sentence .', bos = True, eos = True))
```

Vide[python/example.py](python/example.py)et[python/kenlm.pyx](python/kenlm.pyx)pro magis, inter APIs statal.

### Building kenlm - Using vcpkg

Potes detrahere et installare kenlm utendi the[vcpkg](https://github.com/Microsoft/vcpkg)procurator dependentiae;

    git clone https://github.com/Microsoft/vcpkg.git
    cd vcpkg
    ./bootstrap-vcpkg.sh
    ./vcpkg integrate install
    ./vcpkg install kenlm

Portus kenlm in vcpkg usque ad diem ab Microsoft sodalibus et communitatibus contributorum custoditur. Si versio est de date, quaeso[partum est exitus seu petitionem viverra](https://github.com/Microsoft/vcpkg)in repositio vcpkg.

* * *

Nomen erat idea Hieu Hoang, non mea.
