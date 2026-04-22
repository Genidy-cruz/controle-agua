# 📊 Respostas - App de Ingestão de Água

## 👤 Usuários

### 1. Quantos usuários estão cadastrados no sistema?
SQL:
SELECT COUNT(*) FROM usuarios;

Resposta:
| count |
| 5     |

---

### 2. Qual o peso médio dos usuários?
SQL:
SELECT AVG(peso) FROM usuarios;

Resposta:
| avg                 |
| 73.0000000000000000 |

---

### 3. Qual usuário possui a maior meta diária?
SQL:
SELECT * FROM usuarios ORDER BY meta_diaria_ml DESC LIMIT 1;

Resposta:
| id                                   | nome        | email            | peso  | meta_diaria_ml | criado_em                 |
| ------------------------------------ | ----------- | ---------------- | ----- | -------------- | ------------------------- |
| 33333333-3333-3333-3333-333333333333 | Carlos Lima | carlos@email.com | 90.00 | 3150           | 2026-04-22 14:41:21.61713 |

---

### 4. Qual usuário possui a menor meta diária?
SQL:
SELECT * FROM usuarios ORDER BY meta_diaria_ml ASC LIMIT 1;

Resposta:
| id                                   | nome      | email         | peso  | meta_diaria_ml | criado_em                 |
| ------------------------------------ | --------- | ------------- | ----- | -------------- | ------------------------- |
| 44444444-4444-4444-4444-444444444444 | Ana Paula | ana@email.com | 55.00 | 2000           | 2026-04-22 14:41:21.61713 |

---

## 💧 Consumo de água

### 5. Qual o total de água ingerido por cada usuário?
SQL:
SELECT usuario_id, SUM(quantidade_ml) 
FROM ingestao_agua 
GROUP BY usuario_id;

Resposta:
| usuario_id                           | sum   |
| ------------------------------------ | ----- |
| 55555555-5555-5555-5555-555555555555 | 12300 |
| 11111111-1111-1111-1111-111111111111 | 12300 |
| 33333333-3333-3333-3333-333333333333 | 12300 |
| 22222222-2222-2222-2222-222222222222 | 12300 |
| 44444444-4444-4444-4444-444444444444 | 12300 |

---

### 6. Qual o total de água ingerido em um dia específico?
SQL:
SELECT DATE(data_hora), SUM(quantidade_ml)
FROM ingestao_agua
GROUP BY DATE(data_hora);

Resposta:
| date       | sum   |
| ---------- | ----- |
| 2026-04-18 | 10250 |
| 2026-04-19 | 10250 |
| 2026-04-16 | 10250 |
| 2026-04-20 | 10250 |
| 2026-04-17 | 10250 |
| 2026-04-15 | 10250 |

---

### 7. Qual o usuário que mais bebeu água no período?
SQL:
SELECT usuario_id, SUM(quantidade_ml) AS total
FROM ingestao_agua
GROUP BY usuario_id
ORDER BY total DESC
LIMIT 1;

Resposta:
| usuario_id                           | total |
| ------------------------------------ | ----- |
| 55555555-5555-5555-5555-555555555555 | 12300 |

---

### 8. Qual o usuário que menos bebeu água no período?
SQL:
SELECT usuario_id, SUM(quantidade_ml) AS total
FROM ingestao_agua
GROUP BY usuario_id
ORDER BY total ASC
LIMIT 1;

Resposta:
| usuario_id                           | total |
| ------------------------------------ | ----- |
| 55555555-5555-5555-5555-555555555555 | 12300 |

---

### 9. Qual o consumo médio diário por usuário?
SQL:
SELECT usuario_id, AVG(total_ml)
FROM resumo_diario_agua
GROUP BY usuario_id;

Resposta:
| usuario_id                           | avg                   |
| ------------------------------------ | --------------------- |
| 44444444-4444-4444-4444-444444444444 | 2050.0000000000000000 |
| 33333333-3333-3333-3333-333333333333 | 2050.0000000000000000 |
| 22222222-2222-2222-2222-222222222222 | 2050.0000000000000000 |
| 11111111-1111-1111-1111-111111111111 | 2050.0000000000000000 |
| 55555555-5555-5555-5555-555555555555 | 2050.0000000000000000 |

