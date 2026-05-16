---
name: build-failure-resolver
description: Automatically diagnoses and fixes build failures using a systematic recovery approach.
version: 1.0.0
---

# Build Failure Resolver

## Propósito
Detectar falhas de compilação ou execução de build e aplicar correções automáticas baseadas em logs de erro, evitando interrupções no fluxo de desenvolvimento.

## Quando usar
- Imediatamente após uma falha de comando `npm run build`, `go build`, etc.
- Quando testes de integração falham devido a problemas de ambiente.

## Quando não usar
- Em erros de lógica de negócio que não impedem o build (embora possa ajudar a depurar).

## Entradas esperadas
- Log de erro do console.
- Arquivos afetados pela falha.

## Processo
1. Capturar e analisar o stack trace do erro.
2. Identificar se o erro é de sintaxe, dependência ausente ou configuração.
3. Propor e aplicar o "menor fix possível" para restaurar o build.
4. Validar se o build passa após a correção.

## Saída esperada
- Relatório de causa raiz.
- Código corrigido e build em estado "Verde".

## Critérios de sucesso
- Recuperação do build em menos de 2 tentativas.

## Limites de segurança
- Não forçar builds ignorando testes de segurança.
- Não instalar dependências globais sem permissão.
