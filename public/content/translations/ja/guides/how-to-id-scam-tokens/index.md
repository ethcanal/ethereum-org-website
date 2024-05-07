---
title: 詐欺トークンの見分け方
description: 詐欺トークンの概要、正当なトークンに見せかける仕組み、詐欺に遭わない方法について理解を深める。
lang: ja
---

# 詐欺トークンの見分け方 {#identify-scam-tokens}

イーサリアムの最も一般的な用途の1つは、グループが取引可能なトークン、いわば独自の通貨を作ることです。 こうしたトークンは通常、[ERC-20規格](/developers/docs/standards/tokens/erc-20/)に従ったものです。 価値をもたらす正当なユースケースを提供するトークンがある一方、その価値をトークン発行元が独占するようなトークンも存在します。

こうしたトークンの発行元は、以下のような方法であなたを騙します。

- **詐欺トークンの販売** 正当なトークンを装っており購入意欲をかきたてますが、詐欺師により発行されている無価値のトークンです。
- **悪意のあるトランザクションへの署名** 通常、独自のユーザーインターフェースに誘導された後に署名を求められます。 トークンの発行元は、ERC-20トークンの配布の際にコントラクトアドレスへのアクセスを求め、機密情報を開示させる場合があります。これにより、トークンの発行元がお持ちの資産にアクセスできるようになります。 正当なサイトと瓜二つに見えるこうしたユーザーインターフェースには、隠された罠が存在します。

