---
layout: gridlay
title: Team
subtitle: Corces Lab Members
---

<div class="clear"></div>

<div class="container" style="margin-top:-50px">
  <div class="jumbotron jumbotron-correct">
      <img src="/img/CorcesLab_DrawImpacts_WithLogo_NoText.jpg" alt="The Corces Lab @ The Gladstone Institute For Neurological Disease"><br>
      <h3 style="text-align:center"> Welcome to the Corces Lab!</h3>
      <p style="font-size:14px;margin-top:10px">
        In the Corces lab, we work together to address important unanswered scientific questions. We believe in community as a basis for success and we strive to create an atmosphere where anyone can thrive and be themselves. We understand that everyone approaches science from a different set of personal and academic experiences and that the greatest progress is made when each individual member of our team is supported by those around them. We engage in our community to both educate others about the work that we do and to provide research opportunities for individuals who otherwise may not consider a career in science as a viable option. We prioritize mentorship, scholarship, and collaboration with the goal of improving human health and leaving the world a better place than when we found it.
      </p>
      <br>
      <h5 style="text-align:center"> Interested in joining?</h5>
      <p style="font-size:14px;margin-top:10px">
        The lab is always looking for talented and motivated members (space permitting). If you are a PhD student interested in rotating or a postdoctoral fellow applicant interested in joining, email Ryan at ryan.corces (at) gladstone.ucsf.edu. Highly accomplished postdoctoral fellow applicants are encouraged to apply to the <a href="https://gladstone.org/nomis-gladstone-fellowship-program">NOMIS-Gladstone Fellowship program</a>. This interdisciplinary training and research program offers exceptional postdoctoral scientists the freedom to address big unanswered questions at the intersection of two or more scientific disciplines.
      </p>
  </div>
</div>


<hr>
{% include carousel.html height="50" unit="%" duration="7" number="1" %}
<h4 style="text-align: center;">See more photos <a href="/pages/Photos/">here</a>.</h4>
<hr>

# **Lab Members**
{% for person in site.data.LabMembers %}
<hr>
<!-- The paddingtop and margin-top edits allow anchors to link properly. -->
<div id = "{{person.name}}" class="row" style="padding-top: 60px; margin-top: -60px;">
    <div class="col-sm-3">
        <img class="img-responsive" src="{{person.image}}" {% if person.altimage %} onmouseover="this.src='{{person.altimage}}';" onmouseout="this.src='{{person.image}}';" {% endif %} alt="{{person.name}}"><br>
        <strong>{{person.name}}</strong> <br>
        {% if person.pronouns %}
           <em>{{person.pronouns}}</em> <br>
        {% endif %}
        {{person.position}} <br>
        {% if person.advisor %}
           {{person.advisor}}<br>
        {% endif %}
        <em>{{person.email}}</em> <br>
        {% if person.scholar %}
          <a href= "http://scholar.google.com/citations?user={{person.scholar}}"><span class="fa fa-graduation-cap" aria-hidden="true"></span> Google Scholar </a> <br>
        {% endif %}
        {% if person.orcid %}
          <a href= "https://orcid.org/{{person.orcid}}"><span class="fa fa-book" aria-hidden="true"></span> ORCID </a> <br>
        {% endif %}
        {% if person.twitter %}
          <a href= "http://twitter.com/{{person.twitter}}"><span class="fab fa-twitter" aria-hidden="true"></span> @{{person.twitter}} </a> <br>
        {% endif %}
        {% if person.website %}
          <a href= "{{person.website}}"><span class="fa fa-rss" aria-hidden="true"></span> {{person.website}} </a> <br>
        {% endif %}
    </div>
    <div class="col-sm-8" style="text-align: justify">
        {{person.description | markdownify}}
    </div>
</div>
{% endfor %}

<hr>

### **Alumni**
<hr>
<table>
  <tr>
    <th>Name</th>
    <th>Years in Lab</th>
    <th>Position in Lab</th>
    <th>Subsequent Position</th>
  </tr>

  {% for alumni in site.data.Alumni %}

  <tr>
    <td>{{alumni.name}}</td>
    <td>{{alumni.years}}</td>
    <td>{{alumni.position}}</td>
    <td>{{alumni.nextPosition}}</td>
  </tr>

  {% endfor %}
</table>

### **Rotation Students**
<hr>
<table>
  <tr>
    <th>Name</th>
    <th>Program</th>
    <th>Year / Quarter</th>
    <th>Thesis Lab</th>
  </tr>

  {% for rotation in site.data.Rotation %}

  <tr>
    <td>{{rotation.name}}</td>
    <td>{{rotation.program}}</td>
    <td>{{rotation.quarter}}</td>
    <td>{{rotation.thesisLab}}</td>
  </tr>

  {% endfor %}
</table>