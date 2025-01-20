# Guia de Troubleshooting - Nexus Ligas

## Problemas de Refresh

### 1. Falha Total
```text
# Sintoma
- Refresh não inicia ou falha completamente

# Verificações
1. Conectividade Datasul
2. Permissões banco
3. Recursos gateway
4. Logs de erro

# Soluções
1. Testar conexões
2. Verificar credenciais
3. Reiniciar gateway
4. Escalar suporte
```

### 2. Falha Parcial
```text
# Sintoma
- Algumas tabelas não atualizam

# Verificações
1. Queries específicas
2. Dependências
3. Timeouts
4. Transformações

# Soluções
1. Ajustar queries
2. Verificar joins
3. Aumentar timeouts
4. Otimizar código
```

## Problemas de Performance

### 1. Refresh Lento
```text
# Sintomas
- Tempo > 30 minutos
- Consumo alto recursos

# Análise
1. Monitor gateway
2. Profiler SQL
3. Log Power BI
4. Recursos servidor

# Otimizações
1. Ajustar queries
2. Particionar dados
3. Remover colunas
4. Comprimir strings
```

### 2. Consultas Lentas
```text
# Sintomas
- Filtros demorados
- Cálculos lentos
- Visualizações travando

# Análise
1. DAX Studio
2. Performance Analyzer
3. Vertipaq Analyzer
4. Query Plans

# Otimizações
1. Reescrever DAX
2. Ajustar relações
3. Criar agregações
4. Otimizar modelo
```

## Problemas de Dados

### 1. Inconsistências
```text
# Sintomas
- Totais não batem
- Dados divergentes
- Valores incorretos

# Verificações
1. Queries fonte
2. Transformações
3. Relacionamentos
4. Fórmulas DAX

# Soluções
1. Validar fonte
2. Revisar ETL
3. Checar modelo
4. Testar medidas
```

### 2. Dados Faltantes
```text
# Sintomas
- Registros ausentes
- Períodos vazios
- Dimensões incompletas

# Verificações
1. Filtros ETL
2. Joins queries
3. Relacionamentos
4. RLS/Segurança

# Soluções
1. Ajustar extração
2. Corrigir joins
3. Verificar chaves
4. Revisar permissões
```

## Problemas de Governança

### 1. Segurança
```text
# Sintomas
- Acessos indevidos
- RLS não funciona
- Permissões erradas

# Verificações
1. Configuração RLS
2. Grupos segurança
3. Permissões fonte
4. Logs acesso

# Soluções
1. Ajustar RLS
2. Atualizar grupos
3. Corrigir permissões
4. Auditar acessos
```

### 2. Versionamento
```text
# Sintomas
- Conflitos versão
- Mudanças perdidas
- Deployments falhos

# Verificações
1. Git status
2. Branch history
3. Deployment logs
4. Release notes

# Soluções
1. Resolver conflitos
2. Restaurar versão
3. Ajustar processo
4. Documentar mudanças
```

## Procedimentos de Emergência

### 1. Indisponibilidade
```text
# Ações Imediatas
1. Identificar causa
2. Comunicar usuários
3. Iniciar contingência
4. Acionar suporte

# Plano de Ação
1. Restaurar backup
2. Validar dados
3. Liberar acesso
4. Documentar incidente
```

### 2. Corrupção de Dados
```text
# Ações Imediatas
1. Isolar problema
2. Parar refresh
3. Avaliar impacto
4. Notificar gestores

# Plano de Ação
1. Identificar origem
2. Corrigir dados
3. Reprocessar ETL
4. Validar resultados
```

## Manutenção Preventiva

### 1. Checklist Diário
```text
# Verificações
1. Status refresh
2. Logs erro
3. Performance
4. Dados críticos

# Ações
1. Limpar cache
2. Verificar espaço
3. Monitorar uso
4. Backup rotina
```

### 2. Checklist Semanal
```text
# Verificações
1. Fragmentação
2. Uso recursos
3. Crescimento dados
4. Jobs agendados

# Ações
1. Otimizar modelo
2. Limpar histórico
3. Ajustar recursos
4. Validar schedules
```

### 3. Checklist Mensal
```text
# Verificações
1. Performance geral
2. Tendências uso
3. Segurança
4. Documentação

# Ações
1. Análise completa
2. Planejamento capacidade
3. Revisão acessos
4. Atualizar docs
```