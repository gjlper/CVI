+++
title = "Easy Privacy Policies And Optimizations"
date = "2017-09-28T10:26:15-07:00"
hide_authorbox = false
disable_comments = false
categories = ["Announcements"]
tags = ["releases", "bug fixes", "features", "iubenda", "fonts"]
aliases = ["/post/easy-privacy-policy-optimizations/"]
+++

# Iubenda: Easy Privacy Policies

BluestNight now comes with support for privacy policies generated by [Iubenda](http://iubenda.refr.cc/FMFBN89) (referral link). Iubenda is a simple solution for owners of websites that require a privacy policy (i.e. collect any sort of data from their users). Policies are assembled by choosing data-collecting services from a large list, customizing them as necessary, and clicking "Save."

{{< figure src="/images/post/iubenda-service-list.png" caption="The service selection dialog of Iubenda." >}}

## Free Accounts

Free accounts are limited to a single privacy policy and may only include the policy on the site in the form of a button that opens a dialog box on the page. Inside the dialog box is an `<iframe>` displaying the privacy policy.

{{< figure src="/images/post/iubenda-bluestnight-privacy-policy.png" caption="The default privacy policy available to free Iubenda accounts (BluestNight website)." >}}

## Paid Accounts

Paid pro accounts have some more options available to them, including removing Iubenda branding from the policy button and accessing the policy from a JSON API endpoint. This means that pro users with Hugo can access the text of their privacy policy using Hugo's `getJSON` template function and have it appear directly on a page - this is how BluestNight's [privacy policy]({{< ref "privacy-policy.md" >}}) page is put together, using the new `{{</* iubenda */>}}` [shortcode]({{< ref "docs/site/policies.md#iubenda-shortcode" >}}). Just make an empty page at `content/privacy-policy.md` (see the [previous announcement](https://shadow53.com/post/concurrency-and-polish/#website-policies)) and include that shortcode. The shortcode will use the [Iubenda information]({{< ref "docs/site/policies.md#iubenda-integration" >}}) from your configuration file and fill the page with the policy text.

Iubenda also includes cookie consent banner support for paid accounts. BluestNight currently provides basic theme integration for the banner and some of its options, with untested support for requiring prior consent before loading scripts that set cookies.

# New Typewriter Font

As part of trying to provide useful fonts in different styles, BluestNight now comes with a typewriter font, called Secret Typewriter.

There have been some questions asked in the [Hugo Forums](https://discourse.gohugo.io/t/bluestnight-theme-thoughts/7973) and in [BluestNight issues](https://gitlab.com/BluestNight/BluestNight/issues/73) regarding why I include font files and don't just enable people to specify some Google Fonts URL for the font they want to use. The main reason is one of independence: I don't think a website should be pulling resources from third parties whenever possible. Third parties are not under your own control and may shut down, go down, or otherwise become temporarily or permanently unaccessible, leaving your website crippled.

Fonts are especially important in this, since the use of a different font changes the look and even the feel of the website. Even falling back to the system default sans-serif font can cause the site to look unsettlingly *different*, though the change itself seems minor. So, I've decided that fonts for the website using BluestNight should be downloaded from the same server as the page itself.

That said, I do want to provide some creative ability in the use of different kinds of fonts, hence the inclusion of multiple [handwriting fonts]({{< ref "docs/shortcodes/custom-fonts.md#handwriting-fonts" >}}) and the new inclusion of the [typewriter font]({{< ref "docs/shortcodes/custom-fonts.md#typewriter-font" >}}). Click the previous link to see a preview of the typewriter font in use.

# Optimizations

A number of optimizations have been applied to BluestNight as well, including the use of [cached partials](https://gohugo.io/functions/partialcached/) to greatly descrease site build times and the use of [preloading](https://developer.mozilla.org/en-US/docs/Web/HTML/Preloading_content) in the generated pages to load resources quicker.

# All Changes

- BluestNight website moved to a [new repo](https://gitlab.com/BluestNight/website/)
- [[045d6cbb]](https://gitlab.com/BluestNight/BluestNight/commit/045d6cbb37898567f8e657c8b68562d706ccab47) Pull `static` functionality into a partial and add support for links with `#` ids
- [[3c052b6b]](https://gitlab.com/BluestNight/BluestNight/commit/3c052b6b6c59f620a2b53e13efe5f060628ee0b5) Fix transparency issue in Chromium browsers
- [[982fe603]](https://gitlab.com/BluestNight/BluestNight/commit/982fe603ad73315706cd04380e61ada95b8024f4) Added Iubenda support
- [[3a1ce6e0]](https://gitlab.com/BluestNight/BluestNight/commit/3a1ce6e0fa0ed2be837b3c90fa44cd0d0ec62c17) Added Iubenda **Pro** support
- [[75b48e20]](https://gitlab.com/BluestNight/BluestNight/commit/75b48e20689f96503ff5a08756b1df6195c4d516) Increase page `max-width`
- [[98350e0c]](https://gitlab.com/BluestNight/BluestNight/commit/98350e0cc3be689fa0137b911d33d38d91337b14) Fix nested ordered lists not being indented
- [[346e847b]](https://gitlab.com/BluestNight/BluestNight/commit/346e847ba0ac0f8f39ad9e7178fe77b21a85cd06) Improve site compilation by caching certain partials
- [[984a0e0f]](https://gitlab.com/BluestNight/BluestNight/commit/984a0e0f7f7e72d1089f96103a9050f866b9c98f) Switch to CDNJS for hosting of *minified* Lunr.js and leverage browser preloading for scripts and stylesheets
- [[a6d9d11c]](https://gitlab.com/BluestNight/BluestNight/commit/a6d9d11ca4d807dec3022f4f0c952acc1d50fbf5) Add new typewriter font with shortcode and simplify font shortcodes
- [[8ca7f80a]](https://gitlab.com/BluestNight/BluestNight/commit/8ca7f80ab6b86d3e2d8f1d7365fd8ddc52bebd68) Preload images from articles
- [[768c850e]](https://gitlab.com/BluestNight/BluestNight/commit/768c850e11cfd850088fa2eb66a386ec49c92432) Prevent images from being broken across printed pages (Firefox not compatible)
- [[0503da0d]](https://gitlab.com/BluestNight/BluestNight/commit/0503da0dd2f3253fbfc8e1d320aafcf2ba268296) Improve Iubenda integration for free accounts by making the Terms of Use footer link look like the Iubenda button
- [[e5d4c2e8]](https://gitlab.com/BluestNight/BluestNight/commit/e5d4c2e8c4502e809dc5fccb4d9a59c8e37608b3) Remove excess whitespace on some generated pages
- [[50b487e3]](https://gitlab.com/BluestNight/BluestNight/commit/50b487e37099654e2146abe16a2d54b78fef3431) Add Iubenda prior consent support for the cookie banner