---
layout: "post"
title: "Meraki Post"
tenure: "2015 – present"
subtitle: "IT Architect, Book Reviewer, Podcaster (because, passion)"
sequence: 2
---

A few of us friends started a site, [Meraki Post](https://www.merakipost.com). It has been a journey to better control, performance and UX, with  [Jekyll](https://jekyllrb.com/), [GitLab CI](https://about.gitlab.com/features/gitlab-ci-cd/), [<span class='small-caps'>AWS</span> S3](https://aws.amazon.com/s3/), [CloudFront](https://aws.amazon.com/cloudfront/) and [Slack](https://slack.com/). Ask me about what I built!
<!--more-->

#### The Story

The site was initially set up on [Blogger](https://www.blogger.com/). While Blogger had a good-enough set of features that help many, we needed much more control in terms of layout, build, and user experience. WordPress was an alternative, but it came in at a cost and too less control (WordPress SaaS). Not much better than Blogger in that aspect.

A self-hosted WordPress site came in with more-than-required complexity, half the cost of SaaS, lower security and too much administrative overhead (hosting your own WordPress site requires you to be on top of every aspect of it including handling its security and regular patching).

Meraki Post is a book blog, mostly contributed to by non-tech users. Therefore, something much simpler was needed. Jekyll was the easiest, viable option. We started with setting up the layout and design for better (uncluttered) UX, and moved on to setting up its build logic. Here were the requirements:

1. Posting needed to be simple, preferably, plain text.
2. Test, preview and production sites were needed.
3. Contact form was required.
4. New posts had to go out on schedule.
5. Comments had to be supported.
6. Scheduled content had to be hidden---even in code form.
7. User privacy had to be prioritised.

We chose Ruby-based static site generator, [Jekyll](https://jekyllrb.com/), to generate our site. Setting up the site using GitHub Pages was the easiest option, available at zero additional cost. However, it would not address requirements 2 and 4. Scheduling was still possible with Travis CI, but the model failed to meet requirement 6.

BitBucket took care of 6, but there were serious limits on CI pipeline time, given the number of builds per month. Support for [Wercker](https://app.wercker.com/) was unclear at the time, since BitBucket had introduced its own <span class='small-caps'>CI/CD</span>.

#### The Solution

Here is a basic schematic of what we implemented.

1. Moved the project to [GitLab](https://www.gitlab.com/).
2. Set up [GitLab CI](https://about.gitlab.com/product/continuous-integration/) to build and deploy the project.
3. Deploy the files to the chosen [Amazon S3](https://aws.amazon.com/s3/) bucket (test/preview/production).
4. Use [<span class='small-caps'>AWS</span> CloudFront](https://aws.amazon.com/cloudfront/) as the <span class='small-caps'>CDN</span> for speed.
5. Encrypt the connection using an <span class='small-caps'>SSL</span> certificate from [<span class='small-caps'>ACM</span>](https://aws.amazon.com/certificate-manager/).
6. Implement commenting using [Disqus](https://disqus.com/).

Further, we implemented [Slack](https://slack.com/) for communication within the team. We extended its capabilities to social interactions as well, to post content to the social sites and engage with the audience (Twitter, especially). I also built custom integrations as well, to enable monitoring the site.
