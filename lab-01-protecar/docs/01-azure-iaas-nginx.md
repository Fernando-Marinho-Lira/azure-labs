# Etapa 01 — Azure IaaS, Ubuntu e Nginx

[← Voltar ao ProteCar](../README.md)

## Cenário documentado

O portfólio original descreve a publicação de uma página HTML/CSS em **VM Ubuntu Server** no Microsoft Azure, disponibilizada via **Nginx** e um FQDN associado ao IP público. Trata-se de um laboratório de **IaaS**. **A publicação é histórica: o ambiente de estudos foi encerrado e a página não está mais online.**

| Recurso | Identificação documentada | Finalidade |
|---|---|---|
| Resource Group | `RG-AZ900-PROTECAR` | Organização dos recursos |
| Rede virtual | `VNET-PROTECAR` (`10.10.0.0/16`) | Rede privada da VM |
| Sub-rede | `SUBNET-WEB` (`10.10.1.0/24`) | Conexão da NIC |
| VM | `VM-PROTECAR` | Ubuntu e Nginx |
| IP público e FQDN | `protecar-fernando.brazilsouth.cloudapp.azure.com` | Acesso por nome |
| NSG | TCP 80; SSH 22 quando habilitado | Controle de tráfego |

## Comandos registrados no portfólio

```bash
sudo apt update
sudo apt install nginx -y
sudo systemctl enable nginx
sudo systemctl start nginx
sudo nginx -t
systemctl status nginx --no-pager
systemctl is-active nginx
```

O material cita publicação em `/var/www/html/index.html` e permissões de arquivos. **O código HTML/CSS original e as saídas reais dos comandos ainda não foram anexados ao repositório.**

## Fluxo lógico

Navegador → FQDN no IP público Azure → NSG → NIC/VNet → Ubuntu Server → Nginx → site estático.

## Evidências pendentes

Captura de inventário Azure, configuração Nginx anonimizada, captura real da página e resposta HTTP registrada. A página encontra-se offline por se tratar de um ambiente de estudos; a documentação é mantida como registro histórico.
