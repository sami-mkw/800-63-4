<a name="sec6"></a>

## 6. Assertion Presentation

Assertion は IdP から RP に対して *back-channel* ないしは *front-channel* で提示される (MAY).
どちらのモデルにも利点と欠点があるが, いずれにせよ Assertion を正しく検証する必要があるのは同じである.
Section 4.1.4 にあるように, ある条件下では Federation を簡単にするため IdP と RP の間を Proxy した状態で Assertion をやりとりすることもある.

<!-- Assertions MAY be presented in either a *back-channel* or *front-channel* manner from the IdP to the RP. Each model has its benefits and drawbacks, but both require the proper validation of the assertion. Assertions MAY also be proxied to facilitate federation between IdPs and RPs under specific circumstances, as discussed in section 4.1.4. -->

IdP は RP が明示的に要求した Attribute のみを送信するべきである (SHALL).
また RP は Privacy Risk Assesment を行い, どの Attribute を要求するか決定するべきである (SHALL).

<!-- The IdP SHALL transmit only those attributes that were explicitly requested by the RP. RPs SHALL conduct a privacy risk assessment when determining which attributes to request. -->

(Shoulder Surfing 等により) センシティブな情報を認可なしに露出するリスクを提言するため, 必要に応じてマスキング等の対策を行うべきだが (SHALL),  Subscriber は送信される Attribute を閲覧可能であるべきである (SHALL).
Subscriber は明示的な通知を受け, Subscriber の Attribute が RP に送信される前に明示的同意を行えるべきである (SHALL).
最低限, 最も効果的に通知および同意取得を行える主体により通知が行われるべきである (SHOULD).
どちらの主体が通知と同意取得を行うべきかに関しては, Section 9.2 を参照のこと.
もし利用するプロトコルが Optional Attribute をサポートしている場合, Subscriber はそれらの属性についても RP に渡すか否かの選択肢を与えられるべきである (SHALL).
IdP はある RP に送信された Attribute Bundle を記憶し, 同じ RP へ当該 Attribute Bundle を再送信するような仕組みを導入してもよい (MAY).

<!-- The subscriber SHALL be able to view the attribute values to be transmitted, although masking mechanisms SHALL be employed, as necessary, to mitigate the risk of unauthorized exposure of sensitive information (e.g. shoulder surfing). The subscriber SHALL receive explicit notice and be able to provide positive confirmation before any attributes about the subscriber are transmitted to any RP. At a minimum, the notice SHOULD be provided by the party in the position to provide the most effective notice and obtain confirmation. See section 9.2 for considerations on determining which party should provide the notice and obtain confirmation. If the protocol in use allows for optional attributes, the subscriber SHALL be given the option to decide whether to transmit those attributes to the RP. A IdP MAY employ mechanisms to remember and re-transmit the exact attribute bundle to the same RP. -->

### 6.1. Back-channel presentation

*Back-Channel* Model では, Subscriber は Assertion の参照を渡され, 一般的には Front-Channel を通じてそれを RP に提示することになる.
Assertion の参照はそれ自身では Subscriber に関する情報は持たず, Attacker による偽造や改ざんに耐えねばならない (SHALL).
RP がその参照を IdP に提示して初めて Assertion が取得できる.
また RP が IdP に Assertion の参照を提示する際, 通常は RP の認証が行われる.

<!-- In the *back-channel* model, the subscriber is given an assertion reference to present to the RP, generally through the front channel. The assertion reference itself contains no information about the subscriber and SHALL be resistant to tampering and fabrication by an attacker. The RP presents the assertion reference to the IdP, usually along with authentication of the RP itself, to fetch the assertion. -->

<a name="63cSec6-Figure1"></a>

<div class="text-center" markdown="1">
![Figure 1: Back-channel presentation](sp800-63c/media/indirect.png)

**Figure 6-1: Back-channel presentation**

</div>

このモデルでは, Assertion 自体は IdP から RP に直接渡されるため, (Subscriber 自身を含む) 3rd-party にインターセプトされたり改ざんされるリスクを最小化できる.

<!-- In this model, the assertion itself is requested directly from the IdP to the RP, minimizing chances of interception and manipulation by a third party (including the subscriber themselves). -->

またこの方式では, 最初の Authentication Transaction の後にさらに Back-Channel Communication を継続することもできるため, RP は Assertion に含まれない追加の Attribute を IdP に問い合わせることもできる.

<!-- This method also allows the RP to query the CSP for additional attributes about the subscriber not included in the assertion itself, since back-channel communication can continue to occur after the initial authentication transaction has completed. -->

