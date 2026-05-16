# Long-Running Projects Workflow

Este workflow define como agentes devem lidar com projetos de longa duração, garantindo a preservação da memória e o fatiamento de tarefas ao longo de múltiplas sessões.

## Passos Principais
1. **Restauração de Contexto**: Uso de `project-graph-builder` para reativar o entendimento do projeto.
2. **Sincronização de Memória**: Auditoria da `ai-memory` local contra o estado real do código.
3. **Execução em Fatias**: Uso de `task-slicer` para definir entregas incrementais.
4. **Checkpoint Semântico**: Atualização da memória de longo prazo após cada marco.