---

### 10. Qual o consumo médio por ingestão (copo)?
SQL:
SELECT AVG(quantidade_ml) FROM ingestao_agua;

Resposta:
| avg                  |
| -------------------- |
| 292.8571428571428571 |

---

## 📅 Análise por dia

### 11. Quanto cada usuário bebeu por dia?
SQL:
SELECT usuario_id, DATE(data_hora), SUM(quantidade_ml)
FROM ingestao_agua
GROUP BY usuario_id, DATE(data_hora);

Resposta:
| usuario_id                           | date       | sum  |
| ------------------------------------ | ---------- | ---- |
| 11111111-1111-1111-1111-111111111111 | 2026-04-19 | 2050 |
| 44444444-4444-4444-4444-444444444444 | 2026-04-15 | 2050 |
| 11111111-1111-1111-1111-111111111111 | 2026-04-16 | 2050 |
| 33333333-3333-3333-3333-333333333333 | 2026-04-18 | 2050 |
| 55555555-5555-5555-5555-555555555555 | 2026-04-17 | 2050 |
| 22222222-2222-2222-2222-222222222222 | 2026-04-19 | 2050 |
| 11111111-1111-1111-1111-111111111111 | 2026-04-20 | 2050 |
| 22222222-2222-2222-2222-222222222222 | 2026-04-18 | 2050 |
| 33333333-3333-3333-3333-333333333333 | 2026-04-19 | 2050 |
| 22222222-2222-2222-2222-222222222222 | 2026-04-17 | 2050 |
| 33333333-3333-3333-3333-333333333333 | 2026-04-16 | 2050 |
| 33333333-3333-3333-3333-333333333333 | 2026-04-20 | 2050 |
| 55555555-5555-5555-5555-555555555555 | 2026-04-19 | 2050 |
| 55555555-5555-5555-5555-555555555555 | 2026-04-15 | 2050 |
| 11111111-1111-1111-1111-111111111111 | 2026-04-18 | 2050 |
| 44444444-4444-4444-4444-444444444444 | 2026-04-18 | 2050 |
| 11111111-1111-1111-1111-111111111111 | 2026-04-17 | 2050 |
| 55555555-5555-5555-5555-555555555555 | 2026-04-18 | 2050 |
| 44444444-4444-4444-4444-444444444444 | 2026-04-17 | 2050 |
| 55555555-5555-5555-5555-555555555555 | 2026-04-16 | 2050 |
| 33333333-3333-3333-3333-333333333333 | 2026-04-15 | 2050 |
| 44444444-4444-4444-4444-444444444444 | 2026-04-19 | 2050 |
| 22222222-2222-2222-2222-222222222222 | 2026-04-15 | 2050 |
| 33333333-3333-3333-3333-333333333333 | 2026-04-17 | 2050 |
| 11111111-1111-1111-1111-111111111111 | 2026-04-15 | 2050 |
| 44444444-4444-4444-4444-444444444444 | 2026-04-16 | 2050 |
| 22222222-2222-2222-2222-222222222222 | 2026-04-16 | 2050 |
| 55555555-5555-5555-5555-555555555555 | 2026-04-20 | 2050 |
| 44444444-4444-4444-4444-444444444444 | 2026-04-20 | 2050 |
| 22222222-2222-2222-2222-222222222222 | 2026-04-20 | 2050 |

---

### 12. Qual foi o dia com maior consumo total de água?
SQL:
SELECT DATE(data_hora) AS dia, SUM(quantidade_ml) AS total
FROM ingestao_agua
GROUP BY dia
ORDER BY total DESC
LIMIT 1;

Resposta:
| dia        | total |
| ---------- | ----- |
| 2026-04-18 | 10250 |

---

### 13. Qual foi o dia com menor consumo total?
SQL:
SELECT DATE(data_hora) AS dia, SUM(quantidade_ml) AS total
FROM ingestao_agua
GROUP BY dia
ORDER BY total ASC
LIMIT 1;