詐欺トークンの概要および特定方法を理解するために、1つの例を見ていきましょう：[`wARBの例`](https://etherscan.io/token/0xb047c8032b99841713b8e3872f06cf32beb27b82)。 同トークンは一見、正当な[`ARB`](https://etherscan.io/address/0xb50721bcf8d664c30412cfbc6cf7a15145234ad1)トークンと似ています。

<ExpandableCard
title="ARBとは"
contentPreview=''>

Arbitrumは、<a href="/developers/docs/scaling/optimistic-rollups/">オプティミスティック・ロールアップ</a>の開発および管理を行う組織です。 当初、営利企業として立ち上げられたArbitrumは、その後、分散型組織に切り替わりました。 同プロセスにおいて、Arbitrumは、取引可能な<a href="/dao/#token-based-membership">ガバナンストークン</a>を発行しました。

</ExpandableCard>

<ExpandableCard
title="詐欺トークンがwARBという名前である理由"
contentPreview=''>

イーサリアムでは、暗号資産がERC-20に準拠していない場合、「w」から始まる「ラップ」版の暗号資産を作成する慣習があります。 例として、ビットコインに対するwBTCや<a href="https://cointelegraph.com/news/what-is-wrapped-ethereum-weth-and-how-does-it-work">イーサリアムに対するwETH</a>があります。

すでにイーサリアム上に存在するERC-20トークンのラップ版を作成するのは無意味なことですが、詐欺師は実際の意味よりも、トークンがいかにもっともらしく見えるかということを重視しています。

</ExpandableCard>

## 詐欺トークンの仕組み {#how-do-scam-tokens-work}

イーサリアムの本質は分散にあります。 これは、保有資産を差し押さえたり、スマートコントラクトのデプロイを阻止したりする中央集権型組織が存在しないことを意味します。 しかしこれは、詐欺師があらゆる種類のスマートコントラクトをデプロイできてしまうことも意味するのです。

<ExpandableCard
title="スマートコントラクトとは"
contentPreview=''>

<a href="/developers/docs/smart-contracts/">スマートコントラクト</a>とは、イーサリアムブロックチェーン上で実行可能なプログラムです。 例えば、すべてのERC-20トークンは、スマートコントラクトとして実装できます。

</ExpandableCard>

具体的に、Arbitrumでは`ARB`というシンボルを用いてスマートコントラクトをデプロイします。 しかしこの方法は、他者による、同じシンボルまたは類似のシンボルを用いたスマートコントラクトのデプロイを防ぐわけではありません。 コントラクトの記述者は誰でも、その内容を設定することができます。

## 正当に見せかける方法 {#appearing-legitimate}

詐欺トークンの作成者が、それを正当なものに見せかける方法がいくつかあります。

- **正当な名前およびシンボル**。 前述の通り、ERC-20コントラクトは、他のERC-20コントラクトと同じシンボルおよび名前を保有しています。 こうした内容を信用して、安全性を判断することはできません。

- **正当なトークンの保有者。** 詐欺トークンの発行者は、正当なトークンの保有者と思われるアドレスに対し、多額の詐欺トークンをエアドロップする場合が多くあります。

  `wARB`の例を再び見てみましょう。 [同トークンの約16％](https://etherscan.io/token/0xb047c8032b99841713b8e3872f06cf32beb27b82?a=0x1c8db745abe3c8162119b9ef2c13864cd1fdd72f)が、パブリックタグ[Arbitrum Foundation: Deployer](https://etherscan.io/address/0x1c8db745abe3c8162119b9ef2c13864cd1fdd72f)により保有されています。 これは、_偽のアドレス_ではなく、[イーサリアムメインネット上に正当なARBコントラクトをデプロイしたアドレスです](https://etherscan.io/tx/0x242b50ab4fe9896cb0439cfe6e2321d23feede7eeceb31aa2dbb46fc06ed2670)。

  ERC-20コントラクトストレージの一部にアドレスのERC-20残高が存在するため、コントラクト開発者が希望するものをコントラクトにより指定することができます。 また、正当なユーザーがこうした詐欺トークンを排除できないように、コントラクトにより送金を禁止することもできます。

- **正当な送金。** _正当なトークンの保有者は、詐欺トークンを他者に送金する際に支払いを行うことはありません。つまり、送金が行われたということは正当なトークンであるということです。この考えは_**間違っています**。 `送金`イベントは、ERC-20コントラクトにより作成されます。 詐欺師は、こうしたイベントを作成するようなコントラクトを簡単に記述できてしまいます。

## 詐欺的なウェブサイト {#websites}

詐欺師は、信憑性の高いウェブサイトも作成します。正当なウェブサイトと同一のUIが用いられており、瓜二つに見えますが、すぐには判別できない罠が存在します。 また、正当に見える外部リンクが、実際は、ユーザーを外部の詐欺サイトに誘導するリンクであったという例や、ユーザーに対し、秘密鍵または資金の攻撃者への送付を誘導するような誤った指示がなされたという例も存在します。

詐欺を避ける最善の方法は、訪問するサイトのURLを入念に確認し、正しいサイトのアドレスをブックマークに保存することです。 こうすれば、スペルミスの心配や外部リンクに頼る必要なく、ブックマーク経由で正しいサイトにアクセスできます。

## 詐欺から自分を守る方法 {#protect-yourself}

1. **コントラクトアドレスを確認する。** 正当な組織の正当なトークンであることを確認し、同組織のウェブサイト上でコントラクトアドレスを確認します。 例えば、`ARB`の場合、[こちら](https://docs.arbitrum.foundation/deployment-addresses#token)で正しいアドレスを確認できます。

2. **正当なトークンは流動性を持つ。** 他には、最も利用者の多いトークンスワッププロトコルの1つである[Uniswap](https://uniswap.org/)で、流動性プールの大きさを確認する方法があります。 同プロトコルは流動性プール（投資家が取引手数料からの利回りを期待して保有トークンを預ける仕組み）により機能します。

詐欺師は本物の資産を危険にさらすことを避けるため、一般的に、詐欺トークンの流動性プールが存在しても、小規模なことがほとんどです。 例えば、`ARB`/`ETH`の場合、Uniswapの流動性プールの規模は約100万ドル (最新の数字は[こちら](https://info.uniswap.org/#/pools/0x755e5a186f0469583bd2e80d1216e02ab88ec6ca)を参照) であり、少量の購入や売却で価格が変化することはありません。

![正当なトークンの購入](./uniswap-real.png)

一方、詐欺トークンである`wARB`の購入を試みる場合、少量の購入でも価格が90%以上変動するでしょう。

![詐欺トークンの購入](./uniswap-scam.png)

`wARB`が正当なトークンではないことを示す別の証拠も確認できます。

3. **Etherscanで検索する。** 詐欺トークンの多くは、すでにコミュニティにより特定および報告されています。 こうしたトークンは、[Etherscan](https://info.etherscan.com/etherscan-token-reputation/)においてマークされています。 (分散型ネットワークの性質により、正当性を証明できる正式な情報源が存在しないため) Etherscanは正式な情報源ではありませんが、Etherscanにより詐欺トークンと特定されている場合、詐欺トークンである可能性が高いと言えます。

   ![Etherscan上の詐欺トークン](./etherscan-scam.png)

## まとめ {#conclusion}

世界に価値を持つものがある限り、それを横取りしようとする詐欺師の存在があります。また、分散型の世界では、自分自身以外に自分を守れる人は存在しません。 詐欺トークンを見分けるために、以下の内容を心に留めておいていただけると幸いです。

- 詐欺トークンは、正当なトークンと同一の名前やシンボルなどを用いて正当なトークンを装う場合があります。
- 詐欺トークンは正当なトークンと同一のコントラクトアドレスを_使用することはできません。_
- 正当なトークンのアドレスの最も信頼できる情報源は、同トークンが属する組織のものです。
- または、[Uniswap](https://app.uniswap.org/#/swap)や[Etherscan](https://etherscan.io/)などの信頼性の高いアプリケーションを用いて確認してください。