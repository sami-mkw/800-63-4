<a name="sec4"></a>

## 4. Digital Authentication Model

### <a name="4-1"></a>4.1. Overview

[OMB M-04-04](#M-04-04) にあるとおり, Digital Authentication はある Digital System に提示された個人の Identity に対して確信を得るプロセスである.
各システムは Authenticated Identity を元に, 当該個人が当該オンライントランザクションを実行する権限を持っているかどうかを判断する.
多くの場合, Authentication およびトランザクションは Internet のようなオープンネットワーク上で実施されるが, ネットワークアクセスが制限されており, その制限を考慮したアクセスコントロールがなされる場合もある.

<!-- In accordance with [OMB M-04-04](#M-04-04), digital authentication is the process of establishing confidence in individual identities presented to a digital system. Systems can use the authenticated identity to determine if that individual is authorized to perform an online transaction. In most cases, the authentication and transaction take place across an open network such as the Internet; however, in some cases access to the network may be limited and access control decisions may take this into account. -->

本ガイドラインにおける Digital Authentication Model は, 政府機関で現在用いられている技術およびアーキテクチャを反映したものになっている.
Credential の発行と Attribute の提供が異なる主体によって行われるなど, 複数の主体に機能が分離されたより複雑なモデルも考えられ, ある種のアプリケーションではそういったモデルを採用するメリットがあるだろう.
本ドキュメントではシンプルなモデルを扱うが, これは決して各機関が機能分離モデルの採用を排除するものではない.
また, 本来 Credential Service Provider (CSP) が実施する登録, Identity Proofing, 発行プロセスにおいても, それらのプロセスが Registration Authority (RA) や Identity Manager (IM) と呼ばれる主体に移譲されることもある.
通常は RA/IM と CSP の間には強い関連性があるが, これらの関連の性質は個々のケースで異なり得る.
RA/IM と CSP の関連性やその要件については本ドキュメントのスコープ外とする.
以降では, CSP は RA/IM の機能を含むものとして進める.

<!-- The digital authentication model used in these guidelines reflects current technologies and architectures used in government. More complex models that separate functions, such as issuing credentials and providing attributes, among larger numbers of parties are also available and may have advantages in some classes of applications. While a simpler model is used in this document, it does not preclude agencies from separating these functions. In addition, certain enrollment, identity proofing, and issuance processes performed by the credential service provider (CSP) are sometimes delegated to an entity known as the registration authority (RA) or identity manager (IM). A close relationship between the RA/IM and CSP is typical, and the nature of this relationship may differ among RAs, IMs, and CSPs. The types of relationship and their requirements is outside of the scope of this document.  Accordingly, the term CSP will be used to be inclusive of RA/IM functions. -->

Digital Authentication は登録のフェーズから開始される.
一般的な登録プロセスは次のような手順となる.
Applicant が CSP に登録申請を行う.
申請が認められると, CSP は Credential を生成し, それを1つ以上の Authenticator に紐付ける.
Credential には Identifier (仮名可) が含まれており, CSP が検証した1つ以上の属性が含まれることもある.
Authenticator は CSP が発行することもあれば, Subscriber が直接生成・提示することもあり, 3rd-party が提供することもある.
Authenticator と Credential はそれ以降の Authentication Event で用いられる.

<!-- Digital authentication begins with enrollment. The usual sequence for enrollment proceeds as follows. An applicant applies to a CSP. If approved, the CSP creates a credential and binds it to one or more authenticators. The credential includes an identifier, which can be pseudonymous, and possibly one or more attributes that the CSP has verified. The authenticators may be issued by the CSP, generated/provided directly by the subscriber, or provided by a third party. The authenticator and credential may be used in subsequent authentication events. -->

Applicant が彼らの実世界の Identity と紐付いていることを検証するプロセスが *Identity Proofing* である.
Identity Proofing の強度は Identity Assurance Level (IAL) としてカテゴライズされている.
IAL1 では Identity Proofing は要求されない.
IAL2 および IAL3 では Identity Proofing が要求されるが, CSP は検証済の属性値や Claim, 仮名等をアサートしても良いし, 何もアサートしなくてもよい.
これらの情報は, Relying Party (RP) がアクセスコントロールや認可判断を行うときに有用である.
RP は彼らが必要とする IAL を2ないし3とした上で, 特定の属性のみを必要とすることもあり, また当該個人を特定しない程度の属性のみを必要とすることもある.
こういったケースでは必要な属性のみを要求することでプライバシーを高めることができるが, これは Proofing Process の強度を Authentication Process の強度と分離して定義したことで得られたメリットの1つである.
RP は Identity Proofing, Attribute Collection, Attribute Storage をすべて CSP にゆだねる Federated Identity というアプローチをとることもできる.

<!-- The process used to verify an applicant's association with their real world identity is called *identity proofing*. The strength of identity proofing is described by a categorization called the identity assurance level (IAL). At IAL 1, identity proofing is not required, therefore any attribute information provided by the subscriber is self-asserted and not verified. At IAL 2 and 3, identity proofing is required, but the CSP may assert verified attribute values, verified attribute claims, pseudonymous identifiers, or nothing. This information assists Relying Parties (RPs) in making access control or authorization decisions. RPs may decide that their required IAL is 2 or 3, but may only need specific attributes, and perhaps attributes that retain an individual's pseudonymity. This privacy enhancing approach is one of the benefits of separating the strength of the proofing process from that of the authentication process. A relying party may also employ a federated identity approach where the RP outsources all identity proofing, attribute collection, and attribute storage to a CSP. -->

本ドキュメント群では, 認証される主体を *Claimant*, Identity を検証する主体を *Verifier* と呼ぶ.
Authentication Protocol を通じて Claimant が1つ以上の Authenticator を所有および管理していることを Verifier に示すことで, Verifier は Claimant が正規の Subscriber であることを検証できる.
その後 Verifier は Subscriber に関する Assertion を RP に送る.
Subscriber は仮名 (Pseudonymous) な場合もあれば仮名でない場合もある.
当該 Assertion は Subscriber の識別子を含むと同時に, 氏名や登録時に検証されたその他の属性といった Identity 情報を含むこともある.
(詳細は CSP のポリシーとアプリケーションのニーズに依存する)
Verifier が RP をかねる場合, Assertion は Implicit なこともある.
RP は Verifier が提供した Authenticated Information をもとに, Access Control や Authorization Decision を行うことができる.

<!-- In this document suite, the party to be authenticated is called a *claimant* and the party verifying that identity is called a *verifier*. When a claimant successfully demonstrates possession and control of one or more authenticators to a verifier through an authentication protocol, the verifier can verify that the claimant is a valid subscriber. The verifier passes on an assertion about the subscriber, who may be either pseudonymous or non-pseudonymous, to the RP. That assertion includes an identifier, and may include identity information about the subscriber, such as the name, or other attributes that were verified in the enrollment process (subject to the policies of the CSP and the needs of the application). Where the verifier is also the RP, the assertion may be implicit. The RP can use the authenticated information provided by the verifier to make access control or authorization decisions. -->

Authentication は Claimant Identity の確からしさを確立し, 場合によっては Claimant Attributes に関しても確からしさを確立する.
(例えば, Subscriber が US Citizen であるとか, 特定の大学の学生であるとか, ある機関や組織から特定の番号やコードを割り振られているなど)
Authentication は Claimant が認可されているかやアクセス権を持つかなどを判断するものではなく, それらはまた別の話である.
RP (例: 政府機関) は Subscriber の Authenticated Identity および Attributes をもとに, その他の要素も含めて, Access Control や Authorization Decision を行う.
本ドキュメントは RP が Subscriber を認証した後に追加の情報を要求することを禁止するものではない.

<!-- Authentication establishes confidence in the claimant’s identity, and in some cases in the claimant’s attributes (for example if the subscriber is a US Citizen, is a student at a particular university, or is assigned a particular number or code by an agency or organization). Authentication does not determine the claimant’s authorizations or access privileges; this is a separate decision. RPs (e.g., government agencies) will use a subscriber’s authenticated identity and attributes with other factors to make access control or authorization decisions. Nothing in this document precludes RPs from requesting additional information from a subscriber that has successfully authenticated. -->

Authentication Process の強度は Authenticator Assurance Level (AAL) として記述される.
AAL1 は Single-factor Authencitacion を要求し, 多様な Authenticator の利用を認めている.
AAL2 は AAL1 に加えて2つ目の Authentication Factor を要求している.
もっともレベルの高い AAL3 では, AAL2 の片方の Factor として, ハードウェアベースの Authenticator の利用を要求している.

<!-- The strength of the authentication process is described by a categorization called the authenticator assurance level (AAL). AAL 1 requires single-factor authentication and is permitted with a variety of different authenticator types. At AAL 2, authentication requires two authentication factors for additional security. Authentication at the highest level, AAL 3, requires the use of a hardware-based authenticator and one other factor. -->

Authentication の一環として, Device Identity や Geo-location などのメカニズムを利用し, 誤判定を検知 / 防止することもある.
これらのメカニズムは Authenticator Assurance Level を直接引き上げるものではないが, Security Policy やリスク逓減策として利用できる.
多くの場合, Authentication Process および Authentication Service は多くのアプリケーションや機関に共有されることになるが, 特定のアプリケーションの要件に基づいてアクセス許可やトランザクション実施の判断を行うのは, RP となる個々の機関やアプリケーションである.

<!-- As part of authentication, mechanisms such as device identity or geo-location may be used to identify or prevent possible authentication false positives. While these mechanisms do not directly increase the authenticator assurance level, they can aid in enforcing security policies and mitigate risks. In many cases, the authentication process and services will be shared by many applications and agencies. However, it is the individual agency or application acting as the RP that shall make the decision to grant access or process a transaction based on the specific application requirements. -->

[Figure 4-1](#63Sec4-Figure1) は, Digital Authentication Model に関与する多様な主体およびそれらの間のインタラクションを描いている.
左側は登録, Credential 発行, Lifecycle Management, 個人が Identity Proofing および Authentication の各フェーズで取りうるステータスを示している.
一般的には以下のような一連のインタラクションが行われる.

<!-- The various entities and interactions that comprise the digital authentication model used here are illustrated below in [Figure 4-1](#63Sec4-Figure1). The left shows the enrollment, credential issuance, lifecycle management activities, and the various states an individual transitions to based on the phase of identity proofing and authentication they are in. The usual sequence of interactions is as follows: -->

1. 個人 (Applicant) が登録プロセスを通じて CSP に申し込みを行う.
2. CSP は Applicant に対して Identity Proofing を行い, Proofing が成功すれば Applicant は Subscriber となる.
3. CSP と新規 Subscriber の間で, Authenticator およびそれに対応する Credential が確立される.
4. CSP は (最低限) 当該 Credential 自体, 当該 Credential のステータス, 当該 Credential が有効な間に登録されたデータを管理する. Subscriber は自身の Authenticator を管理する.

<!-- 1.	An individual (applicant) applies to a CSP through an enrollment process.
2.	The CSP identity proofs that applicant. Upon successful proofing, the applicant becomes a subscriber.
4.	An authenticator and a corresponding credential are established between the CSP and the new subscriber.
5. The CSP maintains the credential, its status, and the enrollment data collected for the lifetime of the credential (at a minimum). The subscriber maintains his or her authenticator. -->

これ以外のフローは上記ほど一般的ではないであろうが, 同じ要件を満たす別のやり方も存在しうる.

<!-- Other sequences are less common, but could also achieve the same functional requirements. -->

[Figure 4-1](#63Sec4-Figure1) の右側は, Authenticator を利用して Digital Authentication を行う各主体およびそれらの間でのインタラクションを描いている.
トランザクション実施のために　Subscriber の認証が必要な時には, Subscriber は Verifier に対する Claimant となり, 以下のようなインタラクションを行うことになる.

<!-- The right side of [Figure 4-1](#63Sec4-Figure1) shows the entities and the interactions related to using a authenticator to perform digital authentication. When the subscriber needs to authenticate to perform a transaction, he or she becomes a claimant to a verifier. The interactions are as follows: -->

1. Claimant は自身の Authenticator を所有および管理していることを Authentication Protocol を通じて Verifier に示す.
2. Verifier や CSP とインタラクションをおこない, Subscriber Identity と Authenticator を紐付ける Credential の検証を行う. また同時に CSP から Claimant の属性を取得することもある.
3. Verifier が RP と別の主体の場合, Verifier は RP に対して Subscriber に関する Assertion を提供する. RP は Assertion に含まれる情報を使って Access Control や Authorization Decision を行う.
4. Subscriber と RP の間で認証済セッションが確立される.

<!-- 1.	The claimant proves to the verifier that he or she possesses and controls the authenticator through an authentication protocol.
2.	The verifier interacts with the CSP to validate the credential that binds the subscriber’s identity to his or her authenticator and to optionally obtain claimant attributes.
3.	If the verifier is separate from the RP (application), the verifier provides an assertion about the subscriber to the RP, which may use the information in the assertion to make an access control or authorization decision.
4.	An authenticated session is established between the subscriber and the RP. -->

いかなる場合でも, RP は Claimant の認証前に必要な属性を CSP に要求するべきである.
また Claimant は, Assertion の生成・提供前に, それらの属性提供に対する同意を求められるべきである.

<!-- In all cases, the RP should request the attributes it requires from a CSP prior to authentication of the claimant.  In addition, the claimant should be requested to consent to the release of those attribute prior to generation and release of an assertion. -->

場合によっては, Verifier は CSP とリアルタイムにコミュニケーションを行う必要がないこともある. (例: デジタル証明書を利用する場合など)
したがって Verifier と CSP の間の点線は, それら2つの主体の間の (物理的というより) 論理的なリンクを示すものである.
実装によっては Verifier, RP, CSP は [Figure 4-1](#63Sec4-Figure1) のようにそれぞれ分離・独立していることもあるが, それらが同じプラットフォーム上にある場合, それらの要素間のインタラクションは (Untrusted Network を介したやりとりではなく) 同じシステム上のアプリケーション間のローカルメッセージとなる.

<!-- In some cases, the verifier does not need to communicate in real time with the CSP to complete the authentication activity (e.g., some uses of digital certificates). Therefore, the dashed line between the verifier and the CSP represents a logical link between the two entities rather than a physical link. In some implementations, the verifier, RP and the CSP functions may be distributed and separated as shown in [Figure 4-1](#63Sec4-Figure1); however, if these functions reside on the same platform, the interactions between the components are local messages between applications running on the same system rather than protocols over shared untrusted networks. -->

前述の通り, CSP は自身が発行した Credential のステータスを管理する.
一般的に CSP は Credential の管理期間を限定するため Credential 発行時にその有効期限を定める.
ステータスが変更されたり Credential が有効期限切れに近づくと, Credential は更新されたり再発行されることもあれば, 無効化されたり破棄されることもある.
典型的には, Subscriber が自身の既存かつ有効期限切れでない Authenticator および Credential を使って CSP に対して認証を行い, 新規 Authenticator および Credential の発行を要求することになる.
Subscriber が Authenticator および Credential の期限切れないし無効化前に再発行できなかった場合は, 登録プロセスをやり直して新規 Authenticator や Credential を取得することになる場合もある.
場合によっては CSP が有効期限切れから一定期間は再発行リクエストを受け入れることもある.

<!-- As noted above, CSPs maintain status information about credentials they issue. CSPs will generally assign a finite lifetime when issuing credentials to limit the maintenance period. When the status changes, or when the credentials near expiration, credentials may be renewed or re-issued; or, the credential may be revoked and/or destroyed. Typically, the subscriber authenticates to the CSP using his or her existing, unexpired authenticator and credential in order to request issuance of a new authenticator and credential. If the subscriber fails to request authenticator and credential re-issuance prior to their expiration or revocation, he or she may be required to repeat the enrollment process to obtain a new authenticator and credential. Alternatively, the CSP may choose to accept a request during a grace period after expiration. -->

<a name="63Sec4-Figure1"></a>
<div class="text-center" markdown="1">
![](sp800-63-3/media/model.png)

**Figure 4-1 - Digital Authentication Model**
</div>

### 4.2. Enrollment and Identity Proofing

基準となる要件は [Special Publication 800-63A, Enrollment and Identity Proofing](sp800-63a.ja.html) を参照のこと.

<!-- Normative requirements can be found in [Special Publication 800-63A, Enrollment and Identity Proofing](sp800-63a.html). -->

前セクションでは Digital Authentication Model に登場する複数の主体が登場した.
本セクションでは, それら各主体のうち, 登録および Identity Proofing に関与する主体間の関連や責任分担について詳細にまとめる.

<!-- The previous section introduced the different participants in the conceptual digital authentication model. This section provides additional details regarding the relationships and responsibilities of the participants involved with enrollment and identity proofing. -->

個人はこのステージでは Applicant と呼ばれ, CSP に対して Credential 発行を要求する.
Applicant が Identity Proofing に成功すると, CSP は Credential を発行し, Authenticator を当該 Credential に紐づけ, それをもって当該個人は CSP の Subscriber となる.

<!-- An individual, referred to as an applicant at this stage, requests credentials from a CSP. If the applicant is successfully proofed and a credential is created by a CSP and authenticator(s) are bound to it, the individual is then termed a subscriber of that CSP. -->

CSP は各 Subscriber をユニークに識別するメカニズムを確立し, Subscriber の Credential を登録し, Subscriber に発行された Authenticator を監視する.
Subscriber が登録時に Authenticator を受け取ることもあれば, Subscriber がすでに所有している Authenticator を CSP が紐付けることもあり, あとで必要になった段階で Authenticator を生成することもある.
Subscriber は自身の Authenticator を管理し, CSP に対する自身の責任を果たす義務を負う.
CSP は各 Subscriber の登録レコードを管理し, リカバリなどに対応する.

<!-- The CSP establishes a mechanism to uniquely identify each subscriber, register the subscriber’s credentials, and track the authenticators issued to that subscriber. The subscriber may be given authenticators at the time of enrollment, the CSP may bind authenticators the subscriber already has, or they may be generated later as needed. Subscribers have a duty to maintain control of their authenticators and comply with their responsibilities to the CSP. The CSP maintains enrollment records for each subscriber to allow recovery of enrollment records. -->

### 4.3. Authentication and Lifecycle Management

基準となる要件は [Special Publication 800-63B, Authentication and Lifecycle Management](sp800-63b.ja.html) を参照のこと.

#### 4.3.1. Authenticators

Authentication System における古典的なパラダイムでは, Authentication の基礎となる以下の3つの要素が存在する.

<!-- The classic paradigm for authentication systems identifies three factors as the cornerstone of authentication: -->

* Something you know (for example, a password)
* Something you have (for example, an ID badge or a cryptographic key)
* Something you are (for example, a fingerprint or other biometric data)

Multi-factor Authentication では上記から2つ以上の要素を利用することになる.
Authentication System の強度は大枠としてそのシステムに組み込まれた認証要素数によって決まる.
2つの異なる要素を利用した実装は1要素のみの場合より強度が高いと考えられ, 3要素すべてを利用する場合はより強度が高いと考えられる.
[Section 4.1](#4-1) で述べたように, RP や Verifier が位置情報や Device Identity などのその他の情報を利用して Claimed Identity に関するリスク評価を行うこともあるが, それらは認証要素とはみなされない.

<!-- Multi-factor authentication refers to the use of more than one of the factors listed above. The strength of authentication systems is largely determined by the number of factors incorporated by the system. Implementations that use two different factors are considered to be stronger than those that use only one factor; systems that incorporate all three factors are stronger than systems that only incorporate two of the factors. As discussed in [Section 4.1](#4-1), other types of information, such as location data or device identity, may be used by an RP or verifier to evaluate the risk in a claimed identity, but they are not considered authentication factors. -->

Digital Authentication において, Claimant は CSP に登録された1つ以上の Authenticator を所有・管理し, 自身の Identity を証明する.
Authenticator は Claimant が自身を正規の Subscriber であることを証明するための鍵を含み, Claimant はネットワーク越しに Authenticator を所有・管理していることを示すことで認証を行う.

<!-- In digital authentication the claimant possesses and controls one or more authenticators that have been registered with the CSP and are used to prove the claimant’s identity. The authenticator(s) contains secrets the claimant can use to prove that he or she is a valid subscriber, the claimant authenticates to a system or application over a network by proving that he or she has possession and control of one or more authenticators. -->

Authenticator に含まれる鍵は公開鍵ペア (Asymmetric Keys) ないしは共通鍵 (Symmetric Keys) に基づいている.
公開鍵ペアは公開鍵 (Public Key) およびそれと関連付けられた秘密鍵 (Private Key) から構成され, Private Key は Authenticator 内に保存され Claimant が Authenticator を所有・管理していることを示すために用いられる.
何らかの Credential (典型的には Public Key Certificate) を通じて Claimant の Public Key を知っている Verifier は, Claimant が Private Key を含んだ Authenticator を所有・管理していることを確認することで, Authentication Protocol を通じて Claimant Identity を検証することができる.

<!-- The secrets contained in authenticators are based on either public key pairs (asymmetric keys) or shared secrets (symmetric keys). A public key and a related private key comprise a public key pair. The private key is stored on the authenticator and is used by the claimant to prove possession and control of the authenticator. A verifier, knowing the claimant’s public key through some credential (typically a public key certificate), can use an authentication protocol to verify the claimant’s identity, by proving that the claimant has possession and control of the associated private key authenticator. -->

Authenticator に共通鍵を保存する場合には, その共通鍵は Symmetric Key ないしは Password となる.
(上述の Asymmetric Secret の例と異なり, Subscriber は共通鍵を認証者と共有する必要がある)
Symmetric Key も Password もどちらも類似プロトコルで利用することができるが, 両者はそれらがどのように Subscriber と関連付けられるかという点で異なる.
Symmetric Key は一般的には Subscriber が管理するハードウェアないしソフトウェア内に保存されるが, Password は Subscriber に記憶されることが想定される.
多くのユーザーは記憶および入力を容易にするため短い Password を選ぶため, Password は Cryptographic Key よりも短い文字列となる.
さらにいえば, システムは Symmetric Key をランダムに生成する一方, ユーザーは記憶できる Password を可能な文字列のごく小さなサブセット内から選択し, その多くが似た値となる傾向がある.
したがって, Cryptographic Key がネットワーク越しの推測攻撃に対して強固な一方で, ユーザーが選択した Password は (特にその他の防御策がない場合) 脆弱になりやすい.

<!-- Shared secrets stored on authenticators may be either symmetric keys or passwords (as opposed to the asymmetric secrets described above, which subscribers need not share with the authenticator). While both keys and passwords can be used in similar protocols, one important difference between the two is how they relate to the subscriber. While symmetric keys are generally stored in hardware or software that the subscriber controls, passwords are intended to be memorized by the subscriber. Since most users choose short passwords to facilitate memorization and ease of entry, passwords typically have fewer characters than cryptographic keys. Further, whereas systems choose keys at random, users attempting to choose memorable passwords will often select from a very small subset of the possible passwords of a given length, and many will choose very similar values. As such, whereas cryptographic keys are typically long enough to make network-based guessing attacks untenable, user-chosen passwords may be vulnerable—especially if no defenses are in place. -->

本ドキュメントでは, Authenticator は常に鍵を含む.
古典的認証要素の中には Digital Authentication に直接適用できないものもある.
例えば ID バッジは Something You Have の一種であり対面認証時には有用であるが, Digital Authentication における Authenticator とはならない.
Something You Know に分類される認証要素は必ずしも鍵である必要はなく, Knowledge Based Authentication では Claimant が公開されたデータソースを用いて確認できるような質問に答えることで認証を行うが, そういった認証要素も Digital Authentication で利用できる鍵とはならない.
また一般的に Something You Are に属するものは鍵とはいえない.
したがって本リコメンデーションでは Biometrics を Authenticator として利用することは許可しない.

<!-- In this document, authenticators always contain a secret. Some of the classic authentication factors do not apply directly to digital authentication. For example, an ID badge is something you have, and is useful when authenticating to a human (e.g., a guard), but is not a authenticator for digital authentication. Authentication factors classified as something you know are not necessarily secrets, either. Knowledge based authentication, where the claimant is prompted to answer questions that can be confirmed from public databases, also does not constitute an acceptable secret for digital authentication. More generally, something you are does not generally constitute a secret. Accordingly, this recommendation does not permit the use of biometrics as a authenticator. -->

しかしながら本リコメンデーションでは, Authentication System が上記3要素すべてを用いて2要素のみを利用している場合よりセキュアなシステムを実現することを禁止はしない.
複数要素を用いる Digital Authentication System は, 複数要素を Verifier に提示する形式か, Verifier に提示するための鍵を保護するためにいずれかの要素を用いる形式のいずれかを取りうる.
複数要素を Verifier に提示する場合は, 各要素が Authenticator となり, それぞれが鍵を含むことになる.
単一要素を Verifier に提示し, 追加要素を Authenticator 自体の保護に用いる場合には, 追加要素自体は Authenticator でなくてもよい.

<!-- However, this recommendation does accept that authentication systems that incorporate all three factors offer better security than systems that only incorporate two of the factors. A digital authentication system may incorporate multiple factors in either of two ways. The system may be implemented so that multiple factors are presented to the verifier, or some factors may be used to protect a secret that will be presented to the verifier. If multiple factors are presented to the verifier, each will need to be a authenticator (and therefore contain a secret). If a single factor is presented to the verifier, the additional factors are used to protect the authenticator and need not themselves be authenticators. -->

例えば Cryptographic Key を含んだハードウェア (Authenticator) を指紋認証により保護するなどの例が考えられる.
Biometrics とともに利用する場合, Cryptographic Key の出力が Claimant の Authentication Process に用いられることとなる.
その場合, Subscriber になりすまそうとする攻撃者は, 鍵が保存されたハードウェアを盗むなどの手段によって暗号化された鍵を盗み, その Authenticator を利用するために指紋認証を突破する必要がある.
本ドキュメントでは, 実際の Authentication Protocol 上は Verifier と Claimant の間の単純な鍵所有確認だとしても, そういったデバイスは効率的に2要素認証を提供するものと考える.

<!-- For example, consider a piece of hardware (the authenticator) that contains a cryptographic key (the authenticator secret) where access is protected with a fingerprint. When used with the biometric, the cryptographic key produces an output that is used in the authentication process to authenticate the claimant. An impostor must steal the encrypted key (by stealing the hardware) and replicate the fingerprint to use the authenticator. This specification considers such a device to effectively provide two factor authentication, although the actual authentication protocol between the verifier and the claimant simply proves possession of the key. -->

上述のように, Biometrics は単一の認証要素として用いる場合には Digital Authentication で利用可能な鍵とはみなされないが, 特定の使い方をすれば本仕様の枠組みのなかで利用することもできる.
Biometrics は, Verification の時点で物理的にその場にいた人間の Identity 検証に用いることができる, ユニークに個人を特定する属性である.
顔認証, 指紋認証, 虹彩認証, 声紋認証などが Biometrics に含まれる.
[Special Publication 800-63A, Enrollment and Identity Proofing](sp800-63a.ja.html) では, 登録プロセスにおける Biometrics の利用を推奨している.
登録時に Biometrics を利用することで, Subscriber による登録の否認を防止する一助となったり, 登録において詐欺行為を行った人物を特定したりすることもできるし, Authenticator を Unlock することもできる.
これらにより各 Assurance Level を向上することもできる.

<!-- As noted above, biometrics, when employed as a single factor of authentication, do not constitute acceptable secrets for digital authentication, but they do have their place in this specification. Biometric characteristics are unique personal attributes that can be used to verify the identity of a person who is physically present at the point of verification. They include facial features, fingerprints, iris patterns, voiceprints, and many other characteristics. [Special Publication 800-63A, Enrollment and Identity Proofing](sp800-63a.html) recommends that biometrics be used in the enrollment process for higher levels of assurance to later help prevent a subscriber who is registered from repudiating the enrollment, to help identify those who commit enrollment fraud, and to unlock authenticators. -->

#### 4.3.2. Credentials

前述のように, Credential はその発行プロセスにおいて Authenticator を Identifier を通じて Subscriber に紐付けるものとなる.
Credential は CSP に保管・管理される.
Claimant は Authenticator を所有するが, 必ずしも電子的な Credential を所有する必要はない.
例えばユーザー属性を含む Database Entry は本ドキュメントが目的とするケースにおいては Credential とみなされるが, これは Verifier に所有されるものである.
X.509 Public Key Certificate は Claimant が所有する Credential としての古典的な例である.

<!-- As described in the preceding sections, credentials bind an authenticator to the subscriber, via an identifier, as part of the issuance process. Credentials are stored and maintained by the CSP. The claimant possesses a authenticator, but is not necessarily in possession of the electronic credentials. For example, database entries containing the user attributes are considered to be credentials for the purpose of this document but are possessed by the verifier. X.509 public key certificates are a classic example of credentials the claimant can (and often does) possess. -->

#### 4.3.3. Authentication Process

Authentication Process は, Authentication Protocol を通じて, Claimant が Verifier に対して Asserted Identity に紐づけらた Authenticator を所有・管理していることを示すところから始まる.
一度それが証明されると, Verifier は当該 Credential がまだ Valid であることを検証する.
この検証には往々にして Verifier と CSP とのインタラクションが伴う.

<!-- The authentication process begins with the claimant demonstrating to the verifier possession and control of a authenticator that is bound to the asserted identity through an authentication protocol. Once possession and control has been demonstrated, the verifier verifies that the credential remains valid, usually by interacting with the CSP. -->

Authentication Protocol における Verifier と Claimant の間のインタラクションは, システム全体のセキュリティにとっても非常に重要である.
よくデザインされたプロトコルでは, Claimant と Verifier の間のトラフィックは認証時も認証後も Integrity および Confidentiality が保護されており, 攻撃者が正規の Verifier になりすました場合でもその被害を限定的にすることができる.

<!-- The exact nature of the interaction between the verifier and the claimant during the authentication protocol is extremely important in determining the overall security of the system. Well-designed protocols can protect the integrity and confidentiality of traffic between the claimant and the verifier both during and after the authentication exchange, and it can help limit the damage that can be done by an attacker masquerading as a legitimate verifier. -->

また Verifier 側では, パスワードや PIN などのエントロピーの低い鍵に対するオンライン推測攻撃への対策を行うこともできる.
オンライン推測攻撃対策としては, Rate Limit を設ける方法や, 間違ったリクエストに対する Delay 処理を行うなどの方法があげられる.
一般化すると, これらは間違った施行の回数を監視および制限することで実現できる.
オンライン推測攻撃はその前提としてほとんどの施行が失敗するからである.

<!-- Additionally, mechanisms located at the verifier can mitigate online guessing attacks against lower entropy secrets like passwords and PINs by limiting the rate at which an attacker can make authentication attempts or otherwise delaying incorrect attempts. Generally, this is done by keeping track of and limiting the number of unsuccessful attempts, since the premise of an online guessing attack is that most attempts will fail. -->

Verifier は機能的には独立した役割であるものの, しばしば CSP and/or RP の一部として実装される傾向にある.
Verifier が CSP から独立した主体である場合, Verifier は Subscriber の Authenticator Secret を Authentication Process を通じて知ることがないと保証されることが望ましい.
最低限 Verifier が CSP の保有する鍵に制限なくアクセスできる状態は避けること.

<!-- The verifier is a functional role, but is frequently implemented in combination with the CSP and/or the RP. If the verifier is a separate entity from the CSP, it is often desirable to ensure that the verifier does not learn the subscriber’s authenticator secret in the process of authentication, or at least to ensure that the verifier does not have unrestricted access to secrets stored by the CSP. -->

### 4.4. Federation and Assertions

基準となる要件は [Special Publication 800-63C, Federation and Assertions](sp800-63c.ja.html) を参照のこと.

<!-- Normative requirements can be found in [Special Publication 800-63C, Federation and Assertions](sp800-63c.html). -->

全体的に SP 800-63-3 は Federated Identity Architecture を前提とはしない.
本ガイドラインは市場にある既存のモデルにはとらわれず, 各機関が Digital Authentication Scheme を自身の要件に合わせて採用できるようにしている.
しかしながら National Strategy for Trusted Identities in Cyberspace (NSTIC) [[NSTIC]](#theNSTIC) とも整合をとり, Identity Federation は各機関および RP が個別にサイロ化した Identity System を持つ状況よりも好ましいものとしている.

<!-- Overall, SP 800-63-3 does not presuppose a federated identity architecture; rather, the guideline is agnostic to the types of models that exist in the marketplace, allowing agencies to deploy a digital authentication scheme according to their own requirements. However, identity federation, consistent with the National Strategy for Trusted Identities in Cyberspace (NSTIC) [[NSTIC]](#theNSTIC), is preferred over a number of siloed identity systems that each serve a single agency or RP. -->

Federated Architecture は以下のような重要な利点をもたらす. (以下に挙げたものに限定はしない)

<!-- Federated architectures have many significant benefits, including, but not limited to: -->

* User Experience の向上. 例えばひとたび Identity Proofing を経た個人が, 同じ Credential を複数の RP に対して再利用することができる.
* コスト削減. ユーザーにとっては Authenticator の削減, 各機関にとっては IT インフラの削減.
* データ最小化. 各機関は個人情報の保存にかかる各種データ収集・保管・破棄およびコンプライアンス準拠活動を必要としない.
* Privacy 向上.
* Pseudonymous Attribute Assertion. 各機関はサービス提供のために必要最低限の Claim を含む属性のみをリクエストすることができる.
* Misson Enablement. 各機関は Identity Management にかかる負荷を軽減し, 各々のミッションに集中できる.

<!-- * Enhanced user experience.  For example, an individual can be identity proofed once and can reuse the issued credential at multiple RPs
* Cost reduction, to both the user (one authenticator) and the agency (reduction in IT infrastructure)
* Data minimization: agencies do not need to pay for collection, storage, disposal, and compliance activities related to storing personal information
* Privacy enhancing
* Pseudonymous attribute assertions. Agencies can request a minimized set of attributes, to include claims, to fulfill service delivery.
* Mission enablement. Agencies can focus on mission, rather than the business of identity management. -->

以降のセクションでは Federated Identity Architecture の各要素について議論する.

<!-- The following sections discuss the components of a federated identity architecture should an agency elect this type of model. -->

#### 4.4.1 Assertions

Authentication Process が完了すると, Verifier は認証結果を含む Assertion を生成し, それを RP に提示する.
Verifier が RP の一部として実装されている場合, この Assertion は Implicit である.
Verifier が RP と分離して実装されている場合, それは典型的な Federated Identity モデルであり, Verifier から RP に認証プロセスの結果を伝搬するために Assertion が利用される.
また同時に Subscriber に関する追加の情報も Assertion によって伝搬されることもある.
Assertion は RP に直接渡されることもあれば, Subscriber を通じて伝搬されることもあるが, それはシステムデザインに密接に関係する.

<!-- Upon completion of the authentication process, the verifier generates an assertion containing the result of the authentication and provides it to the RP. If the verifier is implemented in combination with the RP, the assertion is implicit. If the verifier is a separate entity from the RP, as in typical federated identity models, the assertion is used to communicate the result of the authentication process, and optionally information about the subscriber, from the verifier to the RP. Assertions may be communicated directly to the RP, or can be forwarded through the subscriber, which has further implications for system design. -->

RP は Assertion の生成者, 生成日時, および CSP および RP のポリシーおよびプロセスを管轄する Trust Framework の存在などをもとに Assertion を信頼する.
Verifier は Assertion の Integrity を確認できる仕組みを提供する責任がある.

<!-- An RP trusts an assertion based on the source, the time of creation, and the corresponding trust framework that governs the policies and process of CSPs and RPs. The verifier is responsible for providing a mechanism by which the integrity of the assertion can be confirmed. -->

RP は Assertion 生成者 (Verifier) を認証し, Assertion の Integrity を確認する責任がある.
Verifier が Subscriber を介して Assertion を伝搬してくる場合には, Verifier は Subscriber が Assertion を改ざんできないよう Integrity の保護を行う必要がある.
Verifier と RP が直接通信を行う場合は, 保護されたセッションをもって Integrity Protection とすることもできる.
Assertion をオープンなネットワークを介して送る場合, Verifier は Assertion に含まれる Subscriber に関するセンシティブな情報の Confidentiality を確保して信頼できる RP にのみ当該情報が受け取れるようにする責任がある.

<!-- The RP is responsible for authenticating the source (the verifier) and for confirming the integrity of the assertion. When the verifier passes the assertion through the subscriber, the verifier must protect the integrity of the assertion in such a way that it cannot be modified by the subscriber. However, if the verifier and the RP communicate directly, a protected session may be used to provide the integrity protection. When sending assertions across an open network, the verifier is responsible for ensuring that any sensitive subscriber information contained in the assertion can only be extracted by an RP that it trusts to maintain the information’s confidentiality. -->

Assertion の例としては以下のようなものがあげられる.

<!-- Examples of assertions include: -->

* SAML Assertions - SAML Assertion は Mark-up Language を用いて定義されており, Security Assertion の記述を目的とする. 当該 Assertion は Verifier が RP に対して Claimant の Identity に関する Statement を生成する際に利用できる. SAML Assertion はオプションで電子署名がされる.
* OpenID Connect Claims - OpenID Connect Claims は JavaScript Object Notation (JSON) を用いて Security に関する情報およびオプションで User Claims を記述するよう定義されている. JSON 形式のユーザー情報 Claims はオプションで電子署名がされる.
* Kerberos Tickets - Kerberos Ticket は, Ticket Granting Authority が2つの認証された主体に対してセッションキーを発行する仕組みである. Kerberos では Symmetric Key ベースの秘匿化方式 (Encapsulation Scheme)を用いる.

<!-- * SAML Assertions – SAML assertions are specified using a mark-up language intended for describing security assertions. They can be used by a verifier to make a statement to an RP about the identity of a claimant. SAML assertions may optionally be digitally signed.
* OpenID Connect Claims - OpenID Connect claims are specified using JavaScript Object Notation (JSON) for describing security, and optionally, user claims.  JSON user info claims may optionally be digitally signed.
* Kerberos Tickets – Kerberos Tickets allow a ticket granting authority to issue session keys to two authenticated parties using symmetric key based encapsulation schemes. -->

#### 4.4.2. Relying Parties

RP は Authentication Protocol の結果を信頼し Subscriber の Identity および Attributes の確からしさを確立し, オンライントランザクションを行う.
RP は Subscriber の Authenticated Identity (Pseudonymous な場合もあればそうでない場合もある), IAL, AAL and/or FAL およびその他の要素を用いて Access Control や Authorization Decision を行う.
Verifier と RP は同じ主体なこともあれば, 相互に独立した主体であることもある.
両者が相互に独立している場合, RP は通常 Verifier から Assertion を受け取り, Assertion が確かに自身が信頼する Verifier から送られてきたことを確認する.
RP は Assertion に含まれる個人の属性や有効期限などの追加情報もおなじように処理する.
RP は, IAL, AAL, FAL に関係なく, Verifier が提示した Assertion が RP のシステムアクセスに必要な基準を満たすかどうかを最終的に判断する.

<!-- An RP relies on results of an authentication protocol to establish confidence in the identity or attributes of a subscriber for the purpose of conducting an online transaction. RPs may use a subscriber’s authenticated identity (pseudonymous or non-pseudonymous), the IAL, AAL and/or FAL (federation assurance level, indicating the strength of the assertion protocol), and other factors to make access control or authorization decisions. The verifier and the RP may be the same entity, or they may be separate entities. If they are separate entities, the RP normally receives an assertion from the verifier. The RP ensures that the assertion came from a verifier trusted by the RP. The RP also processes any additional information in the assertion, such as personal attributes or expiration times. The RP is the final arbiter concerning whether a specific assertion presented by a verifier meets the RP's established criteria for system access regardless of IAL, AAL, and/or FAL. -->

### 4.5. Assurance Levels

全体的な M-04-04 Level of Assurance (LOA) はアーキテクチャ構成要素個々の Assurance Level の組み合わせによって決定される.
[Table 4-1](#63Sec4-Table1) は, 厳密に M-04-04 Level of Assurance を順守した場合の, 対応する Identity Assurance Level, Authenticator Assurance Level および Federation Assurance Level とのマッピングを示す.

<!-- The M-04-04 Level of Assurance (LOA) is determined by combining the discrete assurance level for each of the components of the architecture. [Table 4-1](#63Sec4-Table1) shows strict adherence to M-04-04 Level of Assurance, mapping corresponding Identity, Authenticator, and Federation Assurance Levels. -->

<a name="63Sec4-Table1"></a>

<div class="text-center" markdown="1">

**Table 4-1.  Legacy M-04-04 Requirements**

</div>

| M-04-04 Level of Assurance (LOA) | Identity Assurance Level (IAL)| Authenticator Assurance Level (AAL) | Federation Assurance Level (FAL)
|:------------------:|:-----------------------------:|:------------------------:|:------------------------:|
| 1 | 1 | 1| 1
| 2 | 2 | 2 or 3 |2
| 3 | 2 | 2 or 3 |2
| 4 | 3 | 3 |4

一方で, [Table 4-2](#63ES-Table2) は各機関のニーズに合わせて IAL, AAL, FAL のコンビネーションを決定することが許容された, M-04-04 Level of Assurance の新たな要件を示す.
詳細は [SP 800-63A](sp800-63a.ja.html), [SP 800-63B](sp800-63b.ja.html), [SP 800-63C](sp800-63c.ja.html) を参照のこと.

<!-- However, [Table 4-2](#63ES-Table2) shows the new requirements that are allowable for M-04-04 Level of Assurance, by combining IAL, AAL, and FAL based on agency need. Further details and normative requirements are provided in are provided in [SP 800-63A](sp800-63a.html), [SP 800-63B](sp800-63b.html), and [SP 800-63C](sp800-63c.html) respectively. -->

<a name="63Sec4-Table2"></a>

<div class="text-center" markdown="1">

**Table 4-2.  Recommended M-04-04 Requirements**

</div>

| M-04-04 Level of Assurance (LOA) | Identity Assurance Level (IAL)| Authenticator Assurance Level (AAL) | Federation Assurance Level (FAL)
|:------------------:|:-----------------------------:|:------------------------:|:------------------------:|
| 1 | 1 | 1, 2 or 3 | 1, 2, 3, or 4
| 2 | 1 or 2 | 2 or 3 |2, 3, or 4
| 3 | 1 or 2 | 2 or 3 |2, 3, or 4
| 4 | 1, 2, or 3 | 3 |3 or 4

このマッピングでは, Identity 要素を Assurance Level と分離することができる.
これにより, 個人の Identity の Identification が不要な場合であっても, Multi-Factor Authentication (MFA) を採用することができる.
言い方を変えれば, より高い LOA を満たすにも, Identity Proofing が不要もしくはごくわずかで済むのである.
例えば M-04-04 LOA 3 を満たすには, 以下の要件を満たせば良い.

<!-- This mapping takes advantage of the ability to separate distinct identity elements per assurance level.  This allows an agency adopt multi-factor authentication (MFA) when identification of the individual identity is not required. Conversely, little or no identity proofing can be performed at the higher LOAs. For instance, to achieve M-04-04 LOA 3: -->

* 登録および Identity Proofing プロセスが最低でも IAL1 ないし IAL2 を満たす.
* Authenticator (もしくは Authenticator の組み合わせ) が AAL2 以上である.
* Authentication Assertion を利用する場合は, それが FAL2 以上である.

<!-- * The enrollment and identity proofing process would, at a minimum, use IAL 1 or 2 processes.
* The authenticator (or combination of authenticators) would have an AAL of 2 or higher.
* Authentication assertions (if used) would have an FAL of 2 or higher. -->

ある LOA に対して許容される IAL は, 各機関のミッションを満たすためのニーズによって決定される.
仮名でのサービス提供を行うには, 各機関はサービス提供のためのパーソナルデータ収集を限定すべきであり, 各 LOA において特定の IAL が要求されるべきではない.
例えば "health tracker" アプリケーションを提供する場合などを考えてみよう.
[Executive Order 13681](#EO13681) が要求する "...Digital Application を通じて市民にパーソナルデータへのアクセスを提供する機関は, 必要に応じて多要素認証と効果的な Identity Proofing プロセスを実施すること." という表現に従うと, 各機関は AAL2 Authenticator が必要な LOA3 を選ぶこともある.
しかしながらこの例では, ユーザーの真の Identity を機関システムが把握する必要はないかもしれない.
いままでは, データのセンシティブさから LOA3 が必要と評価された場合, 当該機関はユーザーの Identity Proofing を実施する必要があったが, これは今後不要となり, 各機関はこのようなケースでは Identity Proofing を行わず, Health Tracker システムのユーザーが IAL1 の仮名な状態でサービスを受けられるようにすることが推奨される.
これにより, AAL2 や AAL3 を満たす MFA Authenticator を利用しても, その Authenticator は IAL1 の Identity と紐付いていることから, パーソナル情報が漏洩することもないだろう.

<!-- Agency mission need will assist in determining the acceptable IAL at a given LOA.  Since agencies should limit the collection of personal data in order to provide services and allow for strong pseudonymity, a specific IAL is not explicitly required for each LOA. For example, an agency may establish a "health tracker" application.  In line with the terms of [Executive Order 13681](#EO13681) requiring "...that all agencies making personal data accessible to citizens through digital applications require the use of multiple factors of authentication and an effective identity proofing process, as appropriate.", the agency could select LOA3 such that an AAL2 authenticator is required.  However, in this example, there may be no need for the agency system to know the true identity of the user.  In the past, the LOA3 assessment of data sensitivity would also require the agency to identity proof the user.  This is no longer necessary and the agency is encouraged in this case to not perform any identity proofing and allow the user of the health tracker system to be pseudonymous at IAL1.  The MFA authenticator at AAL2 or AAL3 will not leak any personal information because it is bound to an IAL 1 identity. -->

HSPD-12 および Personal Identity Verification (PIV) Smart Card が必要な連邦の従業員のケースでは, 機関は LOA4 を満たす必要がある.
このケースでは AAL3 を満たす Authenticator と IAL3 を満たす Identity Proofing が必要となる.

<!-- In the case of HSPD-12 and those federal employees that are required to obtain a Personal Identity Verification (PIV) smart card, the requirement is that agencies meet LOA4. This use case requires an authenticator at AAL3 **and** identity proofing at IAL 3. -->

>Important Note: 政府機関は上記表より高レベルの Assurance Level を受け入れてもよい.
例えば, Federated トランザクションにおいて, 当該アプリケーションが IAL2 を要件とする場合であっても, 政府機関は IAL3 Identity を受け入れることもできる.
これは Authenticator についても同様であり, RP は必要とされるレベルより高いレベルの Authenticator を利用することもできる.
しかしながら RP は, 上記のようなシナリオが CSP が適切にプライバシーを保護している Federated シナリオにおいてのみ発生し, RP が要求した属性のみが提供され, Authenticator や Assertion からパーソナルインフォメーションが漏洩しないことを保証すること.
詳細は [privacy requirements](./sp800-63c.ja.html#sec9) を参照のこと.

<!-- >Important Note: An agency can accept a higher assurance level than those required in the table above.  For example, in a federated transaction, an agency can accept an IAL3 identity if their application is assessed at IAL2.  The same holds true for authenticators; stronger authenticators can be used at RP's that have lower authenticator requirements.  However, RPs will ensure that these scenarios only occur in federated scenarios with appropriate privacy protections by the CSP to ensure that only the requested attributes are provided to the RP and that no personal information leaks from the authenticator or the assertion.  See [privacy requirements](./sp800-63c.html#sec9) in SP 800-63C for more details. -->

各機関はそれぞれの Assurance 要素を考慮するよう推奨されることから, LOA を決定する際の 'low watermark' の概念はもはや存在しない.
IAL1 および AAL2 を満たすアプリケーションが IAL2 および AAL2 を満たすアプリケーションよりセキュアでないといった判断をすべきではない.
そういったアプリケーションの違いは, 各アプリケーションのセキュリティには影響を与えない, 必要な Proofing の量のみである.
ただし, もし機関が xAL を誤って決定してしまった場合には, セキュリティに影響を与える可能性は大いにある.

<!-- As agencies are encouraged to consider each distinct element of assurance, the notion of the 'low watermark' to determine LOA no longer applies.  An IAL1/AAL2 application should not be considered any less secure than an IAL2/AAL application.  The only difference between these applications is the amount of proofing required, which does not impact security of each application. That said, if an agency incorrectly determines the xAL, security could very well be impacted. -->