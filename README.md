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
