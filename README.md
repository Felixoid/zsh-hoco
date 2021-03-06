![Great curassow, image designed by rawpixel.com / Freepik](./docs/hoco.png)

# HOCO - zsh hosts completion
Small function to improve and extend original zsh `_hosts` completion function.

## Objectives
The original zsh hosts completion is not extendable. And when you replace it with `zstyle -e ':completion:*:hosts' hosts 'reply=(...)'`, all original completions should be represented too.

On the other hand, `_hosts` caches all hosts for autocompletion only once, and then uses it. And it's not so obvious how to reset it.

## Solution
The [hoco.zsh](./hoco.zsh) solves both `_hosts` flaws:

- It updates the cache once per `$HOCO_CACHE_AGE` period, the default is 10 minutes
- It allows to update list of hosts dynamically. Each binary or function in `$HOCO_FUNCTIONS` array is executed asynchronously. The list of hosts for completion is updated on readiness.

### Usage

The only thing you need to do is:

```
source hoco.zsh
some-function() {
  echo host1 host2 # it does not matter if hosts are separated by spaces
  echo host3	host4 # or by new lines (LF), or by tabs
}
HOCO_FUNCTIONS=(some-function)

ssh <tab>
```
