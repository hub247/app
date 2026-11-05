# Gym WP — Treinos Thiago & Natália

App de academia em HTML puro (sem React, sem instalar nada), no mesmo layout do `gym_wp_mfit_hybrid_workout_app.tsx`:
perfis Thiago/Natália, Fase 1/Fase 2, fichas, mapa muscular, YouTube Shorts por exercício, registro de séries, timer, nutrição e métricas.

## Publicar no GitHub Pages
1. Crie um repositório (ex.: `gym-wp`).
2. **Add file → Upload files** → envie `index.html`, `manifest.json`, `sw.js`, `icon.svg` → **Commit**.
3. **Settings → Pages** → Branch `main` / `(root)` → **Save**.
4. Link: `https://SEU-USUARIO.github.io/gym-wp/` → no celular, **Adicionar à tela inicial**.

## Vídeos
- Os IDs de YouTube vieram do arquivo .tsx de referência. Abra cada um e confirme se o vídeo é o certo.
- Exercício sem vídeo: **Buscar** → escolha um Short → copie o link → **Colar link**.
- Para fixar no código: edite `yt:"ID_DE_11_CARACTERES"` no exercício.

## Atualizar
Edite `THIAGO` ou `NAT_DAYS` no `index.html`. Ao publicar nova versão, troque `gymwp-v1` para `gymwp-v2` no `sw.js`.

Os dados ficam salvos no próprio celular. Use **Métricas → Exportar** para backup.
