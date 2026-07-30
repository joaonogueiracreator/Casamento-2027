# 💍 Nosso Casamento

App para acompanhar custos, parcelas e o enxoval do casamento — com os dados salvos na nuvem (Supabase) e sincronizados entre os aparelhos dos noivos.

## Como colocar no ar (passo a passo)

### Parte 1 — Supabase (banco de dados + login)

1. No painel do seu projeto, abra **SQL Editor → New query**, cole todo o conteúdo do arquivo `schema.sql` e clique em **Run**.
2. Abra **Authentication → Users → Add user → Create new user**. Defina o **e-mail e senha** que vocês dois vão usar para entrar (marque *Auto Confirm User*).
3. Abra **Project Settings → Data API** e copie o **Project URL**.
4. Abra **Project Settings → API Keys** e copie a chave **anon / public** (pode aparecer como *publishable*).
5. No `index.html`, no comecinho do `<script>`, cole os dois valores:
   ```js
   const SUPABASE_URL      = 'https://xxxxx.supabase.co';
   const SUPABASE_ANON_KEY = 'a-chave-anon-aqui';
   ```
6. Abra o `index.html` no navegador e entre com o e-mail e senha do passo 2. Deve funcionar.

### Parte 2 — GitHub (hospedar de graça)

1. Crie um repositório novo no GitHub (pode ser público — veja a nota de segurança abaixo).
2. **Add file → Upload files** e arraste **todos** estes arquivos juntos (o app e os ícones da tela inicial precisam ficar na mesma pasta):
   - `index.html`
   - `manifest.webmanifest`
   - `apple-touch-icon.png`
   - `icon-192.png`
   - `icon-512.png`

   Confirme com *Commit changes*. (O `README.md` e o `schema.sql` são opcionais — o `schema.sql` é usado só dentro do Supabase.)
3. Vá em **Settings → Pages**, em *Source* escolha a branch `main` e a pasta `/root`, e salve.
4. Em ~1 minuto o GitHub mostra o endereço do site (algo como `https://seu-usuario.github.io/nome-do-repo/`). Abram esse link no celular e salvem na tela inicial.

## É seguro deixar as chaves no arquivo público?

Sim. A chave **anon** do Supabase foi feita para ficar visível no navegador — ela sozinha não dá acesso a nada. Quem protege os dados é o **RLS** (as regras do `schema.sql`) somado ao **login**: sem e-mail e senha, ninguém lê nem grava. Só **nunca** coloque a chave *service_role* / *secret* aqui.

## Bom saber

- **Offline:** o app sempre guarda uma cópia no próprio aparelho; quando a internet volta, ele sincroniza sozinho.
- **Backup:** em *Ajustes* dá para baixar/importar um arquivo `.json` com tudo, como rede de segurança.
- **Atualização entre vocês:** ao reabrir o app, ele puxa a versão mais recente. Se os dois editarem exatamente ao mesmo tempo, vale a última alteração salva.
