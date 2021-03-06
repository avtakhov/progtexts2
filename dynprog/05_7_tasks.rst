Дополнительные задачи
=====================



.. task::

    Найти число способов разложить данное число :math:`N` в сумму
    слагаемых: а) считая разложения, различающиеся порядком слагаемых,
    различными; б) считая разложения, различающиеся порядком слагаемых,
    одинаковыми; в) считая разложения, различающиеся порядком слагаемых,
    одинаковыми и требуя, чтобы все слагаемые в каждом разложении были
    различны; г) и т.п.
    |
    |
    Может быть, тут тоже все проще понять, если
    подумать, как бы вы писали перебор (а в переборе была такая задача :) ).
    Например, вариант а: разложения, различающиеся порядком слагаемых,
    считаются различными. Как бы мы писали перебор: мы бы просто перебирали,
    какое будет очередное слагаемое, и для каждого варианта запускались бы
    рекурсивно. Можно это сделать функцией, которая будет возвращать число
    способов разбиения на слагаемые того, что осталось. Если попытаться
    теперь это превратить в рекурсию с запоминанием результата, то какие
    вызовы функций нам надо объединить, т.е. какие вызовы будут возвращать
    один и тот же результат? Ну ясно, те, которые просто считают число
    способов разбиения для одного и того же числа (т.е. единственный важный
    тут параметр — это сколько нам осталось разбить). Т.е. теперь в динамике
    будем считать :math:`ans[i]` — количество способов разбиения на
    слагаемые числа :math:`i` — и, перебирая первое слагаемое, будем сводить
    к более мелким подзадачам.
    
    А если вариант б: разложения, отличающиеся лишь порядком слагаемых,
    считаем одинаковыми? В переборе уже была у нас полезная идея: учесть это
    требование можно, потребовав, чтобы в разложении слагаемые были
    отсортированы. Как мы тут стали бы писать перебор? Опять, наша функция
    перебирала бы первое слагаемое и запускалась бы рекурсивно, но теперь
    это слагаемое нужно перебирать лишь до некоторого :math:`k`, где
    :math:`k` — это предыдущее слагаемое в разложении (т.е. то, которое мы
    выбрали на предыдущем уровне рекурсии; если мутно, то отвлекитесь и
    сначала напишите или в уме продумайте реализацию перебора). (Я считаю,
    что мы потребовали, чтобы слагаемые убывали; если же хотим, чтобы
    слагаемые возрастали, то перебирать будем от :math:`k` до максимума — до
    :math:`N`, видимо). Соответственно, теперь параметрами динамики будут
    :math:`i` и :math:`k` и будем считать число способов разбиения числа
    :math:`i` на слагаемые, не превосходящие \ :math:`k`.
    
    Остальные варианты разбираются аналогично.
    |



