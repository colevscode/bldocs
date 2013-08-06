{{$meta}}
type: reference
title: Data API
subnav: |
  {{$ each /backlift/files/reference/apis/*.html as entry | if {$ entry.api } is data | sort {$ entry.order } }}
    <li><a href="/reference/dataapi#{$ entry.tag }">{$ entry.title }</a></li>
  {{$ endeach }}
{{$endmeta}}

{{$layout /partials/base.html as content}}

{{$ include /partials/apioverview.html }}

{{$ each /backlift/files/reference/apis/*.html as entry | if {$ entry.api } is data | sort {$ entry.order } }}
  {{$ include /partials/refentry.html }}
{{$ endeach }}
