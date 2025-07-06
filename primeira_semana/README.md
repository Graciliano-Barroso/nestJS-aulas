# 🗂️ Plano de Estudo – Nest.js (Semana 1)

> 🎯 Objetivo: Entender a arquitetura do Nest.js, saber criar módulos, controladores e serviços, e iniciar uma API RESTful organizada.

---

### 🛠️ Pré-requisitos antes de começar:

- Node.js instalado

- Conhecimento básico de TypeScript

- Comandos básicos de terminal

- Editor (VS Code)

---

### 📦 Instalação do Nest.js CLI

```bash
npm i -g @nestjs/cli
nest new projeto-tarefas
```

---

## 🗓️ Dia 1 – Introdução ao Nest.js

### 📚 Conteúdo:

- O que é Nest.js e por que usá-lo?

- Arquitetura baseada em módulos e injeção de dependência

- Como funciona o padrão MVC no Nest

- Primeira execução de um projeto

### 🔧 Atividades:

- Instalar o Nest CLI e criar projeto com `nest new`

- Explorar os arquivos gerados (`main.ts`, `app.module.ts`, etc.)

- Rodar o servidor: `npm run start:dev`

### 🧪 Exercício:

Adicionar um `console.log()` no `main.ts` para verificar o ambiente.

---

## 🗓️ Dia 2 – Controladores (Controllers)

### 📚 Conteúdo:

- O que são controladores

- Decoradores como `@Controller()` e `@Get()`

- Rotas e parâmetros de rota

### 🔧 Atividades:

- Criar um controlador `tarefas.controller.ts`:

```bash
nest g controller tarefas
```

- Criar métodos `GET /tarefas`, `GET /tarefas/:id`

### 🧪 Exercício:

Adicionar mais uma rota: `GET /tarefas/status/:status`

---

## 🗓️ Dia 3 – Serviços (Services)

### 📚 Conteúdo:

- O que são serviços

- `@Injectable()`: como funciona a injeção de dependência

- Separando a lógica de negócio

### 🔧 Atividades:

Criar serviço `tarefas.service.ts`:

```bash
nest g service tarefas
```

- Mover lógica de listagem de tarefas para o serviço

### 🧪 Exercício:

Criar um método `getTarefaPorId(id: string)` no serviço e usá-lo no controller

---

## 🗓️ Dia 4 – DTOs e Tipagem

### 📚 Conteúdo:

- Criando interfaces ou classes para tipos

- O que é DTO (Data Transfer Object)

- Validação básica de dados com TypeScript

### 🔧 Atividades:

- Criar DTO `create-tarefa.dto.ts` com `titulo` e `descricao`

- Criar tipo `Tarefa` com status enum

### 🧪 Exercício:

🧪 Exercício:
Adicionar lógica para `POST /tarefas` com DTO

---

## 🗓️ Dia 5 – Injeção de dependência e boas práticas

### 📚 Conteúdo:

- Injeção de serviços com o `constructor()`

- Boa prática: separar DTOs, entidades, módulos

- Criar status enum para tarefas: `ABERTA`, `EM_ANDAMENTO`, `FINALIZADA`

### 🔧 Atividades:

- Atualizar o método `createTarefa()` para usar status padrão `ABERTA`

### 🧪 Exercício:

- Criar um método `filtrarTarefasPorStatus(status: string)`

---

## 🗓️ Dia 6 – Módulos

### 📚 Conteúdo:

- Entendendo o que são módulos

- Dividindo responsabilidades por domínio

- Reutilização de módulos em aplicações grandes

### 🔧 Atividades:

- Criar novo módulo para tarefas (caso não tenha sido criado junto com controller):

```bash
nest g module tarefas
```

- Garantir que o módulo está importando controller e serviço corretamente

---

## 🗓️ Dia 7 – Revisão e prática

### 📚 Conteúdo:

- Revisar: controller → chama → service → retorna resposta

- Criar mini projeto de API de tarefas (em memória, sem banco de dados)

### 🧪 Exercício final da semana:

Criar uma API de tarefas com os seguintes endpoints:

- `GET /tarefas`: listar todas

- `GET /tarefas/:id`: listar por ID

- `POST /tarefas`: criar tarefa

- `DELETE /tarefas/:id`: remover tarefa

- `PATCH /tarefas/:id/status`: atualizar status

---

### 📦 Pastas organizadas no final da semana:

