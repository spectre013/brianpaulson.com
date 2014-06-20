---
Description: First post of my new blog using Hugo.
Keywords:
- GO
Section: post
Slug: first-post-go-hugo
Tags:
- go
Title: Go 1.3 Released
Topics:
- go
- Personal
date: 2014-06-19
---

Today we are happy to announce the release of Go 1.3. This release comes six months after our last major release and provides better performance, improved tools, support for running Go in new environments, and more. All Go users should upgrade to Go 1.3. You can grab the release from our downloads page and find the full list of improvements and fixes in the release notes. What follows are some highlights.

Godoc, the Go documentation server, now performs static analysis. When enabled with the -analysis flag, analysis results are presented in both the source and package documentation views, making it easier than ever to navigate and understand Go programs. See the documentation for the details.

The gc toolchain now supports the Native Client (NaCl) execution sandbox on the 32- and 64-bit Intel architectures. This permits the safe execution of untrusted code, useful in environments such as the Playground. To set up NaCl on your system see the NativeClient wiki page.


{{% highlight html %}}
<section id="main">
  <div>
   <h1 id="title">{{ .Title }}</h1>
    {{ range .Data.Pages }}
        {{ .Render "summary"}}
    {{ end }}
  </div>
</section>
{{% /highlight %}}