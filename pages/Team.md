---
layout: gridlay
title: Team
subtitle: Corces Lab Members
---

# **Lab Members**
{% for person in site.data.LabMembers %}
<hr>
<!-- The paddingtop and margin-top edits allow anchors to link properly. -->
<div id = "{{person.name}}" class="row" style="padding-top: 60px; margin-top: -60px;">
    <div class="col-sm-3">
        <img class="img-responsive" src="{{person.image}}" {% if person.altimage %} onmouseover="this.src='{{person.altimage}}';" onmouseout="this.src='{{person.image}}';" {% endif %} alt="{{person.name}}"><br>
        <strong>{{person.name}}</strong> <br>
        {{person.position}} <br>
        <em>{{person.email}}</em> <br>
        {% if person.website %}
          <a href= "{{person.website}}">{{person.website}}</a> <br>
        {% endif %}
        {% if person.orcid %}
          <a href="http://orcid.org"><img class="inline-block" src="/static/img/orcid_logo.png"></a>
          <a href="http://{{person.orcid}}"> {{person.orcid}}</a> <br>
        {% endif %}
        {% if person.scholar %}
          <a href= "http://scholar.google.com/citations?user={{person.scholar}}"><span class="fa fa-graduation-cap" aria-hidden="true"></span> Google Scholar </a> <br>
        {% endif %}
        {% if person.twitter %}
          <a href= "http://twitter.com/{{person.twitter}}"><span class="fab fa-twitter" aria-hidden="true"></span> @{{person.twitter}} </a> <br>
        {% endif %}
    </div>
    <div class="col-sm-8" style="text-align: justify">
        {{person.description | markdownify}}
    </div>
</div>
{% endfor %}