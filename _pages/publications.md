---
layout: archive
title: "Publications"
permalink: /publications/
author_profile: true
class: page-publications  
---

{% if site.author.googlescholar %}
  <div class="wordwrap">You can also find a full list of my publications on <a href="{{site.author.googlescholar}}">my Google Scholar profile</a>.</div>
{% endif %}

{% include base_path %}

{% assign pubs = site.publications | sort: 'year' | reverse %}



<div class="publications-page">
  <!-- 按类别分组的出版物列表 -->
  {% assign grouped_pubs = pubs | group_by: 'category' | sort: 'name' %}
  
  {% for group in grouped_pubs %}
    {% assign category_id = group.name | slugify %}
    <div class="publication-category" id="category-{{ category_id }}">
      <h2 class="category-title">
        {{ group.name | default: "Other Publications" }}
        <!-- <span class="publication-count">({{ group.size }})</span> -->
      </h2>
      
      <div class="publications-list">
        {% for pub in group.items %}
          <section class="publication-item" 
                   data-year="{{ pub.year }}" 
                   data-category="{{ category_id }}"
                   data-title="{{ pub.title | downcase }}"
                   data-authors="{{ pub.authors | downcase }}"
                   data-venue="{{ pub.venue | downcase }}">
            <h3 class="publication-title">
              {{ pub.title }}
              <span class="title-resources">
                {% if pub.pdf %}
                  <a href="{{ pub.pdf | prepend: '/files/' | relative_url }}" target="_blank" class="pdf-link" title="Download PDF">
                    <i class="fas fa-file-pdf"></i>
                  </a>
                {% endif %}
                {% if pub.code %}
                  <a href="{{ pub.code }}" 
                    target="_blank" 
                    class="resource-icon code-icon" 
                    title="View Code">
                    <i class="fab fa-github"></i>
                  </a>
                {% endif %}
                {% if pub.video %}
                  <a href="{{ pub.video }}" 
                    target="_blank" 
                    class="resource-icon video-icon" 
                    title="View Video">
                    <i class="fas fa-video"></i>
                  </a>
                {% endif %}
                {% if pub.data %}
                  <a href="{{ pub.data }}" 
                    target="_blank" 
                    class="resource-icon data-icon" 
                    title="View Data">
                    <i class="fas fa-database"></i>
                  </a>
                {% endif %}
                {% if pub.slides %}
                  <a href="{{ pub.slides }}" 
                    target="_blank" 
                    class="resource-icon slides-icon" 
                    title="View Slides">
                    <i class="fas fa-presentation-screen"></i>
                  </a>
                {% endif %}
              </span>
            </h3>
            <div class="publication-meta">
              <div class="publication-authors">
                {{ pub.authors | markdownify | remove: '<p>' | remove: '</p>' }}
              </div>
              <div class="publication-details">
                <em>{{ pub.venue }}</em>, {{ pub.year }}
                {% if pub.pages %} | pp. {{ pub.pages }}{% endif %}
                {% if pub.doi %} | DOI: <a href="https://doi.org/{{ pub.doi }}" target="_blank">{{ pub.doi }}</a>{% endif %}
              </div>
            </div>
            
            <!-- 显示分类标签 -->
            <!-- {% if pub.category %}
              <div class="publication-category-tag">
                <i class="fas fa-tag"></i> {{ pub.category }}
              </div>
            {% endif %} -->
          </section>
        {% endfor %}
      </div>
    </div>
  {% endfor %}
</div>

<!-- 分类过滤器和搜索框 -->
<!-- <div class="publications-toolbar">
  <div class="search-box">
    <i class="fas fa-search"></i>
    <input type="text" id="publication-search" placeholder="Search publications...">
  </div>
  <div class="category-filters">
    <span class="filter-label">Filter by Category:</span>
    <div class="category-buttons">
      <button class="category-btn active" data-category="all">All Publications</button>
      {% assign categories = pubs | map: 'category' | uniq | compact | sort %}
      {% for cat in categories %}
        <button class="category-btn" data-category="{{ cat | slugify }}">{{ cat }}</button>
      {% endfor %}
    </div>
  </div>
</div> -->

<!-- 分类和搜索功能脚本 -->
<!-- <script>
document.addEventListener('DOMContentLoaded', function() {
  // 分类过滤功能
  const categoryButtons = document.querySelectorAll('.category-btn');
  const publicationItems = document.querySelectorAll('.publication-item');
  const publicationCategories = document.querySelectorAll('.publication-category');
  
  categoryButtons.forEach(button => {
    button.addEventListener('click', function() {
      // 更新按钮状态
      categoryButtons.forEach(btn => btn.classList.remove('active'));
      this.classList.add('active');
      
      const category = this.dataset.category;
      
      // 显示/隐藏出版物
      publicationItems.forEach(item => {
        if (category === 'all' || item.dataset.category === category) {
          item.style.display = 'block';
        } else {
          item.style.display = 'none';
        }
      });
      
      // 显示/隐藏分类标题
      publicationCategories.forEach(cat => {
        if (category === 'all') {
          cat.style.display = 'block';
        } else {
          const catId = cat.id.replace('category-', '');
          if (catId === category) {
            cat.style.display = 'block';
          } else {
            cat.style.display = 'none';
          }
        }
      });
    });
  });
  
  // 搜索功能
  const searchInput = document.getElementById('publication-search');
  
  searchInput.addEventListener('input', function() {
    const searchTerm = this.value.toLowerCase().trim();
    
    publicationItems.forEach(item => {
      const title = item.dataset.title;
      const authors = item.dataset.authors;
      const venue = item.dataset.venue;
      
      if (searchTerm === '' || 
          title.includes(searchTerm) || 
          authors.includes(searchTerm) || 
          venue.includes(searchTerm)) {
        item.style.display = 'block';
      } else {
        item.style.display = 'none';
      }
    });
  });
  
  // 初始显示所有出版物
  publicationItems.forEach(item => item.style.display = 'block');
});
</script> -->

