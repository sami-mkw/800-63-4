<a name="sec1"></a>

## 1. <a name="purpose"></a>Purpose

本リコメンデーションおよび SP 800-63A, SP 800-63B, SP 800-63C は, 政府機関に対して Digital Authentication の実装に際した技術的なガイドラインを提示する.

<!-- This recommendation and its companion documents, SP 800-63A, SP 800-63B, and SP 800-63C, provide technical guidelines to agencies for the implementation of digital authentication. -->

<a name="sec2"></a>

## 2. <a name="intro"></a>Introduction

Digital Authentication は, 情報システムに対して提示された User Identity の確からしさを確立するプロセスである.
ネットワーク越しに個人に対して Remote Authentication を行う場合, Digital Authentication は技術的なチャレンジに直面する.
本リコメンデーションは, 政府機関に技術的なガイドラインを提示し, 個人がリモートで Federal Information Technology (IT) システムに対して自身の Identity を認証できるようにする.
また同様に Credential Service Provider (CSP), Verifier, Relying Party (RP) に対するガイドラインも提示する.

<!-- Digital authentication is the process of
establishing confidence in user identities presented to
an information system. Digital authentication presents a technical challenge
when this process involves the remote authentication of individual
people over a network. This recommendation provides technical guidelines
to agencies to allow an individual person to remotely authenticate
his/her identity to a Federal Information Technology (IT) system. This
recommendation also provides guidelines for credential service providers
(CSPs), verifiers, and relying parties (RPs). -->

