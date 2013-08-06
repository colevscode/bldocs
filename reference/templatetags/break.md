{{$ meta }}
title: Break
tag: break
syntax: |
    {{$&nbsp;break&nbsp;}}<br>
{{$ endmeta }} 

{{$raw}}
The `break` tag is used in conjunction with the [tobreak filter??]() in order to write an exerpt of the content from a file. For example, if your file contains the following content:

/myfile.html:

	<h1>My file</h1>
	This is my file. There are many like it but this one is mine.

	{{$ break }}

	Blablabla.

Then later you can use the [include??]() tag in conjunction with the [tobreak??]() filter to write out the content of the file up to the break like this:

	{{$ include /myfile.html | tobreak }}

{{$endraw}}





