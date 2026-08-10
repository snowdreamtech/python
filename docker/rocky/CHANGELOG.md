# Changelog

## [3.12.13](https://github.com/snowdreamtech/python/compare/rocky-v3.12.13...rocky-v3.12.13) (2026-08-10)


### 🐛 Bug Fixes

* **docker:** simplify rocky python version to 3.12.13 to fix dnf build failure and unify versions ([40a9063](https://github.com/snowdreamtech/python/commit/40a906302120b0c2ca4f92be181bd7def72c1cce))
* **docker:** unify rocky python version to 3.12.13 across manifest and changelog ([a2a9d6a](https://github.com/snowdreamtech/python/commit/a2a9d6a61a008712c49a81a8530d3f3f9e9cea20))
* **docker:** update python3 version to 3.12.13 for alpine and rocky ([a9ee6bc](https://github.com/snowdreamtech/python/commit/a9ee6bce4c6480fe4cc0aa1146c6f44875a88e26))
* remove static version defaults from OCI image labels to use variable injection exclusively ([da5645a](https://github.com/snowdreamtech/python/commit/da5645ad4d48467290235abbbd9f31ba70bf690f))
* **rocky:** correct python3 RPM version to 3.12.13-2.el10_2.1 ([123576c](https://github.com/snowdreamtech/python/commit/123576ca5f8f8d1c942d284f082bb8d730b8cdb0))
* **rocky:** fix dnf version pin syntax for python3 to 3.12.13-2.el10_2 ([9b25245](https://github.com/snowdreamtech/python/commit/9b252454606f4053c9d0c66cecf6c80dd89ddc45))
* use ghcr.io for base images to avoid rate limits ([9f1d73a](https://github.com/snowdreamtech/python/commit/9f1d73a75a61f2f368f5572c4bd28f4c92ef8fd5))


### ♻️ Miscellaneous Chores

* add 0-git-keep.sh to prevent empty entrypoint.d directories ([ce77247](https://github.com/snowdreamtech/python/commit/ce77247762becc1edf85ec7b57747d3f3127044a))
* **merge:** merge upstream/dev into dev ([3d6cbe1](https://github.com/snowdreamtech/python/commit/3d6cbe1893d6eda684efbc659ca6862c3ca29965))
* release main ([5a92edb](https://github.com/snowdreamtech/python/commit/5a92edb4ba76b04ee6de7369e9471f785849a7ae))
* release main ([4011a21](https://github.com/snowdreamtech/python/commit/4011a21a23395acc9545168c95ca0ec5c867e7d3))
* release main ([d52be5c](https://github.com/snowdreamtech/python/commit/d52be5cf0c5cff45f7f72e973d62c94b48855e1b))
* release main ([f66597a](https://github.com/snowdreamtech/python/commit/f66597a5feae95e8853f4cc730c81e93e172f6ca))
* release main ([b3a5cc9](https://github.com/snowdreamtech/python/commit/b3a5cc9ef0a64a7bc04ed7c2acf0cca5327c5c26))
* release main ([deb8454](https://github.com/snowdreamtech/python/commit/deb8454df7518d56939ab3851245a4cd7b03d709))
* release main ([d87cb81](https://github.com/snowdreamtech/python/commit/d87cb815685ad9b5b43d4b9a195c68dee2fd8065))
* **release:** deduplicate CHANGELOG headers ([c2bba24](https://github.com/snowdreamtech/python/commit/c2bba247dca89a31accc6e70c5e48b16170b1ce5))
* **release:** deduplicate CHANGELOG headers ([4f07b71](https://github.com/snowdreamtech/python/commit/4f07b71194f58ba214f1fb60ce0dc56d71c499e2))
* **release:** deduplicate CHANGELOG headers ([3068d88](https://github.com/snowdreamtech/python/commit/3068d883bc6167773d046d3b2b0e4c479e4fee39))
* **release:** deduplicate CHANGELOG headers ([82be3d5](https://github.com/snowdreamtech/python/commit/82be3d5576b65b7f69b1a9afb8604f2c8f0e47f7))
* **release:** deduplicate CHANGELOG headers ([d47fb44](https://github.com/snowdreamtech/python/commit/d47fb44cb105b368722d7d0e210a27b525f82d87))
* **release:** deduplicate CHANGELOG headers ([e795177](https://github.com/snowdreamtech/python/commit/e79517795d98b9f8292ef956586a6dc03932d03c))
* **speckit:** manual auto-commit trigger ([5f8a5a9](https://github.com/snowdreamtech/python/commit/5f8a5a9cba5d6bd42a65eaabfecd6e18b01aeeb0))

## [3.12.13](https://github.com/snowdreamtech/python/compare/rocky-v3.12.13...rocky-v3.12.13) (2026-06-20)


### ♻️ Miscellaneous Chores

* remove test comment from Dockerfiles ([d017b0b](https://github.com/snowdreamtech/python/commit/d017b0bfa519e56f106c301cbd51c62cc86a9ce2))
