# Registro de Testes — Versão Aprimorada

Este documento registra todos os testes executados no projeto.

---

##  **Resumo Geral da Execução**

- **Testes BDD executados:** 15 cenários  
- **Testes Frontend Unitários:** 90 testes  
- **Status geral:** 100% aprovado  
- **Ferramentas:** Vitest, Cucumber.js, Supertest, Jest Mocks  
- **Duração total:** ~3.8s

---

## **BDD – API (Back-end)**

| ID | Cenário | Status Esperado | Resultado Obtido | Status | Logs Relevantes |
|----|---------|----------------|------------------|--------|-----------------|
| BDD-01 | Criar novo usuário | 200 + mensagem de sucesso | Status 200 + “Usuário cadastrado com sucesso!” | ✅ | — |
| BDD-02 | Cadastro com e-mail existente | 409 + mensagem de erro | Status 409 + constraint Supabase | ✅ | duplicate key (Supabase) |
| BDD-03 | Login válido | 200 + token | Status 200 + token `visit` | ✅ | __ |
| BDD-04 | Login com senha incorreta | 400 | Status 400 + “Senha incorreta!” | ✅ | — |
| BDD-05 | Login com usuário inexistente | 400 | Status 400 + “Usuário não encontrado” | ✅ | — |
| BDD-06 | Listar imóveis | 200 | Status 200 + lista | ✅ | — |
| BDD-07 | Imóvel por ID | 200 | Status 200 + detalhes | ✅ | — |
| BDD-08 | Criar imóvel | 200 + mensagem | Status 200 + “Imóvel inserido com sucesso" | ✅ | — |
| BDD-09 | Atualizar imóvel | 200 | Status 200 + valor atualizado | ✅ | — |
| BDD-10 | Soft delete | 200 | Status 200 + ativo=false | ✅ | — |
| BDD-11 | Reativar imóvel | 200 | ativo=true | ✅ | — |
| BDD-12 | Deletar imóvel | 200 | “Imóvel removido com sucesso” | ✅ | — |
| BDD-13 | Obter coordenadas | 200 | lat + lon presentes | ✅ | — |
| BDD-14 | Filtro venda | 200 | Lista com 1 imóvel | ✅ | — |
| BDD-15 | Filtro aluguel | 200 | Lista com imóveis tipo Apartamento | ✅ | — |

---

##  **Testes Unitários — Frontend**

###  Resumo de Cobertura
| Id | Página/Componente | RESULTADO/ESPERADO | RESULTADO/OBTIDO | Resultado | Observações |
|-------------------|-----------|-------------|-------------|-------------|-------------|
| FE-01 | Alert | enderização e funcionamento | O componente é renderizado corretamente com base nas props | Todos passaram | — |
| FE-02 | AnuncioCard | Renderização e interaçõe | O card exibe os dados do imóvel e os botões de interação | Todos passaram | — |
| FE-03 | Carrossel | Renderização e navegação | O carrossel é renderizado com os slides e a navegação funciona | Todos passaram | — |
| FE-04 | Header | Renderização condicional | O header exibe o logo e o link de usuário corretamente | Todos passaram | — |
| FE-05 | MapView | Renderização e busca de coords | O mapa é renderizado e as coordenadas são buscadas | Todos passaram | — |
| FE-06 | Sidebar | Renderização e navegação | A sidebar é renderizada e os links de navegação funcionam | Todos passaram | — |
| FE-07 | CreateItem | Validação e submissão de formulário | O formulário valida os campos e envia os dados para a API | Todos passaram | — |
| FE-08 | DeleteItem | Listagem e restauração/exclusão | A página lista imóveis inativos e permite reativar ou excluir | Todos passaram | Erros simulados corretamente (“Erro na resposta do servidor”) |
| FE-09 | EditItem | Carregamento de dados e atualização | A página carrega dados do imóvel, permite edição e salva | Todos passaram | — |
| FE-10 | Home | Renderização e filtros | A página principal é renderizada e os filtros de busca funcionam | Todos passaram | — |
| FE-11 | Login | Autenticação e redirecionamento | A página permite login, valida credenciais e redireciona | Todos passaram | __ |
| FE-12 | Main | Renderização e busca | A página de busca principal renderiza e exibe resultados | 90/90 testes passaram |  |
| FE-13 | PainelAdm | Acesso e gerenciamento de imóveis | A página protege o acesso e permite editar/deletar imóveis | Todos passaram | Logs mostraram mocks de lista: `[ { id: 1, descricao: 'Casa 1'} ]` |
| FE-14 | Filtro | Renderização e funcionamento do filtro | O componente renderiza os campos de filtro e atualiza o estado | Todos passaram | — |
| FE-15 | AnuncioPage | Renderização dos detalhes do anúncio | A página carrega e exibe as informações de um imóvel específico | Todos passaram | — |



