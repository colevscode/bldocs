{{$meta}}
type: reference
title: Template Tags
{{$endmeta}}

{{$layout /index.html as content}}

<style>
  .templatetag span {
    display: inline-block;
    font-size: larger;
    font-family: courier;
  }
</style>


Backlift makes several template tags available for use in HTML files. These tags let you add dynamic data to your website. Please see the discusion about the use of template tags and general syntax [here](/guides/templatelang.html).

{{$ each /reference/templatetags/*.html as tag }}
  asdfasdfasdf
  <div class="templatetag">
    <h2> {$ tag.name } </h2>
    <span> {$ tag.syntax } </span>
    <p> {$ tag.desc } </p>
    {{$ each /examples/*.html as ex | if {$ tag.name } in {$ ex.tags } }}
      <p>
        <em>{$ ex.title }</em>
        <pre>{$ ex.example }</pre>
      </p>
    {{$ endeach /examples/*.html as ex }}
  </div>
{{$ endeach }}