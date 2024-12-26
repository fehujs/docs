# Parsing

## ``parseBase(delimiter1: string, delimiter2: string, raw: string): Record<string, string> {``

This function is the base for all data type that can be parsed by splitting only two times a string, like cookies or request body.

Example:

```txt
key1=val&key2=val2&...&keyN=valN
```

Here, the first delimiter would be "&" because it delimits couples key-value, the second one would be "=" because it delimits keys from values.

## ``parseCookieData(raw: string | undefined): Record<string, string>``

Helper calling ``parseBase`` for request's cookies parsing.

In this case, we have a ``raw`` like this:

```txt
cookie1=value1;cookie2=value2
```
