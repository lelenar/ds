

> **作者：** 彭晴 (暨南大学)  
> **邮箱：**<natasha_pong@163.com>

&emsp;

**提要**：本文介绍 Python 可视化库 seaborn 的基本使用方法，包括 seaborn 的安装、导入、基础设置以及常用绘图函数的使用 (如散点图、回归图、小提琴图、热力图等)，帮助读者快速上手 seaborn，提升数据可视化能力。

- **Title**: Python可视化之seaborn：直方图-密度图-小提琴图-热力图
- **Keywords**: Python绘图, 数据可视化, 小提琴图, violinplot, seaborn, 散点图, scatterplot, 回归图, regplot, 热力图, heatmap

&emsp; 

## 1. Seaborn 简介

**Seaborn** 是一个基于 `matplotlib` 的 **Python** 数据可视化库。由于其是对 `matplotlib` 的二次封装，所以很多语法以及参数设置和 `matplotlib` 很相近，而且能与 `matplotlib` 一起使用。

### 1.1 Seaborn 的安装

Seaborn 有两种安装方式：

第一种安装方式：直接通过 PyPI 安装

```python
pip install seaborn
```

第二种安装方式：通过 Anaconda 安装

```python
conda install seaborn
```

### 1.2 Seaborn 的导入

安装好 Seaborn 包之后，需要 import 这个包才可使用。一般情况下，与 matplotlib 一起导入，配合使用。

```python
import seaborn as sns
import matplotlib.pyplot as plt
```

&emsp;

## 2. Seaborn 的基础设置

### 2.1 Seaborn 的风格设置

**Seaborn** 一共设置了**五种风格**：**darkgrid**（黑色背景带网格线）、**whitegrid**（白色背景带网格线）、**dark**（黑色背景无网格线）、**white**（白色背景无网格线）和**ticks**（白色背景无网格线，且坐标轴带刻度线）。其中，Seaborn 的默认风格为 darkgrid（黑色背景带网格线）。

```python
sns.set()  # 默认风格的设置
```

<img src="https://fig-lianxh.oss-cn-shenzhen.aliyuncs.com/彭晴-seaborn你的绘图神奇-fig01.png" width="550">

其他风格设置的核心代码

```Python
sns.set_style('dark')        # 对应图(A), dark风格
sns.set_style('white')       # 对应图(B)，whith风格
sns.set_style('whitegrid')   # 对应图(C)，whitegrid风格
sns.set_style('ticks')       # 对应图(D)，ticks风格
```

<img src="https://fig-lianxh.oss-cn-shenzhen.aliyuncs.com/彭晴-seaborn你的绘图神奇-fig02.png" width="900">

### 2.2 Seaborn 的边框设置

Seaborn 默认显示图形的四条边框。如果想调整图形的边框，可以通过`sns.despine()`命令调整。

**(1)`sns.despine()`命令，默认只显示左边框和下边框**

```python
sns.set_style('ticks')
sns.regplot(x='bill_length_mm',y='body_mass_g',data=df)
sns.despine()
```

<img src="https://fig-lianxh.oss-cn-shenzhen.aliyuncs.com/彭晴-seaborn你的绘图神奇-fig03.png" width="550">

&emsp;

**(2) 通过设置 `sns.despine()`命令的参数（left、right，top，bottom），可以指定图形显示哪一条边框**

在`sns.despine()`命令中加入参数，如`left=True`，来指定左边是否显示。需要注意的是，`True`表示不显示边框，`False`表示显示边框。下面展示只显示下边框的例子：

```python
sns.set_style('ticks')
sns.regplot(x='bill_length_mm',y='body_mass_g',data=df)
sns.despine(left=True,right=True,top=True,bottom=False)  # 只显示下边框
```

<img src="https://fig-lianxh.oss-cn-shenzhen.aliyuncs.com/彭晴-seaborn你的绘图神奇-fig04.png" width="550">

**（3）通过设置 `sns.despine()`命令的参数（offset），可以调整图形与坐标轴的距离**

```python
sns.set_style('ticks')
sns.regplot(x='bill_length_mm',y='body_mass_g',data=df)
sns.despine(offset=20)
```

<img src="https://fig-lianxh.oss-cn-shenzhen.aliyuncs.com/彭晴-seaborn你的绘图神奇-fig05.png" width="550">

&emsp;

## 3. Seaborn 的可视化实例

### 3.1 样本数据介绍

```Python
# 导入样本数据
df = sns.loaddata('penguins')
```

**penguins** 是 seaborn 自带的数据集，称为企鹅数据集。企鹅数据集一共包括 344 条观测值，7 个变量：species（种类）, island（岛屿）, bill_length_mm（鸟嘴长度）, bill_depth_mm（鸟嘴宽度）, flipper_length_mm（鳍足长度）, body_mass_g（体重）, sex（性别）。除此之外，Seaborn 还有多个自带的数据集，方便初学者学习。

