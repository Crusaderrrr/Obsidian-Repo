---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - algorithms
note type: Informational Note
---
Этот алгоритм используется для поиска кратчайшего пути от одного узла к другому, но при этом он ищется не по количеству рёбер, а по их *весу*. Весом ребра может быть время затраченное на переход от родительского ребра к дочернему. 
**Шаги алгоритма Дейкстры**: 
1. Найти узел с наименьшей стоимостью (то есть узел, до которого можно добраться за минимальное время).
2. Обновить стоимости соседей этого узла (вскоре я объясню, что имеется в виду)
3. Повторять, пока это не будет сделано для всех узлов графа.
4. Вычислить итоговый путь.

**Например**: 
![[IMG_1571.png]]
- В этом графе мы начинаем с начала и устанавливаем стоимость каждого из дочерних узлов A - 6, B - 2
- Затем идём к узлу с наименьшим весом В
- Обновляем значения его дочерних узлов: Конец - 7, А - 5 (2 + 3) 
- Видим что к А можно добраться быстрее и делаем тоже самое с узлом А: Конец - 6 (2 + 3 + 1)
- Конце: в итоге получаем что кратчайший путь равен 6

**Взвешенный граф** это тот, у которого есть вес: 6 минут, 5$ и тд.
**Невзвешенный граф** это тот, у которого нет веса. 

Алгоритм Дейкстры работает только со взвешенными графами. 

Также графы должны не должны иметь **отрицательный вес**, или алгоритм не сработает. Доя таких графов существует другой алгоритм [Беллмана - Форда](https://medium.com/nuances-of-programming/%D0%BD%D0%B0%D0%B3%D0%BB%D1%8F%D0%B4%D0%BD%D0%BE%D0%B5-%D0%BE%D0%B1%D1%8A%D1%8F%D1%81%D0%BD%D0%B5%D0%BD%D0%B8%D0%B5-%D0%B0%D0%BB%D0%B3%D0%BE%D1%80%D0%B8%D1%82%D0%BC%D0%B0-%D0%B1%D0%B5%D0%BB%D0%BB%D0%BC%D0%B0%D0%BD%D0%B0-%D1%84%D0%BE%D1%80%D0%B4%D0%B0-775a32db3c77) 

Код алгоритма Дейкстры:

```Python
def find_lowest_cost_node(costs):
	lowest_cost = float("inf")
	lowest_cost_node = None
	for node in costs: #Перебрать все узлы
		cost = costs[node]
		if cost < lowest_cost and node not in processed:
			lowest_cost = cost
			lowest_cost_node = node
	return lowest_cost_node

node = find_lowest_cost_node(costs)
	while node is not None: cost = costs[node]
		cost = costs[node]
		neighbors = graph[node]
		for n in neighbors.keys(): 
			new_cost = cost + neighbors[n]
			if costs[n] > new_cost:
				costs[n] = new_cost 
				parents[n] = node 
		processed.append(node) 
		node = find_lowest_cost_node(costs)
```