---
title: test01
date: 2024-12-28 04:39:07
tags:
---
# test01

```python
import torch
import torch.nn as nn
import torch.optim as optim
import time

# 确认CUDA和cuDNN是否可用
assert torch.cuda.is_available(), "CUDA is not available"
assert torch.backends.cudnn.enabled, "cuDNN is not enabled"

# 设置设备
device = torch.device("cuda")

# 定义一个简单的卷积神经网络
class ConvNet(nn.Module):
    def __init__(self):
        super(ConvNet, self).__init__()
        self.conv1 = nn.Conv2d(3, 32, kernel_size=3, padding=1)
        self.conv2 = nn.Conv2d(32, 64, kernel_size=3, padding=1)
        self.pool = nn.MaxPool2d(2, 2)
        self.fc1 = nn.Linear(64 * 8 * 8, 512)
        self.fc2 = nn.Linear(512, 10)

    def forward(self, x):
        x = self.pool(torch.relu(self.conv1(x)))
        x = self.pool(torch.relu(self.conv2(x)))
        x = x.view(-1, 64 * 8 * 8)
        x = torch.relu(self.fc1(x))
        x = self.fc2(x)
        return x

# 实例化网络并将其移至GPU
model = ConvNet().to(device)

# 定义损失函数和优化器
criterion = nn.CrossEntropyLoss()
optimizer = optim.Adam(model.parameters(), lr=0.001)

# 生成一些随机输入和标签进行训练
# 假设输入是32x32的彩色图像，批量大小为64
inputs = torch.randn(64, 3, 32, 32).to(device)
labels = torch.randint(0, 10, (64,)).to(device)

# 训练模型
model.train()  # 设置为训练模式
start_time = time.time()  # 记录开始时间
target_duration = 300  # 设置目标运行时间（秒）
epochs = 0  # 初始化epoch计数器
report_interval = 1000  # 设置报告间隔

# 使用for循环代替while True循环
while time.time() - start_time < target_duration:
    optimizer.zero_grad()  # 清除旧的梯度
    outputs = model(inputs)  # 前向传播
    loss = criterion(outputs, labels)  # 计算损失
    loss.backward()  # 反向传播
    optimizer.step()  # 更新参数
    epochs += 1  # 更新epoch计数器

    # 每1000轮打印一次
    if epochs % report_interval == 0:
        print(f"Epoch: {epochs}, Loss: {loss.item()}")

# 循环结束后打印结果
end_time = time.time()  # 记录结束时间
elapsed_time = end_time - start_time  # 计算总耗时
print(f"Training finished. Total time: {elapsed_time:.2f} seconds, Epochs: {epochs}")
```