### 3.2 数据关系图

#### 3.2.1 散点图 scatterplot

`sns.scatterplot()`可用于描绘 x 和 y 的散点图，其核心参数如下：

| `参数`        | `作用`                                             |
| ------------- | -------------------------------------------------- |
| `x,y`         | `指定x轴和y轴的变量`                               |
| `data`        | `指定数据集`                                       |
| `hue`         | 指定分类变量，根据该分类变量生成具有不同颜色的散点 |
| `size`        | 指定分类变量，根据该分类变量生成具有不同大小的散点 |
| `style`       | 指定分类变量，根据该分类变量生成具有不同形状的散点 |
| `palette`     | 指定调色盘                                         |
| `hue_order`   | 使用`hue`时，指定分类变量的顺序                    |
| `sizes`       | 使用`size`时，指定散点的大小                       |
| `size_order`  | 使用`size`时，指定分类变量的顺序                   |
| `markers`     | 使用`style`时，指定散点的形状                      |
| `style_order` | 使用`style`时，指定分类变量的顺序                  |

```python
sns.scatterplot(x='bill_length_mm',y='body_mass_g',data=df)
# 对应图(A), 基础设置

sns.scatterplot(x='bill_length_mm',y='body_mass_g',data=df,hue='sex')
# 对应图(B), 通过散点颜色标识不同的性别

sns.scatterplot(x='bill_length_mm',y='body_mass_g',data=df,size='sex')
# 对应图(C), 通过散点大小标识不同的性别

sns.scatterplot(x='bill_length_mm',y='body_mass_g',data=df,style='sex')
# 对应图(D), 通过散点形状标识不同的性别
```

<img src="https://fig-lianxh.oss-cn-shenzhen.aliyuncs.com/彭晴-seaborn你的绘图神奇-fig06.png" width="900">

#### 3.2.2 回归图 regplot

`sns.regplot()`可用于描绘 x 和 y 的回归关系。对比散点图，回归图可以展示 x 和 y 回归拟合出来的直线。回归图的核心参数如下：

| `参数`               | `作用`                                                                            |
| -------------------- | --------------------------------------------------------------------------------- |
| `x,y`                | `指定x轴和y轴的变量`                                                              |
| `data`               | `指定数据集`                                                                      |
| `scatter`            | 选择`True`则表示描绘散点；选择`False`则表示不描绘散点                             |
| `fit_reg`            | 选择`True`则表示描绘 x 和 y 拟合的直线；选择`False`则表示不描绘 x 和 y 拟合的直线 |
| `ci`                 | 指定置信区间，必须为 0—100 之间的整数，默认值为 95                                |
| `n_boot`             | 指定估计`ci`的抽样次数，默认值为 1000                                             |
| `logistic`           | 选择`True`则表示 y 为二元变量；默认选择`False`                                    |
| `marker`             | 指定散点的形状                                                                    |
| `color`              | 指定颜色                                                                          |
| `{scatter,line}_kws` | 指定散点或直线的参数                                                              |

```python
sns.regplot(x='bill_length_mm',y='body_mass_g',data=df)
# 对应图(A), 基础设置

sns.regplot(x='bill_length_mm',y='body_mass_g',data=df,scatter=False)
# 对应图(B), 不描绘散点

sns.regplot(x='bill_length_mm',y='body_mass_g',data=df,marker='^')
# 对应图(C), 设置散点的形状为三角形

sns.regplot(x='bill_length_mm',y='body_mass_g',data=df,
            line_kws={"linestyle": "--",'color':'k','linewidth':2},
            scatter_kws={'color':'grey','alpha':0.5})
# 对应图(D), 调整散点和直线的样式
```

<img src="https://fig-lianxh.oss-cn-shenzhen.aliyuncs.com/彭晴-seaborn你的绘图神奇-fig07.png" width="900">

#### 3.2.3 分类散点图 stripplot

`sns.stripplot()`可用于描绘分类变量 x 与 y 之间的关系。与散点图和回归图不同的是，`sns.stripplot()`的 x 变量是一个离散的分类变量，其核心参数如下：

| `参数`      | `作用`                                                                             |
| ----------- | ---------------------------------------------------------------------------------- |
| `x,y`       | `指定x轴和y轴的变量`                                                               |
| `data`      | `指定数据集`                                                                       |
| `hue`       | 指定分类变量，根据该分类变量生成具有不同颜色的散点                                 |
| `hue_order` | 使用`hue`时，指定分类变量的顺序                                                    |
| `color`     | 指定颜色                                                                           |
| `palette`   | 指定调色盘                                                                         |
| `size`      | 指定散点的大小                                                                     |
| `edgecolor` | 指定散点边的颜色                                                                   |
| `linewidth` | 指定散点边的粗细                                                                   |
| `orient`    | 选择`v`则指定图形为纵向；选择`h`则指定图形为横向                                   |
| `dodge`     | 使用`hue`时，选择`True`则表示分类的散点不会重叠；选择`False`则表示分类的散点会重叠 |

