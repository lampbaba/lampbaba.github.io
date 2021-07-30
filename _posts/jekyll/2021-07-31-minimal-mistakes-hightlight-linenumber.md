---
layout: custom-single
title:  "Code Blocks Highlight 및 줄 수 표시"
categories:
  - jekyll
tags: [blog, jekyll]

author_profile: true
sidebar:
  nav: "docs"

toc: true
toc_label: "목록"
toc_icon: "bars"
toc_sticky: true

comments: true

date: 2021-07-30
---

<span style="color:darkred">minimal-mistakes 테마 기준으로 작성된 글입니다.</span>  

#### Code Blocks 적용
---
포스팅 내용에서 코드 블럭을 적용하는 방법은 3개의 백틱 \`\`\` 혹은 3개의 물결포 ~~~ 로 코드를 감싼다.

{% highlight default %}
```
func main() {
	fmt.Println("Hello World!")
}
```
{% endhighlight %}

랜더링 되면 다음과 같이 표시된다.

{% highlight default %}
func main() {
	fmt.Println("Hello World!")
}
{% endhighlight %}

#### Highlight 적용
---
코드 블록에 대한 구문 강조를 표시한다. 구문 강조를 추가하기 위해서는 코드블록의 백틱 우측에 언어를 지정한다.

{% highlight default %}
```go
func main() {
	fmt.Println("Hello World!")
}
```
{% endhighlight %}

랜더링 되면 다음과 같이 표시된다.

{% highlight go %}
func main() {
	fmt.Println("Hello World!")
}
{% endhighlight %}

#### 라인 줄 표시 - Code Blocks별 적용
---
Highlight에 라인의 번호를 표시한다. Highlight에 라인을 표시하기 위해서는 liquid 태그로 Highlight를 지정 하여야 한다.
{% highlight liquid %}
{% raw %}{% highlight 하이라이트언어 [linenos] %}
...
{% endhighlight %}{% endraw %}
{% endhighlight %}

{% highlight go %}
{% raw %}{% highlight go %}
func main() {
	fmt.Println("Hello World!")
}
{% endhighlight %}{% endraw %}
{% endhighlight %}

linenos 옵션을 추가하여 라인을 표시한다.

{% highlight go linenos %}
{% raw %}{% highlight go linenos %}
func main() {
	fmt.Println("Hello World!")
}
{% endhighlight %}{% endraw %}
{% endhighlight %}

#### 라인 줄 표시 - 전체 적용
---
모든 Code blocks에 라인줄 수 표시를 기본으로 설정한다.  
수정 파일: `_config.yml`

{% highlight yml linenos %}
markdown: kramdown
kramdown:
  syntax_highlighter: rouge
  syntax_highlighter_opts:
    block:
      line_numbers: true
{% endhighlight %}

#### 라인 줄 복사 방지
---
Highlight에 표시된 라인은 기본적으로 Drag복사시 같이 선택 할 수 있으므로 라인줄 수는 선택되지 않도록 sass파일을 수정한다.  
수정 파일: `_sass/minimal-mistakes/_syntax.scss`  
35번째 줄 쯤에 있는 rouge-gutter에 다음을 추가한다.
{% highlight scss linenos %}
    /* line numbers*/
    &.gutter,
    &.rouge-gutter {
      padding-right: 1em;
      width: 1em;
      color: $base04;
      border-right: 1px solid $base04;
      text-align: right;
      // 라인이 복사되지 않게 한다.
      -webkit-touch-callout: none;
      -webkit-user-select: none;
      -khtml-user-select: none;
      -moz-user-select: none;
      -ms-user-select: none;
      user-select: none;
    }
{% endhighlight %}