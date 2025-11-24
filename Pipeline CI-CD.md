# Pipeline CI/CD

O pipeline CI/CD combina **GitHub Actions** para Integração Contínua e as ferramentas nativas do **[Render](render.com)** para o Deploy Contínuo. Essa abordagem permite um fluxo totalmente automatizado desde o momento do commit até a publicação de novas versões em produção.

------

## CI — Integração Contínua

A CI é implementada por meio de um workflow GitHub Actions definido em arquivo `.yaml`. Esse workflow é executado automaticamente sempre que ocorrer:

- um **push** nas branchs `main` ou `dev`;
- a abertura de um **pull request** direcionado para `main` ou `dev`.

O objetivo é validar o código antes da fusão ou publicação, garantindo confiabilidade.

### **Pipeline CI — Workflow YAML**

```yaml
name: Pipeline CI

on:
  push:
    branches:
      - main
      - dev

  pull_request:
    branches:
      - main
      - dev

jobs:
  build_and_test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Set up Node.js
        uses: actions/setup-node@v4
        with:
          node-version: "20.*"
          cache: "npm"

      - name: Install Frontend Dependencies
        run: npm install

      - name: Test Frontend
        run: npm test

      - name: Build Frontend
        run: npm run build

      - name: Install Backend Dependencies
        working-directory: ./src/api
        run: npm install

      - name: Test Backend
        working-directory: ./src/api
        env:
          SUPABASE_URL: ${{ secrets.SUPABASE_URL }}
          SUPABASE_KEY: ${{ secrets.SUPABASE_KEY }}
          LOCATIONIQ_API_KEY: ${{ secrets.LOCATIONIQ_API_KEY }}
          JWT_SECRET: ${{ secrets.JWT_SECRET }}
        run: npm test
```

### **Este workflow garante**

- Validação automática do backend e frontend.
- Testes executados com variáveis de ambiente seguras via **GitHub Secrets**.
- Build gerado antes do deploy, evitando falhas em produção.

------

## CD — Deploy Contínuo

A entrega contínua (CD) é realizada diretamente pela plataforma **Render**, que está integrada ao repositório GitHub.

- A cada commit na branch configurada ( `main`), o Render inicia automaticamente um novo deploy.
- Variáveis de ambiente e configurações de runtime são definidas diretamente no painel da plataforma.
- O Render reconstrói a aplicação, instala dependências e realiza o build antes de colocar a nova versão no ar.

### **Capturas de Configuração (Render)**

![Configuração Render 1](https://qdktamaxnvzecqpwzbmr.supabase.co/storage/v1/object/public/imoveis-imagens/imagens/docs/Screenshot_2025-11-22_10-30-29.png)

![Configuração Render 2](https://qdktamaxnvzecqpwzbmr.supabase.co/storage/v1/object/public/imoveis-imagens/imagens/docs/Screenshot_2025-11-22_10-30-59.png)

------

## Conclusão

Combinando GitHub Actions e Render, conseguimos um pipeline CI/CD robusto, simples de manter e totalmente automatizado. Esse fluxo garante qualidade constante, rapidez nas entregas e segurança no processo de publicação.