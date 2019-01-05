There are two types of request tokens. The first one has been documented everywhere, but the second one has no documentation as far as I can see. Tokenv1 has a simple implementation in Python:
```
def request_token(self, auth_token, timestamp):
		secret = "iEk21fuwZApXlz93750dmW22pw389dPwOk"
		pattern = "0001110111101110001111010101111011010001001110011000110001000110"
		first = hashlib.sha256((secret + auth_token).encode("UTF-8")).hexdigest()
		second = hashlib.sha256((str(timestamp) + secret).encode("UTF-8")).hexdigest()
		bits = [first[i] if c == "0" else second[i] for i, c in enumerate(pattern)]
		return "".join(bits)
```
Tokenv2 seems to be a superset of tokenv1. Tokenv2 is 162 characters long. Given the same timestamp and auth_token, the first 64 characters of tokenv2 are the same as the first 64 of tokenv1. Tokenv2 is never used with the static token, and therefore is never used before login. 

Comparison of tokenv1 and tokenv2 (tokenv2 is on the bottom, duh)
```
7c173b5c08e9d6fe162d45260e5fbd400c675fe6fbee4afb3651c3d8fdcd70fe
7c173b5c08e9d6fe162d45260e5fbd400c675fe6fbee4afb3651c3d8fdcd70fe546261356062346365353c663937646133f11eb30beef18cd00e54d739553358b3dd702400234b292dea3c9d47cef08644
```
Tokenv1 seems to be used on iOS exclusively and on Android, before login is completed. Using the static token you can find at [GibSec full disclosure](http://gibsonsec.org/snapchat/fulldisclosure/)