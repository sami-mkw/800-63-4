<a name="sec4"></a>

## 4. Federation

Identity / Authentication Information を一連のネットワークシステム間でやりとりするためのプロセス.
Federation シナリオでは, Verifier / CSP は Identity Provider や IdP と呼ばれる. また本ドキュメントでは Relying Party や RP は Federated Identity を受け取る主体である.

<!-- Federation is a process that allows for the conveyance of identity and authentication information across a set of networked systems. In a federation scenario, the verifier or CSP is known as the *identity provider*, or IdP. In this document, the *relying party*, or RP, is the party that receives the federated identity. -->

![Figure 1: Federation](sp800-63c/media/federation.png)

**Figure 1: Federation**

Federation Protocol では, Subscriber, IdP, RP の3者間で三角形の関係がなりたつ.
プロトコルによっては, 異なるタイミングで異なる情報が各辺を流れることもある.
Subscriber は, 通常は Web Browser を通じて IdP, RP 双方とやり取りを行う.
RP と IdP の間のやりとりは, (Subscriber が関与するリダイレクト経由で) Front Channel で行われることもあれば, Back-channel で (Direct Connection を通じて) 行われることもあり, (暗号論的に保護された Self-contained Assertion などのように) パッケージ化された情報を通じて行われることもある.

<!-- In a federation protocol, a triangle is formed between the subscriber, the IdP, and the RP (Figure 1). Depending on the specifics of the protocol, different information passes across each leg of the triangle at different times. The subscriber communicates with both the IdP and the RP, usually through a web browser. The RP and the IdP communicate with each other, though this communication can happen over the front channel (through redirects involving the subscriber), over the back channel (through a direct connection), or via a packaged information bundle (such as a cryptographically protected and self-contained assertion). -->

Subscriber は IdP に対して何らかの Primary Credential を使って自身を認証し, その Authentication Event はネットワーク経由で RP に対して Assert される.
IdP はこのプロセスを通じて Subscriber に関する Attribute Statement を生成することも可能である.
この Attribute および Authentication Event は通常 Assertion を利用して RP に伝えられる. (Section 5 参照)

<!-- The subscriber authenticates to the IdP using some form of primary credential, and then that authentication event is asserted to the RP across the network. The IdP can also make attribute statements about the subscriber as part of this process. These attributes and authentication event information are usually carried to the RP through the use of an assertion (see section 5.). -->

RP と IdP とのやりとりは, Subscriber がトランザクションを行う IdP には明示される.
複数の RP とやりとりする IdP は Subscriber のトランザクションをプロファイリングすることも可能となる.
これは Federation 無しには不可能であったろう.
これは Subscriber の Privacy Interest にそぐわない形での Subscriber Tracking や Profile Information の利用につながりかねない.

<!-- The RP communication with the IdP reveals to the IdP where the subscriber is conducting a transaction. Communications from multiple RPs allow the IdP to build a profile of subscriber transactions that would not have existed absent federation. This aggregation could enable new capabilities for subscriber tracking and use of profile information that do not align with the privacy interests of the subscribers.  -->

IdP は RP 上での Subscriber のアクティビティを第三者に漏らすべきではなく (SHALL NOT), Federated Authentication 目的や法的手続き, 当該ユーザーからの要望による以外でそういった情報を利用すべきでもない (SHALL NOT).
IdP は Subscriber Tracking や Profiling を防止したり Unlinkability を確保するための技術的対策を行うべきである (SHOULD).

<!-- The IdP SHALL NOT disclose information on subscriber activities at an RP to any party, nor use the information for any purpose other than federated authentication, to comply with law or legal process, or in the case of a specific user request for the information. The IdP SHOULD employ technical measures to provide unlinkability and prevent subscriber activity tracking and profiling. -->

IdP は, Subscriber アカウントへの不正ログイン発生時など, セキュリティ目的であれば, Federation の範囲内で他の RP に Subscriber のアクティビティを公表することもできる (MAY).

<!-- A IdP MAY disclose information on subscriber activities to other RPs within the federation for security purposes such as communication of compromised subscriber accounts. -->

各機関には以下の要件が課せられる.

<!-- The following requirements apply specifically to agencies: -->

a) Senior Agency Official for Privacy と協議の上, Privacy Act の要件に照らして, 自身が Identity Federation において IdP となるか RP となるかを分析, 決定する (SHALL).

