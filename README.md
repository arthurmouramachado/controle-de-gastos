# controle-de-gastos
Aplicação web para controle de despesas/receitas usando Spring Boot + Thymeleaf + HTMX.

## Tecnologias
- Java 21, Spring Boot, Spring Data JPA
- Thymeleaf + HTMX
- H2 (dev) / PostgreSQL (prod)
- Docker, Render

## Como rodar localmente
1. `./mvnw spring-boot:run`
2. Acesse `http://localhost:8080`

## Docker
```bash
docker build -t controledegastos .
docker run -p 8080:8080 controledegastos


---

# Deploy no Render (passo a passo prático)
1. Faça login no Render e clique em **New → Web Service**.  
2. Conecte sua conta GitHub e selecione o repositório.  
3. Em **Name** digite exatamente `controledegastos-SeuNomeSobrenome` (substitua pelo seu nome) — assim o URL será `https://controledegastos-SeuNomeSobrenome.onrender.com`. :contentReference[oaicite:8]{index=8}  
4. Em **Environment** escolha **Docker** (o tutorial usa Docker). Quando usa Docker, deixe `Build Command` e `Start Command` vazios (Render usará seu Dockerfile). :contentReference[oaicite:9]{index=9}  
5. Em **Environment Variables** adicione:
   - `SPRING_PROFILES_ACTIVE = prod`  
   - `DB_URL = jdbc:postgresql://<host>:5432/<db>`  (use a URL do Neon/DB que você criar)  
   - `DB_USERNAME`  
   - `DB_PASSWORD`
6. Clique em **Create Web Service**. O Render iniciará o build.  
7. Se usar Neon (ou outro Postgres gerenciado), pegue a string de conexão e preencha `DB_URL` exatamente como JDBC (ou copie o valor provido). :contentReference[oaicite:10]{index=10}

**Dica:** se o build falhar por `MalformedInputException`, aplique os passos do README (limpar `application.properties` e garantir UTF-8 + prop no `pom.xml`). :contentReference[oaicite:11]{index=11}

---

# Problemas comuns & soluções rápidas
- **Build falha por mvnw não executável** → `git update-index --chmod=+x mvnw`, commit e push. :contentReference[oaicite:12]{index=12}  
- **MalformedInputException (codificação)** → salve `application.properties` em UTF-8 e garanta `<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>` no `pom.xml`. :contentReference[oaicite:13]{index=13}  
- **Banco de produção** → use Neon ou outro Postgres; defina variáveis no Render e rode com `SPRING_PROFILES_ACTIVE=prod`.

---