Back-Channel 方式では, ネットワークトランザクションがより多く必要となる一方, やり取りされる情報はそれを必要としている主体以外に渡されることはない.
RP が IdP から直接 Assertion を受け取るため, 攻撃箇所は限定される.

<!-- In the back-channel method, there are more network transactions required, but the information is limited to the parties that need it. Since an RP is expecting to get an assertion only from the IdP directly, the attack surface is reduced. -->

Assertion の参照には以下のような要件が求められる.
<!-- The assertion reference: -->

- 特定 RP にのみ利用可能な制限を行うこと (SHALL)
- Onetime (single-use) であること (SHALL)
- 数秒〜数分程度と有効期限が短いこと (SHOULD)
- RP が認証された状態で提示されること (SHOULD)
<!--
 - SHALL be limited to use by a single RP
 - SHALL be single-use
 - SHOULD be time limited with a short lifetime of seconds or minutes
 - SHOULD be presented along with authentication of the RP
-->

RP は, Cross-Site Scripting やその他の攻撃への対策を行い, 偽造された Assertion や Capture された Assertion を使った Injection 攻撃を防ぐべきである (SHALL).

<!-- The RP SHALL protect itself against injection of manufactured or captured assertion references by use of cross-site scripting protection or other accepted techniques.  -->

Assertion に含まれる Claim は Issuer Verification, Signature Validation, Audience Restriction 等により検証されるべきである (SHALL).

<!-- Claims within the assertion SHALL be validated including issuer verification, signature validation, and audience restriction. -->

IdP から Subscriber, Subscriber から RP へと Assetion の参照を送信する際には, 認証され保護された Channel を利用すべきである (SHALL).
RP から IdP に Assertion の参照を送信する際, IdP から RP に Assertion を送信する際も, 認証され保護された Channel を利用すべきである (SHALL).

<!-- Conveyance of the assertion reference from the IdP to the subscriber as well as from the subscriber to the RP SHALL be made over an authenticated protected channel. Conveyance of the assertion reference from the RP to the IdP as well as the assertion from the IdP to the RP SHALL be made over an authenticated protected channel. -->

Assertion の参照の提示を受ける際には, IdP は Assertion 発行前に RP を認証するべきである (SHOULD).

<!-- Presentation of the assertion reference at the IdP SHOULD require authentication of the RP before an assertion is issued. -->

### 6.2. Front-channel Presentation

*front-channel* Model では, IdP は認証成功後 Assertion を生成し Subscriber に渡す.
Subscriber は渡された Assertion を利用して RP に自身を認証する.
これはしばしば Subscriber のブラウザの機能を用いて実現される.

<!-- In the *front-channel* model, the IdP creates an assertion and sends it to the subscriber after successful authentication. The assertion is used by the subscriber to authenticate to the RP. This is often handled by mechanisms within the subscriber’s browser.) -->

<a name="63cSec6-Figure2"></a>

<div class="text-center" markdown="1">
![Figure 2: Front-channel presentation](sp800-63c/media/direct.png)


**Figure 6-2: Front-channel presentation**

</div>

この方式では, Assertion は Subscriber に閲覧可能である.
これは Assertion に含まれるシステム情報などの漏洩につながる可能性もある.

<!-- In the front-channel method, an assertion is visible to the subscriber, which could potentially cause leakage of system information included in the assertion. -->

Assertion は Subscriber のコントロール下に置かれることから, Subscriber が当該 Assertion を Replay したり, 単一の Assertion を複数の RP に送ることも可能である.

Assertion は Subscriber のコントロール下に置かれることから, Subscriber はブラウザをリプレイして Assertion を複数の RP に送りつけるなどの手段によって, Assertion を本来意図されない主体に送りつけることもできる.
Assertion が Audience Restriction により RP に Reject されたとしても, 意図しない RP への Assertion の提示は Subscriber に関する情報や Subscriber のオンラインアクティビティの漏洩につながりうる.
意図して複数の RP に提示できるよう設計された Assertion を生成することも可能だが, そのような手法は当該 Assertion に対する Audience Restriction を緩め, 当該 RP 間における Subscriber の Privacy および Security 侵害につながりうる.
よってそのような Multi-RP Use は推奨しない.
RP はそれぞれ個別の Assertion を取得するよう推奨される.

<!-- Since the assertion is under the control of the subscriber, the front-channel presentation method also allows the subscriber to submit a single assertion to unintended parties, perhaps by a browser replaying an assertion at multiple RPs. Even if the assertion is audience restricted and rejected by RPs, its presentation at unintended RPs could lead to leaking information about the subscriber and their online activities. Though it is possible to intentionally create an assertion designed to be presented to multiple RPs, this method can lead to lax audience restriction of the assertion itself, which in turn could lead to privacy and security breaches for the subscriber across these RPs. Such multi-RP use is not recommended. Instead, RPs are encouraged to fetch their own individual assertions. -->

