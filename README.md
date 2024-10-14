# Задача Био
Задача фильтрации однофазной жидкости в пороупругой среде может быть описана с помощью дифференциальных уравнений:

<h3 align="center">$div ( C:\epsilon - \alpha \mathbb{I} p) = -\vec{b}$, $\epsilon = \frac{ \nabla \vec{u} + \nabla {\vec{u}}^{T}}{2}$

<h3 align="center"> $dphi/dt -div(K \nabla p) = q$
где $\vec{u} = (u, v, w)$ - смещение точки, $\vec{b}$ - вектор результирующих приложенных к телу внешних сил,
$\epsilon$ - тензор малых деформаций, $С$ - тензор жесткости
$\alpha$ - коэффициент Био, 
$p$ - давление жидкости в порах,
$\phi = \phi _{0} + \alpha div(\vec{u}) + \frac{(\alpha - \phi _{0})}{K} p$ - пористость с учетом деформаций,
$\phi _{0}$ - исходная пористость
$\K$ - модуль объемного расширения,
$q$ - источник или сток,
$K$ - тензор второго ранга абсолютной проницаемости породы

с граничными условиями:

<h4 align="center">$\alpha \vec{u} - \beta \sigma \vec{n} = \vec{\gamma}$ - условия на смещение $\vec{u}$
<h4 align="center">$Ap + B \vec{u}^{T} K \nabla p = C$ - условия на давление $p$

где $A$ - условие на давление жидкости (условия типа Дирихле),
$B$ - условия на поток жидкости (условия типа Неймана),
$C$ - значение давление или потока жидкости

где $\alpha -$ тензор 3-го порядка, условия типа Дирихле, $\alpha$ = ${\alpha}_{\bot} n n^{T}$ - ${\alpha}{||}$ $(n n^{T} - \mathbb{I})$

$\beta -$ тензор 3-го порядка, условия типа Неймана, $\beta$ = ${\beta}_{\bot} n n^{T}$ - $\beta{||} (n n^{T} - \mathbb{I})$

# Задача Терцаги
Пассмотрим задачу фильтрации жидкости в насыщенной пористой среде, находящейся под воздействием нагрузки (среду сдавливают). Насыщенная пористая среда представляет собой параллелипипед размером $xyz = [0, 1]x[0,1]x[0, L = 10]$ и изначально находится в недеформированном состоянии. К левой грани прикладывается сдавливающая сила $[F, 0, 0]$. К боковым граням бруска приложена нулевая сила. Смещения \vec{u} на правой грани зафиксированы. Необходимо определить итоговое поле давление жидкости в порах $\p$ и поле смещений породы $\vec{u}$ во всей области.

Численное решение осуществляется путем дискретизации уравнений методом конечных объемов (МКО) на дуальной сетке (смещения $\vec{u}$ расположены в узлах исходной сетки и в центрах дуальных ячеек) с использованием 
<a href="https://github.com/INMOST-DEV/INMOST ">INMOST</a>

Для данной задачи существует <a href="https://www.sciencedirect.com/science/article/abs/pii/S0045782514001509?via%3Dihub" target="_blank">аналитическое решение</a>

В численном решении задаются граничные условия на верхней ($\vec{n}$ = (0, 0, 1)) и нижней $\vec{n}$ = (0, 0, -1)) гранях по аналитическому решению для смещения при F = 0.1 (для верхней грани) и F = 0 (для нижней грани). $\alpha = \mathbb{I}$, $\beta = 0$

Сравнение аналитического решения с численным на сетке $N_{x} = N_{y} = 2, N_{z} = 10$:

<h1 align="center"> Смещение $u$
  
Численное решение$ |  Аналитическое решение
:-------------------------:|:-------------------------:
![My Image](pics/uvw.png)  |  ![My Image](pics/uvw_an.png)

<h1 align="center"> Давление $p$
  
Численное решение |  Аналитическое решение
:-------------------------:|:-------------------------:
![My Image](pics/p.png)  |  ![My Image](pics/p_an.png)

Из графиков сравнения численного и аналитического решений видим, что визуально решения хорошо совпадают.

Отклонение аналитического решения от численного рассчитывается как L2-norm:

Анализ сходимости:

| dx=dy=dz  |  L2-norm u | L2-norm $\sigma$ | Порядок аппроксимации схемы $p$ по L2-norm-$\sigma$ |
| ------------- | ------------- | ------------- | ------------- |
| 1  | $0.0018$  | $0.046$  | -  |
| 0.5  | $0.00036$  | $0.023$  | $1$  |
| 0.25  | $0.00043$  | $0.011$  | $1.06$  |

L2-norm для $u$ падает быстро с измельчением сетки, а затем перестает падать и значительно изменяться (?).
Порядок схемы, рассчитанный по норме $L2-norm$ тензора напряжений $\sigma$ примерно равен 1