<style>
/* ================= 分类工具栏 ================= */
.publications-toolbar {
  margin: 2rem 0;
  padding: 1.5rem;
  background: #f8f9fa;
  border-radius: 12px;
  display: flex;
  flex-wrap: wrap;
  gap: 1.5rem;
  align-items: center;
  border: 1px solid #e2e8f0;
}

.category-filters {
  flex: 1;
  min-width: 100%;
}

.filter-label {
  font-weight: 600;
  margin-right: 1rem;
  color: #2d3748;
}

.category-buttons {
  display: flex;
  flex-wrap: wrap;
  gap: 0.8rem;
  margin-top: 0.8rem;
}

.category-btn {
  padding: 0.6rem 1.2rem;
  border: 1px solid #e2e8f0;
  border-radius: 50px;
  background: #fff;
  cursor: pointer;
  font-size: 0.9rem;
  transition: all 0.2s;
  box-shadow: 0 1px 3px rgba(0,0,0,0.05);
  
  &.active, &:hover {
    background: #4299e1;
    color: white;
    border-color: #4299e1;
    box-shadow: 0 2px 5px rgba(66, 153, 225, 0.3);
  }
}

.search-box {
  flex: 1;
  min-width: 300px;
  position: relative;
  
  input {
    width: 100%;
    padding: 0.8rem 1rem 0.8rem 40px;
    border: 1px solid #e2e8f0;
    border-radius: 30px;
    font-size: 1rem;
    transition: all 0.3s;
    
    &:focus {
      outline: none;
      border-color: #4299e1;
      box-shadow: 0 0 0 3px rgba(66, 153, 225, 0.2);
    }
  }
  
  .fa-search {
    position: absolute;
    left: 15px;
    top: 50%;
    transform: translateY(-50%);
    color: #a0aec0;
  }
}

/* ================= 分类标题 ================= */
.publication-category {
  margin-bottom: 3rem;
  padding-bottom: 2rem;
  border-bottom: 1px solid #eaeaea;
}

.category-title {
  font-size: 1.6rem;
  margin-bottom: 1.5rem;
  padding-bottom: 0.8rem;
  border-bottom: 2px solid #4299e1;
  display: flex;
  align-items: center;
}

.publication-count {
  font-size: 1rem;
  background: #4299e1;
  color: white;
  border-radius: 20px;
  padding: 0.2rem 0.8rem;
  margin-left: 1rem;
  font-weight: normal;
}

/* ================= 分类标签 ================= */
.publication-category-tag {
  display: inline-flex;
  align-items: center;
  margin-top: 0.8rem;
  padding: 0.4rem 0.8rem;
  background-color: #f0f7ff;
  border-radius: 50px;
  color: #2b6cb0;
  font-size: 0.85rem;
  border: 1px solid #c3dafe;
  
  i {
    margin-right: 0.4rem;
    color: #4299e1;
  }
}

/* ================= 响应式设计 ================= */
@media (max-width: 768px) {
  .publications-toolbar {
    flex-direction: column;
    align-items: stretch;
    gap: 1.5rem;
  }
  
  .category-buttons {
    justify-content: center;
  }
  
  .search-box {
    min-width: 100%;
  }
}

@media (max-width: 480px) {
  .category-buttons {
    gap: 0.5rem;
  }
  
  .category-btn {
    padding: 0.5rem 1rem;
    font-size: 0.85rem;
  }
  
  .category-title {
    font-size: 1.4rem;
    flex-direction: column;
    align-items: flex-start;
  }
  
  .publication-count {
    margin-left: 0;
    margin-top: 0.5rem;
  }
}

/* ================= 资源图标样式 ================= */
.title-resources {
  display: inline-flex;
  gap: 0.6rem;
  margin-left: 0.8rem;
}

.resource-icon {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 24px;
  height: 24px;
  border-radius: 50%;
  color: white !important;
  font-size: 0.9rem;
  transition: all 0.2s ease;
  opacity: 0.8;
  text-decoration: none !important;
  position: relative;
  
  &:hover {
    opacity: 1;
    transform: scale(1.1);
  }
  
  // 悬停提示
  &::after {
    content: attr(title);
    position: absolute;
    bottom: -28px;
    left: 50%;
    transform: translateX(-50%);
    background: rgba(0, 0, 0, 0.85);
    color: white;
    padding: 4px 8px;
    border-radius: 4px;
    font-size: 0.75rem;
    white-space: nowrap;
    opacity: 0;
    visibility: hidden;
    transition: opacity 0.2s;
    z-index: 100;
    pointer-events: none;
  }
  
  &:hover::after {
    opacity: 1;
    visibility: visible;
  }
}

/* 特定图标样式 */
.pdf-link { 
  background-color: #e53e3e; 
  &:hover { background-color: #c53030; }
}
.code-icon { 
  background-color: #2d3748; 
  &:hover { background-color: #1a202c; }
}
.video-icon { 
  background-color: #805ad5; 
  &:hover { background-color: #6b46c1; }
}
.data-icon { 
  background-color: #3182ce; 
  &:hover { background-color: #2b6cb0; }
}
.slides-icon { 
  background-color: #38a169; 
  &:hover { background-color: #2f855a; }
}
</style>