```python
sns.stripplot(x="species", y="body_mass_g", data=df,color='b')
# 对应图(A), 基础设置

sns.stripplot(x="species", y="body_mass_g",data=df,hue='sex',dodge=True)
# 对应图(B), 对性别进行分组，并且分组散点不重叠

sns.stripplot(x="species", y="body_mass_g", data=df,color='b',
              edgecolor='k',linewidth=0.5)
# 对应图(C), 设置散点的边粗细以及颜色

sns.stripplot(x="body_mass_g", y="species", data=df,color='b',orient='h')
# 对应图(D), 设置方向为横向
```

<img src="https://fig-lianxh.oss-cn-shenzhen.aliyuncs.com/彭晴-seaborn你的绘图神奇-fig08.png" width="900">

#### 3.2.4 无重叠的分类散点图 swarmplot

`sns.swarmplot()`也是用于描绘分类变量 x 与 y 之间的关系，被称为蜂巢图。与`sns.stripplot()`不同的是，`sns.swarmplot()`描绘出来的散点不会重叠，因此能看出散点的分布。`sns.swarmplot()`与`sns.stripplot()`的参数基本一致，此处不再重复阐述。

```python
sns.swarmplot(x="species", y="body_mass_g", data=df,color='b')
# 对应图(A), 基础设置

sns.swarmplot(x="species", y="body_mass_g",data=df,hue='sex',dodge=True)
# 对应图(B), 对性别进行分组，并且分组散点不重叠

sns.swarmplot(x="species", y="body_mass_g", data=df,color='b',
              edgecolor='k',linewidth=0.5)
# 对应图(C), 设置散点的边粗细以及颜色

sns.swarmplot(x="body_mass_g", y="species", data=df,color='b',orient='h')
# 对应图(D), 设置方向为横向
```

<img src="https://fig-lianxh.oss-cn-shenzhen.aliyuncs.com/彭晴-seaborn你的绘图神奇-fig09.png" width="900">

### 3.3 数据分布图

#### 3.3.1 直方图 distplot

`sns.distplot()`用于描绘连续变量的直方图，其核心参数如下：

| `参数` | `作用`                                                |
| ------ | ----------------------------------------------------- |
| `hist` | 选择`True`则显示柱状；选择`False`则不显示柱状         |
| `kde`  | 选择`True`则显示分布线；选择`False`则不显示分布线     |
| `rug`  | 选择`True`则显示锯齿分布；选择`False`则不显示锯齿分布 |
| `bins` | 指定柱状的数量                                        |

```python
sns.distplot(df["body_mass_g"])
# 对应图(A), 基础设置

sns.distplot(df["body_mass_g"],kde=False,rug=True)
# 对应图(B), 不显示分布线，显示锯齿分布

sns.distplot(df["body_mass_g"],bins=15,vertical=True)
# 对应图(C), 设置15个柱状，且方向为水平

sns.distplot(df["body_mass_g"],
             hist_kws={"linestyle": "--",'color':'b','linewidth':3,'histtype':'step'},
             kde_kws={'color':'grey','alpha':0.5})
# 对应图(D), 设置柱状和分布线的参数
```

<img src="https://fig-lianxh.oss-cn-shenzhen.aliyuncs.com/彭晴-seaborn你的绘图神奇-fig10.png" width="900">

#### 3.3.2 核密度图 kdeplot

`sns.kdeplot()`用于描绘连续变量的核密度图，其核心参数如下：

| `参数`       | `作用`                                                  |
| ------------ | ------------------------------------------------------- |
| `shade`      | 选择`True`则显示阴影；选择`False`则不显示阴影           |
| `cumulative` | 选择`True`则显示累积分布图；默认选择为`False`           |
| `bw`         | 指定分布线的平滑程度                                    |
| `hue`        | 指定分类变量，根据该分类变量生成具有不同颜色的散点      |
| `hue_order`  | 使用`hue`时，指定分类变量的顺序                         |
| `color`      | 指定颜色                                                |
| `palette`    | 指定调色盘                                              |
| `log_scale`  | 选择`True`则对 X 取对数处理；默认选择为`False`          |
| `rug_kws`    | 指定锯齿分布的参数                                      |
| `vertical`   | 选择`True`则指定图形为横向；选择`False`则指定图形为纵向 |
| `linewidth`  | 指定分布的线条粗细                                      |
| `linestyle`  | 指定分布的线条样式                                      |

```python
sns.kdeplot(data=df["body_mass_g"])
# 对应图(A), 基础设置

sns.kdeplot(data=df["body_mass_g"],cumulative=True,shade=True)
# 对应图(B), 设置阴影，且设置为累积分布图

sns.kdeplot(data=df["body_mass_g"],bw=50)
# 对应图(C), 设置分布的平滑程度

sns.kdeplot(df["body_mass_g"],color='k',linewidth=3,linestyle='--')
# 对应图(D), 设置分布线的粗细、颜色和样式
```

