---
layout: default
title: Projects
permalink: /projects/
---

<div class="col-lg-12">
 <div class="row justify-content-center mr-0">
      <div class="col-lg-12">
              <ul>
                  <div class="row">
                      {% for project in site.author_project_details %}
                      <div class="col-md-3 m-2 card blog-post">
                          <a href="{{project.project_url}}" target="_blank">
                            <img class="card-img-top mx-auto d-block w-50" src="/assets/img/{{project.project_thumbnail}}" alt="{{ project.project_title }}">
                          </a>
                          <div class="card-body center">
                              <a href="{{project.project_url}}" target="_blank">
                                <h4 class="card-title">{{ project.project_title }}</h4>
                              </a>
                              <p class="card-text">{{ project.project_description }} </p>
                          </div>
                      </div>
                      {% endfor %}
                  </div>
              </ul>

        <div class="row center">
          <!-- Pagination links -->
          {% if paginator.total_pages > 1 %}
            <ul class="pagination pagination-sm">
              {% if paginator.previous_page %}
                <li class="pagination-link"><a href="{{ paginator.previous_page_path | prepend: site.baseurl | replace: '//', '/' }}">&laquo;</a></li>
              {% else %}
                <li class="pagination-link disabled"><span aria-hidden="true">&laquo;</span></li>
              {% endif %}

              <li class="pagination-link" ><a href="/blog">First</a></li>

              {% for page in (1..paginator.total_pages) %}
                {% if page == paginator.page %}
             <li class="disabled pagination-link"><span><b>{{ page }}</b></span></li>
                {% elsif page == 1 %}
                  <li class="pagination-link"><a href="/blog">{{ page }}</a></li>
                {% else %}
                  <li class="pagination-link"><a href="{{ site.paginate_path | prepend: site.baseurl | replace: '//', '/' | replace: ':num', page }}">{{ page }}</a></li>
                {% endif %}
              {% endfor %}

              <li class="pagination-link"><a href="/blog/page/{{ paginator.total_pages }}/#/">Last</a></li>

              {% if paginator.next_page %}
                <li class="pagination-link"><a href="{{ paginator.next_page_path | prepend: site.baseurl | replace: '//', '/' }}">&raquo;</a></li>
              {% else %}
                <li class="disabled pagination-link"><span>&raquo;</span></li>
              {% endif %}
            </ul>
          {% endif %}
      </div>
    </div>
 </div>
</div>