# setup-chryse-action

Install dependencies for [Chryse], and optionally the library itself from source. [action.yml] is an easy read.

[Chryse]: https://github.com/chryse-hdl/chryse
[action.yml]: https://github.com/chryse-hdl/setup-chryse-action/blob/v2.3/action.yml

## Base usage

Install:

* Temurin JDK 22 using [actions/setup-java]
* sbt 1.9.8
* Verilator from apt

[actions/setup-java]: https://github.com/actions/setup-java

```yaml
- name: Set up Chryse
  uses: chryse-hdl/setup-chryse-action@v2.3
```

### OSS CAD Suite

Additionally install OSS CAD Suite using [YosysHQ/setup-oss-cad-suite].
The suite's Verilator install is used instead of getting it from apt.

[YosysHQ/setup-oss-cad-suite]: https://github.com/YosysHQ/setup-oss-cad-suite

```yaml
- name: Set up Chryse
  uses: chryse-hdl/setup-chryse-action@v2.3
  with:
    install-oss-cad-suite: true
    github-token: ${{ secrets.GITHUB_TOKEN }}
```

### Chryse from source

Clone [Chryse] and `sbt publishLocal` a particular ref of it.

```yaml
- name: Set up Chryse
  uses: chryse-hdl/setup-chryse-action@v2.3
  with:
    source-ref: main
```

## Rationale

* ChiselSim depends on Verilator 5.x in all but the simplest usage.
* The `ubuntu-22.04` GitHub Actions runner (current `ubuntu-latest`) includes `sbt` in the base image, but the Verilator in apt is 4.x.
* The `ubuntu-24.04` runner has Verilator 5.x in apt, but no `sbt`. -_-

I'm preferring getting ready for 24.04 sooner, so we fetch `sbt` manually, and install Verilator from apt if we're not obtaining OSS CAD Suite (which bundles it).

We don't need OSS CAD Suite if we're not synthesising, and [YosysHQ/setup-oss-cad-suite]'s use of the GitHub API means it's pretty easy to trigger API rate-limits even when providing a token! So I try to make it easy to avoid it.
