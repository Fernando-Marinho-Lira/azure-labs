# Etapa 03 — Docker, reverse proxy, Azure Key Vault e RBAC

[← Voltar ao ProteCar](../README.md)

**Situação atual:** a página ProteCar não está mais online porque o ambiente foi usado para estudos. Os exemplos abaixo documentam a arquitetura proposta/registrada no guia, sem alegar implantação ativa.

## Escopo do guia complementar

O guia descreve a extensão do site ProteCar para servir imagens por um **container Docker com Nginx Alpine** e armazenar material sensível em **Azure Key Vault**, utilizando **Azure RBAC**.

### Container de imagens

| Elemento | Configuração do guia |
|---|---|
| Nome | `protecar-images` |
| Imagem | `nginx:alpine` |
| Porta no host | `127.0.0.1:8090` |
| Diretório persistente | `/srv/protecar-images` |
| Bind mount | `/srv/protecar-images:/usr/share/nginx/html/images:ro` |
| Rota pública no Nginx principal | `/images/` |

**Comando documentado (não executado nesta publicação):**

```bash
sudo docker run -d --name protecar-images --restart unless-stopped \
  -p 127.0.0.1:8090:80 \
  -v /srv/protecar-images:/usr/share/nginx/html/images:ro \
  nginx:alpine
```

**Trecho de configuração descrito no guia:**

```nginx
location /images/ {
    proxy_pass http://127.0.0.1:8090/images/;
}
```

O Nginx principal na VM atende HTTPS; o container utiliza apenas loopback e não representa uma segunda máquina virtual.

### Azure Key Vault e RBAC

O material descreve a criação de um cofre com modelo **Azure role-based access control**, atribuições relacionadas a segredos (como `Key Vault Secrets Officer` e `Key Vault Data Access Administrator`) e armazenamento de material PEM como **Secret**.

**Não há nome confirmado de cofre nem conteúdo de segredo reproduzido aqui.** Nenhuma chave privada deve ser versionada no GitHub.

### Validações descritas

```bash
sudo docker ps
sudo docker logs protecar-images
curl -I http://127.0.0.1:8090/images/carro.jpg
sudo nginx -t
sudo ss -lntp | grep -E ':80|:443|:8090'
```

**Status:** o guia contém procedimentos e uma lista de erros encontrados; não há nesta publicação saídas reais recentes comprovando container, regra RBAC ou funcionamento atual.