<!-- a) The agency SHALL consult with their Senior Agency Official for Privacy to conduct and analysis to determine whether the agency acting as either an IdP, or an RP in an identity federation triggers the requirements of the Privacy Act. -->

b) 適宜 System of Records Notice を公開, ないしは適用範囲を特定する (SHALL).

<!-- b) The agency SHALL publish, or identify coverage by a System of Records Notice as applicable. -->

c) Senior Agency Official for Privacy と協議の上, E-Government Act の要件に照らして, 自身が Identity Federation において IdP となるか RP となるかを分析, 決定する (SHALL).

<!-- c) The agency SHALL consult with their Senior Agency Official for Privacy to conduct an analysis to determine whether the agency acting as either an IdP, or an RP in an identity federation triggers the requirements of the E-Government Act. -->

d) 適宜 Privacy Impact Assessment を公開, ないしは適用範囲を特定する (SHALL).

<!-- d) The agency SHALL publish or identify coverage by a Privacy Impact Assessment, as applicable. -->

### 4.1. Federation Models

本セクションでは, 現在使われているいくつかの Identity Federation の一般的モデルを概観する.
これらのモデルでは, Federation 関係主体間の Trust 確立方法が複数種類存在する.
なかには高レベルの Trust を必須とするモデルもあり, 多様な Trust Relationship を認めるモデルもある.

<!-- This section provides an overview of a few common models of identity federation currently in use. In these models, trust is established between members of the federation in several different ways. Some models mandate that federated parties have a high level of trust. Other models allow for parties with a diversity of trust relationships. -->

#### 4.1.1 Central Authority

Central Authority に対する Trust を前提として, 相互に Trust を確立しメタデータのやりとりを行う Federated Party も存在する.
そういったモデルでは, Central Authority は Federation を行う各主体に対して一定レベルの審査を行い, Security および Integrity Standard に対する準拠を求めることが多い.

<!-- Some federated parties trust a central authority to make trust decisions for them and communicate metadata between parties. In this model, the central authority generally conducts some level of vetting on each party in the federation to verify compliance with predetermined security and integrity standards. -->

Central Authority モデルを用いた Federation の多くでは, Federation に参加しているか否かという単一レベルの Trust のみが存在する.
しかしながら, より洗練した Federation ではより細かな Trust レベルを持ち, より細かく徹底した審査を通過した主体やより高い Trust レベルを満たす主体を扱うことができる.
高レベルの Trust を実現できれば, そういった高レベルな主体に対しては情報を自動的に渡すといったことも可能になる.

<!-- Most federations using the central authority model have a single level of trust - either parties are in the federation or they are not. However, more sophisticated federations have multiple tiers of trust which can be used by federated parties to tell whether other parties in the federation have been more thoroughly vetted or have some common purpose that justifies a higher level of trust. This higher level of trust makes some parties in the federation more likely to automatically release information about their users to the parties in the higher tiers. -->

#### 4.1.2 Manual Registration

Manual Registration モデルでは, System Administorator がメタデータを扱い, システムの相互接続性をテストしたのち, 実際に User Transaction を開始させる.
Federation に参加する主体に関するメタデータは Federated Party のレジストリに手動入力される.
各主体は個別に自身がやりとりする相手を登録したレジストリを管理し, そのレジストリに登録されている相手とは Trust が確立されたとみなす.

<!-- In the manual registration model of federation, system administrators communicate metadata and test system interoperability before transactions take place between users over the wire. Metadata for each party who wishes to participate is manually input into a registry of federated parties. Each party maintains their own registry of other parties whom they have deemed trustworthy. -->

Manual Registration は, Authority や Federation Operator の関与無しに, 個別に行うことができる.
この場合, IdP と RP の間にはすでに Trust Relationship が確立されていることであろう.

<!-- Manual registration can take place on a case by case basis without any authority or federation operator in place. In this case, an existing pairwise trust relationship is generally already in place between the IdP and the RP. -->

Manual Registration は Central Authority モデルと合わせて利用することもできる.
その場合, Central Authority と Trust 関係にある主体を含んだレジストリが事前に構築され, それ以降は必要に応じて手動でのレジストリ登録が行われることになる.

<!-- Manual registration can work in concert with a central authority model. In this case, a registry is pre-populated with parties trusted by the central authority, and more parties are added manually on an as-needed basis. -->

#### <a name="dynamic-registration"></a> 4.1.3 Dynamic Registration

