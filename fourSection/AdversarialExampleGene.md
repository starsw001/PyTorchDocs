# 生成对抗示例
本教程将提高您对ML（机器学习）模型的安全漏洞的认识，并将深入了解对抗性机器学习的热门话题。您可能会惊讶地发现，
为图像添加难以察觉的扰动会导致模型性能大不相同。鉴于这是一个教程，我们将通过图像分类器上的示例探讨该主题。具体来说，我们将
使用第一种也是最流行的攻击方法之一，即快速梯度符号攻击算法（FGSM）来迷惑 MNIST 分类器。

### 1.威胁模型
对于上下文，有许多类别的对抗性攻击，每种攻击具有不同的目标和对攻击者知识的假设。然而，通常，总体目标是向输入数据添加最少
量的扰动以引起期望的错误分类。攻击者的知识有几种假设，其中两种是：白盒子和黑盒子。白盒攻击假定攻击者具有对模型的完全知识和访问权限，包括体系结构，输入，输出和权重。黑盒攻击假设攻击者只能访问模型的输入和输出，并且对底层架构或权重一无所知。还有几种类型的目标，包括错误分类和源/目标错误分类。错误分类的目标意味着攻击者只希望输出分类错误，但不关心新分类是什么。源/目标错误分类意味着攻击者想要更改最初属于特定源类的图像，以便将其归类为特定目标类。

在这种情况下，FGSM攻击是一种白盒攻击，其目标是错误分类。有了这些背景信息，我们现在可以详细讨论攻击。