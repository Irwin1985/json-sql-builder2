# gt Helper
Specifies the comparision **graeter than** `>` Operator as Helper.

#### Supported by
- [MySQL](https://dev.mysql.com/doc/refman/5.7/en/func-op-summary-ref.html)
- [MariaDB](https://mariadb.com/kb/en/library/greater-than/)
- [PostgreSQL](https://www.postgresql.org/docs/9.5/static/functions-comparison.html)
- [SQLite](https://sqlite.org/lang_expr.html)
- [Oracle](https://docs.oracle.com/html/A95915_01/sqopr.htm#sthref149)
- [SQLServer](https://docs.microsoft.com/en-US/sql/t-sql/language-elements/greater-than-transact-sql)

# Allowed Types and Usage

## as Primitive:

Usage of `gt` as **Primitive** with the following Syntax:

**Syntax:**

```javascript
$gt: < String | Number | Boolean >
```

**SQL-Definition:**
```javascript
> <value-param>
```

:bulb: **Example:**
```javascript
function() {
    return sql.build({
        $select: {
            $from: 'people',
            $where: {
                age: { $gt: 18 }
            }
        }
    });
}

// SQL output
SELECT
    *
FROM
    people
WHERE
    age > $1

// Values
{
    "$1": 18
}
```

## as Object:

Usage of `gt` as **Object** with the following Syntax:

**Syntax:**

```javascript
$gt: { ... }
```

**SQL-Definition:**
```javascript
> <value>
```

:bulb: **Example:**
```javascript
function() {
    let avgerageAge = {
        $select: {
            age: { $avg: 'age' },
            $from: 'people'
        }
    };

    return sql.build({
        $select: {
            $from: 'people',
            $where: {
                age: { $gt: avgerageAge }
            }
        }
    });
}

// SQL output
SELECT
    *
FROM
    people
WHERE
    age > (
        SELECT
            AVG(age) AS age
        FROM
            people
    )

// Values
{}
```

## as Function:

Usage of `gt` as **Function** with the following Syntax:

**Syntax:**

```javascript
$gt: sql.<callee>([params])
```

**SQL-Definition:**
```javascript
> <value>
```

:bulb: **Example:**
```javascript
function() {
    let myAvarageAgeFunction = sql.select({ age: { $avg: 'age' } }, {
        $from: 'people'
    });

    return sql.build({
        $select: {
            $from: 'people',
            $where: {
                age: { $gt: myAvarageAgeFunction }
            }
        }
    });
}

// SQL output
SELECT
    *
FROM
    people
WHERE
    age > (
        SELECT
            AVG(age) AS age
        FROM
            people
    )

// Values
{}
```

## Further Examples

:bulb: **Usage as SQL-Function**
```javascript
function() {
    let averageAge = 45;

    return sql.build({
        $select: {
            $from: 'people',
            $where: {
                age: sql.gt(averageAge)
            }
        }
    });
}

// SQL output
SELECT
    *
FROM
    people
WHERE
    age > $1

// Values
{
    "$1": 45
}
```

