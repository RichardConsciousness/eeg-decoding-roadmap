# Day 7 First Baseline

## 1. 今天使用了什么输入特征
今天使用的是最简单的 baseline 特征：把每个 EEG epoch 直接展平为一个一维向量。
原始 epoch 的 shape 为 `64 x 801`，展平后每个样本共有 `51264` 个特征。

## 2. 今天使用了什么分类器
今天使用的是 `StandardScaler + LinearSVC` 的线性 baseline 分类器。

## 3. 多数类 baseline 是多少
当前数据中多数类是 `T0`，多数类 baseline accuracy 约为 `0.48`。

## 4. 模型结果如何
### 单次 stratified train/test split
当前结果如下：
- accuracy: `1.0`
- confusion matrix:
```text
[[4 0 0]
 [0 2 0]
 [0 0 3]]
```
这说明在这一次切分下，`LinearSVC` 明显高于多数类 baseline。

### 5-fold stratified cross-validation
进一步使用 5 折 stratified cross-validation 后，得到结果如下：
- CV scores: `[0.6667, 0.6667, 1.0, 0.6667, 0.8]`
- Mean CV accuracy: `0.76`
- Std CV accuracy: `0.13`
这说明当前数据中确实存在可分信息，模型表现明显高于多数类 baseline。  
但由于样本量较小，且不同折之间仍然有一定波动，所以当前 baseline 还不能认为已经稳定。

## 5. 对这个 baseline 的理解
这个 baseline 的作用是先验证完整分类流程是否能够跑通。

当前结果说明，在当前 subject 和当前 run 上，简单线性分类器已经能够提取到一定的区分信息。

但需要注意以下几点：
- 当前样本数很少
- 训练和测试样本都来自同一个 subject 和同一个 run
- 当前特征仍然比较粗糙，只是直接 flatten 了原始 epoch

因此，这个 baseline 可以说明流程有效、数据中存在可分信息，但还不能直接说明模型已经具有稳定泛化能力。

## 6. 下一步计划
下一步应继续使用更合理的 EEG baseline 方法进行验证，例如：
- 更合适的预处理
- 更合理的时间窗选择
- `CSP + LogisticRegression` 或 `CSP + SVM`
- 更严格的 cross-validation 评估