RP は, Cross-Site Scripting やその他の攻撃への対策を行い, 偽造された Assertion や Capture された Assertion を使った Injection 攻撃を防ぐべきである (SHALL).

<!-- The RP SHALL protect itself against injection of manufactured or captured assertions by use of cross-site scripting protection or other accepted techniques. -->

Assertion に含まれる Claim は Issuer Verification, Signature Validation, Audience Restriction 等により検証されるべきである (SHALL).

<!-- Claims within the assertion SHALL be validated including issuer verification, signature validation, and audience restriction. -->

IdP から Subscriber, Subscriber から RP へと Assetion を送信する際には, 認証され保護された Channel を利用すべきである (SHALL).

<!-- Conveyance of the assertion from the IdP to the subscriber as well as from the subscriber to the RP SHALL be made over an authenticated protected channel. -->

### 6.3. Assertion proxying

実装によっては, IdP, RP, Subscriber の中間者となる Proxy が IdP から Assertion を受け取り, その Assertion を元に RP に対して新たな Assertion を生成することもある.
IdP から見れば, こういった Proxy は RP となる.
RP から見れば, こういった Proxy は IdP となる.
(Section 4.1.4 参照)

<!-- In some implementations, a proxy takes in an assertion from the IdP and creates a derived assertion when interacting directly with the RP, acting as an intermediary between the subscriber, the IdP, and the RP. From the perspective of the true IdP, the proxy is a single RP. From the perspective of the true RPs, the proxy is a single IdP. (See section 4.1.4.) -->

こういった Proxy の利用目的としては, 以下のようなものがあげられる.

<!-- There are several common reasons for such proxies: -->

- 複数のユーザー認証が必要な RP にアクセスするためのポータルサイト.
<!-- - Portals that provide users access to multiple RPs that require user authentication -->

- RP のアクセスコントロールポリシーを満たすために必要な Web Caching の手段. 特に Subscriber が TLS Mutual Authentication を利用している場合.
<!-- - Web caching mechanisms that are required to satisfy the RP’s access control policies, especially when mutually-authenticated TLS with the subscriber is used -->

- TLS を終端しトラフィックを監視・コントロールする必要のあるネットワークモニタリングやフィルタリングの手段.
<!-- - Network monitoring and/or filtering mechanisms that terminate TLS in order to inspect and manipulate the traffic -->

すべての情報のやりとりは, 認証され保護された Channel を通じて行うべきである (SHALL).

<!-- Conveyance of all information SHALL be made over authenticated protected channels. -->

### 6.4. Protecting Information

IdP と RP の間のコミュニケーションは, 認証され保護された Channel を利用して保護するべきである (SHALL).

<!-- Communications between the IdP and the RP SHALL be protected in transit using an authenticated protected channel. -->

IdP は, RP が自身のセキュリティポリシーを適用する際に有用な情報にアクセスできる可能性もある.
こういった情報としては, Device Identity, Location, System Health Check, Configuration Management 等があげられる.
IdP がこういった情報を取得できる場合, Subscriber のプライバシーを侵害しない範囲内で, そういった情報を RP に渡すことも可能であろう.

<!-- Note that the IdP may have access to information that may be useful to the RP in enforcing security policies, such as device identity, location, system health checks, and configuration management. If so, it may be a good idea to pass this information along to the RP within the bounds of the subscriber's privacy preferences. -->

User に関する追加の属性は, Assertion とは別に, RP から IdP への認可されたリクエストを通じてやり取りされてもよい (MAY).
こういった属性へのアクセスに対する認可は, Assertion と一緒に発行することもできる (MAY).
User に関する情報をこのように分離することで, Authentication Assertion 自体には必須な情報のみを含めればよいことになり, ユーザーのプライバシー保護につながる.

<!-- Additional attributes about the user MAY be included outside of the assertion itself as part of a separate authorized request from the RP to the IdP. The authorization for access to these attributes MAY be issued alongside the assertion itself. Splitting user information in this manner can aid in protecting user privacy and allow for limited disclosure of identifying attributes on top of the essential information in the authentication assertion itself. -->

RP は可能な限り全属性ではなく Attribute Claim を要求すべきであり (SHALL), IdP は Attribute Claim をサポートすべきである (SHALL).

<!-- The RP SHALL, where feasible, request attribute claims rather than full attribute values. The IdP SHALL support attribute claims. -->
