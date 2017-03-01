# Github API Note

本文是对 [Github 开发者指南][github developer guides] 中重要信息的归纳总结，完整版请阅读原文。

1. api 支持多种语言 [Api Libraries][api libraries]。
1. 前期熟悉 api 的时候可以使用 `cURL`。
1. `cURL` -i 参数显示 http header 信息。
1. `X-RateLimit-Limit` 和 `X-RateLimit-Remaining`  自定义头部信息代表了你还能在一定时间内发起多少次请求，`X-RateLimit-Reset` 表示下次计数重置的时间，是 `UTC` 时间，以秒为单位。
1. 未认证的客户端一小时最多请求 60 次，认证后可以请求 5000 次。
1. 304 的请求不会减少访问次数。
1. 可以使用 [`/rate_limit`][rate limit] 单独查询次数限制而不会影响次数。另外 [`搜索 API`][search api] 有一个单独的次数限制，次数很少，未认证为 10 次/分钟，认证后为 30 次/分钟。
1. 搜索 api 包含 [`高亮搜索结果功能`][text match]。
1. 认证后才能读写私有信息。
1. 某些请求如果没有权限，可能会返回 404，为了保护用户隐私。
1. 一共有[三种认证][3 authorizations]方式：
    + Basic 认证
    + OAuth2 Token in header
    + OAuth2 Token in url as a parameter
1. 2FA 认证提高安全性，但如果手机丢失，则无法访问账户。这里有一个[恢复账户的后背方法][fallback method to recover accounts]。使用 2FA 前请详细阅读。这里有一篇[丢失 2FA 的经验之谈][lost 2FA]。
1. 非 web 应用可以程序化获取 OAuth2 Token
1. [Media Type][media type] 可以指定请求资源类型，是所有请求的基础。默认可以不带上。
1. 请求指定[数据分页][pagination]。
1. 请求需携带 UA 信息。
1. 支持[条件请求][conditional request]、[JSONP][jsonp]、[跨域][cors]。


## 常用 API

1. profile: https://api.github.com/users/:username
1. search repositories: https://api.github.com/search/repositories
    + q: query keywords
    + sort: stars、fork、updated
    + order: asc、desc(default)
    + 参数于 search repositories 相同，但 q 略有不同。
1. search issues: https://api.github.com/search/issues
    + 参数于 search repositories 相同，但 q 略有不同。
1. search users: https://api.github.com/search/users
    + 参数于 search repositories 相同，但 q 略有不同。
1. more search api: [https://developer.github.com/v3/search/][search api]
1. get repos: https://api/github.com/repos/:owner/:repo
1. list user repos: https://api.github.com/users/:username/repos
    + type=owner
1. list org repos: https://api.github.com/orgs/:orgname/repos
    + type=owner
1. more about repos: [https://developer.github.com/v3/repos/][repos api]
1. list user repo issues: https://api.github.com/repos/:owner/:repo/issues
1. get contents: https://api.github.com/repos/:owner/:repo/contents/:path
1. more about get contents: [https://developer.github.com/v3/repos/contents/][contents api]


<!-- links -->
[github developer guides]: https://developer.github.com/guides/getting-started/
[api libraries]: https://developer.github.com/libraries/
[3 authorizations]: https://developer.github.com/v3/#authentication
[rate limit]: https://developer.github.com/v3/rate_limit/
[search api]: https://developer.github.com/v3/search/
[text match]: https://developer.github.com/v3/search/#text-match-metadata
[fallback method to recover accounts]: https://help.github.com/articles/adding-a-fallback-authentication-method-with-recover-accounts-elsewhere/
[lost 2FA]: http://www.tuicool.com/articles/RfY36nE
[media type]: https://developer.github.com/v3/media/
[pagination]: https://developer.github.com/v3/#pagination
[conditional requests]: https://developer.github.com/v3/#conditional-requests
[jsonp]: https://developer.github.com/v3/#json-p-callbacks
[cors]: https://developer.github.com/v3/#cross-origin-resource-sharing
[search api]: https://developer.github.com/v3/search/
[repos api]: https://developer.github.com/v3/repos/
[contents api]: https://developer.github.com/v3/repos/contents/
