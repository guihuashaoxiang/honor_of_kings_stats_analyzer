# 游戏对局数据分析

本仓库包含对游戏对局数据的分析和可视化代码。通过该代码，您可以分析对局的胜负率、阵营分配、对局时长、击杀数、死亡数、助攻数等关键指标，并通过图表直观展示分析结果。

## 项目结构

```
game-analysis/
│
├── raw.csv                # 原始对局数据文件
├── analysis.ipynb         # 数据分析与可视化的 Jupyter Notebook 文件
└── README.md              # 项目说明文件
```

## 依赖库

确保您已安装以下 Python 库：

- `pandas`
- `numpy`
- `matplotlib`
- `seaborn`

您可以通过以下命令安装这些库：

```bash
pip install pandas numpy matplotlib seaborn
```

## 数据分析内容

### 1. 总对局场数

代码计算了总对局场数，并输出了结果。

```python
total_games = len(df)
print(f"总对局场数: {total_games}")
```

### 2. 胜率与失败率分析

通过饼图展示了胜利和失败的对局占比。

```python
win_count = len(df[df['gameresult'] == 1])
lose_count = len(df[df['gameresult'] == 2])
plt.pie([win_count, lose_count], labels=['胜利', '失败'], autopct=autopct_format([win_count, lose_count]), colors=['red', 'blue'])
plt.title(f'胜率与失败率（总对局场数:{total_games}）', fontproperties=font)
plt.show()
```

### 3. 阵营分配占比

分析了蓝色方和红色方的阵营分配占比，并通过饼图展示。

```python
acnt_camp_distribution = df['AcntCamp'].value_counts()
plt.pie(acnt_camp_distribution, labels=['蓝色方', '红色方'], autopct=autopct_format(acnt_camp_distribution), colors=['blue', 'red'])
plt.title('阵营分配占比', fontproperties=font)
plt.show()
```

### 4. 每天星星数变化

分析了每天星星数的变化，并通过折线图展示。

```python
plt.plot(daily_stars_full['date'], daily_stars_full['stars'], marker='o', color='#DAA520', label='星星数')
plt.title('每天星星数变化（按凌晨5点分割）', fontproperties=font, fontsize=16)
plt.xlabel('日期', fontproperties=font, fontsize=14)
plt.ylabel('星星数', fontproperties=font, fontsize=14)
plt.show()
```

### 5. 对局时长分析

分析了对局时长的分布，并通过柱状图展示。

```python
sns.histplot(df['usedTime'], bins=30, kde=False, color='blue')
plt.title('对局时长分布', fontproperties=font)
plt.xlabel('对局时长 (秒)', fontproperties=font)
plt.ylabel('对局次数', fontproperties=font)
plt.show()
```

### 6. 击杀数、死亡数、助攻数分析

分析了击杀数、死亡数、助攻数的分布，并通过柱状图展示。

```python
plot_distribution(df, 'kills', axes[1][0], '击杀数的分布', '#1f77b4')
plot_distribution(df, 'deaths', axes[1][1], '死亡数的分布', '#ff7f0e')
plot_distribution(df, 'assists', axes[1][2], '辅助数的分布', '#2ca02c')
plt.tight_layout()
plt.show()
```

### 7. MVP 对局占比

分析了 MVP 对局的占比，并通过柱状图展示。

```python
sns.barplot(x=mvp_counts.index, y=mvp_counts.values, palette='viridis', hue=mvp_counts.index, legend=False)
plt.title('MVP 对局占比', fontsize=16)
plt.xlabel('是否有 MVP', fontsize=14)
plt.ylabel('数量', fontsize=14)
plt.show()
```

### 8. 排位类型分析

分析了不同排位类型的占比和胜率，并通过柱状图展示。

```python
sns.barplot(x=map_type_counts.index, y=map_type_counts.values, palette='viridis', hue=map_type_counts.index, legend=False)
plt.title('不同排位类型的占比', fontsize=16)
plt.xlabel('排位类型', fontsize=14)
plt.ylabel('数量', fontsize=14)
plt.show()
```

## 运行代码

1. 将 `raw.csv` 文件放置在项目根目录下。
2. 打开 `analysis.ipynb` 文件并运行所有代码单元。

## 结论

通过该分析，您可以深入了解游戏对局的各方面数据，包括胜负率、阵营分配、对局时长、击杀数、死亡数、助攻数等。这些数据可以帮助您更好地理解游戏中的表现，并为未来的游戏策略提供参考。

## 贡献

如果您有任何改进或建议，欢迎提交 Issue 或 Pull Request。
