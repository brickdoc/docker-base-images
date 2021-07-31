# Brickdoc Docker Base Images

## Images List

- [ruby-3](ruby-3/Dockerfile)

## Why Ubuntu 20.04?

`ubuntu-20.04` is one of the [available environment](https://github.com/actions/virtual-environments#available-environments) of Github Actions. Using cross-compilation and [github action cache](https://docs.github.com/en/actions/guides/caching-dependencies-to-speed-up-workflows) helps seepd up the build of our application images.

Specifically this allows us to complete the dependencies installation via the github action with caching and then add the dependencies files to the docker image.

## License

Copyight (c) 2021 Brickdoc (Ningbo) Cloud Computing Technology LTD

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

[http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
