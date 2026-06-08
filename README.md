# AgroSat Monitor

Sistema de monitoramento agrícola integrado com dados satelitais da NASA em tempo real.

## Sobre o projeto

O AgroSat Monitor é uma solução desenvolvida para monitorar lavouras utilizando
dados reais de satélite fornecidos pela NASA. O sistema processa informações de
eventos naturais (secas, incêndios, tempestades) e imagens da superfície terrestre
para gerar alertas e indicadores que apoiam decisões de manejo agrícola.

O projeto está alinhado com os seguintes Objetivos de Desenvolvimento Sustentável (ODS):
- ODS 2 — Fome Zero: apoio ao monitoramento e proteção de lavouras
- ODS 13 — Ação Climática: uso de dados satelitais para acompanhar eventos climáticos
- ODS 9 — Indústria, Inovação e Infraestrutura: tecnologia espacial aplicada ao agronegócio

## Stack tecnológica

- **Frontend:** React
- **Backend:** C# com ASP.NET Core e Java
- **Pipeline CI/CD:** GitHub Actions
- **Dados satelitais:** NASA EPIC API e NASA EONET API

## APIs da NASA utilizadas

### EPIC — Earth Polychromatic Imaging Camera
Fornece imagens diárias da Terra capturadas pelo satélite DSCOVR, permitindo
visualizar a superfície terrestre e acompanhar mudanças na cobertura vegetal.

Endpoint utilizado:
https://api.nasa.gov/EPIC/api/natural/images?api_key=NASA_API_KEY
### EONET — Earth Observatory Natural Event Tracker
Fornece dados em tempo real sobre eventos naturais como focos de incêndio,
tempestades, secas e inundações — essenciais para alertas de risco às lavouras.

Endpoint utilizado:
https://eonet.gsfc.nasa.gov/api/v3/events
## Segurança — DevSecOps integrado

Este repositório implementa práticas de DevSecOps desde o início do desenvolvimento:

### Gestão de Segredos
A chave de autenticação da NASA (`NASA_API_KEY`) nunca é escrita diretamente
no código-fonte ou em arquivos versionados. Ela é armazenada no GitHub Secrets
e injetada como variável de ambiente durante a execução do pipeline.

No backend C#, a chave é lida com segurança:
```csharp
var apiKey = Environment.GetEnvironmentVariable("NASA_API_KEY");
```

### Análise de Dependências (SAST/SCA)
A cada push ao repositório, o pipeline executa automaticamente:
- `npm audit` — verifica vulnerabilidades nas dependências do frontend React
- Verificação de presença e integridade dos secrets configurados

Builds com vulnerabilidades críticas são bloqueados automaticamente.

### Pipeline de segurança
O arquivo `.github/workflows/security.yml` define o fluxo completo de auditoria,
composto por dois jobs:
- **Auditoria de Dependencias (SCA):** escaneia pacotes npm em busca de CVEs
- **Verificar Configuração de Secrets:** valida que a NASA_API_KEY está configurada
  corretamente sem expor seu valor nos logs

## Estrutura do repositório
agrosat-monitor/
├── .github/
│   └── workflows/
│       └── security.yml      # Pipeline DevSecOps
├── package.json              # Dependências do frontend React
├── requirements.txt          # Dependências do backend
└── README.md

## Evidências de segurança

As evidências da implementação DevSecOps estão documentadas no PDF técnico
entregue junto a este repositório, incluindo:
- Print do secret NASA_API_KEY configurado no GitHub Secrets
- Log do pipeline confirmando a chave configurada sem expor o valor
- Resultado da auditoria de dependências npm com status de aprovação