```lua
src/
├── tarefas/
│   ├── dto/
│   │   └── create-tarefa.dto.ts
│   ├── tarefas.controller.ts
│   ├── tarefas.service.ts
│   ├── tarefas.module.ts
├── main.ts
└── app.module.ts
```

---
---

# 🗂️ Plano de Estudo – Nest.js (Semana 2)

> 🎯 Objetivo: Aprimorar sua API com validações, autenticação básica, tratamento de erros e preparar para integração com banco de dados (TypeORM).

---

## 🗓️ Dia 8 – Pipes e validação de dados

### 📚 Conteúdo:

- O que são Pipes no Nest.js

- Usando `@Body()` com DTOs

- Usando `class-validator` e `class-transformer`

### 🔧 Atividades:

- Instalar os pacotes:

```bash
npm install class-validator class-transformer
```

- Criar validador no `create-tarefa.dto.ts`:

```typescript
import { IsString, IsEnum } from 'class-validator';

export class CreateTarefaDto {
  @IsNotEmpty()
  titulo: string;

  @IsNotEmpty()
  descricao: string;
}
```

### 🧪 Exercício:

- Criar um `FilterDto` para buscar tarefas por `status` e `termo` com validação usando `@IsOptional()`.

---

## 🗓️ Dia 9 – Pipes customizados

### 📚 Conteúdo:

- Criar um pipe de validação de status

- Usar `@Param()` com pipes

### 🔧 Atividades:

- Criar `TarefaStatusValidationPipe`

- Validar se `status` recebido é válido (enum)

### 🧪 Exercício:

- Adicionar pipe no endpoint `PATCH /tarefas/:id/status`

---

## 🗓️ Dia 10 – Exception Filters (tratamento de erros)

### 📚 Conteúdo:

- O que são filtros de exceção

- Usando HttpException e NotFoundException

- Criar filtro global customizado (opcional)

### 🔧 Atividades:

- Criar exceção personalizada se uma tarefa não for encontrada.

```typescript
throw new NotFoundException(`Tarefa com ID "${id}" não encontrada`);
```

### 🧪 Exercício:

Adicionar exceções personalizadas para os métodos `GET`, `DELETE` e `UPDATE`.

---

## 🗓️ Dia 11 – Middleware

### 📚 Conteúdo:

- O que é middleware no Nest.js

- Diferença entre middleware, guards e interceptadores

- Aplicar middleware globalmente ou por rota

### 🔧 Atividades:

- Criar middleware de log:

```bash
nest g middleware logger
```

- Aplicar nas rotas de tarefas

### 🧪 Exercício:

- Adicionar timestamp e rota acessada no log.

---

## 🗓️ Dia 12 – Guards (autenticação básica)

### 📚 Conteúdo:

- O que são guards

- Criar um guard simples (ex: autenticação via token hardcoded)

- Usar `@UseGuards()` no controller

### 🔧 Atividades:

- Criar `AuthGuard` que verifica se `authorization` tem token `meutoken123`.

### 🧪 Exercício:

- Proteger rota de criação de tarefas com guard.

---

## 🗓️ Dia 13 – Configuração com .env e instalação de TypeORM

## 📚 Conteúdo:

- Uso do pacote `@nestjs/config`

- Criar `.env` para credenciais de banco

- Instalar pacotes do TypeORM

```bash
npm install --save @nestjs/typeorm typeorm pg
```

### 🔧 Atividades:

- Criar `.env`:

```env
DB_HOST=localhost
DB_PORT=5432
DB_USERNAME=usuario
DB_PASSWORD=senha
DB_NAME=nest_tarefas
```

- Configurar `TypeOrmModule.forRootAsync()` em `app.module.ts`

### 🧪 Exercício:

- Simular a conexão (sem entidades ainda), garantir que app inicia com sucesso.

---

## 🗓️ Dia 14 – Preparar para uso do banco com TypeORM

### 📚 Conteúdo:

- O que são entidades

- Introdução a decorators do TypeORM

- Diferença entre entidades e DTOs

- Visão geral de `repository`, `migration`, `relation`

## 🔧 Atividades:

- Criar a primeira entidade `TarefaEntity` com os campos `id`, ``titulo``, ``descricao``, ``status``, ``dataCriacao``.