Resposta:
| dia        | total |
| ---------- | ----- |
| 2026-04-18 | 10250 |

---

### 14. Quantos registros de ingestão existem por dia?
SQL:
SELECT DATE(data_hora), COUNT(*)
FROM ingestao_agua
GROUP BY DATE(data_hora);

Resposta:
| date       | count |
| ---------- | ----- |
| 2026-04-18 | 35    |
| 2026-04-19 | 35    |
| 2026-04-16 | 35    |
| 2026-04-20 | 35    |
| 2026-04-17 | 35    |
| 2026-04-15 | 35    |

---

## 🎯 Metas

### 15. Qual usuário atingiu a meta diária em cada dia?
SQL:
SELECT r.usuario_id, r.data, r.total_ml, m.meta_ml
FROM resumo_diario_agua r
JOIN metas_diarias m 
ON r.usuario_id = m.usuario_id AND r.data = m.data
WHERE r.total_ml >= m.meta_ml;

Resposta:
| usuario_id                           | data       | total_ml | meta_ml |
| ------------------------------------ | ---------- | -------- | ------- |
| 44444444-4444-4444-4444-444444444444 | 2026-04-15 | 2050     | 2000    |
| 44444444-4444-4444-4444-444444444444 | 2026-04-18 | 2050     | 2000    |
| 44444444-4444-4444-4444-444444444444 | 2026-04-17 | 2050     | 2000    |
| 44444444-4444-4444-4444-444444444444 | 2026-04-19 | 2050     | 2000    |
| 44444444-4444-4444-4444-444444444444 | 2026-04-16 | 2050     | 2000    |
| 44444444-4444-4444-4444-444444444444 | 2026-04-20 | 2050     | 2000    |

---

### 16. Quantos dias cada usuário bateu a meta?
SQL:
SELECT r.usuario_id, COUNT(*) AS dias
FROM resumo_diario_agua r
JOIN metas_diarias m 
ON r.usuario_id = m.usuario_id AND r.data = m.data
WHERE r.total_ml >= m.meta_ml
GROUP BY r.usuario_id;

Resposta:
| usuario_id                           | dias |
| ------------------------------------ | ---- |
| 44444444-4444-4444-4444-444444444444 | 6    |

---

### 17. Qual a porcentagem da meta atingida por dia por usuário?
SQL:
SELECT r.usuario_id, r.data,
(r.total_ml * 100.0 / m.meta_ml) AS porcentagem
FROM resumo_diario_agua r
JOIN metas_diarias m 
ON r.usuario_id = m.usuario_id AND r.data = m.data;