.. task::

    Найти число правильных скобочных последовательностей,
    состоящих из :math:`N` пар скобок. [Коротко говоря, правильная скобочная
    последовательность — это последовательность открывающих и закрывающих
    скобок, в которой скобки сбалансированы. ``(())`` — это правильная скобочная
    последовательность из двух пар скобок, ``()()`` — тоже, а ``)()(`` и ``())(`` — нет.
    Я надеюсь, смысл определения понятен]. 
    
    а) Используя только круглые
    скобки; 
    
    б) используя круглые, квадратные и фигурные скобки: ``()[]``, ``[{}]`` —
    правильные, а ``({)}`` и ``)()(`` — нет.
    
    Научитесь выводить скобочную последовательность по номеру.
    |
    а) Тут
    есть два решения.
    
    Одно основано на понятии баланса, т.е. разницы между числом открывающих
    и закрывающих скобок в некоторой строке. Строка является правильной
    скобочной последовательностью, если баланс любого её начала
    :math:`\geq 0`, а баланс всей строки равен нулю. Ну так давайте для
    каждого :math:`i` и :math:`j` посчитаем, сколько есть строк длины
    :math:`i` из символов ’(’ и ’)’ с балансом :math:`j`.
    
    Второе вариант — правильная с.п. начинается, конечно, на открывающую
    скобку. Где будет парная к ней закрывающая? Пусть в позиции :math:`2k`
    (позиция, очевидно, должна быть чётной), тогда очевидно, что между ними
    — любая правильная с.п. из :math:`k-1` пары скобок, а после — любая
    правильная с.п. из :math:`N-k` пар. Дальше просто.
    
    Подумайте, можно ли и как эти решения обобщить на пункт б).
    |
    Про
    пункт а). В первом решении считаем :math:`ans[i,j]`, при этом при
    :math:`j>0` получаем :math:`ans[i,j]=ans[i-1,j+1]+ans[i-1,j-1]`, а при
    :math:`j=0` — :math:`ans[i,j]=ans[i-1,1]`.
    
    Во втором решении
    
    .. math:: ans[i]=\sum_{k=1}^N ans[k-1]\cdot ans[N-k],
    
    здесь база динамики — :math:`ans[0]=1`.
    
    Про пункт б). Первое решение я не знаю, как обобщить, а вот второе —
    легко. Первая скобка может быть любого из 3 видов, и для каждого
    варианта у нас будет :math:`\sum_{k=1}^N ans[k-1]\cdot ans[N-k]`
    последовательностей. Итого
    
    .. math:: ans[i]=3\sum_{k=1}^N ans[k-1]\cdot ans[N-k].
    
    Можно считать по этой формуле, но вообще сразу понятно, что ответ на
    задачу б) — это ответ на задачу а), умноженный на :math:`3^N` :).
    |



.. task::

    Сколькими способами можно замостить доску :math:`N\times M`
    доминошками?
    |
    ДП по профилю.
    |
    Посмотрим заполнение доски
    :math:`N\times i`, причём в :math:`i`-ом столбце разрешим некоторым
    доминошкам вылезать за край доски на одну клетку. То, в каких именно
    строках они будут вылезать, и будет профилем. Дальше думайте сами, тут
    немного сложнее обычного определить, какой профиль может следовать за
    каким.
    |



.. task::

    Дана строка :math:`s`, состоящая из букв, и маска :math:`m`.
    Маска может содержать буквы, символы ``*`` и ``?``. Звёздочка может
    обозначать любую строку (в т.ч. пустую), а знак вопроса — любой символ.
    Подходит ли данная строка под эту маску?
    (Например, строка ``abcdefg`` подходит под маску ``ab*f?``, но не под ``ab?f?``.)
    |
    Двумерное ДП. Придумайте
    решение за :math:`O(NM)`.
    |
    Для каждого :math:`i` и :math:`j`
    определим, подходят ли первые :math:`i` символов строки под первые
    :math:`j` символов маски. Если :math:`j`-ый символ маски — буква, то все
    легко: либо ответ сразу нет, либо надо посмотреть на
    :math:`ans[i-1,j-1]`. Если знак вопроса, то просто надо посмотреть на
    :math:`ans[i-1,j-1]`. А вот если звёздочка… С ходу хочется посмотреть на
    :math:`ans[i-k,j-1]` при всех :math:`k`, но можно быстрее,
    воспользовавшись приёмом сведения циклов к предыдущим подзадачам. А
    именно, посмотрим на :math:`ans[i,j-1]` (как будто звёздочка
    соответствует пустой строке) и на :math:`ans[i-1,j]` (если звёздочка
    соответствует непустой строке, то строка на один символ короче тоже
    подходит под ту же маску). Итого сложность :math:`O(NM)`.
    
    Для базы динамики нельзя просто так ввести нулевые элементы и сказать,
    что :math:`ans[0,0]=true`, а остальные :math:`false`: если маска
    начинается со звёздочек, то будут проблемы. Поэтому лучше приписать к
    маске и к строке в начало одну и ту же букву и только после этого
    считать :math:`ans[0,0]=true`, а остальные
    :math:`ans[0,i]=ans[i,0]=false` (а ответы для первой строки и столбца
    уже насчитывать по основной формуле).
    |

