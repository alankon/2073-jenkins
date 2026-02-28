# Leilão (Spring Boot)

Aplicação web de leilões construída com Spring Boot, Thymeleaf, Spring Security e banco H2 em memória.

## O que este projeto faz

- Cadastro e listagem de leilões.
- Registro de lances nos leilões.
- Autenticação de usuários.
- Finalização de leilões expirados com definição de lance vencedor.

## Entendendo a estrutura

- `src/main/java/br/com/alura/leilao/controller`: endpoints web (telas e ações).
- `src/main/java/br/com/alura/leilao/service`: regras de negócio (lances, pagamento, finalização).
- `src/main/java/br/com/alura/leilao/dao`: acesso a dados com Spring Data JPA.
- `src/main/java/br/com/alura/leilao/model`: entidades de domínio (`Leilao`, `Lance`, `Usuario`, etc.).
- `src/main/resources/templates`: páginas Thymeleaf.
- `src/main/resources/data.sql`: dados iniciais para execução local.
- `src/test/java`: testes unitários com JUnit + Mockito.

## Melhoria aplicada

Foi adicionada uma proteção no serviço de finalização para tratar leilões sem lances:

- o leilão é fechado normalmente;
- o lance vencedor não é definido (`null`);
- nenhum e-mail é enviado para vencedor inexistente.

Com isso, evita-se erro em tempo de execução ao finalizar leilões expirados sem propostas.

## Como rodar

### Pré-requisitos

- Java 8+
- Maven 3.6+

### Passos

1. Instale as dependências e rode os testes:

```bash
mvn test
```

2. Suba a aplicação:

```bash
mvn spring-boot:run
```

3. Acesse no navegador:

- `http://localhost:8080/leiloes`

## Usuários de exemplo

Os usuários são carregados por `data.sql`.

- usuário: `fulano`
- usuário: `ciclano`
- usuário: `beltrano`
- senha (todos): `123456`

> As senhas estão salvas com BCrypt no banco H2 em memória.

## Como usar (fluxo rápido)

1. Abra `/leiloes` para ver os leilões cadastrados.
2. Faça login em `/login` com um usuário de exemplo.
3. Crie um novo leilão.
4. Entre em um leilão e faça lances.
5. Execute os testes para validar regras de negócio:

```bash
mvn test
```

## Próximas melhorias sugeridas

- Agendar automaticamente a finalização de leilões com `@Scheduled`.
- Adicionar testes de integração para controllers.
- Melhorar rastreabilidade com logs estruturados.
