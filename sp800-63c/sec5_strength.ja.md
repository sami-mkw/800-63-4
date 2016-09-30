<a name="sec5"></a>

## 5. Assertions

Assertion とは, Authenticated Subscriber に関する一連の Claim および Statement を含んだものである.
Assertion はその利用方法の特徴や保護方法などの複数の軸でカテゴライズされる.

<!-- An assertion contains a set of claims or statements about an authenticated subscriber. Assertions can be categorized along multiple orthogonal dimensions, including the characteristics of using the assertion or the protections on the assertion itself. -->

Assertion に含まれるコアとなるべき (SHOULD) Claim は以下の通りである (が, これに限らない):

<!-- The core set of claims inside an assertion SHOULD include (but is not limited to): -->

- Issuer: Assertion 発行主体 (IdP) の識別子.
- Subject: 当該 Assertion が指し示す主体 (Subscriber) の識別子, 通常は Issuer (IdP) の管理する Namespace 内で有効である.
- Audience: Assertion を受け取る主体 (RP) の識別子.
- Issuance: Assertion が IdP に発行された日時を示すタイムスタンプ.
- Expiration: Assertion の有効期限を示すタイムスタンプ. 有効期限が切れたものは RP に valid な Assertion として受け入れられるべきでない (SHALL). (注: RP におけるセッション有効期限とは異なる)
- Authentication Time: IdP が Primary Authentication Event を通じて Subscriber を認証した日時を示すタイムスタンプ.
- Identifier: 当該 Assertion 自身を識別するランダムでユニークな値. 攻撃者が不正な Assertion を生成して validity check をパスするのを防ぐ目的で利用される.

<!--
 - Issuer: an identifier for the party that issued the assertion (the IdP)
 - Subject: an identifier for the party that the assertion is about (the subscriber), usually within the namespace control of the issuer (the IdP)
 - Audience: an identifier for the party intended to consume the assertion (the RP)
 - Issuance: a timestamp indicating when the assertion was issued by the IdP
 - Expiration: a timestamp indicating when the assertion expires and SHALL no longer be accepted as valid by the RP (note that this is not the expiration of the session at the RP)
 - Authentication Time: a timestamp indicating when the IdP last verified the presence of the subscriber at the IdP through a primary authentication event
 - Identifier: a random value uniquely identifying this assertion, used to prevent attackers from manufacturing malicious assertions which would pass other validity checks
-->

これらのコアとなる Claim の中でも, 特に Issuance と Expiration Claim は, その Assertion が指し示す Authentication Event 自体に関連し, Subscriber に紐付いたその他の付加的な Identity Attributre には関連しない.
Subscriber Attribute は, Assertion 自体の Expiration や Invalidation とは独立して Expire したり Invalidate されたりしうる (MAY).

<!-- These core claims, particularly the issuance and expiration claims, apply to the assertion about the authentication event itself, and not to any additional identity attributes associated with the subscriber, even when those claims are included within the assertion. A subscriber's attributes MAY expire or be otherwise invalidated independently of the expiration or invalidation of the assertion. -->

Assertion は上記以外の Identity Attributes を含んでもよい (MAY).
Attribute を Assertion に含める場合の Privacy 要件については Sec.6 を参照のこと.
RP は, その他の Identity Attributes を, Assertion と同時に発行された Authorization Credential を用いて別 Trancation で IdP から取得できる (MAY).

<!-- Assertions MAY include other additional identity attributes. See sec. 6 for privacy requirements on presenting attributes in assertions. The RP MAY fetch additional identity attributes from the IdP in a separate transaction using an authorization credential issued along side the assertion. -->

