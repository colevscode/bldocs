{{$meta}}
type: reference
title: Authorization API
subnav: |
  {{$ each /backlift/files/reference/apis/*.html as entry | if {$ entry.api } is auth | sort {$ entry.title } }}
    <li><a href="/reference/authapi#{$ entry.tag }">{$ entry.title }</a></li>
  {{$ endeach }}
{{$endmeta}}

{{$layout /partials/base.html as content}}

{{$ include /partials/apioverview.html }}

{{$ each /backlift/files/reference/apis/*.html as entry | if {$ entry.api } is auth | sort {$ entry.title } }}
  {{$ include /partials/refentry.html }}
{{$ endeach }}