Resposta:
| usuario_id                           | data       | porcentagem          |
| ------------------------------------ | ---------- | -------------------- |
| 11111111-1111-1111-1111-111111111111 | 2026-04-19 | 73.2142857142857143  |
| 44444444-4444-4444-4444-444444444444 | 2026-04-15 | 102.5000000000000000 |
| 11111111-1111-1111-1111-111111111111 | 2026-04-16 | 73.2142857142857143  |
| 33333333-3333-3333-3333-333333333333 | 2026-04-18 | 65.0793650793650794  |
| 55555555-5555-5555-5555-555555555555 | 2026-04-17 | 78.8461538461538462  |
| 22222222-2222-2222-2222-222222222222 | 2026-04-19 | 89.1304347826086957  |
| 11111111-1111-1111-1111-111111111111 | 2026-04-20 | 73.2142857142857143  |
| 22222222-2222-2222-2222-222222222222 | 2026-04-18 | 89.1304347826086957  |
| 33333333-3333-3333-3333-333333333333 | 2026-04-19 | 65.0793650793650794  |
| 22222222-2222-2222-2222-222222222222 | 2026-04-17 | 89.1304347826086957  |
| 33333333-3333-3333-3333-333333333333 | 2026-04-16 | 65.0793650793650794  |
| 33333333-3333-3333-3333-333333333333 | 2026-04-20 | 65.0793650793650794  |
| 55555555-5555-5555-5555-555555555555 | 2026-04-19 | 78.8461538461538462  |
| 55555555-5555-5555-5555-555555555555 | 2026-04-15 | 78.8461538461538462  |
| 11111111-1111-1111-1111-111111111111 | 2026-04-18 | 73.2142857142857143  |
| 44444444-4444-4444-4444-444444444444 | 2026-04-18 | 102.5000000000000000 |
| 11111111-1111-1111-1111-111111111111 | 2026-04-17 | 73.2142857142857143  |
| 55555555-5555-5555-5555-555555555555 | 2026-04-18 | 78.8461538461538462  |
| 44444444-4444-4444-4444-444444444444 | 2026-04-17 | 102.5000000000000000 |
| 55555555-5555-5555-5555-555555555555 | 2026-04-16 | 78.8461538461538462  |
| 33333333-3333-3333-3333-333333333333 | 2026-04-15 | 65.0793650793650794  |
| 44444444-4444-4444-4444-444444444444 | 2026-04-19 | 102.5000000000000000 |
| 22222222-2222-2222-2222-222222222222 | 2026-04-15 | 89.1304347826086957  |
| 33333333-3333-3333-3333-333333333333 | 2026-04-17 | 65.0793650793650794  |
| 11111111-1111-1111-1111-111111111111 | 2026-04-15 | 73.2142857142857143  |
| 44444444-4444-4444-4444-444444444444 | 2026-04-16 | 102.5000000000000000 |
| 22222222-2222-2222-2222-222222222222 | 2026-04-16 | 89.1304347826086957  |
| 55555555-5555-5555-5555-555555555555 | 2026-04-20 | 78.8461538461538462  |
| 44444444-4444-4444-4444-444444444444 | 2026-04-20 | 102.5000000000000000 |
| 22222222-2222-2222-2222-222222222222 | 2026-04-20 | 89.1304347826086957  |

---

### 18. Qual usuário tem melhor desempenho (mais dias com meta atingida)?
SQL:
SELECT r.usuario_id, COUNT(*) AS dias
FROM resumo_diario_agua r
JOIN metas_diarias m 
ON r.usuario_id = m.usuario_id AND r.data = m.data
WHERE r.total_ml >= m.meta_ml
GROUP BY r.usuario_id
ORDER BY dias DESC
LIMIT 1;

Resposta:
| usuario_id                           | dias |
| ------------------------------------ | ---- |
| 44444444-4444-4444-4444-444444444444 | 6    |

---

## 🧠 Inteligência / Produto

### 19. Em quais horários ocorre maior consumo de água?
SQL:
SELECT EXTRACT(HOUR FROM data_hora) AS hora, SUM(quantidade_ml) AS total
FROM ingestao_agua
GROUP BY hora
ORDER BY total DESC;

Resposta:
| hora | total |
| ---- | ----- |
| 16   | 12000 |
| 14   | 10500 |
| 20   | 9000  |
| 12   | 9000  |
| 18   | 7500  |
| 10   | 7500  |
| 8    | 6000  |

---

### 20. Qual o intervalo médio entre ingestões por usuário?
SQL:
SELECT usuario_id, AVG(diff) 
FROM (
    SELECT usuario_id,
    EXTRACT(EPOCH FROM (data_hora - LAG(data_hora) OVER (PARTITION BY usuario_id ORDER BY data_hora))) AS diff
    FROM ingestao_agua
) sub
WHERE diff IS NOT NULL
GROUP BY usuario_id;

Resposta:
| usuario_id                           | avg                |
| ------------------------------------ | ------------------ |
| 11111111-1111-1111-1111-111111111111 | 11590.243902439024 |
| 22222222-2222-2222-2222-222222222222 | 11590.243902439024 |
| 33333333-3333-3333-3333-333333333333 | 11590.243902439024 |
| 44444444-4444-4444-4444-444444444444 | 11590.243902439024 |
| 55555555-5555-5555-5555-555555555555 | 11590.243902439024 |