И ещё я дам несколько задач, по которым я почти не буду писать
ответы/подсказки/и т.п.; в разделе «Ответы» вы найдёте только скорее
комментарии по их использованию. Думайте над этими задачами сами :)



.. task::

    При умножении матрицы размера :math:`a\times b` на матрицу
    :math:`b\times c` получается матрица :math:`a\times c`, при этом, 
    чтобы выполнить такое умножение, требуется выполнить :math:`abc` умножений отдельных чисел.
    (Т.е. сложность операции умножения матриц — :math:`O(abc)`.)
    Умножение матриц не коммутативно
    (т.е. матрицы нельзя менять местами: :math:`AB\neq BA`), но ассоциативно
    (т.е. в любом выражении можно расставлять скобки как угодно, результат
    от этого не изменится: :math:`A(BC)=(AB)C`). Правда, от расстановки
    скобок в выражении зависит количество необходимых умножений чисел.
    Соответственно, получается задача. Дано выражение :math:`A_1\cdot
    A_2\cdot\ldots\cdot A_n`, где :math:`A_1`, :math:`A_2` и т.д. — матрицы;
    размер матрицы :math:`A_i` — :math:`r_i\times c_i`, при этом
    :math:`c_i=r_{i+1}` для всех :math:`i`. Требуется в выражении расставить
    скобки (т.е. указать порядок выполнения действий) так, чтобы
    потребовалось как можно меньше умножений чисел.
    |
    |
    |



.. task::

    Дана строка :math:`s_1`. Разрешается за одно действие либо
    удалить произвольный символ текущей строки, либо вставить произвольный
    символ в произвольное место текущей строки, либо изменить произвольный
    символ текущей строки (на любой символ по вашему выбору). 
    
    а) Требуется
    за наименьшее число действий получить данную строку :math:`s_2`. 
    
    б) То
    же самое, но за каждое действие есть штраф: :math:`d` за удаление,
    :math:`i` за вставку и :math:`c` за замену, требуется минимизировать
    штраф. 
    
    в) То же самое, но штрафы зависят от того, что это за символы
    (т.е. штраф за удаление зависит от того, какой символ удаляем и т.д.;
    все эти зависимости заданы во входном файле). 
    
    г) и т.д.
    |
    |
    Эта
    задача может иметь (и имеет) большое применение в различных ситуациях,
    когда вам нужно обрабатывать возможно ошибочный ввод. Например,
    электронные словари могут быть готовы к тому, что пользователь введёт
    слово с ошибкой, и в таком случае выдавать ему список похожих слов;
    «похожесть» будет определяться по алгоритму, аналогичному решению этой
    задачи. Можно даже реализовать пункт в), например, допуская, что
    перепутать в английском слове буквы ’i’ и ’y’, ’c’ и ’k’ легко, но вряд
    ли кто перепутает, например, ’a’ и ’p’. Можно и другие идеи подключить,
    например допустить замену ’oo’ на ’u’ — решаться задача будет
    аналогично.
    
    Другое аналогично применение — системы автоматической проверки
    орфографии. Здесь тоже в качестве возможных вариантов замены надо бы
    выдавать слова, которые отличаются не сильно; и также можно ввести веса
    для разных операций и разных букв (например, логично считать, что можно
    перепутать буквы, которые расположены на клавиатуре рядом, и т.п.).
    |

.. task::

    .. epigraph::

        *TeX's line-breaking algorithm
        has proved to be general enough to handle a surprising variety of
        different applications; this, in fact, is probably the most interesting
        aspect of the whole TeX system.*

        Donald E. Knuth. The TeX book.

    .. epigraph::
        *Алгоритм TeX'а для разбиения строк оказывается достаточно всеобщим для того, чтобы 
        справиться с удивительным разнообразием различных приложений. Фактически, это, вероятно, наиболее 
        интересный аспект в системе TeX.*

        Дональд Е. Кнут. Все про TeX.

        Идея и код фигурного абзаца тоже взяты из TeXbook.

    .. image:: 05_7_tasks/paragraph.png

    |
    |
    |


