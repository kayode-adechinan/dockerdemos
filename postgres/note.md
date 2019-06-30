## See the logs:

```
$ docker logs -f my_postgres
```

## Try running psql:

```
$ docker exec -it my_postgres psql -U postgres
```

## Create database

```
$ docker exec -it my_postgres psql -U postgres -c "create database my_database"
```

## Connect using Python and psycopg2

```
$ python3.6 -m venv myenv
$ source myenv/bin/activate
$ pip install psycopg2-binary
```

```python
# python myscript.py
import psycopg2

conn = psycopg2.connect(
    host='localhost',
    port=54320,
    dbname='my_database',
    user='postgres',
)
cur = conn.cursor()
cur.execute("CREATE TABLE IF NOT EXISTS test (id serial PRIMARY KEY, num integer, data varchar);")
cur.execute("INSERT INTO test (num, data) VALUES (%s, %s)", (100, "abcdef"))
cur.execute("SELECT * FROM test;")
result = cur.fetchone()
print(result)
conn.commit()
cur.close()
conn.close()
```