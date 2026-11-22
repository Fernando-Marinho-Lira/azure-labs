# ☁️ Laboratório Prático Microsoft Azure — Projeto ProteCar

**Portfólio técnico | Azure IaaS • Ubuntu Server • Nginx • Redes • DNS • HTTPS • Docker • Key Vault**

[![Azure](https://img.shields.io/badge/Microsoft_Azure-IaaS-0078D4?style=flat-square&logo=microsoftazure&logoColor=white)](https://azure.microsoft.com/)
![Projeto](https://img.shields.io/badge/Projeto-ProteCar-0A66C2?style=flat-square)
![Ambiente](https://img.shields.io/badge/Ambiente-Off--line%20%7C%20Laborat%C3%B3rio%20de%20estudos-6B7280?style=flat-square)
![Documentação](https://img.shields.io/badge/Documenta%C3%A7%C3%A3o-Preservada-blue?style=flat-square)

> **🗓️ Situação do projeto:** o ProteCar foi desenvolvido como **laboratório de estudos em Microsoft Azure**. A página web esteve publicada durante o aprendizado, mas **não está mais online** porque o ambiente de laboratório foi encerrado. O projeto é apresentado aqui como **registro histórico de aprendizagem**, não como serviço em produção ou demonstração ativa. Não é necessário manter recursos Azure em execução para consultar esta documentação.

> **Escopo e transparência.** Esta documentação foi preparada a partir de três materiais técnicos anteriores do projeto. O portfólio base descreve uma página HTML/CSS publicada em uma VM Ubuntu com Nginx e DNS do Azure. Os guias complementares registram procedimentos de HTTPS/Certbot e Key Vault/Docker. **Checklists, exemplos de comandos e resultados esperados não são tratados como prova de execução atual.** Não há validação de disponibilidade do site ou de recursos Azure nesta publicação.

## 📑 Índice

1. [Objetivo e contexto](#1--objetivo-e-contexto)
2. [Topologia lógica do ProteCar](#2--topologia-lógica-do-protecar)
3. [Inventário dos recursos Azure documentados](#3--inventário-dos-recursos-azure-documentados)
4. [Etapas e documentos técnicos](#4--etapas-e-documentos-técnicos)
5. [Competências abordadas](#5--competências-abordadas)
6. [Matriz de evidências](#6--matriz-de-evidências)
7. [Organização dos arquivos](#7--organização-dos-arquivos)
8. [Boas práticas e melhorias futuras](#8--boas-práticas-e-melhorias-futuras)
9. [Autor e referências](#9--autor-e-referências)

## 1. 🎯 Objetivo e contexto

O **ProteCar** é um laboratório prático de publicação de uma **página web estática** em infraestrutura **IaaS (Infrastructure as a Service)** no Microsoft Azure. O ambiente base utiliza **Ubuntu Server**, **Nginx**, **IP público**, **Network Security Group (NSG)** e um **FQDN do domínio `cloudapp.azure.com`**. O material original descreve a publicação histórica do site e seu acesso pela Internet durante o período de estudos. **Atualmente, a página está offline.** 

Os documentos complementares abrangem a configuração de **HTTPS com Certbot/Let's Encrypt**, o uso de **Docker + Nginx Alpine para servir imagens** e um fluxo de proteção de material sensível com **Azure Key Vault e RBAC**. A distinção entre **procedimento documentado** e **evidência anexada** está indicada nas seções seguintes.

## 2. 🗺️ Topologia lógica do ProteCar

![Topologia lógica da infraestrutura Azure ProteCar](./diagrams/topologia-protecar.svg)

[🔍 Abrir diagrama completo](./diagrams/topologia-protecar.svg)

**Fluxo de referência:** Navegador → FQDN configurado no IP público do Azure → NSG → interface de rede (NIC) da VM Ubuntu → Nginx principal → site estático. No guia de extensão, o Nginx faz reverse proxy de `/images/` para o container local `protecar-images` na porta `127.0.0.1:8090`.

> O diagrama apresenta **arquitetura lógica descrita nos documentos**, não um levantamento de implantação em tempo real. A utilização de HTTPS, Docker e Key Vault deve ser comprovada separadamente pelas evidências originais ou por testes posteriores.

## 3. 🧱 Inventário dos recursos Azure documentados

| Componente | Nome / configuração registrada | Função |
|---|---|---|
| Resource Group | `RG-AZ900-PROTECAR` | Organizar e administrar os recursos do laboratório |
| Rede virtual | `VNET-PROTECAR` — `10.10.0.0/16` | Endereçamento privado |
| Sub-rede | `SUBNET-WEB` — `10.10.1.0/24` | Rede da interface da VM |
| Máquina virtual | `VM-PROTECAR` — Ubuntu Server | Hospedar a aplicação e o Nginx |
| NIC | Interface da VM | Conectar a VM à sub-rede |
| IP público + rótulo DNS | `protecar-fernando.brazilsouth.cloudapp.azure.com` | Acesso por nome público |
| NSG | HTTP TCP 80; SSH TCP 22 conforme configuração documentada | Controle de tráfego |
| HTTPS (guia complementar) | TCP 443; Certbot/Let's Encrypt | Segurança TLS para o site |
| Docker (guia complementar) | `protecar-images`, `nginx:alpine`, `127.0.0.1:8090` | Entrega local de imagens |
| Key Vault (guia complementar) | Nome do cofre não confirmado | Armazenamento protegido de segredo/chave, conforme guia |

**Nota:** o FQDN abaixo é **histórico e não está ativo como página do projeto**. Não publicamos IP público numérico, credenciais, chave SSH, segredos, certificado privado nem inventamos nome de Key Vault. O FQDN é o identificador preservado da documentação original, **não um link para demonstração online**.

## 4. ⚙️ Etapas e documentos técnicos

| Etapa | Escopo | Documento |
|---|---|---|
| **01 — Azure IaaS + Ubuntu + Nginx** | Provisionamento, rede, DNS, publicação HTML/CSS e administração Linux | [Abrir etapa 01](./docs/01-azure-iaas-nginx.md) |
| **02 — HTTPS e certificados** | Nginx, `server_name`, Certbot, Let's Encrypt, TLS e renovação | [Abrir etapa 02](./docs/02-https-certbot.md) |
| **03 — Docker e Key Vault** | Container de imagens, reverse proxy local, RBAC, gestão de segredos | [Abrir etapa 03](./docs/03-docker-keyvault.md) |
| **04 — Evidências e verificação** | Checklist de validação e registros faltantes | [Abrir matriz](./docs/04-evidencias.md) |

## 5. 🧠 Competências abordadas

- **Azure IaaS:** Resource Group, VM, virtual network, subnet, NIC, IP público e NSG.
- **Linux:** acesso remoto, administração de pacotes, `systemd`, arquivos e permissões.
- **Nginx:** entrega de conteúdo estático, server blocks, logs e análise de configuração.
- **DNS e segurança:** FQDN associado ao IP público, portas TCP 22/80/443 e certificados TLS.
- **Containers:** isolamento de serviço web auxiliar, bind mount somente leitura e acesso local.
- **Identity & Security:** conceitos de RBAC para acesso ao Key Vault e cuidados com segredos.
- **Troubleshooting:** diagnóstico de resolução DNS, portas, erros Nginx, acesso SSH e logs.

## 6. 🧪 Matriz de evidências

| Verificação | Evidência desejada | Situação de publicação |
|---|---|---|
| Inventário Azure | Captura do Resource Group / recursos sem dados sensíveis | Ainda não anexada |
| Site estático ProteCar | Captura da página e requisição HTTP | Descrito no portfólio de origem; captura não anexada aqui |
| Configuração Nginx | `nginx -t` + configuração anonimizada | Procedimento documentado; saída original não anexada |
| DNS público | Saída de consulta ao FQDN | Procedimento documentado; saída não anexada |
| Certificado HTTPS | Certificado público e teste de renovação | Guia disponível; evidência de execução não anexada |
| Docker local | `docker ps`, `curl` local e rota `/images/` | Guia disponível; evidência de execução não anexada |
| Key Vault / RBAC | Cofre, atribuição e segredo (sem conteúdo) | Guia disponível; evidência de execução não anexada |

## 7. 📂 Organização dos arquivos

```text
azure-labs/
├── README.md                       # índice de laboratórios
└── lab-01-protecar/
    ├── README.md
    ├── .gitignore
    ├── diagrams/
    │   └── topologia-protecar.svg
    ├── docs/
    │   ├── 01-azure-iaas-nginx.md
    │   ├── 02-https-certbot.md
    │   ├── 03-docker-keyvault.md
    │   └── 04-evidencias.md
    ├── evidencias/
    │   └── README.md
    └── configuracoes/
        └── README.md
```

## 8. 🔐 Boas práticas e melhorias futuras

O **ProteCar foi um laboratório de estudos concluído e documentado**. A aplicação esteve publicada no Microsoft Azure durante o aprendizado, mas o ambiente foi encerrado e **não precisa permanecer online** para integrar este portfólio. Os itens abaixo são sugestões de aprimoramento documental e de segurança, **não pendências obrigatórias para considerar o laboratório válido**.

1. **Preservar evidências históricas, caso disponíveis:** acrescentar capturas reais do Azure, comandos executados e respectivas saídas, sempre ocultando informações sensíveis.
2. **Recuperar o HTML/CSS original, se disponível:** anexar uma cópia revisada da aplicação para demonstrar sua estrutura sem reconstruir ou inventar arquivos.
3. **Registrar aprendizados de segurança:** explicar como funcionavam as regras de NSG, o acesso SSH TCP 22 e possíveis restrições de origem, sem pressupor que o ambiente esteja ativo.
4. **Manter informações confidenciais protegidas:** nunca publicar arquivos `.pem`, `.key`, chaves privadas, segredos, senhas ou dados de terceiros.
5. **Documentar configurações históricas, se recuperadas:** apresentar exemplos revisados e anonimizados do Nginx, Docker e RBAC, distinguindo configurações reais de trechos explicativos dos guias.
6. **Recriação opcional:** somente se o laboratório voltar a ser executado futuramente, registrar o novo ambiente e datar os testes realizados. **Não é necessário religar a VM nem restaurar a página para concluir este portfólio.**

## 9. 👤 Autor e referências

**Fernando Marinho Lira** — Infraestrutura de TI | Linux | Redes | Microsoft Azure  
**Certificação:** Microsoft Azure Fundamentals (AZ-900)

[GitHub](https://github.com/Fernando-Marinho-Lira) · [LinkedIn](https://www.linkedin.com/in/fernando-marinho-lira/)

**Materiais de origem consultados:**
- `Portfolio_Tecnico_Azure_ProteCar_Fernando_Marinho_Lira.docx` — publicação inicial em Azure IaaS.
- `Guia_Completo_Lets_Encrypt_Ubuntu_Nginx_ProteCar.pdf` — HTTPS/Certbot.
- `Guia_Completo_Lab_Azure_KeyVault_Docker_Nginx_ProteCar.docx` — segurança, Docker e integração Nginx.

*Os documentos originais não foram incorporados ao pacote público para evitar republicação acidental de dados sensíveis. Esta versão contém apenas documentação reorganizada e um diagrama ilustrativo.*