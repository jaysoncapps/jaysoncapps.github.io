---
layout: post
title:  "Email Automation With Foundation"
date:   2017-08-11 15:43:44 -0600
categories: Foundation Email
author: "Jayson Capps"
---

<img class="img-thumbnail" src="/assets/img/blog/foundation-screenshot.png" />

At the School of Law we do a lot of email marketing. Building HTML emails can be super difficult and can feel sometimes like you're back in the 90's coding since they rely on tables for layout.

<a href="https://foundation.zurb.com/emails">Foundation for Emails</a> removes a lot of the headache of tables since it built with <a href="https://foundation.zurb.com/emails/docs/inky.html">Inky</a>. Inky takes HTML tags like `<row>` and `<columns>` and converts them to complex tables. The less code the better! Also, their framework is responsive! Please see the examples below.

<p><strong>Inky Example</strong></p>

{% highlight html %}

<container>
  <row>
    <columns>Put content in me!</columns>
  </row>
</container>

{% endhighlight %}

<p><strong>Converts to HTML below</strong></p>
{% highlight html %}

<table align="center" class="container">
  <tbody>
    <tr>
      <td>
        <table class="row">
          <tbody>
            <tr>
              <th class="small-12 large-12 columns first last">
                <table>
                  <tr>
                    <th>Put content in me!</th>
                    <th class="expander"></th>
                  </tr>
                </table>
              </th>
            </tr>
          </tbody>
        </table>
      </td>
    </tr>
  </tbody>
</table>

{% endhighlight %}

In addition to Inky, Foundation come with Gulp, Sass, Inliner, BrowserSync and Image Compression included in the stack. The workflow and automation are simply amazing. 

To see the UNM School of Law tempate, please visit <a href="http://lawschool.unm.edu/admissions/html-email/template.html" target="_blank">UNM School of Law Admissions HTML Email</a> page.

<h2>More Foundation Email Resources</h2>

<ul>
    <li><a href="https://foundation.zurb.com/emails.html">Foundation for Emails Site</a></li>
    <li><a href="https://foundation.zurb.com/emails/zurb-stack.html">Zurb Stack</a></li>
    <li><a href="https://foundation.zurb.com/emails/docs/">Email Docs</a></li>
</ul>
    




