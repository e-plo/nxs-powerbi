# Procedimentos de Manutenção

## Rotinas Diárias

### 1. Refresh das Bases
```powershell
# Ordem de atualização
1. BU-OPERACIONAL (06:00)
2. BU-SOP (07:00)
3. BU-CORP (08:00)
```

### 2. Validações Diárias
- Verificar logs de refresh
- Conferir totais de controle
- Validar últimas datas
- Checar integridade dimensional

### 3. Backup
- Backup automático pós refresh
- Manter últimas 7 versões
- Testar restore mensalmente

## Rotinas Semanais

### 1. Limpeza
- Limpar cache
- Verificar espaço em disco
- Arquivar logs antigos

### 2. Verificações
- Testar conectividade
- Validar permissões
- Checar agendamentos

## Rotinas Mensais

### 1. Processo BGT/MRF
```powershell
# Calendário
- BGT: Dia 1 (após fechamento)
- MRF: Dia 15 (revisão mensal)
```

### 2. Manutenção Bases
- Compactar PBIXs
- Otimizar modelos
- Atualizar partições

### 3. Documentação
- Atualizar mudanças
- Revisar acessos
- Documentar incidentes

## Procedimentos de Emergência

### 1. Falha no Refresh
```powershell
# Sequência de ações
1. Verificar logs
2. Checar conexões
3. Validar fonte dados
4. Executar refresh manual
5. Documentar ocorrência
```

### 2. Restore
```powershell
# Processo de restore
1. Identificar versão
2. Copiar backup
3. Restaurar conexões
4. Validar dados
5. Liberar acesso
```

### 3. Contingência
- Usar última versão válida
- Comunicar usuários
- Executar plano correção

## Otimização de Performance

### 1. Modelo de Dados
- Remover colunas não usadas
- Otimizar tipos de dados
- Verificar relacionamentos

### 2. DAX
- Revisar medidas complexas
- Identificar gargalos
- Otimizar cálculos

### 3. Refresh
- Ajustar particionamento
- Otimizar consultas
- Configurar incremental refresh

## Segurança

### 1. Acessos
- Revisar RLS
- Atualizar grupos
- Auditar logs

### 2. Dados
- Backup diário
- Criptografia
- Classificação dados

### 3. Governança
- Políticas de uso
- Treinamento
- Documentação

## Monitoramento

### 1. Performance
```powershell
# Métricas
- Tempo refresh
- Tamanho arquivo
- Tempo resposta
- Uso memória
```

### 2. Utilização
- Número usuários
- Relatórios acessados
- Horários pico
- Features usadas

### 3. Qualidade
- Acurácia dados
- Tempo atualização
- Disponibilidade
- Satisfação usuário