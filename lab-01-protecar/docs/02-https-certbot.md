# Etapa 02 — HTTPS com Certbot e Let's Encrypt

[← Voltar ao ProteCar](../README.md)

## Escopo do guia original

O guia do laboratório descreve a evolução de HTTP para HTTPS com **Nginx**, **Certbot** e **Let's Encrypt** no FQDN `protecar-fernando.brazilsouth.cloudapp.azure.com`.

| Arquivo | Ajuste documentado |
|---|---|
| `/etc/nginx/sites-available/default` | `server_name`, `root`, `index` e `location`; configurações TLS pelo Certbot |
| `/etc/nginx/nginx.conf` | `server_names_hash_bucket_size 128;` no bloco `http`, para o nome longo |
| `/etc/letsencrypt/live/<FQDN>/` | Certificado e chave privada: **não publicar chaves** |

## Verificações descritas

```bash
systemctl is-active nginx
sudo nginx -t
sudo ss -lntp | grep -E ':80|:443'
getent hosts protecar-fernando.brazilsouth.cloudapp.azure.com
curl -I http://protecar-fernando.brazilsouth.cloudapp.azure.com
```

O guia registra os passos de instalação do Certbot e emissão do certificado:

```bash
sudo snap install --classic certbot
sudo certbot --nginx -d protecar-fernando.brazilsouth.cloudapp.azure.com
```

Para checagem posterior, o guia orienta `sudo certbot certificates`, `curl -I https://...` e `sudo certbot renew --dry-run`.

## Troubleshooting registrado

O guia aborda `ERR_CONNECTION_REFUSED`, erros de `server_names_hash`, falhas de resolução DNS, disponibilidade das portas 80/443 e inspeção dos logs de Nginx e Let's Encrypt.

> **Status de evidência:** o procedimento está documentado, mas não foram anexados logs de emissão, captura do certificado nem saída de renovação. Não se afirma que um teste atual foi realizado.