Dynamic Registration モデルでは, 各システムはその他のシステムが当該システムのメタデータを取得できるように well-known location エンドポイントを持つ.
また新しいシステムが人間の関与無しに自身を登録できるよう, 予測可能な形で API エンドポイントも提供する.
Dynamic Registration を使うシステムは, Subscriber に IdP 上で Identity Federation Transaction に対する明示的許可を要求するなど, 人間が関与する検証ステップを設けるべきである (SHOULD).

<!-- In the dynamic registration model of federation, systems have a well-known location where other systems can find their metadata. They also have predictable API endpoints where new systems can register themselves without human involvement. Systems that make use of dynamic registration SHOULD require verifiable human interaction, such as the approval of the identity federation transaction by the authenticated subscriber at the IdP. -->

Dynamic Registration モデルでは, 各主体は事前に相互の Trust を確立できないことが多く, デフォルトではあまり多くの情報をやりとりしないことが多い.
この問題は, Software Statement と呼ばれる技術を用いれば, ある程度改善される.
Software Statement とは, Dynamic Registration に関与した主体に関する属性を暗号論的に検証可能とするものである.
Software Statement は RP Software に関する属性のリストであり, 認証機関により暗号論的に署名されている.
認証機関を信頼する主体は, 認証機関に対する Trust を Dynamic Registration によって確立したパートナーシップに対しても拡張できる.
これにより Federated Party 間で Trust を確立したり強めたりすることができる.
詳細は [[RFC 7591]](#RFC7591) Section 2.3 を参照のこと.

<!-- Frequently, parties in a dynamic registration model have no way to trust each other ahead of time, so little information is exchanged by default. This problem is somewhat mitigated by a technology called software statements, which allow federated parties to cryptographically verify some attributes of the parties involved in dynamic registration. Software statements are lists of attributes describing the RP software, cryptographically signed by certifying bodies. Because both parties trust the certifying body, that trust can be extended to the other party in the dynamic registration partnership.  This allows trust to be established or elevated between the federating parties. See [[RFC 7591]](#RFC7591) section 2.3 for more information. -->

一定レベルの Trust を確保した状態で Dynamic Registration を利用可能な相手を Whitelist で管理する場合もある.
同時に, Blacklist を利用して, 低レベルの Trust 関係で Dynamic Registration をさせる相手を管理したり Dynamic Registration を禁止したりすることもある.
Whitelist や Blacklist にないものは "Glaylist" にあるものとみなされ, そういった主体は, 一般的に人間によるレビューを経るまで低レベルの Trust を強いられることになる.

<!-- Many federated parties establish whitelists of other federated parties who may dynamically register with some predetermined level of trust. They also establish blacklists of federated parties who may be allowed dynamically register with a low level of trust, or who may not be allowed to dynamically register at all. Everything that is not on a whitelist or a blacklist can be considered to be in a gray area or on a "graylist." Graylisted parties generally start out with a low level of trust until they can be reviewed by a human who can determine an appropriate level of trust. -->

#### 4.1.4 Proxied Federation

Proxied Federation Model では, IdP と RP は, 2者間の直接的コミュニケーションを禁止する形で Proxy される.
この実現方法は様々であるが, 一般的には "Federation Proxy" (or "Proxy") やネットワーク上の "node" として動作する第三者が介在することになる.

<!-- In a proxied federation model, the communication between the IdP and the RP is proxied in a way that prevents direct communication between the two parties. There may be multiple methods of achieving this effect, but common configurations include a third party that acts as a federation proxy (or "broker") or a network of "nodes" that distribute the communications.  -->

この介在者は片や Federation IdP として動作し, もう片方では Federation RP として動作する.
特に Federation Proxy は全ての Federated RP に対して IdP として動作し, 全ての Federated IdP に対して RP として動作する.
よって IdP および RP に適用される Normative Requirements は, 上記介在者にも同様に適用されるべきである (SHALL).

<!-- Effectively, the parties still function in some degree as a federation IdP on one side and a federation RP on the other side. Notably, a federation proxy acts as an IdP to all federated RPs and as an RP to all federated IdPs. Therefore, all normative requirements that apply to IdPs and RPs SHALL apply to the parties of such a system in their respective roles. -->

![Figure 2: Broker](sp800-63c/media/broker.png)

**Figure 2: Broker**

Proxied Federation Model は多様な利点を持つ.
例えば Federation Proxy は RP と IdP の間でインテグレーションが必要な箇所を削減することで技術的インテグレーションを単純化することもできる.
これは [Dynamic Registration](#dynamic-registration) をサポートしないプロトコルでは有効たりうる.
さらに, Proxied Federation Model は RP と IdP の双方を効果的に blind するため, Subscriber のリストをお互いに開示したくない組織にとってビジネス上の機密性を高める効果もある.
また同様に上述の Federation におけるプライバシーリスクを軽減する効果もある.

<!-- A proxied federation model can provide various benefits. For example, federation proxies can enable simplified technical integrations between the RP and IdP by eliminating the need for multiple point to point integrations, which can be onerous for protocols which do not support [dynamic registration](#dynamic-registration). Additionally, to the extent a proxied federation model effectively blinds the RP and IdP from each other, it can provide some business confidentiality for organizations that may not wish to reveal their subscriber lists to each other, as well as mitigate some of the privacy risks of point to point federation described above.  -->

追加のプライバシー保護策を提供しない実装もあれば, Blinding Technology によって多様なプライバシーレベルを提供する実装もある.
(注: Blinding Technology を利用したとしても, Blind された主体が Timestamp や Cookie, Attribute や Attribute Bundle のサイズなどを解析し, Subscriber の行動を推測することは可能である.)
Privacy Policy で IdP, RP, Federation Proxy による適切なデータ利用を宣言していたとしても, Blinding 技術はデータへのアクセス自体を困難にするため, より効率的である.
しかしながらBlinding レベルが上がると, それに比例して技術的・運用上の複雑度は上昇する.

<!-- While some proxied deployments offer no additional privacy protection (such as those that exist as integration points), others can offer varying levels of privacy to the subscriber through a range of blinding technologies. NOTE: even with the use of blinding technologies, it may still be possible for a blinded party to deduce subscriber behavior patterns through analysis of timestamps, cookies, attributes, or attribute bundle sizes. Privacy policies may dictate appropriate use by the IdP, RP, and the federation proxy, but blinding technology can increase effectiveness of these policies by making the data more difficult to access. It should also be noted that as the level of blinding increases, so does the technical and operational implementation complexity. -->

以下に Blinding 実装のパターンを挙げる.

<!-- The following list illustrates a spectrum of blinding implementations: -->

1. Federation Proxy は RP と IdP を相互に Blind しない. Federation Proxy は Subscriber と RP, IdP の関係性を監視・追跡可能であり, Assertion を通じてやりとりされるすべての属性を見ることができる.
<!-- 1. The federation proxy does not blind the RP and IdP from one another. The federation proxy is able to monitor and track all subscriber relationships between the RPs and IdPs, and has visibility into any attributes it is transmitting in the assertion. -->

2. Federation Proxy は RP と IdP を相互に Blind しない. Federation Proxy は Subscriber と RP, IdP の関係性を監視・追跡可能であるが, Assertion の中身を見ることはできない.
<!-- 2. The federation proxy does not blind the RP and IdP from one another. The federation proxy is able to monitor and track all subscriber relationships between the RPs and IdPs, but has no visibility into any attributes it is transmitting in the assertion. -->

3. Federation Proxy は RP と IdP を相互に Blind する. Federation Proxy は Subscriber と RP, IdP の関係性を監視・追跡可能であり, Assertion を通じてやりとりされるすべての属性を見ることができる.
<!-- 3. The federation proxy blinds the RP and IdP from each other. The federation proxy is able to monitor and track all subscriber relationships between the RPs and IdPs, and has visibility into any attributes it is transmitting in the assertion. -->

4. Federation Proxy は RP と IdP を相互に Blind する. Federation Proxy は Subscriber と RP, IdP の関係性を監視・追跡可能であるが, Assertion の中身を見ることはできない.
<!-- 4. The federation proxy blinds the RP and IdP from each other. The federation proxy is able to monitor and track all subscriber relationships between the RPs and IdPs, but has no visibility into any attributes it is transmitting in the assertion. -->

5. Federation Proxy は RP と CSP および Broker 自身を Blind する. Federation Proxy は一切の Subscriber の関係性を監視・追跡することができず, Assertion の中身を見ることもできない.
<!-- 5. The federation proxy blinds the RP, IdP, and itself. The federation proxy cannot monitor or track any subscriber relationships, and has no visibility into any attributes it is transmitting in the assertion. -->
