## INTEGRANTES DO GRUPO: GILVAN FELIPE, JUDSON GABRIEL, NICOLAS FRANCO, THALES MIGUEL


## Justificativas Técnicas

Esta seção apresenta as decisões de modelagem e implementação adotadas no projeto UPA Monitor, explicando como elas contribuem para a integridade dos dados, a confiabilidade dos indicadores e a eficiência das consultas SQL.

### 1. Decisões de modelagem

#### 1.1. Organização das entidades

O modelo foi dividido em entidades com responsabilidades específicas, reduzindo a redundância e facilitando a manutenção dos dados.

| Entidade | Justificativa |
|---|---|
| `UPA` | Identifica as unidades de pronto atendimento. |
| `SETOR` | Organiza os setores vinculados a cada unidade. |
| `PACIENTE` | Permite identificar pacientes sem repetir seus dados em cada atendimento. |
| `ATENDIMENTO` | Registra os episódios de atendimento e seus horários. |
| `FILA` | Representa as filas disponíveis nos setores. |
| `FILA_ATENDIMENTO` | Registra a entrada, a saída e o status dos atendimentos nas filas. |
| `TRIAGEM` | Armazena as avaliações clínicas realizadas durante o atendimento. |
| `CLASSIFICACAO_RISCO` | Centraliza as categorias e os níveis de prioridade clínica. |
| `PROFISSIONAL` | Identifica os profissionais responsáveis pelas atividades previstas no modelo. |
| `MONITORAMENTO` | Registra as coletas de informações das unidades. |
| `MEDICAO` | Permite armazenar valores históricos de indicadores. |

#### 1.2. Separação entre triagem e medição

A separação dessas entidades evita misturar informações clínicas individuais com indicadores estatísticos.

- `TRIAGEM`: representa a avaliação clínica de um paciente, incluindo sua classificação de risco.
- `MEDICAO`: representa um valor quantitativo associado ao monitoramento de uma unidade ou setor.

Indicadores como a quantidade de pacientes aguardando podem ser calculados diretamente por consultas SQL. Portanto, a entidade `MEDICAO` é necessária principalmente quando se deseja armazenar resultados históricos, e não apenas calcular valores sob demanda.

#### 1.3. Chaves e integridade referencial

As chaves foram definidas para garantir a identificação dos registros e os relacionamentos entre as entidades.

| Chave | Finalidade |
|---|---|
| PK — Primary Key | Identifica unicamente cada registro. |
