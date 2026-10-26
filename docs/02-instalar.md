# 2. Instalar o certificado

Após a emissão, você recebe o **certificado do servidor** e a **cadeia** (certificados intermediários). Instalar a cadeia completa evita erros de confiança em parte dos clientes.

## Apache

```apache
<VirtualHost *:443>
    ServerName servidor.exemplo.br
    SSLEngine on
    SSLCertificateFile      /etc/ssl/certs/servidor.exemplo.br.crt
    SSLCertificateKeyFile   /etc/ssl/private/servidor.exemplo.br.key
    SSLCertificateChainFile /etc/ssl/certs/cadeia-intermediaria.crt
</VirtualHost>
```

> No Apache 2.4.8 ou superior, também é possível concatenar o certificado e a cadeia no `SSLCertificateFile`.

```bash
apachectl configtest && systemctl reload apache2
```

## Nginx

O Nginx espera o certificado e a cadeia no mesmo arquivo (certificado do servidor primeiro):

```bash
cat servidor.exemplo.br.crt cadeia-intermediaria.crt > servidor.exemplo.br.fullchain.crt
```

```nginx
server {
    listen 443 ssl;
    server_name servidor.exemplo.br;
    ssl_certificate     /etc/ssl/certs/servidor.exemplo.br.fullchain.crt;
    ssl_certificate_key /etc/ssl/private/servidor.exemplo.br.key;
}
```

```bash
nginx -t && systemctl reload nginx
```

## IIS (Windows)

1. Se o CSR foi gerado com OpenSSL, gere um arquivo **PFX** com a chave e a cadeia:

   ```bash
   openssl pkcs12 -export \
     -out servidor.exemplo.br.pfx \
     -inkey servidor.exemplo.br.key \
     -in servidor.exemplo.br.crt \
     -certfile cadeia-intermediaria.crt
   ```

2. No **Gerenciador do IIS** → *Certificados de Servidor* → **Importar** o `.pfx`.
3. No site → **Associações** → `https` (porta 443) → selecione o certificado importado.

[← Anterior](01-gerar-csr.md) · [Voltar ao README](../README.md) · [Próximo: validar →](03-validar.md)
