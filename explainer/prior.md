By far, the closest analogy to this work is the great work of [BrowserID](https://github.com/mozilla/id-specs/blob/prod/browserid/index.md#web-site-signin-flow) during the [Mozilla Personas](https://developer.mozilla.org/en-US/docs/Archive/Mozilla/Persona/The_navigator.id_API) effort (postmortem [here](https://wiki.mozilla.org/Identity/Persona_AAR)). In many ways, the goals that BrowserID was trying to achieve as well as the mechanisms that were created are a lot alike what’s being proposed here. There are significant differences in strategy and design, but let’s start with the similarities first because there are many.

First, BrowserID was clearly trying to solve similar problems, namely IDP Tracking and friction. The mechanisms that were created clearly had [strong builtin privacy components](https://www.youtube.com/watch?v=qHpFwdQw2wQ) to prevent IDPs from knowing about RPs and vice versa, via the chain of signatures gathered from IDPs (mainly email providers) and certificates generated by the browser.

Second, from a mechanism perspective, there was clearly a separation between an RP to Browser API as well as a Browser to IDP API.

```javascript
navigator.id.get((assertion) => {}, {
  backgroundColor: "#606B72",
  siteName: "My Example Site"
});
```

The [RP calls a browser native API](https://github.com/mozilla/id-specs/blob/prod/browserid/index.md#web-site-signin-flow) to fetch an assertion which gets mediated by the [browser in coordination with the IDP](https://github.com/mozilla/id-specs/blob/prod/browserid/index.md#identity-provisioning-flow).

```javascript
// set up UI
navigator.id.beginAuthentication(function(email) {
  // update UI to display the email address
});
```

The postmortem analysis [here](https://wiki.mozilla.org/Identity/Persona_AAR) is very insightful in understanding what were the challenges faced and gives this proposal a solid place to work from. In many ways, we think some of these insights are rooted in the observation we made earlier about backwards compatibility with RPs and user’s current behavior, which we are deliberately trying to avoid.

# Related Work

- [Building a More Private Web](https://blog.chromium.org/2020/01/building-more-private-web-path-towards.html)
- [Personas](https://wiki.mozilla.org/Identity/Persona_AAR) and [navigator.id](https://developer.mozilla.org/en-US/docs/Archive/Mozilla/Persona/The_navigator.id_API)
- [WebOTP](https://github.com/WICG/WebOTP)
- [Credential Manager](https://w3c.github.io/webappsec-credential-management/#federated)
- Add your work [here](https://github.com/samuelgoto/FedCM/issues/new)