<img src="https://fig-lianxh.oss-cn-shenzhen.aliyuncs.com/彭晴-seaborn你的绘图神奇-fig11.png" width="900">

#### 3.3.3 箱型图 boxplot

`sns.boxplot()`用于描绘分类变量的分布，其核心参数如下：

| `参数`       | `作用`                                                                             |
| ------------ | ---------------------------------------------------------------------------------- |
| `x,y`        | `指定x轴和y轴的变量`                                                               |
| `data`       | `指定数据集`                                                                       |
| `hue`        | 指定分类变量，根据该分类变量生成具有不同颜色的散点                                 |
| `order`      | 指定变量的顺序                                                                     |
| `hue_order`  | 使用`hue`时，指定分类变量的顺序                                                    |
| `color`      | 指定颜色                                                                           |
| `saturation` | 指定颜色的饱和度                                                                   |
| `palette`    | 指定调色盘                                                                         |
| `width`      | 指定箱体的宽度                                                                     |
| `fliersize`  | 指定异常值的大小                                                                   |
| `linewidth`  | 指定散点边的粗细                                                                   |
| `orient`     | 选择`v`则指定图形为纵向；选择`h`则指定图形为横向                                   |
| `dodge`      | 使用`hue`时，选择`True`则表示分类的散点不会重叠；选择`False`则表示分类的散点会重叠 |

```python
sns.boxplot(x="species", y="body_mass_g", data=df,color='b')
# 对应图(A), 基础设置

sns.boxplot(x="species", y="body_mass_g",data=df,hue='sex',dodge=True)
# 对应图(B), 按性别分组显示

sns.boxplot(x="species", y="body_mass_g", data=df,
            order=['Gentoo','Chinstrap','Adelie'],
            palette="Set2",saturation=0.6,width=0.3,fliersize=10,linewidth=3)
# 对应图(C), 设置变量顺序，以及箱体宽度、线条、颜色、异常值大小等样式

sns.boxplot(x="body_mass_g", y="species", data=df,color='b',orient='h')
# 对应图(D), 设置水平方向
```

<img src="https://fig-lianxh.oss-cn-shenzhen.aliyuncs.com/彭晴-seaborn你的绘图神奇-fig12.png" width="900">

#### 3.3.4 增强箱型图 boxenplot

`sns.boxenplot()`用于描绘分类变量的分布。与箱型图不同的是，增强箱型图通过箱体的宽窄更细致地显示变量的分布，其核心参数如下：

| `参数`        | `作用`                                                                                                                                                                             |
| ------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `x,y`         | `指定x轴和y轴的变量`                                                                                                                                                               |
| `data`        | `指定数据集`                                                                                                                                                                       |
| `hue`         | 指定分类变量，根据该分类变量生成具有不同颜色的散点                                                                                                                                 |
| `order`       | 指定变量的顺序                                                                                                                                                                     |
| `hue_order`   | 使用`hue`时，指定分类变量的顺序                                                                                                                                                    |
| `color`       | 指定颜色                                                                                                                                                                           |
| `saturation`  | 指定颜色的饱和度                                                                                                                                                                   |
| `palette`     | 指定调色盘                                                                                                                                                                         |
| `width`       | 指定箱体的宽度                                                                                                                                                                     |
| `outlier_pop` | 定义异常值的区间，数值必须在(0,1]之间，默认为 0.007                                                                                                                                |
| `linewidth`   | 指定散点边的粗细                                                                                                                                                                   |
| `orient`      | 选择`v`则指定图形为纵向；选择`h`则指定图形为横向                                                                                                                                   |
| `dodge`       | 使用`hue`时，选择`True`则表示分类的散点不会重叠；选择`False`则表示分类的散点会重叠                                                                                                 |
| `scale`       | 指定箱型图的宽度，有三个选项（`linear`表示通过线性因子减少箱体宽度；`exponential`表示使用未覆盖数据调整箱体宽度；`area`表示使用覆盖数据的百分比调整箱体宽度），默认为`exponential` |

```python
sns.boxenplot(x="species", y="body_mass_g", data=df,color='b')
# 对应图(A), 基础设置

sns.boxenplot(x="species", y="body_mass_g",data=df,hue='sex',dodge=True)
# 对应图(B), 按性别分组显示

sns.boxenplot(x="species", y="body_mass_g", data=df,
              order=['Gentoo','Chinstrap','Adelie'],
              palette="Set1",saturation=0.5,width=0.5)
# 对应图(C), 设置变量顺序，以及箱体宽度、颜色等样式

sns.boxenplot(x="body_mass_g", y="species", data=df,color='b',orient='h',scale='linear')
# 对应图(D), 设置水平方向，且按照线性的方式来调整箱体宽度
```

