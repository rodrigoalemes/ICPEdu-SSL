<p align="center">
<img src="assets/capa.png" alt="Certificados SSL/TLS — guia prático" width="100%">
</p>

<h1 align="center">Certificados SSL/TLS — guia prático</h1>
<p align="center"><i>Gerar CSR, instalar e validar certificados de servidor</i></p>

<p align="center">
<img src="https://img.shields.io/badge/OpenSSL-721412?style=flat-square&logo=openssl&logoColor=white" alt="OpenSSL">
<img src="https://img.shields.io/badge/IIS-5C2D91?style=flat-square" alt="IIS">
<img src="https://img.shields.io/badge/Apache-D22128?style=flat-square&logo=apache&logoColor=white" alt="Apache">
<img src="https://img.shields.io/badge/Nginx-009639?style=flat-square&logo=nginx&logoColor=white" alt="Nginx">
<img src="https://img.shields.io/badge/tipo-guia-2DD4BF?style=flat-square" alt="tipo: guia">
</p>

## Sumário

- [Sobre](#sobre)
- [Visão geral do processo](#visão-geral-do-processo)
- [Guias](#guias)
- [Checklist rápido](#checklist-rápido)
- [Estrutura do repositório](#estrutura-do-repositório)
- [Autor](#autor)

## Sobre

Guia de referência para o ciclo de um **certificado SSL/TLS de servidor**, do pedido à validação, reunido a partir da experiência com emissão de certificados **ICPEdu**. O conteúdo é genérico e não contém dados de nenhum ambiente.

> [!IMPORTANT]
> O fluxo de solicitação e aprovação do certificado depende da instituição emissora. Siga sempre as orientações oficiais dela; este guia cobre as etapas técnicas no servidor.

## Visão geral do processo

```mermaid
flowchart LR
    A[Gerar chave privada] --> B[Gerar CSR]
    B --> C[Solicitar certificado]
    C --> D[Receber certificado + cadeia]
    D --> E[Instalar no servidor]
    E --> F[Validar HTTPS]
    F --> G[Monitorar validade e renovar]
```

## Guias

| Etapa | Documento |
| --- | --- |
| 1. Gerar chave e CSR com OpenSSL | [docs/01-gerar-csr.md](docs/01-gerar-csr.md) |
| 2. Instalar no servidor (Apache, Nginx, IIS) | [docs/02-instalar.md](docs/02-instalar.md) |
| 3. Validar e renovar | [docs/03-validar.md](docs/03-validar.md) |

## Checklist rápido

- [ ] Chave privada gerada e guardada com acesso restrito
- [ ] CSR com o nome do domínio correto (CN/SAN)
- [ ] Certificado e **cadeia intermediária** instalados
- [ ] HTTPS validado em navegador e por linha de comando
- [ ] Data de expiração registrada e lembrete de renovação criado

## Estrutura do repositório

```text
ICPEdu-SSL/
├── assets/
│   └── capa.png
├── docs/
│   ├── 01-gerar-csr.md
│   ├── 02-instalar.md
│   └── 03-validar.md
└── README.md
```

## Autor

**Rodrigo Lemes** · Analista de TI · Microsoft 365, AD/Entra ID, Automação, Power BI e IA aplicada

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Rodrigo%20Lemes-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/rodrigoalemes/)
[![GitHub](https://img.shields.io/badge/GitHub-rodrigoalemes-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/rodrigoalemes)
