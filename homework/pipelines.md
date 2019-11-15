# Zadanie domowe - obróbka tekstu za pomocą podstawowych narzędzi systemów UNIX

W poniższym pliku znajduje się pipeline, który w przyjemny sposób pokazuję wartość prądu, który importujemy z Niemiec.

![alt text](https://i.imgur.com/kcJltGA.png)

### Polecenie skondensowane

```
wget -qO- https://www.pse.pl/transmissionMapService | sed 's/{/\n/g' | sed 1,3d | sed 's/]/\n/g' | tac | sed 1,1d | tac | sed 's:, "id.*: :g' | sed 's:"wartosc":Wartość:g' | sed 's:"rownolegly":Równoległy?:g' | sed 's:true:tak:g' | sed 's:false:nie:g' | sed 's:"wartosc_plan":Wartość planu:g'
```
### Polecenie rozbite

```
wget -qO- https://www.pse.pl/transmissionMapService \
| sed 's/{/\n/g' \
| sed 1,3d \
| sed 's/]/\n/g' \
| tac \
| sed 1,1d \
| tac \
| sed 's:, "id.*: :g' \
| sed 's:"wartosc":Wartość:g'  \
| sed 's:"rownolegly":Równoległy?:g'  \
| sed 's:true:tak:g' \
| sed 's:false:nie:g' \
| sed 's:"wartosc_plan":Wartość planu:g'
```

## Opis

1. Pobranie JSON'a za pomocą narzędzia wget, ustawionego w taki sposób aby wynik przekazał na wyjście konsoli
2. Podzielenie tekstu za pomocą narzędzia sed. Regex -> znak "{"
3. Usuniecie pierwszych trzech linijek za pomocą narzędzia sed.
4. Podzielenie tekstu za pomocą narzędzia sed. Regex -> znak "]"
5. Odwrócenie linijek tekstu
6. Usuniecie pierwszej linijki za pomocą narzędzia sed.
7. Odwrócenie linijek tekstu. Wracamy do stanu pierwotnego.

Na tym etapie mamy już w miarę czytelny i klarowny wynik.

8. Usunięcie w każdej linijce odpowiedniego tekstu za pomocą narzędzia sed. Regex -> Wszystko co zaczyna się na "\"id" aż do końca.
9. 10, 11, 12, 13. Kosmetyczne podmienianie tekstu na bardziej "polski"