<img src="https://fig-lianxh.oss-cn-shenzhen.aliyuncs.com/彭晴-seaborn你的绘图神奇-fig13.png" width="900">

#### 3.3.5 小提琴图 violinplot

`sns.violinplot()`用于描绘分类变量的分布。与箱型图不同的是，箱型图的箱体无法更进一步显示其分布，而小提琴图的箱体可以通过其宽窄进一步显示分布，其核心参数如下：

| `参数`       | `作用`                                                                                                                                                   |
| ------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `x,y`        | `指定x轴和y轴的变量`                                                                                                                                     |
| `data`       | `指定数据集`                                                                                                                                             |
| `hue`        | 指定分类变量，根据该分类变量生成具有不同颜色的散点                                                                                                       |
| `order`      | 指定变量的顺序                                                                                                                                           |
| `hue_order`  | 使用`hue`时，指定分类变量的顺序                                                                                                                          |
| `color`      | 指定颜色                                                                                                                                                 |
| `saturation` | 指定颜色的饱和度                                                                                                                                         |
| `palette`    | 指定调色盘                                                                                                                                               |
| `width`      | 指定箱体的宽度                                                                                                                                           |
| `fliersize`  | 指定异常值的大小                                                                                                                                         |
| `linewidth`  | 指定散点边的粗细                                                                                                                                         |
| `orient`     | 选择`v`则指定图形为纵向；选择`h`则指定图形为横向                                                                                                         |
| `dodge`      | 使用`hue`时，选择`True`则表示分类的散点不会重叠；选择`False`则表示分类的散点会重叠                                                                       |
| `split`      | 使用`hue`时，选择`True`则表示分类变量结合在一个小提琴显示；默认选项为`False`，表示分类变量分开多个小提琴表示                                             |
| `inner`      | 指定箱型图的内部形态，有五个选项（`box`为箱体表示；`quartile`为分位数表示；`point`用点表示；`stick`用线条表示；`None`表示无内部图形），默认为`box`       |
| `scale`      | 指定小提琴的量纲，有三个选项（`area`表示每个小提琴面积一样；`count`表示观测值频数一样时小提琴的宽度一致；`width`表示每个小提琴的宽度一致），默认为`area` |

```Python
sns.violinplot(x="species", y="body_mass_g", data=df,color='b')
# 对应图(A), 基础设置

sns.violinplot(x="species", y="body_mass_g",data=df,hue='sex',dodge=True)
# 对应图(B), 按性别分组显示

sns.violinplot(x="species", y="body_mass_g", data=df,
        order=['Gentoo','Chinstrap','Adelie'],
        palette="Set2",saturation=0.6,width=0.3,fliersize=10,linewidth=3)
# 对应图(C), 设置变量顺序，以及线条、颜色、异常值大小等样式

sns.violinplot(x="body_mass_g", y="species", data=df,color='b',
        orient='h',inner='quartile')
# 对应图(D), 设置水平方向，且内部显示分位数线条
```

<img src="https://fig-lianxh.oss-cn-shenzhen.aliyuncs.com/彭晴-seaborn你的绘图神奇-fig14.png" width="900">

#### 3.3.6 多变量分布图 pairplot

`sns.pairplot()`用于描绘数据集中连续变量之间的两两关系以及连续变量自身的直方图，其核心参数如下：

| `参数`      | `作用`                                                                                                                         |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `data`      | 指定数据集                                                                                                                     |
| `hue`       | 指定分类变量，根据该分类变量生成具有不同颜色的散点                                                                             |
| `hue_order` | 使用`hue`时，指定分类变量的顺序                                                                                                |
| `palette`   | 指定调色盘                                                                                                                     |
| `vars`      | 指定变量                                                                                                                       |
| `kind`      | 指定两两关系图的类型，有四个选项（`scatter`表示散点图；`kde`表示核密度图；`hist`表示直方图；`reg`表示回归图），默认为`scatter` |
| `diag_kind` | 指定对角线子图的类型，有三个选项（`auto`表示自动选择；`kde`表示核密度图；`hist`表示直方图），默认为`auto`                      |
| `markers`   | 指定散点的形状                                                                                                                 |
| `height`    | 指定每个子图的高度，默认为 2.5                                                                                                 |
| `aspect`    | 指定每个子图的宽度，默认为 2.5                                                                                                 |

```python
sns.pairplot(df,hue='sex')
```

<img src="https://fig-lianxh.oss-cn-shenzhen.aliyuncs.com/彭晴-seaborn你的绘图神奇-fig15.png" width="900">

&emsp;

## 4. 参考资料

