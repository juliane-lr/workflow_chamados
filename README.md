# 🛠️ Sistema Automatizado de Triagem, Alerta e Resposta de Chamados

Este projeto apresenta uma solução de engenharia de software e automação de processos utilizando a plataforma **n8n** (Low-Code/Fair-Code). O objetivo principal é orquestrar uma esteira de dados inteligente que intercepta chamados de clientes em tempo real, centraliza as informações em uma planilha/banco de dados e aplica lógica condicional para acionar diferentes APIs de comunicação baseando-se no nível de criticidade informado.

---

## 📐 Arquitetura do Fluxo e Regras de Negócio

O ecossistema foi desenhado seguindo uma esteira de decisões binárias automatizadas:

1. **Gatilho (Trigger):** Monitoramento ativo e assíncrono de novas linhas no Google Sheets (alimentado via API por um formulário de captação de chamados).
2. **Lógica Condicional (IF Node):** Validação e análise do payload JSON recebido, verificando a string chave do campo 'Urgência'.
3. **Caminho de Alta Prioridade (True Branch):** Se 'Urgência == 'Alta'', o fluxo executa uma requisição HTTP via método 'POST', disparando um payload customizado diretamente para o Webhook do **Discord** para alertar a equipe técnica em tempo real.
4. **Caminho de Média/Normal Prioridade (False Branch):** Se a urgência não for alta, os dados seguem pela rota alternativa conectada à API do **Gmail**, gerando e enviando uma resposta automatizada e personalizada de confirmação de recebimento para o e-mail do cliente.

---

## 🛠️ Tecnologias e Ferramentas Utilizadas

* **n8n Cloud:** Orquestrador e motor central do workflow.
* **Google Sheets API:** Captura de dados e persistência dos registros.
* **REST API / Webhooks:** Integração e transmissão de dados via protocolo HTTP.
* **JSON:** Estruturação, manipulação e mapeamento de dados dinâmicos de entrada e saída.
* **Discord API:** Endpoint de destino para notificações e alertas críticos imediatos.
* **Gmail API / OAuth2:** Disparo de e-mails transacionais automatizados para o usuário final.

---

## 📂 Como Reutilizar este Fluxo

Este repositório armazena o código de infraestrutura do fluxo de automação.

1. Faça o download do arquivo `workflow.json` disponível neste repositório.
2. Acesse sua instância do **n8n**.
3. No menu principal, selecione a opção **Import from File** e envie o arquivo JSON.
4. Configure suas credenciais na autenticação nativa do Google (Sheets e Gmail) e insira a URL do seu Webhook do Discord no nó HTTP Request.
5. Publique o fluxo clicando em **Publish**.
