---
layout: default
title: Estilos de ejemplo
nav_order: 999
permalink: /style-demo/
---

# Demo de estilos (Just the Docs — Style Pack)

<span class="badge">Nuevo</span> <span class="badge success">OK</span> <span class="badge warning">Atención</span> <span class="badge danger">Importante</span>

<div class="callout">
  <div class="title">Nota</div>
  Este es un callout básico con acento de marca.
</div>

<div class="callout success">
  <div class="title">Éxito</div>
  Todo salió bien.
</div>

<div class="callout warning">
  <div class="title">Advertencia</div>
  Revisa la configuración antes de continuar.
</div>

<div class="callout danger">
  <div class="title">Peligro</div>
  Acción destructiva: procede con cuidado.
</div>

## Rejilla de tarjetas
<div class="grid-cards">
  <a class="card" href="{{ '/temario/00_sistemas_de_numeracion/' | relative_url }}">
    <div class="card-title">Sistemas de numeración</div>
    <div class="card-meta">Unidad 00</div>
    <div>Binario, octal, hex, TFN y conversiones.</div>
  </a>
  <a class="card" href="{{ '/temario/01_conectores_en_placa/' | relative_url }}">
    <div class="card-title">Conectores en placa</div>
    <div class="card-meta">Unidad 01</div>
    <div>USB internos, audio frontal, panel y más.</div>
  </a>
  <a class="card" href="{{ '/' | relative_url }}">
    <div class="card-title">Inicio</div>
    <div class="card-meta">Portada</div>
    <div>Ir a la página principal.</div>
  </a>
</div>

## Enlaces y código
Texto con un [enlace de ejemplo]({{ '/temario/' | relative_url }}) y `código inline`.
```bash
# Código con resaltado y borde de acento
git add .
git commit -m "Estilo nuevo"
git push
```
