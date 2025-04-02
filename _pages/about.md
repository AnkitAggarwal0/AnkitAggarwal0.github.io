---
layout: about
title: about
permalink: /
subtitle: Robotics. Controls. Mechatronic Design. 

profile:
  align: right
  image: prof_pic.jpg
  image_circular: false # crops the image to make it circular
  more_info: >
    <p>Carnegie Mellon University</p>
    <p>Pittsburgh, PA</p>

news: false # includes a list of news items
selected_papers: false # includes a list of papers marked as "selected={true}"
social: true # includes social icons at the bottom of the page
---
<h4> Hey! My name is Ankit Aggarwal. I am currently pursuing a Master’s in Robotic Systems Development (MRSD) at the Robotics Institute, Carnegie Mellon University. As part of this program, my capstone project lies in the domain of Space Robotics – <a href = "projects/1_project">Lunar ROADSTER </a>, a Robotic Operator for Autonomous Development of Surface Trails and Exploration Routes. </h4>

<h4> My core interest lies in creating robots in unpredictable environments. This ranges from robots that operate in extra-terrestrial conditions or aid humans work in hard-to-access mining sites. Robotics allows me to explore a broad spectrum of engineering problems, and I enjoy creating complete multi-disciplinary systems from the ground up.  </h4>

<h4> I recently graduated from Manipal Institute of Technology with a Bachelor of Technology degree. My major was Mechatronics, and my minor was Robotics and Automation. During my undergraduate tenure, I led a team of undergraduate students to various international robotics competitions with Mars Rover Manipal and research projects in the domain of parallel robots and IoT. </h4>

<h4> Find my complete CV <a href ="/cv"> here </a>. </h4>


<!--Write your biography here. Tell the world about yourself. Link to your favorite [subreddit](http://reddit.com). You can put a picture in, too. The code is already in, just name your picture `prof_pic.jpg` and put it in the `img/` folder.

Put your address / P.O. box / other info right below your picture. You can also disable any of these elements by editing `profile` property of the YAML header of your `_pages/about.md`. Edit `_bibliography/papers.bib` and Jekyll will render your [publications page](/al-folio/publications/) automatically.

Link to your social media connections, too. This theme is set up to use [Font Awesome icons](https://fontawesome.com/) and [Academicons](https://jpswalsh.github.io/academicons/), like the ones below. Add your Facebook, Twitter, LinkedIn, Google Scholar, or just disable all of them. -->
<br />

<h3> <b> <a href = "/projects"> Projects </a></b> </h3>
<hr>

<!-- pages/projects.md -->
<div class="projects">
{% if site.enable_project_categories and page.display_categories %}
  <!-- Display categorized projects -->
  {% for category in page.display_categories %}
  <a id="{{ category }}" href=".#{{ category }}">
    <h2 class="category">{{ category }}</h2>
  </a>
  {% assign categorized_projects = site.projects | where: "category", category %}
  {% assign sorted_projects = categorized_projects | sort: "importance" %}
  <!-- Generate cards for each project -->
  {% if page.horizontal %}
  <div class="container">
    <div class="row row-cols-1 row-cols-md-2">
    {% for project in sorted_projects %}
      {% include projects_horizontal.liquid %}
    {% endfor %}
    </div>
  </div>
  {% else %}
  <div class="row row-cols-1 row-cols-md-3">
    {% for project in sorted_projects %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
  {% endif %}
  {% endfor %}

{% else %}

<!-- Display projects without categories -->

{% assign sorted_projects = site.projects | sort: "importance" %}

  <!-- Generate cards for each project -->

{% if page.horizontal %}

  <div class="container">
    <div class="row row-cols-1 row-cols-md-2">
    {% for project in sorted_projects %}
      {% include projects_horizontal.liquid %}
    {% endfor %}
    </div>
  </div>
  {% else %}
  <div class="row row-cols-1 row-cols-md-3">
    {% for project in sorted_projects %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
  {% endif %}
{% endif %}
</div>


<br />

<h3> <b> Publications </b> </h3>
<!-- {% include bib_search.liquid %} -->
<div class="publications">

{% bibliography %}

</div>