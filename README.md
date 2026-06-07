# AgroSat Monitor

Sistema de monitoramento agrícola integrado com dados satelitais da NASA.

## Sobre o projeto

O AgroSat Monitor utiliza APIs públicas da NASA (FIRMS e NASA Earthdata) para
monitorar lavouras em tempo real com dados de NDVI, temperatura de superfície
e alertas de focos de incêndio.

## Stack

- Frontend: React
- Backend: C# com ASP.NET Core e Java
- Pipeline CI/CD: GitHub Actions
- Dados: NASA FIRMS API, NASA Earthdata

## Segurança (DevSecOps)

Este repositório implementa as seguintes práticas de segurança:

- **Gestão de Segredos:** a chave NASA_API_KEY é armazenada no GitHub Secrets
  e nunca aparece no código-fonte.
- **Análise de Dependências:** o pipeline executa `npm audit` e auditoria de
  pacotes automaticamente a cada push, bloqueando builds com vulnerabilidades críticas.

## Como rodar localmente

Configure a variável de ambiente antes de rodar:
```bash
export NASA_API_KEY=sua_chave_aqui
```
