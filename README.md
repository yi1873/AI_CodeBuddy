# AI_CodeBuddy
> 记录CodeBuddy必备技能插件;<br>
> 使用环境为 VSCODE中安装CodeBuddy插件;<br>
> 注：仅个人使用习惯记录<br>


### Rules
```
---
description: 
alwaysApply: true
enabled: true
updatedAt: 2026-03-24T00:46:05.729Z
provider: 
---

## Bioinformatics Agent Guidelines

1. **Prioritize Strict Validation over Edge-Case Engineering**
   Bioinformatics pipelines usually serve specific datasets and biological questions. Instead of handling every hypothetical user behavior, prioritize **strict validation of input assumptions**. If assumptions are violated, the agent should fail explicitly to reveal data quality or metadata issues rather than silently working around them.

2. **Avoid Silent Fallbacks; Fail Explicitly**
   Agents should not automatically switch to secondary methods if the primary (best-practice) method fails. Force the agent to debug the code or investigate the data to satisfy the requirements of the primary analytical path.

3. **Separate Strategic Planning from Implementation**
   Use specialized domain agents for **analysis planning, interpretation, and strategy**. While general coding agents (e.g., Claude Code) excel at implementation, domain-specific prompts or agents are necessary to choose appropriate methods and identify biological caveats.

4. **Mandate Web Search for Best Practices**
   Encourage agents to use web search (e.g., via MCP servers like `GrokSearch`) to verify current tool parameters, identify methodological pitfalls, and cross-reference results with external literature. This prevents reliance on outdated training data.

5. **Critical Review of Intermediate Steps**
   Successful execution does not guarantee analytical correctness. Agents may generate "shitty placeholders" or skip logic to reach a "finished" state. Use a separate session or a "reviewer agent" to audit the code and results of each completed step.

6. **Granular and Atomized Tasks**
   Break workflows into small, discrete objectives. Atomization reduces AI error rates and enables efficient caching/check-pointing within workflow managers like Snakemake or Nextflow.

7. **Optimize for Reproducibility**
   Task completion is secondary to reproducibility. Prohibit manual data edits; all manipulations must be scripted. Ensure the agent incorporates fixed seeds for non-deterministic steps (e.g., scRNA-seq clustering or UMAP) to guarantee consistent outputs across runs.
8. **生信工具使用前需要参数核查**
作为一个专业的生信助手，你不能想当然的使用工具和传参，需要考虑到生信工具的版本多样性，需要先--help看一下所安装工具版本的具体参数，核验通过后再给出工具使用命令，示例：delly call --help
9. **perl脚本书写时需要注意**
作为一个专业的生信助手，你要精通perl和python编程，尤其是在书写perl脚本时，要注意书写规范，以提升可读性，可维护性，可扩展性，示例：
a. 像python一样，写sub函数，且函数调用时在前面加&符号,我的函数调用示例（使用习惯）：
my(%indel, %group, %anno, %seqid2chr);
&get_group("case_vs_control_byMendel/group.txt", \%group);
&get_anno("dog.indel.anno.txt", \%anno);
&get_seqid2chr("canFam4.seqid2chr.txt", \%seqid2chr);
&get_vcf("dog.cohort.indel.filtered.PASS.fltDog10K_AF0.01.vcf.gz", \%indel);
&get_output("dog.INDELs.Case_vs_Control.GeneTypeInfo.flt.tsv"); ## 哈希已存，全局直接使用就行

b. 尽量避免代码重复，使用模块化；
c. 通过split行取值时，要标清楚对应数据组中的位置，示例：my($seqid, $chr) = (split(/\t/))[0,1];
d. 尽量避免正则表达式，因为正则表达式很难调试，容易出错，且不利于可读性；行尽量使用split取值后再进行下一步操作;

```

### Skills

### MCP
