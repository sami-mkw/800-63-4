<a name="fal"></a>

## 7. Federation Assurance Level (FAL)

本セクションでは利用可能な Federation Assurance Level (FAL) の一覧を定義する.
FAL はあるトランザクションで利用されている Assertion と Federation Protocol の特徴を記述するものである.
RP が当該トランザクションにおける要求レベルを明示したり, RP と IdP が当該トランザクションにおける必要レベルをあらかじめ設定しておいたりといった利用方法が想定される.

<!-- This section defines allowable Federation Assurance Levels, or FAL. The FAL describes aspects of the assertion and federation protocol used in a given transaction. These levels can be requested by an RP or required by configuration of both RP and IdP for a given transaction.  -->

FAL は [assertion protection strength](#sec5) および [assertion presentation](#sec6) を統合し, 多様な [federation model](#sec4) に適用できる, スカラーで比較可能な値としたものである.
他の様々な要素を組み合わせることも可能だが, FAL の上記3要素を用いて段階的によりセキュアな実装方法の選択肢を提示することにより, 実装ガイドラインとして分かりやすいものを作ることを意図している.
FAL のリストに無いような組み合わせも可能であるが, 本ドキュメントではそういった組み合わせは対象としない.

<!-- The FAL combines aspects of [assertion protection strength](#sec5) and [assertion presentation](#sec6) into a single, increasing scale applicable across different [federation models](#sec4). While many other combinations of factors are possible, this list is intended to provide clear implementation guidelines representing increasingly secure deployment choices. Combinations of aspects not found in the FAL table are possible but outside the scope of this document. -->

以下の表は Assertion の提示方式が Front Channel か Back Channel (= Assertion Reference を利用する) かという点に基づいて, 異なる要件をまとめている.
一連の各レベルは, そのレベル以下の要件をすべて満たすものとする.
Proxy 経由の Federation においては, Proxy された Transaction における最も低いレベルを採用すること (SHALL).

<!-- This table presents different requirements depending on whether the assertion is presented through either the front channel or the back channel (via an assertion reference). Each successive level subsumes and fulfills all requirements of lower levels. Federations presented through a proxy SHALL be represented by the lowest level used during the proxied transaction. -->

<a name="63cSec7-Table1"></a>

<div class="text-center" markdown="1">


**Tbale 7-1: Federation Assertion Levels**

</div>

|FAL|Back-channel Presentation Requirement|Front-channel Presentation Requirement|
|:--:|----|----|
|1|Bearer assertion, asymmetrically signed by IdP|Bearer assertion, asymmetrically signed by IdP|
|2|Bearer assertion, asymmetrically signed by IdP|Bearer assertion, asymmetrically signed by IdP and encrypted to RP|
|3|Bearer assertion, asymmetrically signed by IdP and encrypted to RP|Bearer assertion, asymmetrically signed by IdP and encrypted to RP|
|4|Holder of key assertion, asymmetrically signed by IdP and encrypted to RP|Holder of key assertion, asymmetrically signed by IdP and encrypted to RP|

例えば, FAL 1 は OpenID Connect Implicit Client Profile や SAML Web SSO Profile 等に相当する.
FAL 2 は OpenID Connect Basic Client Profile, SAML Artifact Binding Profile 等に相当する.
FAL 3 では, FAL 2 に加えて, OpenID Connect ID Token や SAML Assertion を当該 RP の公開鍵で暗号化することといった要件が加わる.
FAL 4 では, FAL 3 に加えて, Assertion に紐付いた鍵 (Cryptographic Authenticator 等) の提示が要求される.
FAL 4 で提示される追加の鍵は, Subscriber が IdP に対して認証する際に利用するものと同じである必要はない.

<!-- For example, FAL 1 maps to the OpenID Connect Implicit Client profile or the SAML Web SSO profile, with no additional features. FAL 2 maps to the OpenID Connect Basic Client profile or the SAML Artifact Binding profile, with no additional features. FAL 3 additionally requires that the OpenID Connect ID Token or SAML Assertion be encrypted to a public key representing the RP in question. FAL 4 requires the presentation of an additional key bound to the assertion (for example, the use of a cryptographic authenticator) along with all requirements of FAL3. Note that the additional key presented at FAL 4 need not be the same key used by the subscriber to authenticate to the IdP. -->

どんなプロトコルであれど, Federation Protocol の一部として Assertion の性質に着目すれば, RP はそれがどの FAL レベルに相当するかを簡単に特定できる.
したがって, 当該認証トランザクションで要求すべき FAL の決定や, 実際にそのトランザクションが当該 FAL に適合しているかの検証は, RP の責務である.

<!-- Regardless of what is requested or required by the protocol, the applicable FAL is easily detected by the RP by observing the nature of the assertion as it is presented as part of the federation protocol. Therefore, the RP is responsible for determining which FALs it is willing to accept for a given authentication transaction and ensuring that the transaction meets the requirements of that FAL. -->

[Table 7-2](#63cSec7-Table2) に M-04-04 Level of Assurance に厳格に準拠する場合に必要となる Federation Assurance Level のマッピングを示す.

<!-- [Table 7-2](#63cSec7-Table2) lists strict adherence to M-04-04 Level of Assurance, mapping the corresponding Federation Assurance Levels. -->

<a name="63cSec7-Table2"></a>

<div class="text-center" markdown="1">

**Table 7-2: Legacy M-04-04 FAL Requirements**

</div>

| M-04-04 Level of Assurance (LOA) |  Federation Assurance Level (FAL)
|:------------------:|:-----------------------------:
| 1 |  1
| 2 | 2
| 3 | 2
| 4 | 4

しかしながら M-04-04 Level of Assurance では [Table 7-3](#63cSec7-Table3) のようなマッピングを採用することも可能である.
各機関は算定した M-04-04 LOA に対応した適切な FAL を選択すべきである (SHALL).

<!-- However, [Table 7-3](#63cSec7-Table3) shows the expanded set of FAL's that are allowable to meet M-04-04 Level of Assurance. Agencies SHALL select the corresponding FAL based on the assessed M-04-04 LOA. -->

<a name="63cSec7-Table3"></a>

<div class="text-center" markdown="1">

**Table 7-3: Recommended M-04-04 FAL Requirements**

</div>

| M-04-04 Level of Assurance | Federation Assurance Level
|:------------------:|:-----------------------------:
| 1 | 1, 2, 3, or 4
| 2 | 2, 3, or 4
| 3 | 2, 3, or 4
| 4 | 3 or 4
