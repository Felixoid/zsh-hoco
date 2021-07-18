![Great curassow, image designed by rawpixel.com / Freepik](./docs/hoco.png)

# HOCO - zsh hosts completion
Small function to improve and extend original zsh `_hosts` completion function.

## Objectives
The original zsh hosts completion is not extendable. And when you replace it with `zstyle -e ':completion:*:hosts' hosts 'reply=(...)`, all original completions should be represented too.

On the other hand, `_hosts` caches all hosts for autocompletion only once, and then uses it. And it's not so obvious how to reset it.

## Solution
The [hoco.zsh](./hoco.zsh) solves both `_hosts` flaws:

- It updates the cache once per `$HOCO_CACHE_TTL` period (600 by default)
- It allows to update list of hosts dynamically. Each binary or function in `$HOCO_FUNCTIONS` array is executed asynchronously via [zsh-async](https://github.com/mafredri/zsh-async). The list of hosts for completion is updated on readiness.
