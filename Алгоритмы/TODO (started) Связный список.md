---
aliases:
  - linked lists
  - связный список
  - LinkedList
---
### Что такое LinkedList?
LinkedList или связный список – это структура данных. Связный список обеспечивает возможность создать двунаправленную очередь из каких-либо элементов. Каждый элемент такого списка считается узлом. По факту в узле есть его значение, а также две ссылки – на предыдущий и на последующий узлы. То есть список «связывается» узлами, которые помогают двигаться вверх или вниз по списку. Из-за таких особенностей строения из связного списка можно организовать стек, очередь или двойную очередь.  
  
Давайте визуализируем сухие определения. Теперь у нас есть коты, которые сидят в коробках. И на каждой коробке написано какая она по порядку и за какой должна стоять.  
  
![](https://habrastorage.org/r/w1560/webt/bu/ps/qq/bupsqqzfejptv3cupqjugmawlcq.png)  
  
**Что мы будем делать со связным списком:**  
  
1. Проверять содержится ли в нем тот или иной элемент;
2. Добавлять узлы в конец;
3. Получать значение узла по индексу;
4. Удалять узлы.

  На самом деле опций по работе с ними гораздо больше, но остановимся мы именно на реализации этих основных шагов. Поняв, по какому принципу они строятся, вы сами с легкостью сможете реализовать свои собственные методы.

Начать придется с создания двух классов:  
  ```python
class Box:
  def __init__ (self,cat = None):
    self.cat = cat
    self.nextcat = None

class LinkedList:
  def __init__(self):
    self.head = None
```
В общем случае, у нас получился узел, у которого есть внутри какое-то значение – кот, и ссылка на следующий узел. То есть в классе `Box`, соответственно, есть кот и ссылка на следующую коробку. Как и у любого списка, у связного тоже есть начало, а именно head. Поскольку изначально там ничего нет, начальному элементу присваивается значение `None`.

### Содержится ли элемент в списке
  
![](https://habrastorage.org/r/w1560/webt/le/1b/pq/le1bpq792tq3byqqdbr1ah3lzew.png)  
  
Начнем с простого. Чтобы проверить есть ли какой-то определенный кот в одной из последовательно расположенных коробок, нужно пройтись циклом по всему списку, сверяя имеющееся значение со значениями элемента в списке.  
  
```python
def contains (self, cat):
    lastbox = self.head
    while (lastbox):
      if cat == lastbox.cat:
        return True
      else:
        lastbox = lastbox.nextcat
    return False
```

### Добавить узел в конец списка

![](https://habrastorage.org/r/w1560/webt/cy/ml/do/cymldocexrtjvvfvbgu9chpfoco.png)  
  
Для начала новую коробку нужно создать, а уже в нее поместить нового кота. После необходимо проверять начиная с начала связного списка, есть ли в текущем узле ссылка на следующий и если она есть, то переходить к нему, в противном случае узел — последний, значит нужно создавать ссылку на следующий узел и помещать в него ту самую новую коробку, которую мы создали.  

```python
def addToEnd(self, newcat):
    newbox = Box(newcat)
    if self.head is None:
      self.head = newbox
      return
    lastbox = self.head
    while (lastbox.nextcat):
        lastbox = lastbox.nextcat
    lastbox.nextcat = newbox
```

### Получить узел по индексу
  
![](https://habrastorage.org/r/w1560/webt/eq/s-/w3/eqs-w3pbz1qyx3eyzujo-g9zips.png)  
  
По индексу `catIndex` мы хотим получить узел-коробку, но поскольку как такового индекса у узлов не предусмотрено, нужно придумать какую-то замену, а именно переменную, которая будет выполнять роль индекса. Эта переменная – это `boxIndex`. Мы проходимся по всему списку и сверяем «порядковый номер» узла, и при совпадении его с искомым индексом – выдаем результат.

```python
 def get(self, catIndex):
    lastbox = self.head
    boxIndex = 0
    while boxIndex <= catIndex:
      if boxIndex == catIndex:
          return lastbox.cat
      boxIndex = boxIndex + 1
      lastbox = lastbox.nextcat
```

### Удалить узел
  
![](https://habrastorage.org/r/w1560/webt/bq/vu/y2/bqvuy2bdnqimrbliezpyrwdbovm.png)  
  
Здесь мы рассмотрим удаление элемента не по индексу, а по значению, чтобы внести хоть какое-то разнообразие.  
  
Поиск начинается с головы списка, то есть с первой по счету коробки, и продолжается, пока коробки не закончатся, то есть пока `headcat` не станет `None`. Мы проверяем соответствует ли значение, хранящееся в текущем узле, тому, которое мы хотим удалить. Если нет, то мы просто идем дальше. Однако, если соответствует, то мы удаляем его и «перепривязываем» ссылки, то есть мы удаляем N-ую коробку, при этом коробка N-1 теперь ссылается на коробку N+1.

```python
 def removeBox(self,rmcat):
    headcat = self.head

    if headcat is not None:
      if headcat.cat==rmcat:
        self.head = headcat.nextcat
        headcat = None
        return
    while headcat is not None:
      if headcat.cat==rmcat:
        break
      lastcat = headcat
      headcat = headcat.nextcat
    if headcat == None:
      return
    lastcat.nextcat = headcat.nextcat
    headcat = None
```

### Применение в решении задач
[876. Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/)

Given the `head` of a singly linked list, return _the middle node of the linked list_.
If there are two middle nodes, return **the second middle** node.

**Example 1:**
![](https://assets.leetcode.com/uploads/2021/07/23/lc-midlist1.jpg)

**Input:** `head = [1,2,3,4,5]`
**Output:** `[3,4,5]`
**Explanation:** The middle node of the list is node 3.

**Example 2:**
![](https://assets.leetcode.com/uploads/2021/07/23/lc-midlist2.jpg)

**Input:** `head = [1,2,3,4,5,6]`
**Output:** `[4,5,6]`
**Explanation:** Since the list has two middle nodes with values 3 and 4, we return the second one.

```python
def middleNode(head: Optional[ListNode]) -> Optional[ListNode]:
	
```

https://www.youtube.com/watch?v=lvO88XxNAzs&t=1712s