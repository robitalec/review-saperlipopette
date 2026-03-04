### Editor checks:

- [X] **Documentation**: The package has sufficient documentation available online (README, pkgdown docs) to allow for an assessment of functionality and scope without installing the package. In particular,
    - [X] Is the case for the package well made?
    - [X] Is the reference index page clear (grouped by topic if necessary)?
    - [X] Are vignettes readable, sufficiently detailed and not just perfunctory?
- [X] **Fit**: The package meets criteria for [fit](https://devguide.ropensci.org/policies.html#package-categories) and [overlap](https://devguide.ropensci.org/policies.html#overlap).
- [X] **Installation instructions:** Are installation instructions clear enough for human users?
- [ ] **Tests**: If the package has some interactivity / HTTP / plot production etc. are the tests using [state-of-the-art tooling](https://devguide.ropensci.org/building.html#testing)?
- [ ] **Contributing information**: Is the documentation for contribution clear enough e.g. tokens for tests, playgrounds?
- [ ] **License:** The package has a CRAN or OSI accepted license.
- [X] **Project management**: Are the issue and PR trackers in a good shape, e.g. are there outstanding bugs, is it clear when feature requests are meant to be tackled?
---

#### Editor comments

Hello @maelle, thanks for your submission. The package is looking to be in great shape! I'll list a few things below that I'm hoping to clear up before we start looking for reviewers. 

License:

- I'm seeing two different license related files: [LICENSE](https://github.com/ropensci-training/saperlipopette/blob/9f0ea401ff9cb6e24ec4456274b0306a4a5ee92a/LICENSE) and [LICENSE.md](https://github.com/ropensci-training/saperlipopette/blob/9f0ea401ff9cb6e24ec4456274b0306a4a5ee92a/LICENSE.md). 

Contributing: 

- We could use a bit more information - right now we see "Please open an issue for any larger change (new exercise for instance).", but what about recommendations for eg. filing bugs, asking for help, contributing smaller changes?

Submission template: 

- I edited the template to remove these two lines, they didn't seem to correspond to anything relevant:

```
Sub-directory: .
Sub-directory: .
```

- When we are ready to look for reviewers, could you edit the template to include the version number under "Version submitted"?

README:

- There are two [code coverage badges](https://github.com/ropensci-training/saperlipopette/blob/9f0ea401ff9cb6e24ec4456274b0306a4a5ee92a/README.Rmd#L20-L21) in the README

tools/update.paper.qmd:

- The tool that Claude wrote for keeping the vignette updated based on the paper in inst/. Is it possible you could just use the [Includes](https://quarto.org/docs/authoring/includes.html) syntax instead? This works when I check locally with `pkgdown::build_site` and a basic render. But I'm not sure if it would work/be accepted everywhere (eg. CRAN).  

`vignettes/articles/paper.md`

```
---
title: "saperlipopette, a risk-free playground for learning more Git"
bibliography: paper.bib
knitr:
  opts_chunk:
    collapse: true
    comment: '#>'
---

{{< include ../../inst/paper/paper.md >}}
```


tests:

- I see failing tests locally related to the testthat snapshots of gert::git_log hashes. These don't appear on the tests run through GitHub Actions, so I'm trying to figure them out. I've made sure my packages (gert, testthat) and version of libgit2 are updated. I see 1) mostly differences in Git hashes (eg. test-blame and test-committed-to-main) but also 2) some differences in test-create-all that might be due to snapshots not having RStudio Projects files, whereas my local tests generates them? Let me know what you think might be going on. 


```r
R: library(saperlipopette)
R: 
R: devtools::test('../saperlipopette')
ℹ Testing saperlipopette
✔ | F W  S  OK | Context
✖ | 1        1 | blame                                                                          
────────────────────────────────────────────────────────────────────────────────────────────────
Failure (test-blame.R:6:3): exo_blame() works
Snapshot of code has changed:
old vs new
  Code
    gert::git_log(repo = path)[["commit"]]
  Output
-   [1] "99738a808b6d5529d8de83fb20c0588ec5afff41"
+   [1] "e776cc8573afe6cb331159e4b9113ac60d49709e"
-   [2] "a334b44fc56f21a609989b187685bbcfbcaac4d7"
+   [2] "01bdc274b5d54de9a7ab4cad8869fdbe629ebd04"
-   [3] "d5ff861dede667b9856f42417585df40d5c0fb76"
+   [3] "376f91dfb553475c7a1e7632bb342a11dcb52384"
-   [4] "595c3093fe615679519631bf045b1bdd76a729cf"
+   [4] "797d5c39d7b5e8b08f3dc4f15b4eea971dd85b19"
-   [5] "2ee32ca74a45769de57f2cf4149adff0f1d9e61b"
+   [5] "1d65bddf84e335aa3bb32f1656a103648adf3714"
-   [6] "e227ecc55e421f70b6e30602e6a2eee02aad42e0"
+   [6] "b59b4809e7f0ec8a0df85b443baa73b332bd3b5b"
* Run testthat::snapshot_accept("blame", "/home/alecr/Documents/Local-git/saperlipopette/tests/testthat") to accept the change.
* Run testthat::snapshot_review("blame", "/home/alecr/Documents/Local-git/saperlipopette/tests/testthat") to review the change.
────────────────────────────────────────────────────────────────────────────────────────────────
✔ |          1 | check-editor                                                                   
✖ | 1        1 | clean-dir                                                                      
────────────────────────────────────────────────────────────────────────────────────────────────
Failure (test-clean-dir.R:6:3): exo_clean_dir() works
Snapshot of code has changed:
old vs new
  Code
    gert::git_log(repo = path)[["commit"]]
  Output
-   [1] "2a61d9da6865eb7f7272c9f901f13c1da377a01e"
+   [1] "aec15965c3581c3dcba6359f74c91cd54fb5939d"
-   [2] "e227ecc55e421f70b6e30602e6a2eee02aad42e0"
+   [2] "c090f52d68d5a007775eddfe026b2e72e66eedcd"
* Run testthat::snapshot_accept("clean-dir", "/home/alecr/Documents/Local-git/saperlipopette/tests/testthat") to accept the change.
* Run testthat::snapshot_review("clean-dir", "/home/alecr/Documents/Local-git/saperlipopette/tests/testthat") to review the change.
────────────────────────────────────────────────────────────────────────────────────────────────
✖ | 1        1 | committed-to-main                                                              
────────────────────────────────────────────────────────────────────────────────────────────────
Failure (test-committed-to-main.R:6:3): exo_committed_to_main() works
Snapshot of code has changed:
old vs new
  Code
    gert::git_log(repo = path)[["commit"]]
  Output
-   [1] "2ff0d31f566e68ae0ee94b6028a3fa2e24ed066a"
+   [1] "e7889516408acd1619610931f0e68a1b3c577007"
-   [2] "e227ecc55e421f70b6e30602e6a2eee02aad42e0"
+   [2] "1f4724b272699cdc79512cf053ef9bc66feaf8ca"
* Run testthat::snapshot_accept("committed-to-main", "/home/alecr/Documents/Local-git/saperlipopette/tests/testthat") to accept the change.
* Run testthat::snapshot_review("committed-to-main", "/home/alecr/Documents/Local-git/saperlipopette/tests/testthat") to review the change.
────────────────────────────────────────────────────────────────────────────────────────────────
✖ | 1        1 | committed-to-wrong-branch                                                      
────────────────────────────────────────────────────────────────────────────────────────────────
Failure (test-committed-to-wrong-branch.R:6:3): exo_committed_to_wrong() works
Snapshot of code has changed:
old vs new
  Code
    gert::git_log(repo = path)[["commit"]]
  Output
-   [1] "83ee0e3cc5afed932cd9e3f2f34274c60bfe1166"
+   [1] "380f963522865ce2be3a06d9a611cf73e2e0b23a"
-   [2] "e48ac924412914278ed7d3ee6e82d0fe3122741a"
+   [2] "56591fc55e10052367efa3cea143b9b063f4d266"
-   [3] "e227ecc55e421f70b6e30602e6a2eee02aad42e0"
+   [3] "569711c966f498b8aa7a7554496e3a702d934568"
* Run testthat::snapshot_accept("committed-to-wrong-branch", "/home/alecr/Documents/Local-git/saperlipopette/tests/testthat") to accept the change.
* Run testthat::snapshot_review("committed-to-wrong-branch", "/home/alecr/Documents/Local-git/saperlipopette/tests/testthat") to review the change.
────────────────────────────────────────────────────────────────────────────────────────────────
✖ | 1        1 | conflict                                                                       
────────────────────────────────────────────────────────────────────────────────────────────────
Failure (test-conflict.R:6:3): exo_conflict() works
Snapshot of code has changed:
old vs new
  Code
    gert::git_log(repo = path)[["commit"]]
  Output
-   [1] "5d871367c8a247a5e63bd0701d7bce830d1dc614"
+   [1] "d4f7a10710d1b61c9664303663b5fe467d9e2215"
-   [2] "2a61d9da6865eb7f7272c9f901f13c1da377a01e"
+   [2] "fe387b39814b24ba7ef653a0546b4b4796cd9357"
-   [3] "e227ecc55e421f70b6e30602e6a2eee02aad42e0"
+   [3] "f0a62988268a33177343cde2ad009aee53f107c1"
* Run testthat::snapshot_accept("conflict", "/home/alecr/Documents/Local-git/saperlipopette/tests/testthat") to accept the change.
* Run testthat::snapshot_review("conflict", "/home/alecr/Documents/Local-git/saperlipopette/tests/testthat") to review the change.
────────────────────────────────────────────────────────────────────────────────────────────────
✖ | 1        0 | create-all [3.9s]                                                              
────────────────────────────────────────────────────────────────────────────────────────────────
Failure (test-create-all.R:5:3): create_all_exercises() works
Snapshot of code has changed:
     old                    | new                                   
 [3] Output                 | Output                 [3]            
 [4]                        |                        [4]            
 [5]   +-- bisect           |   +-- bisect           [5]            
 [6]   |   \-- R            -   |   +-- R            [6]            
 [7]   |       \-- script.R -   |   |   \-- script.R [7]            
                            -   |   \-- bisect.Rproj [8]            
 [8]   +-- blame            |   +-- blame            [9]            
 [9]   |   \-- R            -   |   +-- R            [10]           
[10]   |       \-- script.R -   |   |   \-- script.R [11]           
                            -   |   \-- blame.Rproj  [12]           
 ... ...                      ...                    and 11 more ...
     old                      | new                                               
[21]   |   \-- debugging      |   |   \-- debugging                [25]           
[22]   +-- committed-to-main  |   +-- committed-to-main            [26]           
[23]   |   +-- R              |   |   +-- R                        [27]           
[24]   |   \-- bla            -   |   +-- bla                      [28]           
                              -   |   \-- committed-to-main.Rproj  [29]           
[25]   +-- committed-to-wrong |   +-- committed-to-wrong           [30]           
[26]   |   +-- R              |   |   +-- R                        [31]           
[27]   |   +-- bla            |   |   +-- bla                      [32]           
                              -   |   +-- committed-to-wrong.Rproj [33]           
[28]   |   \-- fix.txt        |   |   \-- fix.txt                  [34]           
 ... ...                        ...                                and 56 more ...
* Run testthat::snapshot_accept("create-all", "/home/alecr/Documents/Local-git/saperlipopette/tests/testthat") to accept the change.
* Run testthat::snapshot_review("create-all", "/home/alecr/Documents/Local-git/saperlipopette/tests/testthat") to review the change.
────────────────────────────────────────────────────────────────────────────────────────────────
✖ | 1        1 | debug [1.6s]                                                                   
────────────────────────────────────────────────────────────────────────────────────────────────
Failure (test-debug.R:6:3): exo_bisect() works
Snapshot of code has changed:
old vs new
  Code
    gert::git_log(repo = path)[["commit"]]
  Output
-     [1] "d1e99031240ba2b6a78117f09df1c3b7b089f41a"
+     [1] "affb2beec0c0da8ffc1238e0e47d6950d538ffa3"
-     [2] "f26c132d3ab725336f321b6f0c403022e0ad7372"
+     [2] "bd69e88b0e744e568a729831caac348fb50670af"
-     [3] "85cebcf1f5c19397a19a009747353d7246979c52"
+     [3] "78f61cce1b2949633cd2d6f8878af2d3fb3616f2"
-     [4] "978a4d7a52ce0c4e5a3f82f53fff6d804f4efeeb"
+     [4] "79a6ed2bb6ee936b1bb3a0b7e48c34400d06ce56"
-     [5] "2add1f6723f3d88c68999d97b3ffebe1fe119642"
+     [5] "2f5028c4d3a11a24fe2d87f041a4ea7df14f5ed0"
-     [6] "beb2fa1f91f2cc320c2c8da9ba295e72cf0b1021"
+     [6] "b7923e30e46f9e836be467ffefed23becb97de0e"
-     [7] "4113e395ef532fd197de37528c914af919a6d90a"
+     [7] "a57f764dc0489d422e866560bd82251eff6ed3c5"
and 93 more ...
* Run testthat::snapshot_accept("debug", "/home/alecr/Documents/Local-git/saperlipopette/tests/testthat") to accept the change.
* Run testthat::snapshot_review("debug", "/home/alecr/Documents/Local-git/saperlipopette/tests/testthat") to review the change.
────────────────────────────────────────────────────────────────────────────────────────────────
✖ | 1        1 | edit-latest-message                                                            
────────────────────────────────────────────────────────────────────────────────────────────────
Failure (test-edit-latest-message.R:6:3): exo_latest_message() works
Snapshot of code has changed:
old vs new
  Code
    gert::git_log(repo = path)[["commit"]]
  Output
-   [1] "d3d35a17a880eee777868a5fbe99ce1bfe3b31bb"
+   [1] "6740f4094f9d80f2bf20cea36b16d329345b33d2"
-   [2] "e227ecc55e421f70b6e30602e6a2eee02aad42e0"
+   [2] "517cffaed99afdb2143fc9a408b08ac5ef5faca7"
* Run testthat::snapshot_accept("edit-latest-message", "/home/alecr/Documents/Local-git/saperlipopette/tests/testthat") to accept the change.
* Run testthat::snapshot_review("edit-latest-message", "/home/alecr/Documents/Local-git/saperlipopette/tests/testthat") to review the change.
────────────────────────────────────────────────────────────────────────────────────────────────
✖ | 1        1 | log-deleted-file                                                               
────────────────────────────────────────────────────────────────────────────────────────────────
Failure (test-log-deleted-file.R:6:3): exo_log_deleted_file() works
Snapshot of code has changed:
old vs new
  Code
    gert::git_log(repo = path)[["commit"]]
  Output
-    [1] "8d49564daf69f7da3208dce5db26e832d52a01d1"
+    [1] "e48a98ca70738acccbdca3de1d3da01561c1058d"
-    [2] "b6af1dca46a09968c561b22af44ad35ee4ea413b"
+    [2] "b5fd33c3575b7a50f0c1ead29f54ea3eb5d3a0f9"
-    [3] "ab0ec48cd3306cc2a29341d84d634e0264a6b558"
+    [3] "0d0c4a4ce6f30ddc63bc79be178eb9cb9dcdf905"
-    [4] "f1e91f7e99f4783a778790512d7bf8cbdbe73436"
+    [4] "87c7a33e9d944ea4337e19952654447796f790cd"
-    [5] "5b9bce029eb8363b54e257ff3c27ccca0810f181"
+    [5] "f5598c92ed9f82fefc04030e5977cf7632ff5f08"
-    [6] "7b1ad57aae390d25d0f12b6b88a5e890eb0ffead"
+    [6] "ca0126a96d2373972b97c0927fb296a201ffeacb"
-    [7] "b6ba25ffa8b4f2302f17fb5bebe7f8305c5f7834"
+    [7] "038a6954ff7f626919ff369371669f1e80cf67e2"
and 8 more ...
* Run testthat::snapshot_accept("log-deleted-file", "/home/alecr/Documents/Local-git/saperlipopette/tests/testthat") to accept the change.
* Run testthat::snapshot_review("log-deleted-file", "/home/alecr/Documents/Local-git/saperlipopette/tests/testthat") to review the change.
────────────────────────────────────────────────────────────────────────────────────────────────
✖ | 1        1 | log-deleted-line                                                               
────────────────────────────────────────────────────────────────────────────────────────────────
Failure (test-log-deleted-line.R:6:3): exo_log_deleted_line() works
Snapshot of code has changed:
old vs new
  Code
    gert::git_log(repo = path)[["commit"]]
  Output
-    [1] "9162b22638c61c25790b5c60da6034928bd084ee"
+    [1] "a166ab10bf643c7eeeb6746e976a74872c3d9f9e"
-    [2] "963cbe002216fc14feddac7927594f1a160df505"
+    [2] "9993ba4d7b248076755979968ae337768753f67c"
-    [3] "5e9ace09746de941c4b177dbf8ddffdb91071ce3"
+    [3] "e88bb306477fbfca519c94f6034bfc1c1422bfd7"
-    [4] "5ea923a3ab33fda78c073ab84b9e9276777b2fca"
+    [4] "608fd6a9782dde40c73ffcf4f6b81d9d375af2cc"
-    [5] "27b8c167ba1b06a1c1758e254cf43aa060021baa"
+    [5] "35eba4dfa498c2bbc3c53ddb0b3e6c618c11e621"
-    [6] "d1e464d9da59120d4e64f3beee884ab4197aed93"
+    [6] "4ff3594c93deddd6e5818bff155bfe9ce0e9aee0"
-    [7] "544d738b703fdbdc0511beba1f622ce893e6c818"
+    [7] "c5412c2428086c62d361aff84f5c564fa9c0bd65"
and 4 more ...
* Run testthat::snapshot_accept("log-deleted-line", "/home/alecr/Documents/Local-git/saperlipopette/tests/testthat") to accept the change.
* Run testthat::snapshot_review("log-deleted-line", "/home/alecr/Documents/Local-git/saperlipopette/tests/testthat") to review the change.
────────────────────────────────────────────────────────────────────────────────────────────────

Maximum number of failures exceeded; quitting.
ℹ Increase this number with (e.g.) testthat::set_max_fails(Inf) 
R: 
R: sessionInfo()
R version 4.5.2 (2025-10-31)
Platform: x86_64-pc-linux-gnu
Running under: Arch Linux

Matrix products: default
BLAS:   /usr/lib/libblas.so.3.12.0 
LAPACK: /usr/lib/liblapack.so.3.12.0  LAPACK version 3.12.0

locale:
 [1] LC_CTYPE=en_CA.UTF-8       LC_NUMERIC=C               LC_TIME=en_CA.UTF-8       
 [4] LC_COLLATE=en_CA.UTF-8     LC_MONETARY=en_CA.UTF-8    LC_MESSAGES=en_CA.UTF-8   
 [7] LC_PAPER=en_CA.UTF-8       LC_NAME=C                  LC_ADDRESS=C              
[10] LC_TELEPHONE=C
R: 
R: # Version of libgit2 installed:
R: # extra/libgit2 1:1.9.2-1
```

- Tests have a very similar structure for all the exercises. Tests check for 1) the filepath returned from the example function matches the expected filepath name (as in, does `dir_create` create a directory named as expected) and 2) the snapshot of git commit hashes returned from `gert::git_log` match the snapshot. 

eg. test-edit-latest-message.R

```r
rlang::local_options(cli.default_handler = function(msg) invisible(NULL))
parent_path <- withr::local_tempdir()
path <- exo_latest_message(parent_path = parent_path)
expect_identical(fs::path_file(path), "latest-message")
expect_snapshot(gert::git_log(repo = path)[["commit"]])
```


It seems that maybe this could be turned into a helper function that might make it simpler for future contributors with new lessons to easily reuse the same testing framework? Here's a quick draft below with an example in my fork of saperlipopette [here](https://github.com/robitalec/saperlipopette/tree/feat/helper-test-exo). 

`tests/testthat/helper-test-exo.R`

```r
helper_test_exo <- function(fn, nm) {
  test_that(paste0(quote(fn), "() works"), {
    rlang::local_options(cli.default_handler = function(msg) invisible(NULL))
    parent_path <- withr::local_tempdir()
    path <- do.call(fn, list(parent_path = parent_path))
    expect_identical(fs::path_file(path), nm)
    expect_snapshot(gert::git_log(repo = path)[["commit"]])
  })
}
```

Thanks! Let me know what you think. 
