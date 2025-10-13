# Fix de logo para Just the Docs

## 1) Copia este archivo en tu repo
Ruta: `_sass/custom/custom.scss`

> Si no existen las carpetas, créalas tal cual (`_sass/custom/`).

## 2) Verifica la ruta del logo en `_config.yml`
Debe existir una línea como:
```
logo: "/assets/logo.png"
```
y el archivo real en `assets/logo.png` (respetando mayúsculas/minúsculas).

Si tu sitio es de tipo "project site" (URL `https://TU_USUARIO.github.io/NOMBRE_REPO/`):
```
baseurl: "/NOMBRE_REPO"
```
Copia EXACTO el nombre del repo (respetar guiones y mayúsculas).

## 3) Prueba rápida en `index.md`
Añade temporalmente estas líneas para comprobar la imagen directa:
```
![Test 1]({{ "/assets/logo.png" | relative_url }})
![Test 2]({{ site.baseurl }}/assets/logo.png)
```
- Si **Test 1** carga, la imagen y el `baseurl` están bien.
- Si carga el **Test 2** pero no el 1, revisa `baseurl`.
- Si ninguna carga, revisa que `assets/logo.png` exista de verdad (ruta y nombre).

## 4) Publica
Haz commit/push y espera a que GitHub Pages recompilen (normalmente <2 min).
Luego limpia caché/recarga dura (Ctrl+F5 / ⌘+Shift+R).