現在の政府システムは Authentication と Attribute Provider の機能を分離してはいないが, アプリケーションによってはこれらは異なる主体によって提供されることもありうる.
本ドキュメント群は Authenticator Assurance と Identity Assurance を異なる指標として扱い, それらの指標と全体の Level of Assurance とのマッピングを提示する.
これらの技術的なガイドラインは OMB のガイドラインである *E-Authentication
Guidance for Federal Agencies* \[[OMB M-04-04](#M-04-04)\] を補完し, NIST SP 800-63-1 および SP 800-63-2 を置き換えるものである.
OMB M-04-04 は, 誤った認証結果や Credential の誤用などによりもたらされる結果といった観点から, Level1 から Level4 まで4つの Level of Assurance を定義している.
なお Level1 が最低で Level4 が最高の Assurance Level となる.
この OMB のガイダンスでは, 誤った認証結果によりもたらされるであろう結果という観点から, 必要となる Level of Assurance を定義している.
より深刻な影響が想定されるほど, 必要となる Level of Assurance も高くなる.
OMB ガイダンスは, 政府機関に対して, 特定のデジタルトランザクションおよびシステムにおいて必要となる Level of Assurance を定めるための基準を提供している.
必要となる Level of Assurance は, リスクやその発生確率に基づいて求められる.

<!-- Current government systems do not separate the functions of
authentication and attribute providers. However, in some applications, these
functions are provided by different parties. This document suite describes authenticator assurance and identity assurance as separate metrics, and provides a mapping between these metrics and overall level of assurance.
These technical guidelines supplement OMB guidance, *E-Authentication
Guidance for Federal Agencies* \[[OMB M-04-04](#M-04-04)\] and
supersede NIST SP 800-63-1 and SP 800-63-2. OMB M-04-04 defines four levels of
assurance, Levels 1 to 4, in terms of the consequences of authentication
errors and misuse of credentials. Level 1 is the lowest assurance level
and Level 4 is the highest. The guidance defines the required level of
assurance in terms of the likely consequences of an
authentication error. As the consequences of an authentication error
become more serious, the required level of assurance increases. The OMB
guidance provides agencies with criteria for determining the level of
assurance required for specific digital transactions
and systems, based on the risks and their likelihood of occurrence. -->

SP 800-63 は以下のドキュメント群からなる.

<!-- SP 800-63 is organized as a suite of documents as follows: -->

- SP 800-63A *Enrollment and Identity Proofing* - Credential, および Credential に関連付けられた Authenticator を, 特定の個人に紐付けるプロセスを扱う. このプロセスは一般的に Identity システムに個人が登録される際に, Identity Proofing プロセスを通じて行われる.

<!-- - SP 800-63A *Enrollment and Identity Proofing* - Deals with the processes by which a credential, and authenticator(s) associated with that credential can be bound to a specific individual. This typically happens when that individual is enrolled in an identity system, through the identity proofing process. -->

- SP 800-63B *Authentication and Lifecycle Management* - 情報システムに対して Remote の Subscriber を特定の Authenticator Assurance Level で認証する際の, Authenticator (以前は *token* と呼ばれていた) の選択, 利用, 管理に関するガイドラインを提供する.

<!-- - SP 800-63B *Authentication and Lifecycle Management* - provides guidelines on the selection, use, and management of authenticators (formerly called *tokens*) to authenticate a remote subscriber to an identity system at specified authenticator assurance levels. -->

- SP 800-63C *Federation and Assertions* - Authentication Process の結果を Relying Party に伝搬する際の Assertion の利用に関するガイドラインを提供する.

<!-- - SP 800-63C *Federation and Assertions* - Provides guidelines on the use of assertions to convey the results of authentication processes to a relying party. -->

SP 800-63A, SP 800-63B, SP 800-63C は今後非同期に改定されることが予想されるが, 各々の最新リビジョンを用いることとする.

<!-- It is anticipated that SP 800-63A, SP 800-63B, and SP 800-63C will be revised asynchronously with each other and with this document. The latest revision of each should be used. -->

OMB ガイダンスは政府機関が Authentication Assurance 要件を満たすために以下の5つのステップからなるプロセスを用いるよう述べている.

<!-- OMB guidance outlines a five-step process by which agencies should meet
their authentication assurance requirements: -->

1.  *Conduct a risk assessment of the government system* – 特別なリスクアセスメントの手法が規定されているわけではないが, NIST Special Publication (SP) 800-30 [[SP 800-30]](#SP800-30) はリスクアセスメントとリスク軽減策のための一般的なプロセスを提示している.
また NIST Special Publication (SP) 800-37 Revision 1 [[SP 800-37]](#SP800-37) は, 組織全体に渡る情報セキュリティ対策の一環として, 情報システムに対するセキュリティ管理策の選択や利用可能な標準仕様に関するガイドラインを提示している.
本ガイドラインは情報システムにおける処理に関与する組織や個人に対するリスクの特定の一助となるであろう.
<!-- 1.  *Conduct a risk assessment of the government system* – No specific
    risk assessment methodology is prescribed for this purpose;
    however, NIST Special
    Publication (SP) 800-30 [[SP 800-30]](#SP800-30) offers a general
    process for risk assessment and risk mitigation, and NIST Special Publication (SP) 800-37 Revision 1 [[SP 800-37]](#SP800-37) provides guidelines on the selection and specification of security controls for an information system as part of an organization-wide information security program. This guideline supports the identification of risk to the organization or to individuals associated with the operation of an information system. -->

2.  *Map identified risks to the appropriate assurance level* – OMB M-04-04 の Section 2 は各機関がリスクに見合った Assurance Level のマッピングを行うために必要なガイダンスを提供している.
<!-- 2.  *Map identified risks to the appropriate assurance level* – Section
    2.2 of OMB M-04-04 provides the guidance necessary for agencies to
    perform this mapping. -->

3.  *Select technology based on digital authentication technical guidance* – 適切な Assurance Level を決定したら, OMB ガイダンスに従い各機関は本ドキュメント群が指定する技術要件に見合う技術を選択すべきである.
機関によっては既存の Digital Authentication 技術を所有しているものもあるであろう.
その場合, 各機関は既存技術が本ドキュメント群が指定する要件に適合するか検証を行うべきである.
<!-- 3.  *Select technology based on digital authentication technical guidance* –
    After the appropriate assurance level has been determined, OMB
    guidance states that agencies should select technologies that meet
    the corresponding technical requirements, as specified by
    this document suite. Some agencies may possess existing
    digital authentication technology. Agencies should verify that any
    existing technology meets the requirements specified in
    this document suite. -->

4.  *Validate that the implemented system has met the required assurance
    level* – 実装上の問題によりその実装特有のリスクを生み出す可能性もあることから, 各機関は当該システムがユーザーと当該機関との間の一連のプロセスに渡って要求される Assurance Level を満たしているかどうか, 最終確認を行うべきである.
    NIST SP 800-53A [[SP 800-53A]](#SP800-53A) はこの検証プロセスにおける実装済システムのアセスメントに関するガイドラインを提供している.
    この検証は NIST SP 800-37, Revision 1 [[SP 800-37]](#SP800-37) に記述されている Security Authorization プロセスの一環として行われるべきである.
<!-- 4.  *Validate that the implemented system has met the required assurance
    level* – As some implementations may create or compound particular
    risks, agencies should conduct a final validation to confirm that
    the system achieves the required assurance level for the
    user-to-agency process. NIST SP 800-53A [[SP 800-53A]](#SP800-53A)
    provides guidelines for the assessment of the implemented system
    during the validation process. Validation should be performed as
    part of a security authorization process as described in NIST SP
    800-37, Revision 1 [[SP 800-37]](#SP800-37). -->

5.  *Periodically reassess the information system to determine
    technology refresh requirements* – 各機関は情報システムに関する定期的な再アセスメント行い, Identity Authentication に関する要件が引き続き満たされているかを確認すべきである.
    NIST SP 800-37, Revision 1 [[SP 800-37]](#SP800-37) は, 定期的な再アセスメントに関する頻度, 深さ, 広さについてのガイドラインを提供している.
    また, 最初の検証プロセス同様, セキュリティアセスメントに関しては SP 800-53A [[SP 800-53A]](#SP800-53A) に示されたアセスメントガイドラインに従うこと.
<!-- 5.  *Periodically reassess the information system to determine
    technology refresh requirements* – The agency shall periodically
    reassess the information system to ensure that the identity
    authentication requirements continue to be satisfied. NIST SP
    800-37, Revision 1 [[SP 800-37]](#SP800-37) provides guidelines on
    the frequency, depth and breadth of periodic reassessments. As with
    the initial validation process, agencies should follow the
    assessment guidelines specified in SP 800-53A [[SP
    800-53A]](#SP800-53A) for conducting the security assessment. -->

本ドキュメント群は上記プロセスの Step 3 の実装に対するガイドラインを提供する.
特に本ドキュメントは OMB M-04-04 が定義する4段階の Level of Assurance を対応する Authenticator Assurance Level および Identity Assurance Level にマッピングしている.
また本ドキュメント群の他のドキュメントは, 下記のようなエリアに関する Identity Assurance および Authenticator Assurance 固有の技術要件に関して言及している.

<!-- This suite of documents provides guidelines for implementing the third step of the
above process. In particular, this document maps the four (4) Levels of Assurance defined in OMB M-04-04 into corresponding authenticator assurance and identity assurance levels. Other documents in the suite state specific technical
requirements for identity assurance and authenticator assurance in the following
areas: -->

- Identity Proofing および Applicant の登録 (SP 800-63A)

<!-- -   Identity proofing and registration of applicants (covered in SP 800-63A) -->

- Credential Lifecycle および Credential Management 方式 (SP 800-63A)

<!-- -   Credential lifecycle and management mechanisms (covered in SP 800-63A) -->

- 認証に用いる Authenticators (一般には暗号鍵やパスワードなど) (SP 800-63B)

<!-- -   Authenticators (typically a cryptographic key or password) for
    authentication (covered in SP 800-63B) -->

- Authenticator Lifecycle および Authenticator Management 方式 (SP 800-63B)

<!-- -   Authenticator lifecycle and management mechanisms (covered in SP 800-63B) -->

- Claimant と Verifier の間の認証のために利用できるプロトコル (SP 800-63B)

<!-- -   Protocols used to support the authentication mechanism between the
    claimant and the verifier (covered in SP 800-63B) -->

- Remote Authentication の認証結果を他の主体とやりとりするための Assertion 方式 (SP 800-63C).

<!-- -   Assertion mechanisms used to communicate the results of a remote
    authentication if these results are sent to other parties (covered
    in SP 800-63C). -->

M-04-04 Level of Assurance は, 上記の各要素に対して達成された Identity Assurance Level, Authenticator Assurance Level, Federation Assurance Level を考慮した上で, 全要素を満たすものとして決定される.

<!-- The M-04-04 Level of Assurance is determined by considering the identity assurance level, authenticator assurance level, and federation assurance level achieved for each of the elements listed above, and determining the Level of Assurance satisfied by all elements. -->

設定された Level of Assurance の範囲内で, 各機関は追加のリスク緩和策と補完コントロール (補完統制) を行ってもよい.
Credential Assurance Level を緩和することで, サービス利用可能顧客を増やすこともできる.
ただしその場合でも, 各機関はシステムに設定した Assurance Level が意図しているセキュリティおよびプライバシーレベルを保証すること.
また, センシティブな情報を扱わない機能に関しては低い Level of Authentication および Level of Attribute Assurance を許容しつつ, センシティブな情報を扱う時にはより高い Level of Assurance を要求するといったように, Digital Authentication を行うアプリケーションを機能ごとに分割することもできる.

<!-- Within a given level of assurance, agencies may employ additional risk mitigation measures and compensating controls. Easing credential assurance level requirements may result in benefits such as
increasing the size of the enabled customer pool, but agencies shall
ensure mitigations and compensating controls do not degrade the intended security and privacy of the selected assurance levels. Alternatively, agencies may consider partitioning the
functionality of a digital authentication enabled application to allow less
sensitive functions to be available at a lower level of authentication
and attribute assurance, while more sensitive functions are available
only at a higher level of assurance. -->

これらの技術ガイドラインはネットワーク経由の IT システムに対する Remote Digital Authentication をカバーしているが, 対面による認証に関しては言及しない.
例えばある建物への入館時等にリモート利用可能な Credential や Authenticator を Local Authentication に用いることもあるが, そういったユースケースは対象外である.
当技術ガイドラインは,　認証プロトコルに関与する連邦の IT システムおよびサービスプロバイダーが Subscriber を認証する際の要件をまとめている.
しかしながら Machine-to-Machine (Router-to-Router 等) の Authentication などには言及しない.
また人間を相手にする Authentication Protocol において Machine や Server に対して Authentication Credential や Authenticator を発行するといったことも対象外である.

<!-- These technical guidelines cover remote digital authentication of
human users to IT systems over a network. They do not address the
authentication of a person who is physically present, for example, for
access to buildings, although some credentials and authenticators that are used
remotely may also be used for local authentication. These technical
guidelines establish requirements that Federal IT systems and service
providers participating in authentication protocols be authenticated to
subscribers. However, these guidelines do not specifically address
machine-to-machine (such as router-to-router) authentication, or
establish specific requirements for issuing authentication credentials
and authenticators to machines and servers when they are used in
authentication protocols with people. -->

本ドキュメント群の枠組みにおいては, 個人を登録し, Authenticator を発行し, 個人の Identity を Authenticator に紐付けることで Registration プロセスを実施することになる.
その後個人は Authentication Protocol に基づいて Authenticator を用いてシステムやアプリケーションに対してネットワーク経由でリモート認証を行う.
この Authentication Protocol は, Authenticator Secret が様々な種類の攻撃から守られた状態で, 当該本人が Authenticator を所持および管理していることを Verifier に提示できるようなものである.
より高い Authenticator Assurance Level では, より強固な Authentication Mechanism, より良い Protocol, より高度な Authenticator および関連する鍵の保護策が必要となる.
より高い Identity Assurance Level では, より強固な Registration 手続きが要求される.

<!-- The paradigm of this document suite is that individuals are enrolled, issued an authenticator, and
undergo a registration process in which their identity is bound to that authenticator. Thereafter, the individuals are remotely authenticated to systems
and applications over a network, using the authenticator in an authentication
protocol. The authentication protocol allows an individual to
demonstrate to a verifier that he or she has possession and control of
the authenticator, in a manner that protects the authenticator secret from
compromise by different kinds of attacks. Higher authenticator assurance levels require use of stronger authentication mechanisms, better protocols, and better protection of
the authenticator(s) and related secrets from attacks. Higher identity assurance levels require stronger registration procedures. -->

本ドキュメント群は, 認可を受けていない主体にはアクセスできないような鍵を含み, 簡単には偽造できないような Authenticator にフォーカスしている.
また本ドキュメント群が対象としている以外のコンテキストでは, この Authenticator を利用しないことが望ましい.
Biometrics Authentication は人間の特徴を利用するものであり, それは攻撃者にも利用可能な場合がある.
したがって, Authentication 目的での Biometrics の利用は, 特別な物理 Authenticator のアクティベーションに限定する.
また, そういった Authenticator は, Biometrics が強固に紐づけられ, 許容される連続アクティベーション失敗回数が制限されており, それを超えるとその他のアクティベーション要素や Authenticator が必要となるものとする.
本ドキュメント群は, 登録の否認防止, および登録プロセスの全フェーズにおいて同一人物が関与していることの検証の目的でも, Biometrics の利用をサポートする.

<!-- This document suite focuses on authenticators that are difficult to forge because they contain some type of secret information that is not available to unauthorized parties and that is preferably not used in unrelated contexts. Biometric authentication uses human characteristics that in some cases may be available to an attacker. Accordingly, the use of biometrics for authentication is limited to activation of a specific physical authenticator to which it is strongly bound, and the number of consecutive activation failures is limited, beyond which another activation factor or authenticator is required. This document suite also supports the use of biometrics to prevent repudiation of registration, and to verify that the same individual participates in all phases of the registration process. -->

Knowledge Based Authentication では, パブリックなデータベースに対して当該個人の知識をチェックすることになる.
この情報はプライベートであると考えられるが, 実際には秘匿情報ではなく, 当該個人の Identity に関する確証を得ることは困難たりうる.
また Knowledge Based Authentication システムの複雑さと相互依存性は定量化が困難である.
しかしながら Knowledge Based Verification の技術は本ドキュメント群の Registration の一部として含まれている.

<!-- Knowledge based authentication achieves authentication by testing the
personal knowledge of the individual against information obtained from
public databases. As this information is considered private but not
actually secret, confidence in the identity of an individual can be hard
to achieve. In addition, the complexity and interdependencies of
knowledge based authentication systems are difficult to quantify.
However, knowledge based verification techniques are included as part
of registration in this document suite. -->

本ドキュメント群は Remote Authentication のための最低限の技術要件を特定するものである.
各機関はそれぞれのリスク分析に基づいて特定コンテキストにおいて適切な追加対策を行ってもよい.
特にプライバシー要件とリーガルリスクは, 各機関が Authentication やその他のプロセスにおける追加の保護策の採用を決める要因となりうる.
Digital Authentication のプロセスおよびシステムを構築するにあたって, 各機関は *OMB Guidance for Implementing the Privacy Provisions of the E-Government Act of 2002* \[[OMB M-03-22](#M-03-22)\] を参照すべきである.
*Guide to Federal Agencies on Implementing Electronic Processes* \[[DOJ 2000](#DOJ2000)\] は, *Use of Electronic Signatures in Federal Organization Transactions* \[[GSA ESIG](#GSAESIG)\] と同様に, リーガルリスクに関する追加情報として, 特に Legal Standards of Proof を満たし否認を防止するのに必要な要件を提供する.

<!-- This document suite identifies minimum technical requirements for remotely
authenticating users. Agencies may determine based on their risk
analysis that additional measures are appropriate in certain contexts.
In particular, privacy requirements and legal risks may lead agencies to
determine that additional authentication measures or other process
safeguards are appropriate. When developing digital authentication processes
and systems, agencies should consult *OMB Guidance for Implementing the
Privacy Provisions of the E-Government Act of 2002* \[[OMB
M-03-22](#M-03-22)\]. See the *Guide to Federal Agencies on
Implementing Electronic Processes* \[[DOJ 2000](#DOJ2000)\] for
additional information on legal risks, especially those that are related
to the need to satisfy legal standards of proof and prevent repudiation,
as well as *Use of Electronic Signatures in Federal Organization
Transactions* \[[GSA ESIG](#GSAESIG)\]. -->

さらに, 本ガイドラインを実装する連邦政府機関は, Title III of the E-Government Act (*Federal Information Security Management Act* \[[FISMA](#FISMA)\]), および関連する NIST 標準 & ガイドラインの要件に準拠すべきである.
FISMA は, 各政府機関に対して, 当該機関のオペレーションおよびアセットを支える情報および情報システムにおける情報セキュリティを確保する機関全体を通したプログラムの開発, 記録, 実装を要求する.
Digital Authentication をサポートする IT システムにおける Security Authorization も対象に含む.
連邦政府機関以外がこれらのガイドラインを実装する場合も, Security Management, Certification, Accreditation (適格性認定) に関する同等の基準に従い, Digital システムにおけるセキュアなオペレーションを保障すべきである.

<!-- Additionally, Federal agencies implementing these guidelines should
adhere to the requirements of Title III of the E-Government Act,
entitled the *Federal Information Security Management Act*
\[[FISMA](#FISMA)\], and the related NIST standards and guidelines.
FISMA directs Federal agencies to develop, document, and implement
agency-wide programs to provide information security for the information
and information systems that support the operations and assets of the
agency. This includes the security authorization of IT systems that support
digital authentication. It is recommended that non-Federal entities
implementing these guidelines follow equivalent standards of security
management, certification and accreditation to ensure the secure
operations of their digital systems. -->

### 2.1. How to Use this Suite of Special Publications

初期の Special Publication 800-63 がリリースされた頃と比較すると, ビジネスモデル, マーケットプレイス, Identity Service の提供形態などは大幅に変化している.
特に CSP は, 異なるビジネス主体によって独立して運用・管理されたコンポーネントの組み合わせとして実現されるようになった.
また Identity Proofing が不要なケースでも, 強固な Authenticator を利用するメリットが明らかになってきてもいる.
こういった背景から, これらの新しいモデルを促進し, 全体の Digital Authentication モデルの特定の機能要素に求められる固有の要件に容易にたどり着けるように, 800-63 以下の一連の Special Publication が作成されたのである.
各ドキュメントは独立しているが, すべての CSP は (たとえコンポーネント化されていても) [SP 800-63A](sp800-63a.html) および [SP 800-63B](sp800-63b.ja.html) への準拠が求められている.
CSP が Identity Federation をサポートする場合には, [SP 800-63C](sp800-63c.ja.html) もその要件となる.
なお, Standaline の CSP よりも Identity Federation をサポートする CSP が好まれることを注記しておく.

<!-- The business model, marketplace, and the composition of the way identity services are delivered has drastically changed since initial versions of Special Publication 800-63 were released.  Notably, CSPs can be componentized and composed of multiple independently operated and owned business entities.  In addition, there is a significant benefit to provide strong authenticators even if no identity proofing is required.  Therefore, a suite of special publications under the 800-63 moniker has been created to facilitate these new models and make it easy to access the specific requirements for the function an entity may serve under the overall digital authentication model.  Each document stands alone.  However, it is expected that all CSPs, even componentized, will be required to meet the guidelines in [SP 800-63A](sp800-63a.html) and [SP 800-63B](sp800-63b.html).  If the CSP also participates in an identity federation, which is preferred over a standalone CSP, meeting the requirements of [SP 800-63C](sp800-63c.html) will apply. -->

### 2.2. Relationship to Other Standards and Guidelines

本ドキュメントは連邦政府機関のニーズに合わせて記述されている.
しかしながら, 市民サービスが世界中に広がり, Identity Assurance および Authentication Assurance への要求が拡大する中, 国際的な Identity Federation や相互接続性を促進させるようなユースケースも増大している.
よって, 国家的ないしは国際的な Level of Identity Assurance の標準を確立することも, 本ガイドラインの目的となる.
[Table 2-1](#63Sec2-Table1) provides a representative snapshot of mappings to various international and national assurance documents.
[Table 2-1](#63Sec2-Table1) は多くの国家的・国際的な Assurance ドキュメントとの代表的なマッピングを示している.
IAL および AAL と国家的・国際的な様々な標準との間の直接的な相関があるわけでは無いが, 本ドキュメントはそういった標準が明示する基準を満たすものとなろう.

<!-- This document has been written to satisfy the needs of federal agencies. However, with the expansion of citizen services throughout the world that require identity and authentication assurance, as well as an increasing number of use cases that promote international identity federation and interoperability, this guideline is intended to achieve alignment to national and international standards that describe levels of identity assurance. [Table 2-1](#63Sec2-Table1) provides a representative snapshot of mappings to various international and national assurance documents. This is not meant to imply that there is direct correlation between the IALs and AALs in this document and the levels in those standards, but that it is seen that this document fulfils the criteria as demonstrated in those standards. -->

<a name="63Sec2-Table1"></a>

<div class="text-center" markdown="1">

**Table 2-1.  800-63 Mapping to Other Standards and Guidelines**

</div>

SP 800-63|[[GPG 45]](#GPG45)|[[RSDOPS]](#RSDOPS)|STORK 2.0|29115:2011|ISO 29003|Government of Canada
:---------:|:----:|:----:|:-------:|:--------:|:-------:|:------------------:
N/A|N/A|Level 01|N/A|N/A|N/A|N/A
AAL/IAL 1|Level 1|Level 1|QAA Level 1|LoA 1|LoA 1|IAL/CAL 1
AAL/IAL 1|Level 2|Level 2|QAA Level 2|LoA 2|LoA 2|IAL/CAL 2
AAL/IAL 2|Level 3|Level 3|QAA Level 3|LoA 3|LoA 3|IAL/CAL 3
AAL/IAL	 3|Level 4|N/A2|QAA Level 4|LoA 4|LoA 4|IAL/CAL 4

### 2.2. Change History

#### 2.2.1. SP 800-63-1

NIST SP 800-63-1 は NIST SP 800-63 の更新版として, 当時の Authenticator (Token) 技術を反映し, Digital Authentication アーキテクチャモデルの理解をより深めるべく再構成されたものである.
また同時に追加の (かつ最小限の) 技術要件が, CSP, 認証情報伝送用のプロトコル, (利用する場合は) Assertion に対して要求されている.
その他の NIST SP 800-63 からの変更点は以下の通りである.

<!-- NIST SP 800-63-1 updated NIST SP 800-63 to reflect current authenticator (then referred to as token)
technologies and restructured to provide a better understanding of the
digital authentication architectural model used here. Additional (minimum)
technical requirements were specified for the CSP, protocols utilized to
transport authentication information, and assertions if implemented
within the digital authentication model. Other changes to NIST SP 800-63
included: -->

- 従来の Token タイプに対する専門用語の変更や, Pre-registered Knowledge Token や Look-up Secret Token, Out-of-band Token 等のより多種多様な Token タイプへの言及.
<!-- -   Recognition of more types of tokens, including pre-registered
    knowledge token, look-up secret token, out-of-band token, as well
    as some terminology changes for more conventional token types; -->

- Assertion Protocol と Kerberos に対する詳細な要求.
<!-- -   Detailed requirements for assertion protocols and Kerberos; -->

- Token and Credential Management という新たなセクション.
<!-- -   A new section on token and credential management; -->

- パスワードエントロピーと Throttling に関するよりシンプルなガイドライン.
<!-- -   Simplification of guidelines for password entropy and throttling; -->

- Federal IT システムを対象としたドキュメントであることの強調.
<!-- -   Emphasis that the document is aimed at Federal IT systems; -->

- Figure 1 に示す連邦 IT システムにおけるシンプルなモデル以外のより幅広い Digital Authentication モデル, Assertion モデル, Proxy モデルなどへの言及. (Figure 6 参照)
<!-- -   Recognition of different models, including a broader
    digital authentication model (in contrast to the simpler model common
    among Federal IT systems shown in Figure 1) and an additional
    assertion model, the Proxy Model, presented in Figure 6; -->

- Table 12 における Level 3 と Level 4 の差異の明確化.
<!-- -   Clarification of differences between Levels 3 and 4 in Table 12; and -->

- 既存の Credential を利用して新たな Credential を発行するための新たなガイドライン.
<!-- -   New guidelines that permit leveraging existing credentials to issue
    derived credentials. -->

NIST SP 800-63-1 では, それ以外にも RA, CSP, Verifier, RP のそれぞれに関するセキュアな実装のための一連の Recommendation を提示している.
なお, これら一連の要素の全てがそれぞれセキュアに実装されて初めて, 必要とされる Level of Assurance を実現できることに注意すること.
したがって NIST SP 800-63-1 では以下のような想定がなされている.

<!-- The subsequent sections of NIST SP 800-63-1 presented a series of
recommendations for the secure implementation of RAs, CSPs, Verifiers,
and RPs. It should be noted that secure implementation of any one of
these can only provide the desired level of assurance if the others are
also implemented securely. Therefore, the following assumptions were
made in NIST SP 800-63-1: -->

- RA, CSP, Verifier はそれぞれ Trusted Entity である. これら Trusted Entity を実装する各機関は, それらがインタラクションを行うその他の Trusted Entity も同様に, 必要とされる Security Level を満たすよう適切に実装されていることに確証を持っている.
<!-- -   RAs, CSPs, and Verifiers are trusted entities. Agencies implementing
    any of the above trusted entities have some assurance that all other
    trusted entities with which the agency interacts are also
    implemented appropriately for the desired security level. -->

- RP は Trusted Entity とはみなされないが, 認証システムによっては, Verifier が RP との関係性を維持し, セキュアコミュニケーションを推進して RP が責任を持って動作できるときにのみ本来の価値を発揮できるよう, なんらかの Security Control を行う場合もある. また Subscriber は, RP が要求されたサービスを適切に提供し, 関連する Privacy Policy に従うであろうと信頼している.
<!-- -   The RP is not considered a trusted entity. However, in some
    authentication systems the Verifier maintains a relationship with
    the RP to facilitate secure communications and may employ security
    controls which only attain their full value when the RP
    acts responsibly. The subscriber also trusts the RP to properly
    perform the requested service and to follow all relevant
    privacy policy. -->

- Certification のプロセスによって, 各機関が自分自身が実装した Trusted Entity 以外に対しても, 上記の各項目に対する確証を得ることができる.
<!-- -   It is assumed that there exists a process of certification through
    which agencies can obtain the above assurance for trusted entities
    which they do not implement themselves. -->

- Trusted Entity は当該ドキュメントの推奨にしたがって適切に実装され, 悪意を持って不正を働かない.
<!-- -   A trusted entity is considered to be implemented appropriately if it
    complies with the recommendations in this document and does not
    behave maliciously. -->

- Trusted Entity は悪意を持って不正を働かないと想定されるが, 当該ドキュメントには Trusted Entity の悪意や過失によってもたらされるダメージを低減・分離するための Recommendation も含まれている.
<!-- -   While it is generally assumed that trusted entities will not behave
    maliciously, this document does contain some recommendations to
    reduce and isolate any damage done by a malicious or negligent
    trusted entity. -->

#### 2.2.2. SP 800-63-2

NIST SP 800-63-2 は Special Publication 800-63-1 の限定的なアップデートであり, 実質的な変更点は Section 5 *Registration and Issuance Processes* に限定されていた.
これらの変更は Identity Proofing プロセスにおける Professional Credential の利用推進を目的としており, Level 3 の Remote Registration において Credential 発行のために当該住所に対して郵便を送る必要性を低減することを目的としていた.
Section 5 に対するその他の変更は軽微である.

<!-- NIST SP 800-63-2 was a limited update of Special Publication 800-63-1 and
substantive changes were made only in section 5. *Registration and
Issuance Processes*. The substantive changes in the revised draft were
intended to facilitate the use of professional credentials in the
identity proofing process, and to reduce the need to use postal mail to
an address of record to issue credentials for level 3 remote
registration. Other changes to section 5 were minor explanations and
clarifications. -->

#### 2.2.3. SP 800-63-3

NIST SP 800-63-3 では, Special Publication 800-63-2 に対して大幅な改定と再構成を行っている.
本リビジョンでは Authenticator Assurance Level, Identity Assurance Level および Federation Assurance Level という概念を導入し, 認証強度と Claimant の Identity に関する確度を分離して扱いたいというニーズ (例えば仮名を使った強固な認証等) の高まりに答えている.
また同時に単一のドキュメントであったものを, SP 800-63-3 を最上位とした4つのドキュメント群に分割している.

<!-- NIST SP 800-63-3 is a substantial update and restructuring of Special Publication 800-63-2. It introduces the concepts of authenticator assurance level, identity assurance level, and federation assurance level to support the growing need for independent treatment of authentication strength and confidence in the claimant's identity (for example, in strong pseudonymous authentication). It also moves from a single document describing authentication to a suite of four documents, of which SP 800-63-3 is the top-level document. -->

SP 800-63-2 からのその他の変更は以下の通りである.

<!-- Other areas of update to SP 800-63-2 include: -->

- Assertion 技術における *Token* という用語との混同を防ぐため, 従来の *Token* という用語を *Authenticator* に置き換え.
- Security 技術および脅威の拡大に対応すべく, Authentication および Assertion に関する要件を更新.
- Verifier に対する長期間有効な Secret の保存に関する要件の追加.
- Identity Proofing モデルの再構成.
- "something you have" として利用されるチャネルおよびデバイスとしては, 独立したものを利用することという要件の明確化.
- Pre-registered Knowledge Token (Authenticator) は (往々にして弱い) パスワードの特別な形態であるという認識のもと, Pre-registered Knowledge Token を関する記述の削除.
- Authenticator を紛失したり盗難にあったりした場合における Account Recovery に関する要件の追加.
- Reauthentication および Session Management に関するさらなる議論.
- Identity Federation に関するさらなる議論. Federation コンテキストにおける Assertion の再構成.

<!-- -	Terminology changes, primarily the use of *authenticator* in place of *token* to avoid conflicting use of the word *token* in assertion technologies
-	Updates to authentication and assertion requirements to reflect advances in both security technology and threats
-	Requirements on the storage of long-term secrets by verifiers
-   Restructured identity proofing model
-	Updated requirements regarding remote identity proofing
-	Clarification on the use of independent channels and devices as “something you have”
-	Removal of pre-registered knowledge tokens (authenticators), with the recognition that they are special cases of (often very weak) passwords.
-	Requirements regarding account recovery in the event of loss or theft of an authenticator
-   Expanded discussion of reauthentication and session management
-   Expanded discussion of identity federation; restructuring of assertions in the context of federation -->
