
## Проект 2. Сравнительный анализ различных алгоритма поиска равновесного распределения транспортных потоков по путям в моделях Бэкмана и Стабильной динамики.

План работ. Прочитать статью https://arxiv.org/pdf/2008.02418.pdf (если что-то будет не понятно, можно подсмотреть детали тут https://arxiv.org/pdf/2003.12160.pdf) и ознакомиться с питон-кодом к статье (при возникновении вопросов стоит писать Мерузе Кубентаевой kubentayeva-m@yandex.ru). Описанная в статье задача и численные алгоритмы на практике многократно используются при изучении вопросов перераспределения транспортных потоков. Проведите исследование, какой из численных методов, описанных в статье более чувствителен к удачному выбору точки старта. Мотивация в такой постановке следующая: часто бывает уже известно равновесие в транспортной сети, но сеть немного поменялась, например, поменялись характеристики части ребер (пропускные способности изменились), нужно найти новое равновесие. Понятно, что если поменялись характеристики небольшого числа ребер, то мы вправе ожидать, что равновесия будут близкими. Разные алгоритмы могут иметь разную чувствительность к выбору точки старата. В данном контексте интересны такие алгоритмы, которые наиболее чувствительны к удачному выбору точки старта. P.S. Наиболее интересны сравнения алгоритмов типа условного градиента и различных двойственных методов для модели Бэкмана.

## Результаты проекта 
Эксперимент с различными точками старта и проверка чувствительности метода находится в ноутбуке Stable Dynamic & Beckman/Anaheim_Beckmann_Experiments_sensitive_starting_point.ipynb
Эксперимент с методом стартером и методом доводчиком находится в Stable Dynamic & Beckman/Anaheim_Beckmann_new_start.ipynb
Для загрузки результатов через pickle можно воспользоваться сохраненными данными с дисков:
local_results.txt - https://drive.google.com/file/d/1MjfvvUzq2RXSdzZjlpnYLhoCmTU_FVVH/view?usp=sharing
local_results_depth - https://drive.google.com/file/d/1K9ENxQfvQ9DtvP-77YrYrvrgxZAGM7nZ/view?usp=sharing
initial_results - https://drive.google.com/file/d/1sIoghC1pwwR0c0Wmbw5wlUeOgUtmhrS3/view?usp=sharing
anaheim_result_new_start_beckmann.pickle - https://drive.google.com/file/d/112MJC2s5D8ovTfYpxRC4KHX3tj4tqHQA/view?usp=sharing



# [Stable Dynamic & Beckmann models](https://github.com/MeruzaKub/TransportNet/tree/master/Stable%20Dynamic%20%26%20Beckman)

The project contains implementations of several primal-dual subgradient methods for searching traffic equilibria in the Stable Dynamics model and the Beckmann model. 
Results of experiments on the [Anaheim transportation network](https://github.com/bstabler/TransportationNetworks) are included.

The following methods are implemented:
1.	Universal gradient method [[ref](http://www.optimization-online.org/DB_FILE/2013/04/3833.pdf)]
2.	Universal method of similar triangles [[arXiv:1701.02473](https://arxiv.org/ftp/arxiv/papers/1701/1701.02473.pdf)]
3.  Method of Weighted Dual Averages [[ref](https://ium.mccme.ru/postscript/s12/GS-Nesterov%20Primal-dual.pdf)]
4.	Subgradient method with adaptive step size [[arXiv:1604.08183](https://arxiv.org/ftp/arxiv/papers/1604/1604.08183.pdf)].

Convergence rates of UMST, UGM, composite and non-composite WDA-methods for the Stable Dynamics model:

<img src="https://github.com/MeruzaKub/TransportNet/blob/master/Stable%20Dynamic%20%26%20Beckman/pics/sd_convergence_rel_eps.jpg" width="500">

Convergence rates of UMST, UGM, composite and non-composite WDA-methods, and the Frank–Wolfe method for the Beckmann model:

<img src="https://github.com/MeruzaKub/TransportNet/blob/master/Stable%20Dynamic%20%26%20Beckman/pics/beckmann_convergence_rel_eps.jpg" width="500">


## Installing graph-tool
Native installation of [graph-tool](https://graph-tool.skewed.de/) on Windows isn't supported. But if you have Docker installed, you can easily download the following container image with all the packages required to run the project:
https://hub.docker.com/r/ziggerzz/graph-tool-extra 

## How to Cite
1. Kubentayeva, M.; Gasnikov, A. Finding Equilibria in the Traffic Assignment Problem with Primal-Dual Gradient Methods for Stable Dynamics Model and Beckmann Model. Mathematics 2021, 9, 1217. https://doi.org/10.3390/math9111217
2. The source code: Kubentayeva M. TransportNet. https://github.com/MeruzaKub/TransportNet. Accessed Month, Day, Year.

## More Resources
More information about the models can be found in [[Nesterov-de Palma](https://link.springer.com/article/10.1023/A:1025350419398)] and [[Beckmann](https://cowles.yale.edu/sites/default/files/files/pub/misc/specpub-beckmann-mcguire-winsten.pdf)].

# [Stochastic Nash-Wardrop Equilibria in the Beckmann model](https://github.com/MeruzaKub/TransportNet/tree/master/Stochastic%20Nash-Wardrop%20equilibrium)
Agents’ behavior is not completely rational, what is described by the introduction of Markov logit dynamics: any driver selects a route randomly according to the Gibbs’ distribution taking into account current time costs on the edges of the graph.
<img src="https://render.githubusercontent.com/render/math?math=\gamma > 0"> is a stochasticity parameter (when <img src="https://render.githubusercontent.com/render/math?math=\gamma \rightarrow 0"> the model boils down to the ordinary Beckmann model). The figure below shows convergence of flows in stochastic equilibrium to equilibrium flows in non-stochastic case as  <img src="https://render.githubusercontent.com/render/math?math=\gamma"> tends to zero.

<img src="https://github.com/MeruzaKub/TransportNet/blob/master/Stochastic%20Nash-Wardrop%20equilibrium/pics/anaheim_error_vs_gamma_eps_1e-3.png" width="500">

## How to Cite
1. [Article](http://crm.ics.org.ru/uploads/crmissues/crm_2018_3/2018_01_07.pdf): Gasnikov A.V., Kubentayeva M.B. Searching stochastic equilibria in transport networks by universal primal-dual gradient method // Computer Research and Modeling, 2018, vol. 10, no. 3, pp. 335-345. DOI: 10.20537/2076-7633-2018-10-3-335-345.
2. The source code: Kubentayeva M. TransportNet. https://github.com/MeruzaKub/TransportNet. Accessed Month, Day, Year.

<!--- Convergence process on 10 000 iterations for Stable Dynamic model:--->
<!---![](methods_stable_dynamic.png)--->

<!---Convergence process on 8000 iterations for Beckmann model (+ Frank-Wolfe algorithm):--->
<!---![](methods_beckmann.png)--->

<!--[Anaheim_Experiments.ipynb](https://github.com/MeruzaKub/TransportNet/blob/master/Stable%20Dynamic%20%26%20Beckman/Anaheim_Experiments.ipynb) contains code of experiments on comparison of the above methods and Frank-Wolfe algorithm (only for the Beckmann model).-->

