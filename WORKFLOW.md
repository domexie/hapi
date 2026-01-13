# Git 工作流

本项目是 [tiann/hapi](https://github.com/tiann/hapi) 的个人 fork，用于日常使用和功能开发。

## 仓库结构

```
upstream → https://github.com/tiann/hapi (原项目)
origin   → https://github.com/domexie/hapi (个人 fork)
```

## 分支策略

| 分支 | 用途 |
|------|------|
| `main` | 保持与 upstream/main 同步，用于创建 PR |
| `personal/improvements` | 个人日常使用，包含所有个人修改 |
| `feature/*` | 新功能分支，从 main 创建，可贡献回原项目 |
| `fix/*` | 修复分支，从 main 创建，可贡献回原项目 |

## 常用操作

### 1. 同步上游更新

```bash
# 获取上游最新代码
git fetch upstream

# 更新本地 main
git checkout main
git merge upstream/main
git push origin main

# 将个人分支 rebase 到最新 main
git checkout personal/improvements
git rebase main
git push --force-with-lease
```

### 2. 开发新功能（可贡献回原项目）

```bash
# 确保 main 是最新的
git checkout main
git pull upstream main

# 创建功能分支
git checkout -b feature/xxx

# 开发完成后推送
git push origin feature/xxx

# 在 GitHub 上创建 PR 到 tiann/hapi
```

### 3. 将功能合并到个人分支

**方式一：Cherry-pick（推荐，精确控制）**
```bash
git checkout personal/improvements
git cherry-pick <commit-hash>
git push --force-with-lease
```

**方式二：等功能合并到 main 后 rebase**
```bash
git checkout personal/improvements
git rebase main
git push --force-with-lease
```

### 4. 处理 Rebase 冲突

```bash
# 冲突时，解决冲突后
git add <resolved-files>
git rebase --continue

# 放弃 rebase
git rebase --abort

# 出问题时恢复
git reflog                    # 找到 rebase 前的 commit
git reset --hard HEAD@{n}     # 恢复到那个状态
```

## 注意事项

- 始终用 `--force-with-lease` 而非 `--force`
- 功能分支必须从 `main` 创建才能贡献回原项目
- 定期同步上游更新，避免分歧过大
