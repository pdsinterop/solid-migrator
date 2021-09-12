# Solid Migrator: Linkrot Mitigation: Memento

[Memento](http://mementoweb.org/) wants to make it as straightforward to access the Web of the past as it is to access the current Web. It does this by making accessing archives of web content seamless. It [specifies its own protocol](hhttps://tools.ietf.org/rfc/rfc7089.txt) to access these archives and there is a plugin for Google Chrome and Mozilla Firefox that will make this a seamless experience. There are also a number of third party apps.

It also provides a website, https://timetravel.mementoweb.org/, which combines multiple archives together.

Pro's

- Multiple implementations and multiple archive providers make it a much more robust solution than other archiving options
- There is an actual RFC there, which [seems to be supported by the W3C](https://blog.dshr.org/2016/09/memento-at-w3c.html)

Con's

- Memento doesn't specify a way to make a new archive copy of a page. This is upto the supporting archives themselves. Although there is an apache plugin called siteStory that allows you to archive content from apache, which can be accessed using Memento. You will need to be the owner/administrator of that apache server though.
