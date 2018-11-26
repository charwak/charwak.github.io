---
title: "Stories"
layout: archive
permalink: "/stories/"
author_profile: true
header:
  image: "/images/fort point.png"
---
Lorem ipsum dolor sit amet consectetur adipiscing elit sollicitudin nunc, quam id libero suscipit fusce mauris eleifend venenatis velit tellus, ornare ut sagittis in senectus lacus nulla tristique. Aptent adipiscing eget mollis morbi cum platea parturient, massa per viverra tellus dictumst torquent, quisque feugiat conubia iaculis diam vulputate. Vulputate taciti facilisi elit ridiculus vitae id curae nullam habitasse, integer metus lectus dignissim natoque curabitur massa sapien, nam odio scelerisque per enim fringilla cubilia elementum. Hac consectetur elit potenti aenean viverra nibh ipsum, mattis facilisi enim vel odio nullam commodo tristique, in himenaeos bibendum eget primis suscipit.


\begin{equation*}
\mathbf{V}_1 \times \mathbf{V}_2 =  \begin{vmatrix}
\mathbf{i} & \mathbf{j} & \mathbf{k} \\
\frac{\partial X}{\partial u} &  \frac{\partial Y}{\partial u} & 0 \\
\frac{\partial X}{\partial v} &  \frac{\partial Y}{\partial v} & 0
\end{vmatrix}
\end{equation*}

import pandas as pd
import seaborn as sns
%matplotlib inline

url = "https://archive.ics.uci.edu/ml/machine-learning-databases/iris/iris.data"
names = ['sepal-length', 'sepal-width', 'petal-length', 'petal-width', 'class']
iris = pd.read_csv(url, names=names)

iris.head()
iris.describe()

sns.pairplot(x_vars=["petal-length"], y_vars=["petal-width"], data=iris, hue="class", size=10)
