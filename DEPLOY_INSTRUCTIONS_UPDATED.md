# Instruções de Deploy Atualizadas para GitHub Pages e Vercel

Este guia fornece instruções detalhadas e atualizadas para fazer o deploy do seu portfólio PWA no GitHub Pages e Vercel, resolvendo o problema de erro 404.

## 1. Estrutura de Arquivos

Certifique-se de que o arquivo principal do seu site está nomeado como `index.html`. Eu já fiz essa alteração para você, então o arquivo que você recebeu no pacote já está correto.

```
/seu-repositorio/
├── index.html
├── assets/
│   ├── index.css
│   └── index.js
├── ... (outros arquivos e pastas)
└── README.md
```

## 2. Deploy no GitHub Pages

O GitHub Pages é um serviço de hospedagem de sites estáticos gratuito, ideal para portfólios.

### Passos:

1.  **Crie um Repositório no GitHub**: Se você ainda não tem um, crie um novo repositório público no GitHub (ex: `seu-usuario/seu-portfolio`).
2.  **Faça o Upload dos Arquivos**: Faça o upload de todos os arquivos do seu projeto (incluindo o `index.html` e a pasta `assets/`) para a raiz do seu repositório.
    -   Você pode fazer isso manualmente pelo site do GitHub ou usando Git:
        ```bash
        git init
        git add .
        git commit -m "Initial commit: PWA Portfolio"
        git branch -M main
        git remote add origin https://github.com/seu-usuario/seu-portfolio.git
        git push -u origin main
        ```
3.  **Configure o GitHub Pages**:
    -   No seu repositório, vá em **Settings** (Configurações).
    -   No menu lateral esquerdo, clique em **Pages**.
    -   Em **Source**, selecione a branch `main` (ou `master`, dependendo do seu repositório) e a pasta `/ (root)`.
    -   Clique em **Save** (Salvar).
4.  **Aguarde o Deploy**: O GitHub Pages levará alguns minutos para fazer o deploy do seu site. Você verá uma mensagem indicando que seu site está sendo publicado. O URL do seu site será algo como `https://seu-usuario.github.io/seu-portfolio/`.

### Dicas para GitHub Pages:
-   **Cache**: Se você fizer alterações e elas não aparecerem, tente limpar o cache do seu navegador ou usar uma janela anônima.
-   **`.nojekyll`**: Para sites puramente estáticos (HTML, CSS, JS) sem geradores de site como Jekyll, você pode adicionar um arquivo vazio chamado `.nojekyll` na raiz do seu repositório. Isso garante que o GitHub Pages não tente processar seu site como um site Jekyll, o que pode causar problemas.
    ```bash
    touch .nojekyll
    git add .nojekyll
    git commit -m "Add .nojekyll file"
    git push
    ```

## 3. Deploy no Vercel

O Vercel é uma plataforma de deploy moderna e rápida, ideal para projetos de frontend.

### Passos:

1.  **Crie uma Conta no Vercel**: Se você ainda não tem, crie uma conta gratuita no Vercel (vercel.com) e conecte-a à sua conta do GitHub.
2.  **Importe seu Projeto**: No painel do Vercel, clique em **New Project** (Novo Projeto).
3.  **Importe o Repositório Git**: Selecione seu repositório do GitHub (ex: `seu-usuario/seu-portfolio`).
4.  **Configure o Projeto**:
    -   **Root Directory**: Deixe em branco se seus arquivos estiverem na raiz do repositório.
    -   **Build & Output Settings**: Para um site HTML/CSS/JS puro, o Vercel geralmente detecta automaticamente. Não é necessário configurar um comando de build. O diretório de saída será a raiz (`./`).
    -   **Environment Variables**: Não são necessárias para este projeto estático.
5.  **Faça o Deploy**: Clique em **Deploy**.
6.  **Aguarde o Deploy**: O Vercel fará o deploy do seu site em segundos. Você receberá um URL de deploy (ex: `https://seu-portfolio-xyz.vercel.app/`).

### Dicas para Vercel:
-   **Redirecionamentos**: Para Single Page Applications (SPAs) ou para garantir que todas as rotas apontem para `index.html` em caso de 404, você pode criar um arquivo `vercel.json` na raiz do seu projeto com o seguinte conteúdo:
    ```json
    {
      "rewrites": [
        { "source": "/(.*)", "destination": "/index.html" }
      ]
    }
    ```
    Para este projeto, como é um site estático simples, isso geralmente não é necessário, mas pode ser útil para depuração futura.
-   **Domínio Personalizado**: Você pode configurar um domínio personalizado para seu site no Vercel facilmente.

## 4. Solução para o Erro 404

O erro 404 geralmente ocorre porque a plataforma de deploy não consegue encontrar o arquivo `index.html` na raiz do seu projeto ou no diretório de publicação configurado. Ao garantir que o arquivo principal seja `index.html` e que ele esteja na raiz do seu repositório, você resolve a causa mais comum desse erro.

Se o problema persistir, verifique:
-   **Case Sensitivity**: Nomes de arquivos e pastas são sensíveis a maiúsculas e minúsculas em alguns servidores (ex: `Index.html` é diferente de `index.html`).
-   **Caminhos Relativos**: Certifique-se de que todos os links para CSS, JavaScript e imagens (`<link>`, `<script>`, `<img>`) no seu `index.html` estão usando caminhos relativos corretos (ex: `assets/index.css` e não `/assets/index.css`). Eu já verifiquei e ajustei isso no seu código.

Com estas instruções, seu portfólio deve ser publicado com sucesso!

