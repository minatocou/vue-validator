<a name="2.0.0-alpha.16"></a>
# [2.0.0-alpha.16](https://github.com/vuejs/vue-validator/compare/v2.0.0-alpha.15...v2.0.0-alpha.16) (2016-01-22)


### Bug Fixes

* **base:** fix input wrong behavior ([2dcafeb](https://github.com/vuejs/vue-validator/commit/2dcafeb)), closes [#141](https://github.com/vuejs/vue-validator/issues/141) [#142](https://github.com/vuejs/vue-validator/issues/142)
* **validate:** cannot compile validator when using v-for and v-model ([9ade590](https://github.com/vuejs/vue-validator/commit/9ade590)), closes [#140](https://github.com/vuejs/vue-validator/issues/140)
* **validations:** fix other wrong behaviors ([bf6e7d0](https://github.com/vuejs/vue-validator/commit/bf6e7d0))



<a name="2.0.0-alpha.15"></a>
# [2.0.0-alpha.15](https://github.com/vuejs/vue-validator/compare/v2.0.0-alpha.14...v2.0.0-alpha.15) (2016-01-19)

### Bug Fixes

* **validate:** occured TypeError when use v-if ([9ca17b4](https://github.com/vuejs/vue-validator/commit/9ca17b4)), closes [#139](https://github.com/vuejs/vue-validator/issues/139)


<a name="2.0.0-alpha.14"></a>
# [2.0.0-alpha.14](https://github.com/vuejs/vue-validator/compare/v2.0.0-alpha.13...v2.0.0-alpha.14) (2016-01-18)


> Skipped 2.0.0-alpha.14 because it contains an incorrect dist file.



<a name="2.0.0-alpha.13"></a>
# [2.0.0-alpha.13](https://github.com/vuejs/vue-validator/compare/v2.0.0-alpha.12...v2.0.0-alpha.13) (2016-01-17)


### Bug Fixes

* **validate:** read property access error when use v-model and v-for ([e7c7714](https://github.com/vuejs/vue-validator/commit/e7c7714)), closes [#137](https://github.com/vuejs/vue-validator/issues/137)

### Features

* **custom:** support local registration ([74b1631](https://github.com/vuejs/vue-validator/commit/74b1631)), closes [#125](https://github.com/vuejs/vue-validator/issues/125)



<a name="2.0.0-alpha.12"></a>
# [2.0.0-alpha.12](https://github.com/vuejs/vue-validator/compare/v2.0.0-alpha.11...v2.0.0-alpha.12) (2016-01-16)


### Bug Fixes

* **validate:** expression evaluating error ([f918e39](https://github.com/vuejs/vue-validator/commit/f918e39)), closes [#35](https://github.com/vuejs/vue-validator/issues/35) [#103](https://github.com/vuejs/vue-validator/issues/103) [#111](https://github.com/vuejs/vue-validator/issues/111)



<a name="2.0.0-alpha.11"></a>
# [2.0.0-alpha.11](https://github.com/vuejs/vue-validator/compare/v2.0.0-alpha.10...v2.0.0-alpha.11) (2016-01-14)


### Features

* **validate:** support field attribute ([4fbaf3a](https://github.com/vuejs/vue-validator/commit/4fbaf3a)), closes [#46](https://github.com/vuejs/vue-validator/issues/46) [#129](https://github.com/vuejs/vue-validator/issues/129)



<a name="2.0.0-alpha.10"></a>
# [2.0.0-alpha.10](https://github.com/vuejs/vue-validator/compare/v2.0.0-alpha.9...v2.0.0-alpha.10) (2016-01-13)

### Bug Fixes

* **util:** fix Firefox dispatchEvent bug ([e2bd08f](https://github.com/vuejs/vue-validator/commit/e2bd08f)), closes [#132](https://github.com/vuejs/vue-validator/issues/132)

### Features

* **validate:** support v-model validation ([0859cd4](https://github.com/vuejs/vue-validator/commit/0859cd4)), closes [#94](https://github.com/vuejs/vue-validator/issues/94)
* **validator:** support camelizable name attribute ([c812cea](https://github.com/vuejs/vue-validator/commit/c812cea)), closes [#118](https://github.com/vuejs/vue-validator/issues/118)



<a name="2.0.0-alpha.9"></a>
# [2.0.0-alpha.9](https://github.com/vuejs/vue-validator/compare/v2.0.0-alpha.8...v2.0.0-alpha.9) (2016-01-01)


### Features

* **checkbox:** support checkbox validation ([7f46bad](https://github.com/vuejs/vue-validator/commit/7f46bad))
* **custom:** support global error message ([c75480f](https://github.com/vuejs/vue-validator/commit/c75480f))
* **radio:** support radio button validaton ([848f3f5](https://github.com/vuejs/vue-validator/commit/848f3f5))
* **select:** support select validation ([42284f6](https://github.com/vuejs/vue-validator/commit/42284f6))



<a name="2.0.0-alpha.8"></a>
# [2.0.0-alpha.8](https://github.com/vuejs/vue-validator/compare/v2.0.0-alpha.7...v2.0.0-alpha.8) (2015-12-13)


### Bug Fixes

* **asset:** fix cannot register validator issue ([dce7e96](https://github.com/vuejs/vue-validator/commit/dce7e96)), closes [#108](https://github.com/vuejs/vue-validator/issues/108)

### Features

* **lazy:** support lazy initialization ([f5c24c9](https://github.com/vuejs/vue-validator/commit/f5c24c9)), closes [#25](https://github.com/vuejs/vue-validator/issues/25)
* **validation:** support kebab-case ([b26a108](https://github.com/vuejs/vue-validator/commit/b26a108)), closes [#102](https://github.com/vuejs/vue-validator/issues/102)



<a name="2.0.0-alpha.7"></a>
# [2.0.0-alpha.7](https://github.com/vuejs/vue-validator/compare/v2.0.0-alpha.6...v2.0.0-alpha.7) (2015-12-10)


### Features

* **syntax:** support array syntax on v-validate expression ([bf33bb4](https://github.com/vuejs/vue-validator/commit/bf33bb4))



<a name="2.0.0-alpha.6"></a>
# [2.0.0-alpha.6](https://github.com/vuejs/vue-validator/compare/v2.0.0-alpha.6...v2.0.0-alpha.6) (2015-12-07)


### Performances

* **bundle**: more compact the vue-validator
  about 20% smaller build with rollupjs.

  - before
    - vue-validator.min.js 11701
    - vue-validator.js 26180
  - after
    - vue-validator.min.js 9309
    - vue-validator.js 20713



<a name="2.0.0-alpha.5"></a>
# [2.0.0-alpha.5](https://github.com/vuejs/vue-validator/compare/v2.0.0-alpha.4...v2.0.0-alpha.5) (2015-11-24)


### Features

* **messages:** support messages validation property ([34564ec](https://github.com/vuejs/vue-validator/commit/34564ec))



<a name="2.0.0-alpha.4"></a>
# 2.0.0-alpha.4 (2015-11-23)


### chore

* chore(npm): add commitizen config ([bf23fc3](https://github.com/vuejs/vue-validator/commit/bf23fc3))
* chore(READEME): modify baduge urls ([0cc7b0e](https://github.com/vuejs/vue-validator/commit/0cc7b0e))
* chore(sauce): remove unnecessary sauce setting ([edf8383](https://github.com/vuejs/vue-validator/commit/edf8383))
* chore(travis): change node version ([8c7845c](https://github.com/vuejs/vue-validator/commit/8c7845c))

### docs

* docs(README): add commitizen badge ([1f3399e](https://github.com/vuejs/vue-validator/commit/1f3399e))
* docs(spec): This is the spec ([6da4e9a](https://github.com/vuejs/vue-validator/commit/6da4e9a))

### feat

* feat(install): support automatically install for standalone ([d8fb356](https://github.com/vuejs/vue-validator/commit/d8fb356))

### fix

* fix(lint): resolve eslint error ([72c3d1b](https://github.com/vuejs/vue-validator/commit/72c3d1b))



<a name="2.0.0-alpha.3"></a>
# 2.0.0-alpha.3 (2015-11-23)


### chore

* chore(lint): fix eslint errors ([0e58704](https://github.com/vuejs/vue-validator/commit/0e58704))
* chore(npm): update npm-scripts ([8c866d1](https://github.com/vuejs/vue-validator/commit/8c866d1))

### fix

* fix(override): occured error when using plugin ([3d9fe74](https://github.com/vuejs/vue-validator/commit/3d9fe74)), closes [#92](https://github.com/vuejs/vue-validator/issues/92)



<a name="2.0.0-alpha.2"></a>
# 2.0.0-alpha.2 (2015-11-22)


### docs

* docs(README): fix typo ([5c7cb78](https://github.com/vuejs/vue-validator/commit/5c7cb78))

### fix

* fix(validator): remove test property from validation scope ([3e862dd](https://github.com/vuejs/vue-validator/commit/3e862dd))


### BREAKING CHANGE

* bower: not support `bower` package manager ([28f87ea](https://github.com/vuejs/vue-validator/commit/28f87ea))

I think that bower is dead.


# 2.0.0-alpha.1 / 2015-11-22

* Release for Vue 1.0

# v1.4.4 / 2015-09-26

* Fix validator configration options passing (#55, #57)

# v1.4.3 / 2015-09-06

* Fix validation data access error bug (#53)

# v1.4.2 / 2015-08-16

* Fix dirty bug (#43)

# v1.4.1 / 2015-07-31

* Fix code bundling issue

# v1.4.0 / 2015-07-31

* Add async validation

# v1.3.3 / 2015-07-23

* Fix component $destroy bug (#38)

# v1.3.2 / 2015-07-19

* Fix `required` validator bug (#37)

# v1.3.1 / 2015-07-18

* Fix dirty property bug (#36)

# v1.3.0 / 2015-07-14

* Support reactivity (#6)

# v1.2.2 / 2015-07-10

* Fix validates option read access error (#32)

# v1.2.1 / 2015-07-09

* Fix unbind error (#30)
* Fix invalid v-validate directive
* Change `$emit` interface for `wait-for` attribute

# v1.2.0 / 2015-07-06

* Add delay initialization of validation feature (#25)

# v1.1.2 / 2015-07-04

* Fix objectable v-model unbind error (#29) [@torniker]

# v1.1.1 / 2015-06-27

* Fix undefined method access error (#26)

# v1.1.0 / 2015-06-23

* Support Vuejs 0.12 (#23)
* Fix pattern validator regex issue (#17)

# v1.0.7 / 2015-06-22

* Fix unbind issue of directive (#19)

# v1.0.6 / 2015-06-05

* Support objects and arrays in required validator (#16)

# v1.0.5 / 2015-06-02

* Add dirty of all models

# v1.0.4 / 2015-05-08

* Fix number option of v-model (#13)

# v1.0.3 / 2015-05-04

* Fix keypath specific model (#12)

# v1.0.2 / 2015-04-02

* Update READEME
* Fix saucelabs failed on the travis ci

# v1.0.1 / 2015-03-30

* Update READEME
* Add example for require.js
* Update examples

# v1.0.0 / 2015-02-12

* Bump to latest version

# v0.11.3 / 2015-01-31

* Change namespace for vuejs orginaization

# v0.11.2 / 2014-12-29

* Change saucelabs account

# v0.11.1 / 2014-12-26

* Add end-to-end and saucelabs tests

# v0.11.0 / 2014-12-12

* Release vue-validator for Vue.js 0.11.2 later

# v0.10.0 / 2014-11-07

* Bump to latest version

# v0.1.1 / 2014-10-11

* Support bower

# v0.1.0 / 2014-05-29

* Release first
