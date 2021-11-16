<head>
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">
  <!-- 最新版本的 Bootstrap 核心 CSS 文件 -->
<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css" integrity="sha384-HSMxcRTRxnN+Bdg0JdbxYKrThecOKuH5zCYotlSAcp1+c8xmyTe9GYg1l9a69psu" crossorigin="anonymous">

<!-- 可选的 Bootstrap 主题文件（一般不用引入） -->
<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap-theme.min.css" integrity="sha384-6pzBo3FDv/PJ8r2KRkGHifhEocL+1X2rVCTTkUfGk7/0pbek5mMa1upzvWbrUbOZ" crossorigin="anonymous">

<!-- 最新的 Bootstrap 核心 JavaScript 文件 -->
<script src="https://stackpath.bootstrapcdn.com/bootstrap/3.4.1/js/bootstrap.min.js" integrity="sha384-aJ21OjlMXNL5UyIl/XNwTMqvzeRMZH2w8c5cRVpzpU8Y5bApTppSuUkhZXN0VxHd" crossorigin="anonymous"></script>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.15.1/dist/katex.min.css" integrity="sha384-R4558gYOUz8mP9YWpZJjofhk+zx0AS11p36HnD2ZKj/6JR5z27gSSULCNHIRReVs" crossorigin="anonymous">
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.15.1/dist/katex.min.js" integrity="sha384-z1fJDqw8ZApjGO3/unPWUPsIymfsJmyrDVWC8Tv/a1HeOtGmkwNd/7xUS0Xcnvsx" crossorigin="anonymous"></script>
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.15.1/dist/contrib/auto-render.min.js" integrity="sha384-+XBljXPPiv+OzfbB3cVmLHf4hdUFHlWNZN5spNQ7rmHTXpd7WvJum6fIACpNNfIR" crossorigin="anonymous"></script>
<script>
    document.addEventListener("DOMContentLoaded", function() {
        renderMathInElement(document.body, {
          // customised options
          // • auto-render specific keys, e.g.:
          delimiters: [
              {left: '$$', right: '$$', display: true},
              {left: '$', right: '$', display: false},
              {left: '\\(', right: '\\)', display: false},
              {left: '\\[', right: '\\]', display: true}
          ],
          // • rendering keys, e.g.:
          throwOnError : false
        });
    });
</script>
</head>

<div class="container">
  
## NER解码新方法——GlobalPointer

CRF作为NER经典的解码方法，虽然可以站在句子全局上去预测标签序列，但是其计算量大、耗时长的缺点一直饱受诟病。GlobalPointer是一个基于span预测的解码方法，不仅成绩优于CRF，计算效率也更高。

GlobalPointer构造了一个如下图所示的上三角形，每一个格子对应一个有效的span，借助任意span的起始和终止token的representation可以计算该span为某类实体的分数。

![](https://spaces.ac.cn/usr/uploads/2021/05/2377306125.png)
  
具体地，假设第$i$个token的representation为$h_i$，引入$W_q, b_q, W_k, b_k$来计算span(i,j)的分数：
  
$$
\begin{aligned}
q_i & = W_q h_i + b_q \\
k_i & = W_k h_j + b_k \\
s(i,j) & = q_i^{\top}k_j
$$

上面的计算方法在实践中成绩很差，因为它忽略了$i$和$j$二者的位置信息，在位置编码方面，GlobalPointer采用了RoPE（旋转位置编码）来融入相对位置信息。

### RoPE


RoPE在复平面上通过旋转位置嵌入得到不同的位置编码结果。和Transformer中对三角函数计算方法不同

</div>
