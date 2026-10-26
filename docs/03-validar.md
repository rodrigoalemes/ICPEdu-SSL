# 3. Validar e renovar

## Conferir o certificado servido

```bash
openssl s_client -connect servidor.exemplo.br:443 -servername servidor.exemplo.br -showcerts </dev/null
```

Procure por `Verify return code: 0 (ok)` e confira se a cadeia aparece completa.

## Ver validade e nomes

```bash
echo | openssl s_client -connect servidor.exemplo.br:443 -servername servidor.exemplo.br 2>/dev/null \
  | openssl x509 -noout -subject -issuer -dates -ext subjectAltName
```

## Conferir se chave e certificado combinam

```bash
openssl x509 -noout -modulus -in servidor.exemplo.br.crt | openssl md5
openssl rsa  -noout -modulus -in servidor.exemplo.br.key | openssl md5
```

Os dois resultados devem ser iguais.

## Erros comuns

| Sintoma | Causa provável | Ação |
| --- | --- | --- |
| Navegador acusa certificado não confiável | Cadeia intermediária ausente | Instalar a cadeia completa |
| Nome não confere | Domínio fora do CN/SAN | Emitir novo certificado com o nome correto |
| Serviço não sobe após a troca | Chave e certificado não combinam | Comparar o *modulus* (acima) |

## Renovação

- Registre a data de expiração em um controle (planilha, calendário ou ferramenta de monitoramento).
- Inicie a renovação com antecedência e repita as etapas 1 a 3.

[← Anterior](02-instalar.md) · [Voltar ao README](../README.md)
