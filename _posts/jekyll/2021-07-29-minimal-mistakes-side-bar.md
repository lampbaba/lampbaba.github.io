---
layout: custom-single
title:  "사이드바 메뉴 설정"
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

#### 사이드바 메뉴 목록 설정
---
참조 블로그 - [식빵맘](https://ansohxxn.github.io/)  

`_data/navigation.yml` 파일에 사이드바 메뉴를 구성을 추가한다.

{% highlight yml linenos %}
docs:
  - title: Database
    children:
      - title: "Oracle"
        url: oracle/
        category: "oracle"
      - title: "MS-SQL"
        url: mssql/
        category: "mssql"
      - title: "MariaDB"
        url: mariadb/
        category: "mariadb"
  - title: Server
    children:
      - title: "Ubuntu"
        url: ubuntu/
        category: "ubuntu"
      - title: "Windows Server"
        url: windows-server/
        category: "windows-server"
  - title: Etc
    children:
      - title: "Jekyll"
        url: jekyll/
        category: "jekyll"
{% endhighlight %}
#### 메뉴에 포스트수 표시
---
메뉴의 우측에 게시글 수를 추가하기 위해서 `_includes\nav_list` 파일을 수정한다.

기존파일의 메뉴 명칭을 표시하는 부분을 찾는다.

{% highlight html linenos %}
{% raw %}{% for child in nav.children %}
<li><a href="{{ child.url | relative_url }}"{% if child.url == page.url %} class="active"{% endif %}>{{ child.title }}</a></li>
{$ endfor %}{% endraw %}
{% endhighlight %}

해당 카테고리를 찾아서 글수를 표시하는 부분을 추가한다.

{% highlight html linenos %}
{% raw %}{% for child in nav.children %}
{% assign category = site.categories[child.category] | where_exp: "item", "item.hidden != true" %}
  <li><a href="{{ child.url | relative_url }}"{% if child.url == page.url %} class="active"{% endif %}>{{ child.title }} ({{ category.size }})</a></li>
{% endfor %}{% endraw %}
{% endhighlight %}

완성된 파일

{% highlight html linenos %}
{% raw %}{% assign navigation = site.data.navigation[include.nav] %}

<nav class="nav__list">
  {% if page.sidebar.title %}<h3 class="nav__title" style="padding-left: 0;">{{ page.sidebar.title }}</h3>{% endif %}
  <input id="ac-toc" name="accordion-toc" type="checkbox" />
  <label for="ac-toc">{{ site.data.ui-text[site.locale].menu_label | default: "Toggle Menu" }}</label>
  <ul class="nav__items">
    {% for nav in navigation %}
      <li>
        {% if nav.url %}
          <a href="{{ nav.url | relative_url }}"><span class="nav__sub-title">{{ nav.title }}</span></a>
        {% else %}
          <span class="nav__sub-title">{{ nav.title }}</span>
        {% endif %}

        {% if nav.children != null %}
        <ul>
          {% for child in nav.children %}
          {% assign category = site.categories[child.category] | where_exp: "item", "item.hidden != true" %}
            <li><a href="{{ child.url | relative_url }}"{% if child.url == page.url %} class="active"{% endif %}>{{ child.title }} ({{ category.size }})</a></li>
          {% endfor %}
        </ul>
        {% endif %}
      </li>
    {% endfor %}
  </ul>
</nav>{% endraw %}
{% endhighlight %}

#### 카테고리 페이지 만들기
---
`_pages` 폴더 밑에 `categories` 라는 폴더(변경가능)를 만든 뒤 카테고리 별로 파일을 생성한다.  
ex) `_pages/categories/jekyll.md`

{% highlight ruby linenos %}
---
layout: archive
permalink: jekyll
title: "Jekyll"

author_profile: true
sidebar:
  nav: "docs"
---
{% raw %}
{% assign posts = site.categories.jekyll %}
{% for post in posts %}
  {% include custom-archive-single.html type=entries_layout %}
{% endfor %}{% endraw %}
```

`_includes` 폴더 밑에 `custom-archive-single.html` 파일을 추가한다.
```html
{% raw %}{% if post.header.teaser %}
  {% capture teaser %}{{ post.header.teaser }}{% endcapture %}
{% else %}
  {% assign teaser = site.teaser %}
{% endif %}

{% if post.id %}
  {% assign title = post.title | markdownify | remove: "<p>" | remove: "</p>" %}
{% else %}
  {% assign title = post.title %}
{% endif %}

<div class="{{ include.type | default: 'list' }}__item">
  <article class="archive__item" itemscope itemtype="https://schema.org/CreativeWork">
    <div>
      <span>
        <a href="{{ post.url }}">{{post.title}}</a>
      </span>
      <small> 
        <i class="fas fa-fw fa-calendar-alt" aria-hidden="true"> </i>{{ post.date | date: " %Y.%m.%d" }}
        {% if site.category_archive.type and post.categories[0] and site.tag_archive.type and post.tags[0] %}
          {%- include post__taxonomy.html -%}
        {% endif %}
      </small>
    </div>
  </article>
</div>{% endraw %}
```

#### 포스팅 하기
---
포스팅 파일의 헤더부분에 카테고리를 추가한다.
```ruby
---
layout: single
title:  "사이드바 메뉴 설정"
folder: "jekyll"
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

date: 2021-07-30
---
{% endhighlight %}