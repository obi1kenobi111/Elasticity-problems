# Elasticity-problems
Elasticity Problems

Для моделирования сдвига бруска будем решать задачу линейной упругости (в приближении малых деформаций):

<h3 align="center">$div \vec{u} = -\vec{b},$ $\sigma = C:\epsilon,$ $\epsilon = \frac{ \nabla \vec{u} + \nabla {\vec{u}}^{T}}{2}$

где $\vec{u} = (u, v, w)$ - смещение точки, $\vec{b}$ - вектор результирующих приложенных к телу внешних сил,
$\epsilon$ - тензор малых деформаций, $С$ - тензор жесткости

с граничными условиями:

<h3 align="center">$\alpha \vec{u} - \beta \sigma \vec{u} = \vec{\gamma}$

где $\alpha -$ тензор 3-го порядка, условия типа Дирихле, $\alpha$ = ${\alpha}_{\bot} n n^{T}$ - $\alpha{||} (n n^{T} - \mathbb{I})$

$\beta -$ тензор 3-го порядка, условия типа Неймана, $\beta$ = ${\beta}_{\bot} n n^{T}$ - $\beta{||} (n n^{T} - \mathbb{I})$

# Описание задачи о сдвиге бруска
Рассматрим задачу о сдвиге бруска. Изначально брусок размером $xyz = [-1, 1]x[-1,1]x[0, L]$ находится в недеформированном состоянии. К верхней грани прикладывается сила $[0, -F, 0]$. К боковым граням бруска приложена нулевая сила. Смещения \vec{u} на нижней грани бруска зафиксированы. Необходимо определить итоговое поле напряжений $\sigma$ и смещений $\vec{u}$ во всем бруске.

Для данной задачи существует <a href="http://algowiki-project.org/ru/%D0%9C%D0%B5%D1%82%D0%BE%D0%B4_%D0%9D%D1%8C%D1%8E%D1%82%D0%BE%D0%BD%D0%B0_%D0%B4%D0%BB%D1%8F_%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC_%D0%BD%D0%B5%D0%BB%D0%B8%D0%BD%D0%B5%D0%B9%D0%BD%D1%8B%D1%85_%D1%83%D1%80%D0%B0%D0%B2%D0%BD%D0%B5%D0%BD%D0%B8%D0%B9" target="_blank">аналитическое решение</a>

Численное решение |  Аналитическое решение
:-------------------------:|:-------------------------:
![My Image](pics/u_.jpg)  |  ![My Image](pics/u_an.jpg)

Анализ сходимости:

| dx=dy=dz  |  L2-norm u | L2-norm $\sigma$ | Порядок аппроксимации схемы $p$ по L2-norm-$\sigma$ |
| ------------- | ------------- | ------------- | ------------- |
| 1  | $0.0018$  | $0.046$  | -  |
| 0.5  | $0.00036$  | $0.023$  | $1$  |
| 0.25  | $0.00043$  | $0.011$  | $1.06$  |

Таким образом, порядок схемы, рассчитанный по норме $L2-norm$ давления $\sigma$ примерно равен 1
