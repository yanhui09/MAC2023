---
layout: page
title: Staff
description: A listing of all the course staff members.
---

# Staff

## Course Instructor

{% assign course_instructors = site.staffers | where: 'role', 'Course Instructor' %}
{% for staffer in course_instructors %}
{{ staffer }}
{% endfor %}

{% assign lesson_teacher = site.staffers | where: 'role', 'Lesson Teacher' %}
{% assign num_lesson_teacher = lesson_teacher | size %}
{% if num_lesson_teacher != 0 %}
## Lesson Teacher

{% for staffer in lesson_teacher %}
{{ staffer }}
{% endfor %}
{% endif %}
