
# 1 Python Version


|                       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Python 2 und python 3 | Python 2.x and Python 3.x are different. <br><br>Python Version 2.0 (allgemein "Python 2" genannt) wurde 2000 eingefuehrt.<br><br>Python 3, erschien 2008 und war ein Major-Release ohne Rueckwaertskompatibilitaet zu Python 2.<br><br>Aus diesem Grund wurde noch lange an Python 2 festgehalten und auch lange nach dem Release von Python 3 musste fuer Diskussionen klar gestellt werden, um welche Major-Version es sich handelt.<br><br>2020 wurde Python 2 offiziell abgekuendigt. Zu diesem Zeitpunkt ist Python (3) die zweitbeliebteste Programmiersprache der Welt, nach Javascript.<br><br>Insbesondere in den Bereichen der mathematischen Auswertung, statistischen Analyse und maschinellem Lernen (als Alternative zu Matlab und R) findet Python oft Nutzen. |
| Minor Version         | upgrading from 3.x to 3.y (minor)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| Patch version         | 3.x.y to 3.x.z (patch) Python version                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |


# 2 PIP

Pip ist der offizielle Paket-Manager von Python, der zuerst 2011 veroeffentlicht wurde.
Die IVU hostet intern ein eigenes PyPi-Repository (analog zu [https://pypi.org/](https://pypi.org/)), das wir nutzen, um relevante interne Tools und Libraries teilen zu koennen: [https://nexus3.ivu.de/#browse/browse:Ivu-Pypi](https://nexus3.ivu.de/#browse/browse:Ivu-Pypi) .


# 3 PyPi

Das offizielle Python-Paket-Repository ist "PyPi" ([https://pypi.org/](https://pypi.org/)) und wird von pip als Standardquelle verwendet.


# 4 PEP

另外的 packet （私人自己开发的 ）
Haufig im Kontext von Python referenziert sind "PEPs" (Python Enhancement Proposals ).
Ein PEP ist ein Dokument von Informationen, die offiziell als Teil der Sprache anerkannt sind.

Dies koennen
- Features der Sprache sein ([https://www.python.org/dev/peps/pep-0468/](https://www.python.org/dev/peps/pep-0468/)),
- Elemente der Standardbibliothek ([https://www.python.org/dev/peps/pep-0628/](https://www.python.org/dev/peps/pep-0628/)) oder
- rein informative Texte ([https://www.python.org/dev/peps/pep-0569/](https://www.python.org/dev/peps/pep-0569/)).

Eine Liste aller PEPs ist zu finden unter: [https://www.python.org/dev/peps/](https://www.python.org/dev/peps/)



# 5 Python 32bit and 64 bit 

Python 32- and 64-bit editions: What's the difference and why does it matter?
https://www.youtube.com/watch?v=XZrThBBpFlo


Python32bit 的劣势
32-bits edition of python centers around compatibility with with third-party .
some python package/ third-party module require binary components to be built for specific platforms in a format called a wheel (= binary component).
If you can find a precompiled wheel for a package you're looking for, But many suffer maintainers are not making precompiled 32-bit. Demand for them (in 32 bits) has faded, becase  most everyone is using a 64-bit  os and a 64-bit edition of Python to go with it
32bits python will be harder to work with mannequins to third-party module


Python 64 bit 的优势  
it a provide access to more than 4 GB of contiguous memory
the 64-bit edition of python ought to be  your default choice at this point given how many  people are providing pre-compiled binaries for it 
he only time you really need to use the 32-bit  edition is if you're stuck with a 32-bit operating  system  or if you have to force compatibility with  a 32-bit component