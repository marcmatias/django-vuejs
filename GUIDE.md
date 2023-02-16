# GUIDE

## Django 4

Criamos um projeto Django seguindo os passos do guia

- [Guia integração Django e Vuejs](https://github.com/rg3915/django-vuejs-02-vue-cli-static)

## LiveReload

Foi instalado o pacote livereload no Django para hotreload de templates

```bash
    pyenv exec pip install livereload
```

Com ele foi possível executar `pyenv exec python ./manage.py livereload 127.0.0.1:8000` junto com o `pyenv exec python manage.py runserver` e ter no FF as páginas tendo o hotreload a cada modificação mesmo para arquivos de template alterados pelo rebuild do Vuejs como no nosso caso, por exemplo.

Foi necessário adicionar ao `settings.py` do projeto Django

```python
if DEBUG:
    INSTALLED_APPS.append('livereload')
    MIDDLEWARE.append('livereload.middleware.LiveReloadScript')
    INTERNAL_IPS = [
        '127.0.0.1',
    ]
    LIVE_RELOAD_ENABLED = True

```

## Vuejs 3

Na parte de instalação do Vuejs seguimos gerando o projeto

```bash
    # Nas respostas setamos para usar lint prettify e rotas para projeto SPA
    npm init vue@latest
```

Acessamos a pasta do projeto

```bash
    cd frontend
```

Fazemos a primeira instalação

```bash
    npm install
```

Modificamos o arquivo `vite.config.js` para gerar projeto em pastas específicas

```javascript
import { fileURLToPath, URL } from "node:url";

import { defineConfig } from "vite";
import vue from "@vitejs/plugin-vue";

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [vue()],
  build: {
    outDir: "../core/templates",
    assetsDir: "static",
  },
  resolve: {
    alias: {
      "@": fileURLToPath(new URL("./src", import.meta.url)),
    },
  },
});
```

Modificamos o arquivo `package.json` adicionando o script para podermos ter o comando `npm run watch` que refaz o build automaticamente a cada alteração feita no front

```json
    "watch": "vite build --watch --mode development"
```
