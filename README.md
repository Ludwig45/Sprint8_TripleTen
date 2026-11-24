# Análise ConnectaTel — Perfil e segmentação de clientes

Projeto do Sprint 8 do MBA em Análise de Dados e IA. O objetivo é analisar o comportamento dos clientes da ConnectaTel, empresa de telecomunicações da América Latina, com dados registrados até 2024. A análise identifica padrões de consumo, comportamentos atípicos e segmentos de clientes, e leva a recomendações para retenção e para os planos oferecidos.

## Datasets

Os três arquivos são carregados direto de URLs públicas, então não é preciso baixar nada para rodar o notebook.

| Arquivo | Conteúdo |
| --- | --- |
| `plans.csv` | Catálogo de planos: preço, minutos e GB incluídos, custo por extra |
| `users_brasil.csv` | Clientes: idade, cidade, data de cadastro, plano e churn |
| `usage.csv` | Uso real dos serviços: chamadas, mensagens, duração e comprimento das mensagens |

## Etapas da análise

1. **Carregar e explorar:** leitura dos três datasets, `head()`, `shape` e `info()`.
2. **Qualidade dos dados:** contagem e proporção de valores ausentes, detecção de sentinels (`-999` em `age`, `"?"` em `city`) e revisão dos anos em `reg_date` e `date`.
3. **Limpeza básica:** `-999` substituído pela mediana de `age`, `"?"` convertido em `NA`, datas fora de 2024 marcadas como ausentes e verificação de que os nulos de `duration` e `length` dependem de `type` (MAR).
4. **Estatísticas por usuário:** agregação de `usage` por `user_id` (`quant_mensagens`, `quant_chamadas`, `quant_minutos_chamada`) e junção com `users`, gerando `user_profile`.
5. **Distribuições e outliers:** histogramas por plano, boxplots e limites pelo método IQR.
6. **Segmentação:** `grupo_uso` (Baixo uso, Uso médio, Alto uso) e `grupo_idade` (Jovem, Adulto, Idoso), com gráficos de contagem.
7. **Insight executivo:** conclusões e recomendações comerciais para os stakeholders.

### Regras de segmentação

| Grupo | Regra |
| --- | --- |
| Baixo uso | chamadas < 5 e mensagens < 5 |
| Uso médio | chamadas < 10 e mensagens < 10 |
| Alto uso | demais casos |
| Jovem | idade < 30 |
| Adulto | idade < 60 |
| Idoso | demais casos |

## Como executar

1. Abra o notebook no [Google Colab](https://colab.research.google.com/) (`File → Upload notebook`) ou em um Jupyter local.
2. Use um ambiente com acesso à internet, porque os dados são lidos de URLs.
3. Execute todas as células em ordem (`Runtime → Run all`).

Bibliotecas usadas: `pandas`, `numpy`, `seaborn` e `matplotlib`. Para rodar localmente:

```bash
pip install pandas numpy seaborn matplotlib jupyter
```

## Guia de reprodução

- Execute as células na ordem, sem pular etapas: a limpeza da etapa 3 altera `users` e `usage` em memória, e as etapas seguintes dependem disso.
- Para repetir a análise do zero, reinicie o kernel e rode tudo de novo.
- As decisões de limpeza e os critérios de segmentação estão documentados nos comentários do notebook.

## Estrutura do repositório

```
.
├── README.md
└── Project_ConnectaTel.ipynb
```

## Autor

Enzo Manfredi — [GitHub](https://github.com/EnzoMakers)
