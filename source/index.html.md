---
title: TokenAnalyst Docs

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href="https://sid296635.typeform.com/to/abg0kL" target="_blank">Get your API key</a>

includes:
  - dateandtime
  - bitcoinfundamentalsv2
  - ethereumfundamentalsv2
  - erc20tokenstatsv2
  - stablecoinstatsv2
  - binancestats
  - bitcoinexchangeflowsv2.md
  - ethereumexchangeflows
  - stablecoinexchangeflows
  - erc20exchangeflows
  - minerflows
  - price

search: true
---

<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=UA-113322596-8"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'UA-113322596-8');
</script>

# Introduction

Welcome to the TokenAnalyst API. We provide simple and powerful endpoints, which you can use to get information on basic transaction data and aggregate on-chain statistics derived directly from the blockchain. This API reference provides information on available endpoints and how to interact with them.

# Authentication

TokenAnalyst uses API keys to allow access to the API. To obtain your API key contact us <a href="https://sid296635.typeform.com/to/abg0kL" target="_blank">here</a>
.

TokenAnalyst expects for the API key to be included in all API requests to the server. You can simply include the key in the URL parameters like:

`key=API_KEY`

<aside class="notice">
You must replace <code>API_KEY</code> with your personal API key.
</aside>
