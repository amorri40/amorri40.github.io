---
layout: page
title: Glasgow Based Web UI & Mobile Software Developer
tagline: Javascript, Python, C++ and More!
subtitle:   <h3> <a role="button" class="btn btn-primary hvr-grow-shadow" href="http://alasdairmorrison.com/cv/Alasdair_Morrison_CV_web.pdf" target="_blanks">
                 Download My CV
            </a></h3>
           
                            
css: ['about.css', 'sidebar-popular-repo.css', '../../bower_components/flag-icon-css/css/flag-icon.min.css']
---
<section class="content container">

    <div class="row">

        <!-- Post List -->
        <div class="col-md-8">

            <ol class="post-list">
                {% for post in site.posts %}
                <li class="post-list-item">
                    <h2 class="post-list-title">
                        <a class="hvr-underline-from-center" href="{{ site.url }}{{ post.url }}">{{ post.title }}</a>
                    </h2>
                    <p class="post-list-description">
                        {{ post.excerpt | strip_html | strip }}
                    </p>
                    <p class="post-list-meta">
                        <span class="octicon octicon-calendar"></span> {{ post.date | date: "%Y/%m/%d" }}
                    </p>
                </li>
                {% endfor %}
            </ol>

            <!-- Pagination -->
            {% include pagination.html %}

            <!-- Comments -->
            {% include disqus-comments.html %}

        </div>

        <div class="col-md-4">
            {% include sidebar-popular-repo.html %}
        </div>

    </div>

</section>

