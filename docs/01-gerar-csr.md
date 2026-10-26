# 1. Gerar chave privada e CSR

O **CSR** (Certificate Signing Request) é o pedido enviado à autoridade certificadora. Ele leva a chave pública e os dados do domínio; a chave privada **nunca** sai do servidor.

## Chave e CSR em um comando

```bash
openssl req -new -newkey rsa:2048 -nodes \
  -keyout servidor.exemplo.br.key \
  -out servidor.exemplo.br.csr \
  -subj "/C=BR/ST=SP/L=Campinas/O=Minha Organizacao/CN=servidor.exemplo.br"
```

## Com nomes alternativos (SAN)

```bash
openssl req -new -newkey rsa:2048 -nodes \
  -keyout servidor.exemplo.br.key \
  -out servidor.exemplo.br.csr \
  -subj "/C=BR/ST=SP/L=Campinas/O=Minha Organizacao/CN=servidor.exemplo.br" \
  -addext "subjectAltName=DNS:servidor.exemplo.br,DNS:www.servidor.exemplo.br"
```

> `-addext` exige OpenSSL 1.1.1 ou superior.

## Conferir o CSR antes de enviar

```bash
openssl req -in servidor.exemplo.br.csr -noout -text
```

Verifique o `CN`, os `DNS` do SAN e o tamanho da chave.

## Segurança da chave

```bash
chmod 600 servidor.exemplo.br.key
```

[← Voltar ao README](../README.md) · [Próximo: instalar →](02-instalar.md)
