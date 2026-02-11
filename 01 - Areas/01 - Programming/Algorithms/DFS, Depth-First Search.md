---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - algorithms
  - programming
note type: Informational Note
---
Деревья это по сути [[BFS, Breadth-First Search|графы]] но только направленные в одну сторону. Также есть *родительские* и *дочерние* узлы, деревья не могут быть цикличны и должны быть последовательны. Последний узел на ветке называется *листовым* узлом.
Пример: 
![[IMG_1430.jpeg]]

Код снизу похож на поиск в ширину, но выполнен для вывода каждого файла в одной системе (дереве) папок. 
```python
from os import listdir
from os.path import isfile, join
from collections import deque

def printnames(start_dir):
	search_queue = deque()
	search_queue.append(start_dir)
while search_queue:
	dir = search_queue.popleft()
	for file in sorted(listdir(dir)):
		fullpath = join(dir, file)
		if isfile(fullpath):
			print(file) else:
		search_queue.append(fullpath)
		
printnames("pics")
```

Следующий код это хороший пример поиска в глубину, который реализован с помощью [[Стек и Рекурсия|рекурсии]] и выполняет ту же задачу, что и предыдущий. Его **главное** отличие это то, что он сначала доходит из корня до лиственного узла одной линии и затем переходит к другой.
```python
from os import listdir
from os.path import isfile, join

def printnames(dir):
	for file in 
	    sorted(listdir(dir)):
		fullpath = join(dir, file)
		if isfile(fullpath):
			print(file) else:
		printnames(fullpath)
		
printnames("pics")
```


**Бинарные деревья** это деревья каждый узел которых может иметь только 2 дочерних: 
![[IMG_1431.jpeg]]