---
layout: gridlay
title: Team
subtitle: Corces Lab Members
---

<div class="clear"></div>

<div class="container" style="margin-top:-50px">
  <div class="jumbotron jumbotron-correct">
      <img src="/img/CorcesLab_DEI-Illustration_DrawImpacts_WithLogo.jpg" alt="The Corces Lab @ The Gladstone Institute For Neurological Disease"><br>
      <h3 style="text-align:center"> Welcome to the Corces Lab!</h3>
      <p style="font-size:14px;margin-top:10px">
        In the Corces lab, we know it takes a diverse group of empowered individuals to effectively address the most important scientific questions. However, we also believe that equity and inclusion are important beyond the benefits they provide to the science we do. In this lab, we understand identity as intersectional and layered and engage with each other and our science through this lens. As such, we are committed to ensuring that gender expression, race, age, sexual orientation, ability status, and socioeconomic status do not play a role in defining who is afforded the opportunity to excel in science. To us, this includes (i) regularly participating in science outreach including the Gladstone PUMAS program for undergraduate students, (ii) posting our job openings on websites that attract diverse applicants and removing implicit bias from personnel decisions, (iii) thinking deeply about diversity, equity, and inclusion and our own roles in perpetuating inequity through workshops and lab-specific DEI journal clubs, and (iv) a commitment to eschewing convenient silence when we can use our positions to build equal access to science for everyone. The structural and systemic nature of inequity that persists in our society makes it inadequate to simply offer a seat at the lab bench, and we are dedicated to fundamentally changing the role that science plays in perpetuating that inequity. We know that this commitment and the growth it involves is a continuous journey and feel strongly that it is worth the thought, courage, and humility that it requires.
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