```ts
@Entity()
export class Tarefa {
  @PrimaryGeneratedColumn('uuid')
  id: string;

  @Column()
  titulo: string;

  @Column()
  descricao: string;

  @Column()
  status: TarefaStatus;

  @CreateDateColumn()
  dataCriacao: Date;
}
```

---

### 🧠 Ao final da semana, você terá:

✅ API validando dados
✅ Erros tratados corretamente
✅ Middleware e autenticação básica funcionando
✅ Projeto pronto para usar TypeORM com banco de dados real

---
---

# 🗂️ Plano de Estudo – Nest.js (Semana 3)

> 🎯 Objetivo: Persistência com banco de dados usando TypeORM, criação de entidades, relacionamento, autenticação com JWT e finalização de um projeto completo.

---

## 🗓️ Dia 15 – Integrar TypeORM com Nest.js

### 📚 Conteúdo:

- Relembrar `.env` com variáveis de conexão

- Importar `TypeOrmModule` no `AppModule`

- Conectar ao PostgreSQL (ou outro)

### 🔧 Atividades:

- Configurar `TypeOrmModule.forRoot()` com dados do `.env`

- Testar conexão

- Criar entidade ``TarefaEntity``

```ts
@Entity('tarefas')
export class TarefaEntity {
  @PrimaryGeneratedColumn('uuid')
  id: string;

  @Column()
  titulo: string;

  @Column()
  descricao: string;

  @Column()
  status: TarefaStatus;
}
```

### 🧪 Exercício:

- Criar repositório de tarefas e salvar tarefa no banco.

---

## 🗓️ Dia 16 – CRUD com banco de dados

### 📚 Conteúdo:

- Criar ``TarefaRepository``

- Uso do ``InjectRepository``

- Métodos: ``save``, ``find``, ``findOne``, ``delete``

🔧 Atividades:
Refatorar ``tarefas.service.ts`` para usar o banco de dados em vez de array

🧪 Exercício:
Implementar os métodos: ``findAll``, ``findById``, ``create``, ``delete``, ``updateStatus``

---

## 🗓️ Dia 17 – Autenticação com JWT (parte 1)

### 📚 Conteúdo:

- Criar módulo de usuários

- Criar entidade ``UsuarioEntity``

- Instalar pacotes:

```bash
npm install @nestjs/jwt @nestjs/passport passport passport-jwt bcryptjs
```

## 🔧 Atividades:

- Criar ``UsuarioModule``, ``UsuarioService``, ``UsuarioEntity``

- Registrar e salvar novo usuário com senha criptografada (bcrypt)

---

## 🗓️ Dia 18 – Autenticação com JWT (parte 2)

### 📚 Conteúdo:

- Criar ``AuthModule`` e serviço de autenticação

- Validar login, gerar token JWT

- Criar Guard com Passport para proteger rotas

### 🔧 Atividades:

- Criar rota ``POST /auth/login``

Implementar ``JwtStrategy`` para validar token

### 🧪 Exercício:

- Proteger rotas de tarefas com ``@UseGuards(AuthGuard())``

---

## 🗓️ Dia 19 – Relacionamentos com TypeORM

### 📚 Conteúdo:

- Criar relacionamento ``User → Tarefa`` (1:N)

- Usar ``@ManyToOne()`` e ``@OneToMany()``

### 🔧 Atividades:

- Alterar entidade ``TarefaEntity`` para ter um campo ``usuario``

```ts
@ManyToOne(() => UsuarioEntity, usuario => usuario.tarefas, { eager: false })
usuario: UsuarioEntity;
```

- Ajustar criação de tarefas para registrar o usuário dono da tarefa

### 🧪 Exercício:

- Buscar tarefas de um usuário logado (usando o token JWT)

---

## 🗓️ Dia 20 – Filtros, DTOs avançados e refatorações

### 📚 Conteúdo:

- Criar DTO para login e registro

- DTOs para atualizar tarefas com validações

- Filtros com parâmetros opcionais

### 🔧 Atividades:

- Refatorar rotas para usar DTOs consistentes

- Criar filtros por status, título e usuário

### 🧪 Exercício:

- Adicionar ``GET /tarefas?status=ABERTA&busca=texto`` usando query params

---

## 🗓️ Dia 21 – Finalizando o projeto

### 📚 Conteúdo:

- Testar todas as rotas

- Documentar API com Swagger

- Preparar deploy local (opcional)

### 🔧 Atividades:

- Instalar Swagger:

