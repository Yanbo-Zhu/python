
# 1 Venv
virtual environment,

Mehr Informationen zu venv: [https://docs.python.org/3/tutorial/venv.html](https://docs.python.org/3/tutorial/venv.html)

Python unterstuetzt seit PEP 405 virtuelle Interpreter bzw Umgebungen (virtual environment, kurz: venv).

Eine virtuelle Umgebung ist eine Ansammlung von einer Python-Installation, -Konfiguration und Paketen, die fuer ueblich einem oder ggf. auch mehreren Projekten zugeordnet werden.  (每个umgebung 中可以自己配置 信息 ，python version )
Diese Umgebung existiert unabhaengig von anderen virtuellen Umgebungen und insbesondere unabhaengig von der Systeminstallation von Python.

Der Vorteil einer virtuellen Umgebung ist die Isolation von Projekten;
Abhaengigkeiten von Paketen muessen nicht global im System installiert werden, sondern bleiben lokal auf ein Projekt beschraenkt.
Insbesondere kommt es dadurch nicht zu Versionskonflikten, wenn ein Projekt auf eine aeltere Paket-Version angewiesen ist.  (适应 venv 能够避免的问题)

Die Standardbibliothek enthaelt ab Python 3.3 ein venv-Modul, das automatisiertes Erzeugen von virtuellen Umgebungen ermoeglicht. Virtuelle Umgebungen werden fuer ueblich lokal in einem Unterordner des Projekts angelegt und tragen den Namen venv oder .venv .


# 2 Poetry 

Offizielle Poetry-Website: https://python-poetry.org/ 

Poetry ist ein Dependency-Manager für Python-Projekte. 
Neben der definierten Syntax um Paketabhängigkeiten zu beschreiben, bietet Poetry Funktionalität zum automatischen erstellen einer virtuellen Umgebung mit allen nötigen Abhängigkeiten, sowie Hilfen zum Bauen und Veröffentlichen (z.B. auf PyPi) des Pakets.  

Der Grund für die Entscheidung für poetry als entsprechendes Tool ist die gemeinsame Lösung für das Erstellen von virtuellen Umgebungen, das Definieren von Abhängigkeiten, das Bauen von Paketen und der Upload zu einem Python-Repository. 
Für alle diese Aufgaben existierten bereits andere Tools, aber (unserem Wissensstand nach) keins, dass alle vereint erfüllt.

(能干什么。 1 包关系， 2 产生 venv 3 发布 code 到 repo 上面  )

pyproject.toml-Datei ： 
Poetry nutzt dafür die pyproject.toml-Datei (siehe PEP 518), die ebendiese Abhängigkeiten und andere Optionen definiert. 
Diese Datei bietet damit eine Alternative zu der weitverbreiteten setup.py-Datei, die ein Python-Skript definiert, dass das Paket bauen soll.  (是 setup.py 的替代物 )
Alternative Pakete / Tools zu poetry, die einem vor allen in externen Projekten begegnen können: setuptools, setup.py, twine, distribute

poetry.lock-Datei： 
Neben der pyproject.toml-Datei erstellen poetry eine poetry.lock-Datei. 
Diese Datei wird bei VCS eingecheckt, damit alle Entwickler des Pakets die gleiche Datei teilen. 
Während die pyproject.toml-Datei für Pakete Mindest- und Maximal-Versionen festlegt, gibt es im Normalfall mehrere konkrete Versionen, die diese Restriktionen erfüllen. Welche tatsächlichen Versionen genutzt werden, damit alle (auch rekursiven) Abhängigkeiten erfüllt sind, legt poetry automatisch fest und schreibt diese Informationen in die poetry.lock-Datei. 
Zum Beispiel erfüllen sowohl Version 1.1.0 als auch 1.2.1 die Abhängigkeit "^1.1", aber nur eine davon wird in der .lock-Datei zu finden sein. 


Ein Beispiel für eine pyproject.toml-Datei ist unten zu sehen.
```
[tool.poetry]
name = "paketname"
version = "1.9.5"
description = "Paketbeschreibung"
authors = ["Max Mustermann <mmu@ivu.de>"]
readme = "README.md"
 
# Damit IVU-interne Pakete in den Abhängigkeiten definiert werden.
[[tool.poetry.source]]
name = "ivu"
url = "https://nexus3.ivu.de/repository/Ivu-Pypi/simple"
 
# Paket-Abhängigkeiten zum Ausführen / Nutzen
[tool.poetry.dependencies]
python = "^3.8"
mako = "^1.1"
grt-gparser = "^1.3.0"
anytree = "^2.8.0"
 
# Paket-Abhängigkeiten zur Entwicklung
[tool.poetry.dev-dependencies]
bitstring = "^3.1"
pytest = "^5.3"
 
# "Entry Points". In diesem Beispiel ist nach der Installation des Pakets "foo" ein Kommandozeilenbefehl, der die gegebene main-Funktion aufruft.
[tool.poetry.scripts]
foo = "paketname.__main__:main"
 
[build-system]
requires = ["poetry>=0.12"]
build-backend = "poetry.masonry.api"

```

# 3 poetry 命令

```
# Erzeugen einer pyproject.toml in einem neuen Projekt
poetry init
 
# Erzeugen einer virtuellen Umgebung mit poetry
poetry install

# Berechnen der Abhängigkeiten und Erstellen / Überschreiben der poetry.lock
poetry update
 
# Veröffentlichen von Paketen im IVU-PyPi
poetry publish -r ivu --build  # Die Nutzerdaten fuer den Schreibzugriff auf das PyPi-Repository koennen vom DELI-Team erfragt werden.

```


1 Installation ueber Powershell: 
(Invoke-WebRequest -Uri https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py -UseBasicParsing).Content | python - --version=1.0.10

Die installierte Version muss der oben genannten Anforderung entsprechen. Siehe https://github.com/python-poetry/poetry/issues/977 für einen Bug, der sonst dabei auftreten kann.
Weitere Informationen, siehe: https://python-poetry.org/docs/ .


2  poetry config
```
Nach der Installation von poetry (s.o.) muessen einmalig folgende Kommandozeilen ausgefuehrt werden:

poetry config virtualenvs.create true
poetry config virtualenvs.in-project true
poetry config repositories.ivu https://nexus3.ivu.de/repository/Ivu-Pypi/

```


3 poetry uninstall
```
Falls Probleme mit poetry haben, und deinstalliert werden müss, kann man den Datei get-poetry.py  benutzen.
python get-poetry.py --uninstall
```

