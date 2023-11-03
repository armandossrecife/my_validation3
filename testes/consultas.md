# Consultas

Filtra as linhas de um dataframe baseado em uma lista
```python
df_inspected = df_issues_in_commits_with_critical_classes[df_issues_in_commits_with_critical_classes['issue_key'].isin(lista_keys)]
df_inspected
```
