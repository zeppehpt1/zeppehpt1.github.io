Drop rows based on a condition in the column
```python
df = df.drop(df[df.score < 50].index)
```

Access value from other column based on value
```python
located_value = df.loc[df.column1 == selected_value, 'desired_column'].values[0]
```