[1][tutorial for seaborn](https://seaborn.pydata.org/tutorial.html)

&emsp;

## 5. 相关推文

> Note：产生如下推文列表的 Stata 命令为：  
> &emsp; `lianxh 可视化 Python`  
> 安装最新版 `lianxh` 命令：  
> &emsp; `ssc install lianxh, replace`

- 专题：[专题课程](https://www.lianxh.cn/blogs/44.html)
  - [⏩ 连享会公开课：实证研究中的数据可视化](https://www.lianxh.cn/news/9c86f40c6f17a.html)
  - [Stata+Python：同花顺里爬取创历史新高的股票](https://www.lianxh.cn/news/35e3f9f6a79ad.html)
- 专题：[数据分享](https://www.lianxh.cn/blogs/34.html)
  - [Python+Stata：如何获取中国气象历史数据](https://www.lianxh.cn/news/b26d2b4f29053.html)
- 专题：[Stata 入门](https://www.lianxh.cn/blogs/16.html)
  - [使用 Jupyter Notebook 配置 Stata\Python\Julia\R](https://www.lianxh.cn/news/1b7c55f899314.html)
- 专题：[Stata 教程](https://www.lianxh.cn/blogs/17.html)
  - [Stata-Python 交互-9：将 python 数据导入 Stata](https://www.lianxh.cn/news/929a3cc22307b.html)
  - [Stata-Python 交互-8：将 Stata 数据导入 Python](https://www.lianxh.cn/news/17c9d76816839.html)
  - [Stata-Python 交互-7：在 Stata 中实现机器学习-支持向量机](https://www.lianxh.cn/news/f1359e7fa9488.html)
  - [Stata-Python 交互-6：调用 APIs 和 JSON 数据](https://www.lianxh.cn/news/957b9df0d08e1.html)
  - [Stata-Python 交互-5：边际效应三维立体图示](https://www.lianxh.cn/news/303e9d5a0087c.html)
  - [Stata-Python 交互-4：如何调用 Python 宏包](https://www.lianxh.cn/news/b7fd8023587cf.html)
  - [Stata-Python 交互-3：如何安装 Python 宏包](https://www.lianxh.cn/news/5c93706797ad1.html)
  - [Stata-Python 交互-2：在 Stata 中调用 Python 的三种方式](https://www.lianxh.cn/news/290a48d428074.html)
  - [Stata-Python 交互-1：二者配合的基本设定](https://www.lianxh.cn/news/285493e301c8a.html)
- 专题：[Stata 命令](https://www.lianxh.cn/blogs/43.html)
  - [Stata 与 Python 等价命令](https://www.lianxh.cn/news/98f592b0a9d9e.html)
- 专题：[数据处理](https://www.lianxh.cn/blogs/25.html)
  - [Stata：边际处理效应及其可视化-mtefe-T309](https://www.lianxh.cn/news/edd2a0cf9fa6a.html)
  - [Stata: 约翰霍普金斯大学 COVID-19 疫情数据处理及可视化](https://www.lianxh.cn/news/ca5082adbf97f.html)
- 专题：[Stata 绘图](https://www.lianxh.cn/blogs/24.html)
  - [Stata 绘图：回归系数可视化-multicoefplot](https://www.lianxh.cn/news/3e052bd3291dd.html)
  - [Stata 绘图-可视化：组间差异比较散点图](https://www.lianxh.cn/news/b5fc0aeb1d7b7.html)
  - [Stata 可视化：biplot 一图看尽方差、相关性和主成分](https://www.lianxh.cn/news/3173ebd034f12.html)
  - [Stata 绘图-组间差异可视化：不良事件火山图、点阵图](https://www.lianxh.cn/news/f9680c4be14fe.html)
  - [forest-森林图：分组回归系数可视化](https://www.lianxh.cn/news/472768848cd8d.html)
  - [Stata 绘图：回归系数可视化-论文更出彩](https://www.lianxh.cn/news/324f5e3053883.html)
  - [Stata 绘图：世行可视化案例-条形图-密度函数图-地图-断点回归图-散点图](https://www.lianxh.cn/news/96989b0de4d83.html)
  - [Stata 绘图：随机推断中的系数可视化](https://www.lianxh.cn/news/ce93c41862c16.html)
- 专题：[Stata 程序](https://www.lianxh.cn/blogs/26.html)
  - [Stata 程序：是否有类似-Python-中的-zip()-函数](https://www.lianxh.cn/news/08e4b2b6f56ca.html)
- 专题：[结果输出](https://www.lianxh.cn/blogs/22.html)
  - [Stata 可视化：让他看懂我的结果！](https://www.lianxh.cn/news/01607de7be5e8.html)
- 专题：[回归分析](https://www.lianxh.cn/blogs/32.html)
  - [Stata：在线可视化模拟-OLS-的性质](https://www.lianxh.cn/news/555995cc140a8.html)
- 专题：[文本分析-爬虫](https://www.lianxh.cn/blogs/36.html)
  - [Stata+Python：爬取创历史新高股票列表](https://www.lianxh.cn/news/741fb511af2a1.html)
  - [Python：爬取东方财富股吧评论进行情感分析](https://www.lianxh.cn/news/788ffac4c50fb.html)
  - [VaR 风险价值: Stata 及 Python 实现](https://www.lianxh.cn/news/5001362259713.html)
  - [支持向量机：Stata 和 Python 实现](https://www.lianxh.cn/news/4997d62149216.html)
  - [Python 爬虫: 《经济研究》研究热点和主题分析](https://www.lianxh.cn/news/2fb619662956e.html)
- 专题：[Python-R-Matlab](https://www.lianxh.cn/blogs/37.html)
  - [Python：多进程、多线程及其爬虫应用](https://www.lianxh.cn/news/8c175c980bcd9.html)
  - [Python：爬取动态网站](https://www.lianxh.cn/news/0b6fd3e71afe9.html)
  - [Python 爬取静态网站：以历史天气为例](https://www.lianxh.cn/news/63ffc529caf31.html)
  - [Python：绘制动态地图-pyecharts](https://www.lianxh.cn/news/113f0d9abb4e8.html)
  - [Python 爬虫 1：小白系列之 requests 和 json](https://www.lianxh.cn/news/b4f20b9c35e27.html)
  - [Python 爬虫 2：小白系列之 requests 和 lxml](https://www.lianxh.cn/news/22c7f1ab6295e.html)
  - [Python 爬虫：爬取华尔街日报的全部历史文章并翻译](https://www.lianxh.cn/news/e080bab8798f9.html)
  - [Python 爬虫：从 SEC-EDGAR 爬取股东治理数据-Shareholder-Activism](https://www.lianxh.cn/news/f2ec917e39a6c.html)
  - [Python：爬取巨潮网公告](https://www.lianxh.cn/news/94192bcec139e.html)
  - [司继春：Python 学习建议和资源](https://www.lianxh.cn/news/e353969e44de9.html)
  - [Stata 交互：Python-与-Stata-对比](https://www.lianxh.cn/news/83f922ff1daea.html)
  - [Python：拆分文件让百万级数据运行速度提高 135 倍](https://www.lianxh.cn/news/00dd20363b364.html)
  - [Python+Stata：批量制作个性化结业证书](https://www.lianxh.cn/news/1164f7ad9b4cc.html)
  - [Python+Wind：用 Pyautogui 轻松下载 Wind 数据](https://www.lianxh.cn/news/4abccd481a8e7.html)
  - [Python：爬取上市公司公告-Wind-CSMAR](https://www.lianxh.cn/news/ca3a4a5b54758.html)
  - [Python: 如何优雅地管理微信数据库？](https://www.lianxh.cn/news/d34f09cb214e0.html)
  - [Python: 6 小时爬完上交所和深交所的年报问询函](https://www.lianxh.cn/news/0e57c635cd225.html)
  - [Python: 使用正则表达式从文本中定位并提取想要的内容](https://www.lianxh.cn/news/7c2e4aed24196.html)
  - [Python 调用 API 爬取百度 POI 数据小贴士——坐标转换、数据清洗与 ArcGIS 可视化](https://www.lianxh.cn/news/a72842993b22b.html)
  - [Python 调用 API 爬取百度 POI 数据](https://www.lianxh.cn/news/223fabe3b6724.html)
  - [Python 调用 API 进行逆地理编码](https://www.lianxh.cn/news/c79e366974316.html)
  - [Python 调用 API 进行地理编码](https://www.lianxh.cn/news/b08df4d49099f.html)
  - [Python: 批量爬取下载中国知网(CNKI) PDF 论文](https://www.lianxh.cn/news/a27e2dd57f12e.html)
- 专题：[工具软件](https://www.lianxh.cn/blogs/23.html)
  - [知乎热议：有哪些一用就爱上的可视化工具？](https://www.lianxh.cn/news/67e8b9c15a0e9.html)
- 专题：[其它](https://www.lianxh.cn/blogs/33.html)
  - [数据可视化：带孩子们边玩边学吧](https://www.lianxh.cn/news/5a0f12c4ea08a.html)
  - [ES 期望损失: Stata 及 Python 实现](https://www.lianxh.cn/news/5e74f7966cf51.html)

<img src="https://fig-lianxh.oss-cn-shenzhen.aliyuncs.com/Lianxh_装饰黄线.png" width="700">

&emsp;

## 相关课程

> ### 免费公开课

- [直击面板数据模型](https://lianxh.duanshu.com/#/brief/course/7d1d3266e07d424dbeb3926170835b38) - 连玉君，时长：1 小时 40 分钟，[课程主页](https://gitee.com/arlionn/PanelData)，[Bilibili 站版](https://www.bilibili.com/video/BV1oU4y187qY)
- [Stata 33 讲](http://lianxh-pc.duanshu.com/course/detail/b22b17ee02c24015ae759478697df2a0) - 连玉君, 每讲 15 分钟. [课程主页](https://gitee.com/arlionn/stata101)，[课件](https://gitee.com/arlionn/stata101)，[Bilibili 站版](https://space.bilibili.com/546535876/channel/detail?cid=160748)
- [Stata 小白的取经之路](https://lianxh.duanshu.com/#/brief/course/137d1b7c7c0045e682d3cf0cb2711530) - 龙志能，时长：2 小时，[课程主页](https://gitee.com/arlionn/StataBin)
- 部分直播课 [课程资料下载](https://gitee.com/arlionn/Live) (PPT，dofiles 等)

> ### 最新课程-直播课

| 专题                                                                   | 嘉宾   | 直播/回看视频                                                                                                                                                                                                                                                                            |
| ---------------------------------------------------------------------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| &#x2B50; **[最新专题](https://www.lianxh.cn/news/46917f1076104.html)** |        | 文本分析、机器学习、效率专题、生存分析等                                                                                                                                                                                                                                                 |
| 研究设计                                                               | 连玉君 | [我的特斯拉-实证研究设计](https://lianxh.duanshu.com/#/course/5ae82756cc1b478c872a63cbca4f0a5e)，[-幻灯片-](https://gitee.com/arlionn/Live/tree/master/%E6%88%91%E7%9A%84%E7%89%B9%E6%96%AF%E6%8B%89-%E5%AE%9E%E8%AF%81%E7%A0%94%E7%A9%B6%E8%AE%BE%E8%AE%A1-%E8%BF%9E%E7%8E%89%E5%90%9B) |
| 面板模型                                                               | 连玉君 | [动态面板模型](https://efves.duanshu.com/#/brief/course/3c3ac06108594577a6e3112323d93f3e)，[-幻灯片-](https://quqi.gblhgk.com/s/880197/o7tDK5tHd0YOlYJl)                                                                                                                                 |
| 面板模型                                                               | 连玉君 | [直击面板数据模型](https://lianxh.duanshu.com/#/brief/course/7d1d3266e07d424dbeb3926170835b38) [免费公开课，2 小时]                                                                                                                                                                      |

- Note: 部分课程的资料，PPT 等可以前往 [连享会-直播课](https://gitee.com/arlionn/Live) 主页查看，下载。

&emsp;

> #### &#x26F3; [课程主页](https://www.lianxh.cn/news/46917f1076104.html)

[<img src="https://fig-lianxh.oss-cn-shenzhen.aliyuncs.com/lianxhbottom01.png)](https://www.lianxh.cn/news/46917f1076104.html" width="700">

[<img src="https://fig-lianxh.oss-cn-shenzhen.aliyuncs.com/lianxhbottom02.png)](https://www.lianxh.cn/news/46917f1076104.html" width="700">

[<img src="https://fig-lianxh.oss-cn-shenzhen.aliyuncs.com/lianxhbottom03.png)](https://www.lianxh.cn/news/46917f1076104.html" width="700">

> #### &#x26F3; [课程主页](https://www.lianxh.cn/news/46917f1076104.html)

&emsp;

> ### 关于我们

- **Stata 连享会** 由中山大学连玉君老师团队创办，定期分享实证分析经验。
- [连享会-主页](https://www.lianxh.cn) 和 [知乎专栏](https://www.zhihu.com/people/arlionn/)，700+ 推文，实证分析不再抓狂。[直播间](http://lianxh.duanshu.com) 有很多视频课程，可以随时观看。
- **公众号关键词搜索/回复** 功能已经上线。大家可以在公众号左下角点击键盘图标，输入简要关键词，以便快速呈现历史推文，获取工具软件和数据下载。常见关键词：`课程, 直播, 视频, 客服, 模型设定, 研究设计, stata, plus, 绘图, 编程, 面板, 论文重现, 可视化, RDD, DID, PSM, 合成控制法` 等

&emsp;

> 连享会小程序：扫一扫，看推文，看视频……

[<img src="https://fig-lianxh.oss-cn-shenzhen.aliyuncs.com/连享会小程序二维码180.png)](https://www.lianxh.cn/news/46917f1076104.html" width="700">

&emsp;

> 扫码加入连享会微信群，提问交流更方便

<img src="https://fig-lianxh.oss-cn-shenzhen.aliyuncs.com/连享会-学习交流微信群001-150.jpg" width="700">

> &#x270F; 连享会-常见问题解答：  
> &#x2728; <https://gitee.com/lianxh/Course/wikis>

&emsp;

> <font color=red>New！</font> **`lianxh` 命令发布了：**  
> 随时搜索连享会推文、Stata 资源，安装命令如下：  
> &emsp; `. ssc install lianxh`  
> 使用详情参见帮助文件 (有惊喜)：  
> &emsp; `. help lianxh`

<img src="https://fig-lianxh.oss-cn-shenzhen.aliyuncs.com/Lianxh_装饰黄线.png" width="700">