```bash
npm install --save @nestjs/swagger swagger-ui-express
```

- Documentar rotas com decorators ``@ApiTags``, ``@ApiBody``, ``@ApiResponse``, etc.

### 📦 Estrutura do projeto ao final da 3ª semana:

```cpp
src/
├── auth/
│   ├── auth.module.ts
│   ├── auth.service.ts
│   ├── jwt.strategy.ts
│   └── dtos/
├── usuario/
│   ├── usuario.entity.ts
│   ├── usuario.service.ts
├── tarefas/
│   ├── tarefa.entity.ts
│   ├── tarefas.controller.ts
│   ├── tarefas.service.ts
├── common/
│   └── pipes/
├── main.ts
├── app.module.ts
```

---

### ✅ Ao final da 3ª semana, você terá:

- API com banco de dados real (PostgreSQL ou outro)

- CRUD completo persistente com autenticação

- Validação com DTOs e Pipes

- Segurança com JWT e Guards

- Relacionamentos com usuários e entidades protegidas

- Documentação com Swagger

#
---
---

# 📘 Dia 1 – Introdução ao Nest.js

### 📚 Conteúdo

### ✅ O que é o Nest.js?

- Nest.js é um framework Node.js para a construção de aplicações escaláveis, eficientes e modularizadas, baseado em TypeScript.

- Ele utiliza princípios de Programação Orientada a Objetos, Programação Funcional e Arquitetura Modular.

### ✅ Por que usar Nest.js?

- Código limpo e estruturado (sem caos de arquivos soltos)

- Baseado em módulos: cada domínio da aplicação tem seu próprio módulo

- Compatível com bibliotecas do Express e Fastify

- Suporte nativo a TypeORM, JWT, Swagger, WebSockets e muito mais

- Fácil escalabilidade para projetos grandes

### ✅ Arquitetura e Injeção de Dependência

- Usa arquitetura modular: divide funcionalidades em módulos (ex: TarefasModule, UsuarioModule)

- Usa Injeção de Dependência (DI) para desacoplar classes: os serviços são injetados nos controladores via construtor

- Baseado no padrão MVC: Controller → Service → Repository (quando usa banco)

---

### 🔧 Atividades Práticas

1️⃣ Instalar o Nest CLI

```bash
npm install -g @nestjs/cli
```

2️⃣ Criar um novo projeto Nest

```bash
nest new projeto-tarefas
```

Você será perguntado qual gerenciador de pacotes deseja usar. Pode escolher ``npm`` ou ``yarn``.

3️⃣ Estrutura de arquivos gerada

Após a criação, observe os principais arquivos:

```bash
projeto-tarefas/
├── src/
│   ├── app.controller.ts        // Controlador padrão
│   ├── app.service.ts           // Serviço padrão
│   ├── app.module.ts            // Módulo raiz
│   └── main.ts                  // Ponto de entrada da aplicação
├── test/                        // Testes gerados automaticamente
├── package.json                 // Dependências e scripts
├── tsconfig.json                // Configuração TypeScript
```

4️⃣ Rodar o servidor de desenvolvimento

Acesse a pasta do projeto:

```bash
cd projeto-tarefas
npm run start:dev
```

Você verá algo como:

```bash
[Nest] 3456  - 23/06/2025, 14:00:00   [NestFactory] Starting Nest application...
[Nest] 3456  - 23/06/2025, 14:00:01   [RoutesResolver] AppController {/}: +1 route
[Nest] 3456  - 23/06/2025, 14:00:01   [NestApplication] Nest application successfully started on port 3000
```

Acesse http://localhost:3000 e verá a mensagem:

```bash
Hello World!
```

---

### 🧪 Exercício Final

Abra o arquivo ``src/main.ts`` e adicione um ``console.log()`` para verificar se o ambiente está em desenvolvimento:

```ts
async function bootstrap() {
  console.log('Ambiente atual:', process.env.NODE_ENV || 'desenvolvimento');

  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

Execute novamente com:

```bash
npm run start:dev
```

Verifique no terminal a saída do console.

---

✅ O que você aprendeu hoje:
✔ O que é o Nest.js e por que ele é utilizado
✔ Como criar um projeto usando Nest CLI
✔ Como a arquitetura modular funciona
✔ Como rodar e explorar a estrutura inicial do projeto
✔ Como modificar o ponto de entrada e testar algo no console

#
---


