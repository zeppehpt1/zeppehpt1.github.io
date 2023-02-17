Drop rows based on a condition in the column
 df = df.drop(df[df.score < 50].index)