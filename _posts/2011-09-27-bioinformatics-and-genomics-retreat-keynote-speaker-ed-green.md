---
layout: post
title: Bioinformatics and Genomics Retreat – Keynote speaker Ed Green
tags:
- bioinformatics
- reseach
- science
- seminar
status: publish
type: post
published: true
meta:
  _searchme: '1'
  _edit_last: '1'
  original_post_id: '1863'
  _wp_old_slug: '1863'
---
<a href="http://green.soe.ucsc.edu/">Ed Green</a> 一个月前来讲过<a href="http://zh.wikipedia.org/wiki/%E5%B0%BC%E5%AE%89%E5%BE%B7%E7%89%B9%E4%BA%BA">尼安德特人</a>（<a href="http://en.wikipedia.org/wiki/Neanderthal">Neanderthal</a>）基因组的故事，于是这次 retreat 主要侧重技术方面的细节。这些细节看似很枯燥，其实充满了 insight，Ed 实在是很靠谱的。

背景懒得说了，没看过这篇长达13页的 Science 文章的童鞋请速速围观：

Science 7 May 2010:Vol. 328 no. 5979 pp. 710-722
<a href="http://www.sciencemag.org/content/328/5979/710.full">A Draft Sequence of the Neandertal Genome</a>

分析尼安德特人基因组的主要难题在于，尼安德特人是已知的和人类最相似的物种，两个尼安德特人基因组之间的差异都有可能高于尼安德特人和我们的平均差异。尼安德特人的DNA是从腿骨标本里提取的，在标本漫长的发掘保存过程中，会受到现代人的DNA的污染，因此正确区分尼安德特人的DNA和现代人的DNA是非常关键的。

首先，他们在研究中发现，测序得到的 reads 与人类基因组比对的时候，reads 5’端和3’端的错配（mismatch）概率最高，在5’端通常是C变成T，而3’端是G变成A。这个很神奇，因为尼安德特人的DNA应该是随机断裂的，为什么会在DNA片段的端点有更高的错配呢？原因是，古老的DNA片段的5’端会自发进行胞嘧啶（C）脱氨基变成尿嘧啶（U）的过程，而测序的结果中，U显示成T。那么3’端又是什么情况？错配刚好和5’端是互补的。Ed 推测说，很可能DNA片段不是 blunt end，而是有 1nt overhang，因此测序时的扩增就自行在3’端加上了U的互补碱基A。

然后，Ed讲到如何估算现代人类和尼安德特人的进化距离。这就需要用另外一个物种作为 out-group。于是已经有完整基因组序列的现存人类最接近的物种黑猩猩就登场了。但是，他们研究中发现，先把尼安德特人和人类的序列比对，然后再和黑猩猩比对，间接得到的尼安德特人和黑猩猩的比对结果，不同于直接比对黑猩猩和尼安德特人的结果。原因是，序列比对算法有偏差，总是强迫两个序列尽可能接近，而真实情况可能并不是理论上最接近的情况。因此他们自己写了 3-way orthology 的比对算法，以解决这个问题。3-way算法得到，人类和尼安德特人的金华距离是人类和黑猩猩的12%，而如果先比对尼安德特人和黑猩猩（这样会人为导致尼安德特人和黑猩猩的相似程度比实际高），则得到15%。假设我们相信人和黑猩猩的进化距离是650万年的话（这个数字很有争议），那么乘以12%得到，人类和尼安德特人的进化距离是80万年。

然后，Ed提到短序列的偏差问题，就是如果测序得到的序列过短（尼安德特人的DNA降解的很厉害，所以通常只有几十个核苷酸长度），就可能被 map 到基因组很多地方，如果此时选择差异最小的比对，也许低估了实际的距离。因此他们在计算进化距离时，只考虑能被唯一 map 到基因组的序列。

回到最开始说的问题，如何区分人类和尼安德特人的DNA。因为人和黑猩猩的DNA序列差异是1%，则人和尼安德特人的DNA序列差异小于0.1%，和高达2%的测序错误相比，几乎可以忽略。于是他们需要一些方法来估计测序得到的序列中人类DNA的比例。他们用了3种独立的方法：

1. 线粒体DNA

在2008年，他们已经得到了完整并且相当准确的<a href="http://www.ncbi.nlm.nih.gov/pmc/articles/PMC2602844/">尼安德特人线粒体DNA序列</a>。因此他们可以通过判断多少比例的序列中含有人和尼安德特人线粒体DNA的SNP来估计人类DNA的污染，结果是 0.27%

2. Y染色体序列

因为尼安德特人的DNA样本都来自女性，因此可以通过测得的序列中 map 到人类Y染色体序列的比例来估计来自男性人类DNA的污染，结果是 0.6%。Ed 也承认这个估计没办法得到女性人类的DNA污染比例。

3. 找到一些位点，人类的序列和黑猩猩及2个尼安德特人都不同，然后检验第3个尼安德特人的这个位点的序列，和人类相同的比例。如果第3个尼安德特人的这个位点和人类相同，而和祖先序列不同，则可能是2种情况：A、人类序列的污染；B、尼安德特人种内的差异。这样估计的结果是0.7%

总体来说，测序结果中，现代人类序列的污染应该小于1%。

下面讲到现代人之间的差异。两个非洲人之间的差异和一个非洲人同一个欧亚人的差异差不多，这说明人类的多样性在非洲得到了充分体现。而欧亚大陆的人之间的差异性很小，说明进化过程中遇到了<a href="http://en.wikipedia.org/wiki/History_of_Eurasia#Population_bottleneck">瓶颈</a>，丢失了多样性。

通常人类的单倍体图谱是下图左边的结构，非洲人群（A）差异最大。但是有少数的位点，最大的差异并不存在于非洲人之间，而是存在于欧亚人（nA）之间，下图右边：


![](/images/2011/09/haplotype.png)

同时，与非洲人相比，尼安德特人和欧亚人有更多相同的SNP，这些都表明，尼安德特人很可能和欧亚人有过基因交流。

最后，Ed 讲了最近关于丹尼索瓦人（<a href="http://en.wikipedia.org/wiki/Denisova_hominin">Denisova hominin</a>）的研究进展，丹尼索瓦人和尼安德特人的亲缘关系比人和尼安德特人的还要近。然后时间不够了，Ed 一边迅速的翻过剩下的十几张幻灯片，一边遗憾的叹息道：这些都是很有趣的故事呀，可惜我没时间了。
