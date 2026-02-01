# Slides 制作计划：Formalizing Group Action in Lean

**生成日期**: 2025-02-01  
**代码版本**: `v1.2.1-lean-only` (https://github.com/FrankieeW/GroupAction)  
**基于**: Report (`../Report/report.tex`)  
**模板**: Imperial College Beamer (`template_presentation.tex`)

---

## 一、演讲基本信息

| 项目 | 内容 |
|------|------|
| **主题** | Formalizing Group Action in Lean |
| **时长** | 10-15 分钟 |
| **场景** | MATH70040 课程作业汇报 |
| **Slides 数量** | 15-18 张 (含可选示例) |
| **侧重** | 数学定义与定理、证明思路与步骤、Lean 代码展示 |
| **代码引用** | `https://github.com/FrankieeW/GroupAction/blob/v1.2.1-lean-only/lean/GroupAction/` |

---

## 二、内容来源 (Report 结构)

Report 的三大组件：
1. **Core Definitions**: `GroupAction` typeclass, Faithful, Transitive
2. **Concrete Examples**: 7 个具体示例 (全部制作供选取)
3. **Key Theorems**: Theorem 16.3 (置换表示), Theorem 16.12 (稳定子)

---

## 三、Slides 结构详细规划

### Part 0: Opening (2 slides)

| # | 类型 | 标题 | 内容 | 时长 |
|---|------|------|------|------|
| 1 | Title | Formalizing Group Action in Lean | 作者、课程、日期、GitHub | 30s |
| 2 | Agenda | Outline | 5 部分概览 | 30s |

### Part I: Introduction (1-2 slides, ~1.5 min)

| # | 类型 | 标题 | 内容 | 时长 |
|---|------|------|------|------|
| 3 | Content | What is Group Action? | 数学动机 + 项目目标 (3 组件) | 1min |
| 4 | Content | Main Results Preview | Theorem 16.3 & 16.12 陈述 | 30s |

### Part II: Core Definitions (2-3 slides, ~2.5 min)

| # | 类型 | 标题 | 内容 | 代码来源 (v1.2.1-lean-only) |
|---|------|------|------|----------------------------|
| 5 | Two-column | Group Action Definition | 数学定义 vs Lean `class GroupAction` | `Defs.lean:15-22` |
| 6 | Two-column | Faithful Actions | 数学定义 vs Lean `def Faithful` | `Defs.lean:26-28` |
| 7 | Two-column | Transitive Actions | 数学定义 vs Lean `def Transitive` | `Defs.lean:33-35` |

### Part III: Examples (7 slides, 用户选取)

| # | 类型 | 标题 | 内容 | 代码来源 (v1.2.1-lean-only) | 优先级 |
|---|------|------|------|----------------------------|--------|
| 8 | Code | Symmetric Group on X | $\mathrm{Sym}(X)$ 作用于 $X$ | `Examples.lean:20-27` | **高** |
| 9 | Code | Symmetric Group Properties | Faithful & Transitive 证明 | `Examples.lean:29-44` | 高 |
| 10 | Code | Left Multiplication | $G$ 左乘自身 | `Examples.lean:46-54` | 高 |
| 11 | Code | Subgroup on Group | 子群 $H$ 作用于 $G$ | `Examples.lean:58-65` | 中 |
| 12 | Code | Conjugation Action | 共轭作用 $h_1 h_2 h_1^{-1}$ | `Examples.lean:67-78` | 中 |
| 13 | Code | Scalar on Complex Vectors | $\mathbb{C}^\times$ 作用于 $\mathbb{C}^n$ | `Examples.lean:82-92` | 中 |
| 14 | Code | Dihedral Group $D_4$ | $D_4$ 作用于 $\mathbb{Z}/4$ | `Examples.lean:108-156` | **高** |

### Part IV: Main Theorems (5-6 slides, ~5 min)

#### Theorem 16.3: Permutation Representation

| # | 类型 | 标题 | 内容 | 代码来源 (v1.2.1-lean-only) |
|---|------|------|------|----------------------------|
| 15 | Highlight | Theorem 16.3 Statement | $\phi: G \to \mathrm{Sym}(X)$ 是群同态 | - |
| 16 | Diagram | Proof Path: 5 Steps | 步骤流程图 | - |
| 17 | Code | Step 1-2: Define $\sigma_g$ & Prove Bijection | `sigma` 和 `sigmaPerm` | `Permutation.lean:24-27, 30-67` |
| 18 | Code | Step 3-4: Construct $\phi$ & Verify Homomorphism | `phi`, `phi_mul`, `phi_one` | `Permutation.lean:69-100` |
| 19 | Code | Step 5: Package Theorem | `group_action_to_perm_representation` | `Permutation.lean:102-114` |

#### Theorem 16.12: Stabilizer Subgroup

| # | 类型 | 标题 | 内容 | 代码来源 (v1.2.1-lean-only) |
|---|------|------|------|----------------------------|
| 20 | Two-column | Theorem 16.12 Statement | $G_x$ 是子群 | - |
| 21 | Code | Stabilizer Definition & Proof | `stabilizerSet`, `stabilizer` | `Stabilizer.lean:22-56` |

### Part V: Reflection & Conclusion (3 slides, ~2 min)

| # | 类型 | 标题 | 内容 |
|---|------|------|------|
| 22 | Content | What Lean Guarantees | 类型正确、无隐藏假设、公理匹配、子群验证 |
| 23 | Content | Challenges Encountered | Typeclass resolution, Equiv 机制, Coercions, ext |
| 24 | Content | Conclusion & Future | 总结 + Future Extensions |

### Part VI: Closing (1 slide)

| # | 类型 | 标题 | 内容 |
|---|------|------|------|
| 25 | Thank You | Thank You & Questions | GitHub URL, 联系方式 |

---

## 四、关键代码片段提取清单 (v1.2.1-lean-only)

**GitHub 基础 URL**: `https://github.com/FrankieeW/GroupAction/blob/v1.2.1-lean-only/lean/GroupAction/`

### Defs.lean

| 行号 | 内容 | 用于 Slide |
|------|------|------------|
| 15-22 | `class GroupAction` (含 `act`, `ga_mul`, `ga_one`) | #5 |
| 26-28 | `def GroupAction.faithful` | #6 |
| 33-35 | `def GroupAction.transitive` | #7 |

**代码片段 - GroupAction class**:
```lean
class GroupAction (G : Type*) [Monoid G] (X : Type*) where
  act : G → X → X
  ga_mul : ∀ g₁ g₂ x, act (g₁ * g₂) x = act g₁ (act g₂ x)
  ga_one : ∀ x, act 1 x = x
```

**代码片段 - Faithful**:
```lean
def GroupAction.faithful {G : Type*} [Group G] {X : Type*} [GroupAction G X] : Prop :=
  ∀ g₁ g₂ : G, (∀ x : X, GroupAction.act g₁ x = GroupAction.act g₂ x) → g₁ = g₂
```

**代码片段 - Transitive**:
```lean
def GroupAction.transitive {G : Type*} [Group G] {X : Type*} [GroupAction G X] : Prop :=
  ∀ x₁ x₂ : X, ∃ g : G, GroupAction.act g x₁ = x₂
```

### Examples.lean

| 行号 | 内容 | 用于 Slide |
|------|------|------------|
| 20-27 | `instance permGroupAction` | #8 |
| 29-44 | `theorem permGroupAction_faithful`, `permGroupAction_transitive` | #9 |
| 46-54 | `instance groupAsGSet` (左乘) | #10 |
| 58-65 | `instance subgroupAsGSet` (子群作用) | #11 |
| 67-78 | `instance subgroupAsGSetConjugation` (共轭) | #12 |
| 82-92 | `instance vectorSpaceAsCStarSet` (复标量) | #13 |
| 108-156 | `D4`, `d4Act`, `instance d4ActionZMod4` | #14 |

**代码片段 - Symmetric Group**:
```lean
instance permGroupAction (X : Type*) : GroupAction (Equiv.Perm X) X :=
  { act := fun g x => g x
    ga_mul := by intro g1 g2 x; rfl
    ga_one := by intro x; rfl }
```

**代码片段 - Left Multiplication**:
```lean
instance groupAsGSet (G : Type*) [Group G] : GroupAction G G :=
  { act := fun g1 g2 => g1 * g2
    ga_mul := by intro g1 g2 g3; rw [mul_assoc]
    ga_one := by intro g; rw [one_mul] }
```

**代码片段 - Dihedral D4**:
```lean
abbrev D4 := DihedralGroup 4

def d4Act (g : D4) (x : ZMod 4) : ZMod 4 :=
  match g with
  | DihedralGroup.r i => x - i      -- Rotation
  | DihedralGroup.sr i => i - x     -- Reflection

instance d4ActionZMod4 : GroupAction D4 (ZMod 4) :=
  { act := d4Act
    ga_mul := by intro g1 g2 x; cases g1 <;> cases g2 <;> simp [d4Act, sub_eq_add_neg] <;> ring
    ga_one := by intro x; simp [DihedralGroup.one_def, d4Act, -DihedralGroup.r_zero] }
```

### Permutation.lean

| 行号 | 内容 | 用于 Slide |
|------|------|------------|
| 24-27 | `def sigma` | #17 |
| 30-67 | `def sigmaPerm` (含 `left_inv`, `right_inv` 证明) | #17 |
| 69-72 | `def phi` | #18 |
| 74 | `lemma phi_apply` | #18 |
| 80-93 | `lemma phi_mul` | #18 |
| 95-100 | `lemma phi_one` | #18 |
| 102-114 | `theorem group_action_to_perm_representation` | #19 |

**代码片段 - sigma**:
```lean
def sigma (g : G) : X → X :=
  fun x => GroupAction.act g x
```

**代码片段 - sigmaPerm** (核心):
```lean
def sigmaPerm (g : G) : Equiv.Perm X :=
  { toFun := sigma g
    invFun := sigma g⁻¹
    left_inv := by
      intro x
      calc GroupAction.act g⁻¹ (GroupAction.act g x)
          = GroupAction.act (g⁻¹ * g) x := by simpa using (GroupAction.ga_mul g⁻¹ g x).symm
        _ = GroupAction.act (1 : G) x := by simp
        _ = x := GroupAction.ga_one x
    right_inv := ... }
```

**代码片段 - phi homomorphism**:
```lean
lemma phi_mul (g₁ g₂ : G) : phi (X := X) (g₁ * g₂) = phi (X := X) g₁ * phi (X := X) g₂ := by
  apply Equiv.ext
  intro (x : X)
  calc phi (g₁ * g₂) x = GroupAction.act (g₁ * g₂) x := rfl
    _ = GroupAction.act g₁ (GroupAction.act g₂ x) := GroupAction.ga_mul g₁ g₂ x
```

**代码片段 - Final Theorem**:
```lean
theorem group_action_to_perm_representation :
  ∃ (φ : G → Equiv.Perm X),
    (∀ g x, φ g x = GroupAction.act g x) ∧
    (∀ g₁ g₂, φ (g₁ * g₂) = φ g₁ * φ g₂) ∧
    (φ 1 = 1) := by
  exact ⟨phi, ⟨phi_apply, ⟨phi_mul, phi_one⟩⟩⟩
```

### Stabilizer.lean

| 行号 | 内容 | 用于 Slide |
|------|------|------------|
| 22-23 | `def stabilizerSet` | #21 |
| 26-54 | `def stabilizer` (Subgroup 构造) | #21 |
| 56-59 | `theorem stabilizer_set_is_subgroup` | #21 |

**代码片段 - stabilizerSet**:
```lean
def stabilizerSet (x : X) : Set G :=
  { g : G | GroupAction.act g x = x }
```

**代码片段 - stabilizer Subgroup**:
```lean
def stabilizer (x : X) : Subgroup G := by
  exact
    { carrier := stabilizerSet (G := G) (X := X) x
      one_mem' := by simp [stabilizerSet, GroupAction.ga_one x]
      mul_mem' := by
        intro g₁ g₂ hg₁ hg₂
        calc GroupAction.act (g₁ * g₂) x
            = GroupAction.act g₁ (GroupAction.act g₂ x) := by simpa using (GroupAction.ga_mul g₁ g₂ x)
          _ = GroupAction.act g₁ x := by rw [hg₂]
          _ = x := hg₁
      inv_mem' := by
        intro g hg
        calc GroupAction.act g⁻¹ x
            = GroupAction.act g⁻¹ (GroupAction.act g x) := by rw [hg]
          _ = GroupAction.act (g⁻¹ * g) x := by simpa using (GroupAction.ga_mul g⁻¹ g x).symm
          _ = x := by simp [GroupAction.ga_one] }
```

---

## 五、视觉设计指南

### 颜色方案 (Imperial Theme)
- **Primary**: ICLBlue (#003E74)
- **Secondary**: ICLDarkBlue, ICLCream, ICLLightGrey
- **Code Background**: Light grey or cream

### 布局原则
1. **数学定义 slides**: 两栏布局 (左数学，右Lean)
2. **代码 slides**: 大字体 (≥10pt for code)，语法高亮
3. **定理 slides**: 居中高亮框
4. **步骤 slides**: 编号列表或流程图

### 字体
- 正文: Imperial Sans (已配置)
- 代码: FreeMono 或等宽字体
- 数学: 默认 LaTeX math

### 代码展示最佳实践
- 使用 `minted` 或 `listings` 包
- Lean4 语法高亮
- 代码块最大 12-15 行/slide
- 重要部分用颜色标注

---

## 六、时间分配

| Section | Slides | 时长 | 占比 |
|---------|--------|------|------|
| Opening | 2 | 1 min | 8% |
| Introduction | 2 | 1.5 min | 12% |
| Definitions | 3 | 2.5 min | 19% |
| Examples | 2-7 (选) | 2-3 min | 15-23% |
| **Theorems** | **7** | **5 min** | **38%** |
| Reflection | 3 | 2 min | 15% |
| **Total** | **19-25** | **~13 min** | 100% |

> **注**: Examples 部分全部制作 (7个)，演讲时根据时间选取 2-3 个展示。

---

## 七、文件结构

```
Slides/
├── main.tex                    # 主演示文件 [待创建]
├── .sisyphus/PLAN.md           # 本计划文件
├── AGENTS.md                   # 项目知识库
├── template_presentation.tex   # Imperial 模板参考
├── beamerthemeImperial.sty     # 主题文件
├── beamercolorthemeImperial.sty
├── beamerinnerthemeImperial.sty
├── beamerouterthemeImperial.sty
├── Fonts/                      # 字体
├── Images/                     # 图片资源
│   ├── ICL_Logo_Blue.pdf
│   ├── ICL_Logo_White.pdf
│   └── ...
└── out/                        # 输出目录
```

---

## 八、制作检查清单

- [x] 创建 `main.tex` 基础框架
- [x] Title Slide + Agenda
- [x] Introduction (2 slides)
- [x] Definitions (3 slides)
  - [x] GroupAction class
  - [x] Faithful
  - [x] Transitive
- [x] Examples - 全部 7 个
  - [x] Symmetric Group instance
  - [x] Symmetric Group properties (faithful/transitive)
  - [x] Left Multiplication
  - [x] Subgroup Action
  - [x] Conjugation
  - [x] Complex Scalars
  - [x] Dihedral $D_4$
- [x] Theorem 16.3 (5 slides)
  - [x] Statement
  - [x] Proof Path diagram
  - [x] sigma & sigmaPerm
  - [x] phi & homomorphism
  - [x] Final theorem
- [x] Theorem 16.12 (2 slides)
  - [x] Statement
  - [x] Stabilizer code
- [x] Reflection (2 slides)
- [x] Conclusion + Thank You
- [x] 编译测试 (XeLaTeX)
- [x] 视觉检查

---

## 九、参考资源

- **代码仓库**: https://github.com/FrankieeW/GroupAction (tag: `v1.2.1-lean-only`)
- **Report**: `../Report/report.tex`
- **教材**: Fraleigh & Katz, *A First Course in Abstract Algebra*, Section 16
- **Imperial 模板**: `template_presentation.tex`

---

## 十、执行命令

完成计划后，使用以下命令开始执行：

```bash
/start-work
```

这将启动 Sisyphus 工作流程，按照本计划创建 Slides。
