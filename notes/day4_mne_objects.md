# Day 4 MNE Objects

## 1. Raw 对象是什么
Raw 对象表示连续 EEG 原始信号。它包含多个 channel 的时间序列数据，以及采样率、通道信息等元数据。它对应Day 3 中的 raw signal，也就是还没有按任务切分的连续脑电数据。

## 2. info 里最重要的字段是什么
`sfreq`、`ch_names` 和 `nchan`。`sfreq` 表示采样频率，决定每秒采多少个时间点；`ch_names` 表示通道名称；`nchan` 表示通道数量。这些信息会直接影响后续的可视化、切片和建模。

## 3. channel 是什么
Channel 是一个记录通道，通常对应一个电极位置上的时间序列信号。EEG 数据不是单条信号，而是多个 channel 同时记录得到的多变量时间序列。

## 4. events 是怎么来的
events 是从 raw 的 annotations 中提取出来的。它们表示实验任务、刺激或提示在时间轴上的发生位置。后续可以根据这些 events，从连续信号中切出与任务相关的 epoch。

## 5. Raw、events、epochs 的关系
Raw 是连续的原始 EEG 信号。Events 是时间轴上的任务标记或事件锚点。Epochs 是围绕 events 从 raw 中切出来的时间窗样本。后续分析和建模通常基于 epochs，而不是整段连续 raw。
