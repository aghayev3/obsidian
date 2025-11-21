# Enumerating SSH

When we try `ssh 192.168.0.134` and get this:

```
Unable to negotiate with ... No matching key exchange method found. Their offer: ...
```

we can do `ssh 192.168.0.134 -oKexAlgorithms=+<their offer>`

no matching cipher found

so we add to the command ``ssh 192.168.0.134 -oKexAlgorithms=+<their offer> -c <cipher`

We don't exploit at this point, we're just trying to see if there is a banner