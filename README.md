# Versionierung
## Standard-Versionierung
```bash
# Neue Major-Version (Inkompatibilität mit früheren Releases)
# bspw. v1.1.0 -> v2.0.0
npm version major
# Neue Minor-Version (Neue Funktionalität, aber Abwärtskompatibilität ist gewährleistet)
# bspw. v1.1.0 -> v1.2.0
npm version minor
# Patch (Bugfixes)
# bspw. v1.1.0 -> v1.1.1
npm version patch
```
## Versionierung von Release-Kandidaten
Wenn eine neue Version (Major, Minor, Patch) getestet wird und ggf. vor dem Release noch Bugfixes erfolgen müssen (z.B. nach Bereitstellung auf Testserver)
```bash
# Vorbereitung einer neuen Minor-Version
# bspw. v1.1.0 -> v1.2.0-0
npm version preminor
# Kontinuierliche Verbesserung des RC erfolgt dann durch
npm version prerelease
# v1.2.0-0 -> v1.2.0-1 -> v1.2.0-2 etc.
# Wenn das Release fertig ist:
npm version minor
# v1.2.0-2 .> v1.2.0
```

## Abhängigkeit in package.json
Prerelease-Versionen werden normalerweise nicht berücksichtigt, d.h. `~0.0.2` oder `<=1.0.0` laden bspw. auch die Version `0.0.3`, aber nicht die Versionen `0.0.3-0`, `0.0.3-1` usw.
Angenommen, die letzte Version war `0.0.2` und die nächste wird `0.0.3` werden. Dann muss als Abhängigkeit `~0.0.3-0` angegeben werden, damit alle Prereleases von `0.0.3` geladen werden.
Das spätere Release `0.0.3` ist bei dieser Abhängigkeit mit eingeschlossen.
Das ist an der Versions-Historie erkennbar (die Minor-Release Nummer ändert sich ja nicht):
```bash
npm view @tecracer/zzz-playground versions
[ '0.0.1',
'0.0.2-1',
'0.0.2',
'0.0.3-0',
'0.0.3',
'0.0.4-0',
'0.0.4-1',
'0.0.4-2',
'0.0.4',
'0.0.5-0',
'0.0.5',
'1.0.0-0' ]
```

## Login mit Token statt Username/Password
`export NPM_TOKEN="229b1152-514d-40ce-8bab-c5823331e61f"`