詳細は Federation Protocol ごとに異なるが, Assertion は RP での個々のログインイベントのみを表現するべきである (SHOULD).
ひとたび RP が Assertion を受け取って処理を完了すれば, その後は [session management](sp800-63b.ja.html#sec7) の段階に移り, 当該 Assertion を直接利用することはない.
Assertion の有効期限は RP におけるセッション有効期限を示すべきではない (SHALL NOT).

<!-- Although details vary based on the exact federation protocol in use, an assertion SHOULD be used only to represent a single log-in event at the RP. After the RP consumes the assertion, [session management](sp800-63b.html#sec7) at the RP comes into play and the assertion is no longer used directly. The expiration of the assertion SHALL NOT represent the expiration of the session at the RP. -->

### 5.1. Assertion possession category

Assertion は, Assertion を所有している主体が Assertion の Subject となるか, Assertion とは別に Subject であることを示す証拠が必要かという, 所有者の表現方法で分類できる.

<!-- An assertion can be classified based on whether possession of the assertion itself is sufficient for representing  the subject of the assertion, or if additional proof is necessary along side the assertion. -->

#### 5.1.1. Holder-of-Key Assertions

Holder-of-Key Assertion は, Subscriber の持つ共通鍵ないしは (秘密鍵とペアとなる) 公開鍵の参照を含む.
RP は, 自身のポリシーに従って, いつ Subscriber に対して当該鍵を所有している証拠を示すべきかを決定することができる.
しかしながら, RP は Assertion を Holder-of-Key Assertion として受けとる場合, Subscriber に Assertion が参照する鍵の所有を示すよう要求すべきである (SHALL).
ユーザーが鍵の所有を示さずに鍵の参照を含む Assertion を提示する場合, 当該 Assertion は Bearer Assertion (5.1.2) として扱われる.

<!-- A holder-of-key assertion contains a reference to a symmetric key or a public key (corresponding to a private key) possessed by and representing the subscriber. An RP MAY decide when to require the subscriber to prove possession of the key, depending on the policy of the RP. However, the RP SHALL require the subscriber to prove possession of the key that is referenced in the assertion in parallel with presentation of the assertion itself in order for the assertion to be considered holder-of-key. Otherwise, an assertion containing reference to a key which the user has not proved possession of will be considered a bearer assertion (5.1.2). -->

Holder-of-Key Assertion 参照される鍵は, Client ではなく Subscriber を示す.
この鍵は Subscriber が IdP に対して認証を行う際に利用される鍵とは別のものでも良い (MAY).

<!-- The key referenced in a holder-of-key represents the subscriber, not the client. This key MAY be distinct from any key used by the subscriber to authenticate to the IdP. -->

Subscriber が鍵を所有している証拠を提示できれば, Subscriber は当該 Assertion の正式な Subject であることをある程度の確からしさを持って証明できる.
攻撃者が Subscriber あてに発行された Holder-of-Key Assertion を盗んだとしても, 攻撃者は Subscriber の鍵も同時に盗まなければならず, 盗んだ Assertion を利用するのは困難となる.

<!-- In proving possession of the subscriber’s secret, the subscriber also proves with a certain degree of assurance that they are the rightful subject of the assertion. It is more difficult for an attacker to use a stolen holder-of-key assertion issued to a subscriber, since the attacker would need to steal the referenced key material as well. -->

鍵の参照は Assertion の Issuer がその他の Claim 同様に Assert するものであるから, その参照もまた当該 Assertion に含まれる他の Claim と同じレベルの信頼度を持った情報として扱うべきである (SHALL).

<!-- Note that the reference to the key material in question is asserted by the issuer of the assertion as are any other claims therein, and reference to a given key SHALL be trusted at the same level as all other claims within the assertion itself. -->

Assertion は Holder-of-Key を表現するために利用する Private / Symmetric Key を暗号化せずに含むべきでない (SHALL NOT).

<!-- The assertion SHALL NOT include an unencrypted private or symmetric key to be used with holder-of-key presentation. -->

#### 5.1.2. Bearer Assertions

Bearer Assertion は, Bearer (持参人) 自身が誰であれ, Bearer 自身の Identity の証拠としてその Assertion を提示することができる.
その他の鍵などへのリファレンスは不要である.
もし攻撃者が Subscriber を示す正規の Assertion をキャプチャまたは生成できてしまえば, 攻撃者はその Assertion を RP に提示するだけで Subscriber になりすますことができる.

<!-- A bearer assertion can be presented by any party as proof of the bearer's identity, without reference to external materials. If an attacker is able to capture or manufacture a valid assertion representing a subscriber, and that attacker is able to successfully present that assertion to the RP, then the attacker will be able to impersonate the subscriber at that RP. -->

ただし Bearer Assertion を取得することだけが Subscriber になりすます条件であることは稀であり, 後述の Indirect Federation Model (Section 6.1) のように, 実際には Assertion に RP の識別情報を含んだり Assertion Injection を防いだりといった, RP への不正なアクセスを防ぐ追加の防御策が施されているものである (MAY)

<!-- Note that mere possession of a bearer assertion is not always enough to impersonate a subscriber. For example, if an assertion is presented in the indirect federation model (Section 6.1), additional controls MAY be placed on the transaction (such as identification of the RP and assertion injection protections) that help to further protect the RP from fraudulent activity. -->

### 5.2. Assertion protection category

上記の Assertion の所有方式や Section 4 で触れた Assertion 取得に用いる Federation Model とは別に, Assertion は偽造や他 RP に対する再利用を防ぐ何らかの保護策を内包する必要がある.

<!-- Regardless of the possession mechanism (discussed above) or the federation model used to obtain them (described in section 4), assertions need to include an appropriate set of protections to the assertion data itself to prevent attackers from manufacturing valid assertions or re-using captured assertions at disparate RPs. -->

#### 5.2.1. Assertion Identifier

Assertion は偽造防止の目的で十分なエントロピーを持つべきである (SHALL).
同様に nonce, timestamp, assertion identifier, それらの組み合わせやその他のテクニックを使ってもこの目的を達成できる (MAY).

<!-- Assertions SHALL contain sufficient entropy to prevent an attacker from manufacturing a valid assertion and using it with a target RP. Assertions MAY accomplish this by use of an embedded nonce, timestamp, assertion identifier, or a combination of these or other techniques.  -->

その他の暗号論的保護策がない場合, こういったランダム性を IdP と RP の間で Assertion をユニークに識別するための共有鍵として扱うべきであろう (SHALL).

<!-- In the absence of additional cryptographic protections, this source of randomness SHALL function as a shared secret between the IdP and the RP to uniquely identify the assertion in question. -->

#### 5.2.2. Signed Assertion

IdP は Assertion に暗号論的に署名することもできる (MAY).
RP は IdP の鍵を用いて各 Assertion の署名を検証すべきである (SHALL).
この署名は, Issuer, Audience, Subject, Expiration, その他の各種識別子等, Assertion に含まれる重要なフィールド全体に対してなされるべきである (SHALL).

<!-- Assertions MAY be cryptographically signed by the IdP, and the RP SHALL validate the signature of each such assertion based on the IdP's key. This signature SHALL cover all vital fields of the assertion, including its issuer, audience, subject, expiration, and any unique identifiers. -->

IdP が公開鍵を公開する鍵ペアによって署名を行うこともでき (MAY), その場合 RP は公開鍵を (IdP がホストする HTTPS URL などから) 動的かつセキュアに取得することができる (MAY).
鍵は (RP の設定段階において) out-of-band で RP に提供されてもよい (MAY).

<!-- The signature MAY be asymmetric based on the published public key of the IdP. In such cases, the RP MAY fetch this public key in a secure fashion at runtime (such as through an HTTPS URL hosted by the IdP), or the key MAY be provisioned out of band at the RP (during configuration of the RP). -->

IdP と RP の間で何らかの方法で共有された共通鍵による署名を用いることもできる (MAY).
その場合 IdP は RP ごとに異なる鍵を用いるべきである (SHALL).

<!-- The signature MAY be symmetric based on a key shared out of band between the IdP and the RP. In such circumstances, the IdP SHALL use a different shared key for each RP. -->

署名には Approved Signing Method のいずれかを利用すべきである (SHALL).

<!-- All signatures SHALL use approved signing methods. -->

#### 5.2.3. Encrypted Assertion

意図された Audience のみが復号できる形で Assertion を暗号化することもできる (MAY).
IdP は RP の公開鍵で Assertion を暗号化すべきである (SHALL).
その場合 IdP は RP の公開鍵を (RP がホストする HTTPS URL などから) 動的かつセキュアに取得することができる (MAY).
鍵はそれ以外の何らかの方法で (RP の登録時などに) IdP に提供されてもよい (MAY).

<!-- Assertions MAY be encrypted in such a fashion as to allow only the intended audience to decrypt the claims therein. The IdP SHALL encrypt the payload of the assertion using the RP's public key. The IdP MAY fetch this public key in a secure fashion at runtime (such as through an HTTPS URL hosted by the RP), or the key MAY be provisioned out of band at the IdP (during registration of the RP). -->

暗号化には Approved Encryption Method のいずれかを利用すべきである (SHALL).

<!-- All encrypted objects SHALL use approved encryption methods. -->

#### 5.2.4. Audience Restriction

すべての Assertion は Audience Restriction を施し, RP が当該 Assertion の発行先が自分自身であるかどうかを検知できるようにすべきである (SHOULD).
Audience が含まれている場合, RP は Assertion の Audience をチェックし, ある RP に対して発行された Assertion がその他の RP に対して利用されることを防止しべきである (SHALL).

<!-- All assertions SHOULD use audience restriction techniques to allow an RP to recognize whether or not it is the intended target of an issued assertion. All RPs SHALL check the audience of an assertion, if provided, to prevent the injection and replay of an assertion generated for one RP at another RP. -->

#### 5.2.5. Pairwise Pseudonymous Identifiers

ある条件下では, IdP 上の Subscriber のアカウントが共通の識別子を通じて複数の RP 間でリンクされることを防ぎたい場合もある.
そのような場合, IdP は RP に対して Pairwise Pseudonymous Subject Identifier を含んだ Assertion を発行するべきであり (SHALL), IdP は各 RP ごとに異なる識別子を生成するべきである (SHALL).
(詳細は [Pairwise Pseudonymous Identifier Generation](#ppi-gen) を参照のこと)

<!-- In some circumstances, it is desirable to prevent the subscriber's account at the IdP from being linked through one or more RPs through use of a common identifier. In these circumstances, pairwise pseudonymous subject identifiers SHALL be used within the assertions generated by the IdP for the RP, and the IdP SHALL generate a different identifier for each RP. (See [Pairwise Pseudonymous Identifier Generation](#ppi-gen) for more information.) -->

RP ごとに固有の Pseudonymous Identifier を用いたとしても, 複数の RP が結託し Subscriber に関するその他の属性を通じて名寄せを行う可能性はある.
例えば2つの独立した RP が同じ Subscriber を異なる Pseudonymous Identifier によって識別したとしても, 両 RP がそれぞれ Pseudonymous Identifier と同時に得た氏名, Email アドレス, 住所, その他の識別可能な属性によって, 当該 Subscriber を同一人物と特定することもできる.
Privacy Policy でこのような名寄せを禁止する場合においても, Pseudonymous Identifier は属性の名寄せに必要な作業を増加させるため, ポリシー運用を効率的にする.

<!-- When unique pseudonymous identifiers are used with RPs along side of identity attribute bundles, it may still be possible for multiple colluding RPs to fully identify and correlate a subscriber across systems using these attributes. For example, given that two independent RPs will each see the same subscriber identified with a different pairwise pseudonymous identifier, the RPs could still determine that the subscriber is the same person by comparing their name, email address, physical address, or other identifying attributes carried alongside the pairwise pseudonymous identifier. Privacy policies may prohibit such correlation, but pairwise pseudonymous identifiers can increase effectiveness of these policies by increasing the administrative effort in managing the attribute correlation.  -->

Proxied Federation Model では, 末端の IdP は末端の RP に対して Pairwise Pseudonymous Identifier の生成を行えないこともある.
この Proxy は Subscriber がどの RP にアクセスしているかを IdP に知らせないこともありうるからである.
このようなケースでは, Pairwise Pseudonymous Identifier は IdP と Federation Proxy の間で生成される.
IdP として動作する Proxy は, 自身が Downstream の RP に対して Pairwise Pseudonymous Identifier を提供することもある.
プロトコルによっては, Federation Proxy は Pairwise Pseudonymous Identifier を Upstream IdP が発行した Identifier に紐付ける必要がある場合もある.
そのような場合, 当該 Proxy は同一 Subscriber に紐づく複数の Pairwise Pseudonymous Identifier を名寄せし Track することができる.

<!-- Note that in a proxied federation model, ultimate IdP may be unable to generate a pairwise pseudonymous identifier for the ultimate RP, since the proxy could blind the IdP from knowing which RP is being accessed by the subscriber. In such situations, the pairwise pseudonymous identifier is usually between the IdP and the federation proxy itself. The proxy, acting as an IdP, can itself provide pairwise pseudonymous identifiers to downstream RPs. Depending on the protocol, the federation proxy may need to map the pairwise pseudonymous identifiers back to the associated identifiers from upstream IdPs in order to allow the identity protocol to function. In such cases, the proxy will be able to track and determine which pairwise pseudonymous identifiers represent the same subscriber at different RPs. -->

#### 5.2.6. <a name="ppi-gen"></a>Pairwise Pseudonymous Identifier Generation

Pairwise Pseudonymous Identifier は opaque で推測不可能かつ Subscriber の識別情報を含まないべきであり (SHALL), 単一の IdP-RP ペア以外に知られることなくそのペア間のみで利用されるべきである (SHALL).

<!-- Pairwise pseudonymous identifiers SHALL be opaque and unguessable, containing no identifying information about the subscriber. Additionally, the identifiers SHALL only be known by and used by one IdP-RP pair.  -->

IdP は RP の要求に答えて同じ Identifier を複数の RP に生成してもよい (MAY) が, それはあくまで以下のようなケースに限ること.

<!-- An IdP MAY generate the same identifier for a subscriber at multiple RPs at the request of those RPs, but only if: -->

* 当該 RP 群が, セキュリティドメインや法的なオーナーシップを共有しているなど, 相互連携を行う必要性を正当化できるような関係性を示せること.
* Identifier を共有するすべての RP が, その相互連携を承諾すること.

<!--
* Those RPs have a demonstrable relationship that justifies an operational need for the correlation, such as a shared security domain or shared legal ownership, and
* All RPs sharing an identifier consent to being correlated in such a manner.
-->

RP は Privacy リスクアセスメントを行い, 共通 Identifier を扱うに際したプライバシーリスクについて検討を行うべきである (SHALL).
IdP は意図された RP のみが相互連携を行うことを保証すべきであり (SHALL), 不正な RP がグループの一員のふりをして当該 Pseudonymous Identifier を取得できないようにすること.

<!-- The RPs SHALL conduct a privacy risk assessment to consider the privacy risks associated with requesting a common identifier. The IdP SHALL ensure that only intended RPs are correlated; otherwise, a rogue RP could learn of the pseudonymous identifier for a correlation by fraudulently posing as part of that correlation. -->
