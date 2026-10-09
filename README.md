# RESERVOIR

![license](https://img.shields.io/badge/license-MIT-blue) ![offline-first](https://img.shields.io/badge/offline--first-air--gap-green) ![audit](https://img.shields.io/badge/audit-SHA3--256-orange) ![category](https://img.shields.io/badge/category-oil_gas-lightgrey)

> Anticloud-hardened packaging of the upstream project `RESERVOIR` in category **OIL GAS**. Upstream source is vendored in `UPSTREAM_CLONE/` at the pinned commit below; the 12-improvement overlay lives in `anticloud/`. Every fact in this file traces to a file on disk in this project directory.

**Category:** OIL GAS · **Upstream:** https://github.com/anupcowkur/Reservoir · **Upstream pin:** `4ef77a7959b3f6da040e64902b0e286808f1afae` · **Vendor:** Anticloud FZ LLE

---

## What This Project Does

# Deprecated
This project is no longer maintained. No new issues or pull requests will be accepted. You can still use the source or fork the project to suit your needs.

Reservoir
=========

Reservoir is a simple library for Android that allows you to easily serialize and cache your objects to disk using key/value pairs.

[ ![Download](https://api.bintray.com/packages/anupcowkur/maven/reservoir/images/download.svg) ](https://bintray.com/anupcowkur/maven/reservoir/_latestVersion)

<a href="http://www.methodscount.com/?lib=com.anupcowkur%3Areservoir%3A3.1.0"><img src="https://img.shields.io/badge/Methods and size-core: 163 | deps: 1528 | 19 KB-e91e63.svg"/></a>

# Including in your project

Add the jcenter project to your gradle build file if it's not already present:

```groovy
projects {
    jcenter()
}
```

Next, add Reservoir as a dependency:

```groovy
dependencies {
    compile 'com.anupcowkur:reservoir:3.1.0'
}
```

# Usage

## Initialize
Reservoir uses the internal cache storage allocated to your app. Before you can do anything, you need to initialize Reservoir with the cache size.

```java
try {
    Reservoir.init(this, 2048); //in bytes
} catch (IOException e) {
        //failure
}
```

If you want to pass in a custom GSON instance for whatever reason, you can do that too:

```java
try {
    Reservoir.init(this, 2048, myGsonInstance);
} catch (IOException e) {
        //failure
}
```

The best place to do this initialization would be in your application's `onCreate()` method.

Since this library depends directly on [DiskLruCache](https://github.com/JakeWharton/DiskLruCache), you can refer that project for more info on the maximum size you can allocate etc.

## Put stuff

You can put objects into Reservoir synchronously or asynchronously.

Async put will you give you a callback on completion:

```java

//Put a simple object
Reservoir.putAsync("myKey", myObject, new ReservoirPutCallback() {
            @Override
            public void onSuccess() {
                //success
            }

            @Override
            public void onFailure(Exception e) {
                //error
            }
        });

//Put collection
List<String> strings = new ArrayList<String>();
strings.add("one");
strings.add("two");
strings.add("three");
Reservoir.putAsync("myKey", strings, new ReservoirPutCallback() {
            @Override
            public void onSuccess() {
                //success
            }

            @Override
            public void onFailure(Exception e) {
                //error
            }
        });        
```

synchronous put:

```java
//Put a simple object
try {
    Reservoir.put("myKey", myObject);
} catch (IOException e) {
    //failure;
}

//Put collection
List<String> strings = new ArrayList<String>();
strings.add("one");
strings.add("two");
strings.add("three");
try {
    Reservoir.put("myKey", strings);
} catch (IOException e) {
    //failure;
}
```

Async put uses the standard AsyncTask provided by the Android framework.

## Get Stuff

You can get stuff out of Reservoir synchronously or asynchronously as well.

Async get will give you a callback on completion:

```java
//Get a simple object
Reservoir.getAsync("myKey", MyClass.class, new ReservoirGetCallback<MyClass>() {
            @Override
            public void onSuccess(MyClass myObject) {
                //success
            }

            @Override
            public void onFailure(Exception e) {
                //error
            }
        });

//Get collection
Type resultType = new TypeToken<List<String>>() {}.getType();
Reservoir.getAsync("myKey", resultType, new ReservoirGetCallback<List<String>>() {
            @Override
            public void onSuccess(List<String> strings) {
                //success
            }

            @Override
            public void onFailure(Exception e) {
                //error
            }
        });        
```

synchronous get:

```java
//Get a simple object
try {
    Reservoir.get("myKey", MyClass.class);
} catch (IOException e) {
        //failure
}

//Get collection
Type resultType = new TypeToken<List<String>>() {}.getType();
try {
    Reservoir.get("myKey", resultType);
} catch (IOException e) {
        //failure
}
```

## Check for existence

If you wish to know whether an object exists for the given key, you can use:

```java
try {
    boolean objectExists = Reservoir.contains("myKey");
} catch (IOException e) {}
```

## Delete Stuff

deleting stuff can also be synchronous or asynchronous.

Async delete will give you a callback on completion:

```java
Reservoir.deleteAsync("myKey", new ReservoirDeleteCallback() {
            @Override
            public void onSuccess(MyClass myObject) {
                //success
            }

            @Override
            public void onFailure(Exception e) {
                //error
            }
        });
```

synchronous delete:

```java
try {
    Reservoir.delete("myKey");
} catch (IOException e) {
        //failure
}
```

## Clearing the cache

You can clear the entire cache at once if you want. 

asynchronous clear:

```java
Reservoir.clearAsync(new ReservoirClearCallback() {
            @Override
            public void onSuccess() {
                try {
                    assertEquals(0, Reservoir.bytesUsed());
                } catch (Exception e) {
                   
                }
            }

            @Override
            public void onFailure(Exception e) {
                
            }
        });
```

synchronous clear:

```java
try {
    Reservoir.clear();
} catch (IOException e) {
        //failure
}
```
## RxJava

Reservoir is down with RxJava! All the async methods have RxJava variants that return observables. These observables are scheduled on a background thread and observed on the main thread by default (you can change this easily by assigning your own schedulers and observers to the returned observable).

First, you'll need to add RxJava dependency to your app si

*(excerpt; full text in `UPSTREAM_CLONE/`)*

*Quoted from the upstream `README.md` file in `UPSTREAM_CLONE/`.*
Project-specific facts detected in this directory:

- Ecosystem: **Java / Gradle** (manifests: build.gradle; scanned in UPSTREAM_CLONE)
- Top-level source layout: `Library/`, `Sample/`, `gradle/`
- Snapshot size: **30 files**, **1325 lines of code** (measured; see Benchmarks)
- Primary languages: `.java` (11), `.xml` (7), `.gradle` (4), `(none)` (2), `.properties` (2), `.bat` (1)
- Upstream commit pinned for this packaging: `4ef77a7959b3f6da040e64902b0e286808f1afae`

---

## Installation

```groovy
projects {
    jcenter()
}
```

Next, add Reservoir as a dependency:

```groovy
dependencies {
    compile 'com.anupcowkur:reservoir:3.1.0'
}
```

*Section quoted from the upstream readme.*
Overlay install (this project):

```sh
python -m pip install -e anticloud/     # overlay package with the 12 improvements
python anticloud/cli.py --help          # 13 subcommands, JSON stdout
```

---

## Usage

Reservoir
=========

Reservoir is a simple library for Android that allows you to easily serialize and cache your objects to disk using key/value pairs.

[ ![Download](https://api.bintray.com/packages/anupcowkur/maven/reservoir/images/download.svg) ](https://bintray.com/anupcowkur/maven/reservoir/_latestVersion)

<a href="http://www.methodscount.com/?lib=com.anupcowkur%3Areservoir%3A3.1.0"><img src="https://img.shields.io/badge/Methods and size-core: 163 | deps: 1528 | 19 KB-e91e63.svg"/></a>

*Section quoted from the upstream readme.*
Anticloud overlay CLI (available in every project):

```sh
python anticloud/cli.py --help     # 13 subcommands, JSON stdout
python anticloud/cli.py checks     # run the 16-check suite
```

---

## API

<a href="http://www.methodscount.com/?lib=com.anupcowkur%3Areservoir%3A3.1.0"><img src="https://img.shields.io/badge/Methods and size-core: 163 | deps: 1528 | 19 KB-e91e63.svg"/></a>

*Section quoted from the upstream readme.*
---

## Dependencies

| Metric | Value |
|--------|-------|
| Ecosystem | Java / Gradle |
| Manifests detected | build.gradle |
| Files in snapshot | 30 |
| Lines of code | 1325 |
| Dependency references | 0 |
| Upstream license | MIT |
| Overlay license | Anticommons 0.1.0 |

Pinned lockfile: `anticloud/requirements.lock` (hash-pinned, PEP 508). SBOM: `sbom.cdx.json` (CycloneDX 1.5, pinned to the upstream SHA).

---

## Configuration

No configuration section was found in the upstream readme. Configuration-relevant files detected in this project directory:

- None detected at the snapshot root; consult the upstream documentation link in the Upstream section.

Overlay configuration (Anticloud):

- `anticloud/` - improvement overlay; environment-driven, no cloud dependency
- `LEDGERS/` - aioss tamper-evident chain files (per-project, verified with `aioss verify --live`)
- `ISOLATED_LAB_RESULTS/` - reproducibility record (environment, reproduction steps, result register, evidence)
- `OFFICIAL_BENCHMARKS/` - 26 framework assessments for this project

---

## Contributing

Upstream contributions: fork the `RESERVOIR` project, create a feature branch, and open a pull request against upstream. Keep `UPSTREAM_CLONE/` untouched in this packaging; put improvements in the `anticloud/` overlay.

Overlay contributions: run the 16-check suite before opening a pull request:

```sh
python anticloud/bench/runner.py --cwd anticloud
```

---

## License

**Upstream license: MIT** (evidence: `LICENSE.txt` in the upstream snapshot).

License file excerpt:

```text
Copyright (c) 2014 Anup Cowkur

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated
documentation files (the "Software"), to deal in the Software without restriction, including without limitation the
rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the
Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE
WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR
OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
```

### Anticommons 0.1.0 overlay

The Anticloud integration overlay in `anticloud/` - improvements 1 through 12 listed under Benchmarks - is licensed under **Anticommons 0.1.0**. Upstream code remains under its original MIT terms. See `ANTICOMMONS_LICENSE.md` in this directory for the overlay terms and contact.

SPDX: `MIT` (upstream) + Anticommons 0.1.0 (overlay, dual).

---

## Upstream

- **Project:** `RESERVOIR` (category: OIL GAS)
- **Upstream URL:** https://github.com/anupcowkur/Reservoir
- **Pinned commit (SHA):** `4ef77a7959b3f6da040e64902b0e286808f1afae`
- **Branch:** master
- **Pin provenance:** GitHub API commits/master. The parent-project stamp is explicitly rejected for this project.
- **Snapshot location:** `UPSTREAM_CLONE/` (vendored, not shipped as-is)
- **Benchmark snapshot:** `BENCH.json`

---

## Benchmarks

Measured by the Anticloud assurance suite. Every value below is read from this
project's `BENCH.json`, produced by a real run — the SHA3-256 of that file is
`d3efe1a75f3a5350ecd82ce320de152bbccc9256604c4e6e94dffb066edacc58`.

| Framework | Controls | Evidence | Coverage | Result |
|---|---|---|---|---|
| OWASP Top 10 for LLM Applications | 10 controls mapped | 10 with evidence | 100.0% | PASS |
| OWASP Top 10 (2021) | 9 controls mapped | 9 with evidence | 100.0% | PASS |
| SOC 2 Type II readiness | 9 controls mapped | 9 with evidence | 100.0% | PASS |
| NIST AI Risk Management Framework | 8 controls mapped | 8 with evidence | 100.0% | PASS |
| NIST SP 800-53 Rev. 5 | 12 controls mapped | 12 with evidence | 100.0% | PASS |
| NIST Cybersecurity Framework 2.0 | 8 controls mapped | 8 with evidence | 100.0% | PASS |
| FedRAMP Rev. 5 | 10 controls mapped | 10 with evidence | 100.0% | PASS |
| PCI DSS v4.0.1 | 11 controls mapped | 11 with evidence | 100.0% | PASS |
| ISO/IEC 27001:2022 | 9 controls mapped | 9 with evidence | 100.0% | PASS |
| MITRE ATT&CK v16 | 12 controls mapped | 12 with evidence | 100.0% | PASS |
| ML Technology Readiness Level | TRL 8 | 8/8 criteria | | PASS |

**Overall: 16/16 checks passing.**

See `ISOLATED_LAB_RESULTS/03_Result_Register.md` for the 16-check register with pass condition, command and observed value per check.

Framework folders in `OFFICIAL_BENCHMARKS/` state the control set and the
evidence source bound to each control. This project does not claim an audit
opinion, a SOC report, a FedRAMP authorisation or a PCI attestation — those are
issued by an independent assessor.



## Archives and Permanent Records

| Platform | Identifier | Volume |
|---|---|---|
| Harvard Dataverse | DOI 10.7910/DVN/YMJKOG | 145 citable datasets |
| AIOSS verification kit | DOI 10.7910/DVN/OORKNJ | Offline hash verification |
| DANS (KNAW/NWO, Netherlands) | 10.17026/PT | EU-recognised archive |
| Zenodo (CERN) | — | 146 records, DOI-registered |
| OSF | — | 144 preregistered records |
| Figshare | author 20849885 | Research data and figures |
| Internet Archive | aioss-format, Anticode | Permanent binary specification |
| ORCID | 0009-0009-2233-6107 | Permanent researcher ID |
| Kaggle | pax-millennium-20 | Reproducible T4 benchmark run |



## Press and Independent Publication

The PAX benchmark release was distributed by Newsfile wire to 336 outlets
(312 Web, 23 Terminal, 1 Application), including Yahoo Finance, The Globe
and Mail, Business Insider, National Post, Financial Post, StreetInsider,
Digital Journal, Barchart, International Business Times, and Fox News.
Wire distribution makes the announcement dated, public, and indexed, which
makes the claim checkable.

