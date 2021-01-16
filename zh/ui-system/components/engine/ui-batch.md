# UI 合批规则说明

UI 合批的规则是哈希材质、贴图源以及贴图采样都相同则进行合批。同哈希的意思是即使使用的是相同的材质，如果它们的哈希值不一样，还是会打断合批，就比如两个材质涉及到 Uniform 的修改，导致不能合批。精灵和文本也是一样，因为贴图不一致。当然，在严格控制的情况下也是可以一个图集的，但这是后话。

UI 的渲染数据采集是一个基于节点树的渲染方式，因此，在你递归节点树的过程中如果遇到 UIMeshRenderer，Mask，Graphics 这三个组件，以及上述情况，都会打断合批，所以我们建议分模块制作，独立模块的贴图进行合图，来减少 DrawCall，但要达到大量数据的合批，就需要严格进行节点布局。