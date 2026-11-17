# 🌐 WebServidor — Servidor HTTP Nativo com Node.js

Servidor back-end minimalista construído com **Node.js** puro, projetado para atuar como fornecedor de dados (API) para aplicações front-end por meio do protocolo HTTP e formato JSON.

---

## 🎯 Contexto
Em um cenário de desenvolvimento back-end voltado para a construção da base de uma API, era necessário criar um servidor capaz de receber pedidos de aplicações externas (sites ou apps) e entregar informações estruturadas usando apenas recursos nativos do **Node.js**, sem depender de frameworks prontos como Express.

## ⚠️ Problema
Uma interface visual (front-end) isolada não armazena informações e precisa buscar dados em algum lugar para exibir na tela. Ao mesmo tempo, usar frameworks prontos desde o início esconde como a comunicação cliente-servidor realmente funciona:
* **Falta de um provedor de dados:** Interfaces sem acesso a uma fonte centralizada para consultar listas de usuários.
* **Caixa-preta na comunicação HTTP:** Dificuldade em enxergar como o servidor lê rotas (`URL`), identifica métodos (`GET`), define cabeçalhos (`Content-Type`) e empacota dados para tráfego na rede[cite: 14].

## 🛠️ Solução (O que e como foi feito)
Construí um servidor HTTP do zero em **JavaScript (Node.js)** utilizando o módulo nativo `http`:

1. **Abertura de Porta e Escuta (`index.js`):**
   * Configuração do servidor com `http.createServer` rodando na porta `3000`, exibindo no terminal cada requisição recebida (método e rota).
2. **Base de Dados Simulada (`mock/users.js`):**
   * Criação de uma lista de usuários (`Clarissa`, `José` e `Maria`) separada em um módulo independente, simulando a resposta de um banco de dados.
3. **Roteamento e Entrega em JSON:**
   * Quando o cliente acessa `GET /users`, o servidor empacota a lista em texto universal **JSON** (`JSON.stringify`) com cabeçalho `application/json` e status `200`, permitindo que qualquer front-end (Web ou Mobile) leia e transforme esses dados na tela.
   * Para qualquer outra rota acessada, o servidor responde com uma página HTML padrão (`text/html`).

## 📊 Resultado (Antes x Depois)

| Aspecto | ❌ Antes | ✅ Depois |
| :--- | :--- | :--- |
| **Consumo de Dados** | Front-end estático, sem fonte externa para buscar informações dinâmicas. | API funcional entregando dados em **JSON** prontos para serem lidos por qualquer interface. |
| **Controle do Servidor** | Dependência de bibliotecas externas que escondem o funcionamento da rede. | Controle manual e transparente de rotas, status HTTP (`200`) e tipos de resposta (`JSON` e `HTML`) com **0 dependências externas**. |
| **Manutenção** | Dados chumbados diretamente na tela ou misturados à lógica de rede. | Separação clara entre o servidor (`index.js`) e a camada de dados (`mock/users.js`). |
