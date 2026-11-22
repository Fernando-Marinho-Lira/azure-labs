# Etapa 04 — Evidências e validação do ProteCar

[← Voltar ao ProteCar](../README.md)

## Estado atual

**Ambiente de estudos encerrado:** a página ProteCar publicada anteriormente no Azure não está mais online. Não se exige recriar o serviço para manter este portfólio; evidências históricas podem ser adicionadas apenas se estiverem disponíveis e sem dados sensíveis.

Os materiais de origem são um portfólio técnico e guias de laboratório. Eles descrevem arquitetura, comandos, problemas e resultados esperados. **Esta publicação não possui capturas de tela originais, saídas datadas e verificações independentes para todas as etapas.**

| Área | O que está documentado | Evidência a anexar |
|---|---|---|
| Azure IaaS | VM, VNet, subnet, NIC, IP público e NSG | Inventário anonimizado e configuração de rede |
| Web HTTP | Publicação de HTML/CSS via Nginx | Captura original da aplicação e resposta HTTP |
| HTTPS | Guia com Certbot e Let's Encrypt | Evidência do certificado e teste da época |
| Docker | Container de imagens e Nginx reverso | `docker ps`, logs e teste `curl` |
| Key Vault | Modelo RBAC e armazenamento de segredo | Captura das atribuições sem valores confidenciais |

## Como registrar um teste real

1. Data e ambiente da verificação;
2. Objetivo do teste;
3. Comando efetivamente executado;
4. Saída real anonimizada;
5. Resultado observado e limites;
6. Correção aplicada, se houver.

**Não publicar:** arquivos `.pem`, `.key`, segredos, senhas, tokens, dados de clientes ou exportações de segurança sem revisão.
