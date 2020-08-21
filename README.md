# Tableau
## Intervalo de semanas no mês
Partindo de uma data qualquer, calcula todas as semanas do mês relativas a essa data (começando em domingo).
> A pasta de trabalho de exemplo destaca em qual semana se encontra a data selecionada.
### Semana 1
```js
IF
	[Data] >= DATETRUNC('month', [Data], 'sunday') // primeiro dia do mês
AND
	[Data] <= DATEADD('day', 7 - DATEPART('weekday', DATETRUNC('month', [Data], 'sunday')), DATETRUNC('month', [Data], 'sunday'))
THEN
    1
ELSE
    0
END
```
### Semana 2
```js
IF
	[Data] >= DATEADD('day', (1 * 7) - DATEPART('weekday', DATETRUNC('month', [Data], 'sunday')), DATETRUNC('month', [Data], 'sunday')) + 1
AND
	[Data] <= DATEADD('day', (2 * 7) - DATEPART('weekday', DATETRUNC('month', [Data], 'sunday')), DATETRUNC('month', [Data], 'sunday'))
THEN
    1
ELSE
    0
END
```
### Semana 3
```js
IF
	[Data] >= DATEADD('day', (2 * 7) - DATEPART('weekday', DATETRUNC('month', [Data], 'sunday')), DATETRUNC('month', [Data], 'sunday')) + 1
AND
	[Data] <= DATEADD('day', (3 * 7) - DATEPART('weekday', DATETRUNC('month', [Data], 'sunday')), DATETRUNC('month', [Data], 'sunday'))
THEN
    1
ELSE
    0
END
```
### Semana 4
```js
IF
	[Data] >= DATEADD('day', (3 * 7) - DATEPART('weekday', DATETRUNC('month', [Data], 'sunday')), DATETRUNC('month', [Data], 'sunday')) + 1
AND
	// verifica pois pode ser a última semana do mês (mês com 4 semanas)
	[Data] <= IIF(
        MONTH(DATEADD('day', (4 * 7) - DATEPART('weekday', DATETRUNC('month', [Data], 'sunday')), DATETRUNC('month', [Data], 'sunday'))) > MONTH([Data]) OR
        YEAR(DATEADD('day', (4 * 7) - DATEPART('weekday', DATETRUNC('month', [Data], 'sunday')), DATETRUNC('month', [Data], 'sunday'))) > YEAR([Data]),
        DATEADD('day', -1, DATEADD('month', 1, DATETRUNC('month', [Data]))),
        DATEADD('day', (4 * 7) - DATEPART('weekday', DATETRUNC('month', [Data], 'sunday')), DATETRUNC('month', [Data], 'sunday'))
    )
THEN
    1
ELSE
    0
END
```
### Semana 5
```js
IF
	[Data] >= DATEADD('day', (4 * 7) - DATEPART('weekday', DATETRUNC('month', [Data], 'sunday')), DATETRUNC('month', [Data], 'sunday')) + 1
AND
	// verifica pois pode ser a última semana do mês (mês com 5 semanas)
	[Data] <= IIF(
        MONTH(DATEADD('day', (5 * 7) - DATEPART('weekday', DATETRUNC('month', [Data], 'sunday')), DATETRUNC('month', [Data], 'sunday'))) > MONTH([Data]) OR
        YEAR(DATEADD('day', (5 * 7) - DATEPART('weekday', DATETRUNC('month', [Data], 'sunday')), DATETRUNC('month', [Data], 'sunday'))) > YEAR([Data]),
        DATEADD('day', -1, DATEADD('month', 1, DATETRUNC('month', [Data]))),
        DATEADD('day', (5 * 7) - DATEPART('weekday', DATETRUNC('month', [Data], 'sunday')), DATETRUNC('month', [Data], 'sunday'))
    )
THEN
    1
ELSE
    0
END
```
### Semana 6 (se chegou até aqui, essa será a última semana)
```js
IF
	[Data] >= DATEADD('day', (5 * 7) - DATEPART('weekday', DATETRUNC('month', [Data], 'sunday')), DATETRUNC('month', [Data], 'sunday')) + 1
AND
	[Data] <= DATEADD('day', -1, DATEADD('month', 1, DATETRUNC('month', [Data]))) // último dia do mês
THEN
    1
ELSE
    0
END
```