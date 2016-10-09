<a name="sec3"></a>

# 3. Definitions and Abbreviations

Authentication 分野で使われる用語は幅広く, 多くの用語は SP 800-63 との整合性を保っているものの, いくつかは本リビジョンから定義が変更になっている.
多くの用語に複数の定義がありうるため, 本ドキュメントにおける定義を明確にする必要がある.

<!-- There is a wide variety of terms used in the area of authentication. While the definitions of many terms are consistent with earlier versions of SP 800-63, some have changed in this revision. Since there is no single, consistent definition of many of these terms, careful attention to how the terms are defined here is warranted. -->

本セクションでは, 本ドキュメントで利用される用語の定義を行う.
SP 800-63 ドキュメント群のその他のドキュメントで利用される定義や略語は, それぞれのドキュメントにて定義する.

<!-- The definitions in this section are primarily those that are referenced in this document. Refer to the other documents in the SP 800-63 document family for additional definitions and abbreviations specific to their content. -->

#### Address of Record

許可された手段によって特定個人とのコミュニケーションに利用可能な, 有効かつ検証済の (物理的またはデジタルの) 場所情報.

<!-- The validated and verified location (physical or digital) where an individual can receive communications using approved mechanisms. -->

#### Applicant

登録および Identity Proofing のプロセスを受けている主体.

<!-- A party undergoing the processes of registration and identity proofing. -->

#### Assurance

[[OMB M-04-04]](#M-04-04) および本ドキュメントのコンテキストにおいては, Assurance とは 1) 当該 Credential を発行された個人の Identity を確立する審査プロセスにおける確からしさの度合い, および 2) 当該 Credential の提示者が当該 Credential の発行対象の個人と同一であることの確からしさの度合い, の2つを持って定義される.

<!-- In the context of [[OMB M-04-04]](#M-04-04) and this document, assurance is defined as 1) the degree of confidence in the vetting process used to establish the identity of an individual to whom the credential was issued, and 2) the degree of confidence that the individual who uses the credential is the individual to whom the credential was issued. -->

#### Asymmetric Keys

公開鍵と秘密鍵からなる鍵ペア.
暗号化と復号, 署名生成と署名検証など, 対となるオペレーションに用いられる.

<!-- Two related keys, consisting of a public key and a private key, that are used to perform complementary operations such as encryption and decryption or signature verification and generation. -->

#### Attack

認可を持たない個人が, Security Control を無効化する試み.
例えば Credential Service Provider を騙して正規の Subscriber として登録するなど.

<!-- An attempt by an unauthorized individual to defeat security controls. For example, to cause a credential service provider to register an impostor as the subscriber. -->

#### Attacker

不正な意図を持ち情報システムに不正アクセスする主体.

<!-- A party who acts with malicious intent to compromise an information system. -->

#### Attribute

人や物に関する生来の性質や特徴.

<!-- A quality or characteristic ascribed to someone or something. -->

#### Attribute Claim

Subscriber のプロパティをアサートする Statement.
Identity Information を含まなくても良く, フォーマットは問わない.
例えば "birthday" という属性に対して, "18歳以上" とか "12月生まれ" などが Attribute Claim となりうる.

<!-- A statement asserting a property of a subscriber without necessarily containing identity information, independent of format. For example, for the attribute 'birthday', a claim could be 'older than 18' or 'born in December'. -->

#### Attribute Value

Subscriber のプロパティをアサートする完全な Statement.
フォーマットは問わない.
例えば "birthday" という属性に対して, "12/1/1980" や "December 1, 1980" などが Attribute Value となりうる.

<!-- A complete statement asserting a property of a subscriber, independent of format. For example, for the attribute 'birthday', a value could be '12/1/1980' or 'December 1, 1980'. -->

#### Authentication

User や情報システムの Identity について確証を得るプロセス.

<!-- The process of establishing confidence in the identity of users or information systems. -->

#### Authentication Protocol

Claimant (要求者) が自身の Identity を確立するための正当な Authenticator を保持および制御していることを示す, Claimant と Verifier の間での一連のメッセージのやりとり.
セキュアな Authentication Protocol は, Claimant が正規の Verifier とやりとりしていることも明示する.

<!-- A defined sequence of messages between a claimant and a verifier that demonstrates that the claimant has possession and control of one or more valid authenticators to establish his/her identity. Secure authentication protocols also demonstrate to the claimant that he or she is communicating with the intended verifier. -->

#### Authenticator

Claimant が所有および管理するもので, 典型的な例としては暗号モジュールやパスワード等がある.
Authenticator は Claimant の Identity を認証するために用いられる.
SP 800-63 の前リビジョンにおいて *token* と呼ばれていたものと同等である.

<!-- Something that a claimant possesses and controls (typically a cryptographic module or password) that is used to authenticate the claimant’s identity. In previous editions of SP 800-63, this was referred to as a *token*. -->

#### Authenticity

データが意図された情報源から得られたものであるという性質.

<!-- The property that data originated from its purported source. -->

#### Authoritative Source

身分証 (Identity Evidence) に記載された情報の正当性を, その発行元 (Issuing Source) から十分な情報を得て確認することができる機関 (Authority).
Issuing Source 自身が Authoritative Source であることもありうる.

<!-- An authority that has access to sufficient information from an issuing source that they are able to confirm the validity of a piece of identity evidence. An issuing source may also be an authoritative source. -->

#### Biometrics

個人の行動や生体情報をもとに個人を自動認証すること.

<!-- Automated recognition of individuals based on their behavioral and biological characteristics. -->

本ドキュメントでは, Biometrics は Authenticator のアンロックや登録の否認防止目的で用いられることもある.

<!-- In this document, biometrics may be used to unlock authenticators and prevent repudiation of registration. -->

#### Claimant

1つ以上の Authentication Protocol により Identity を検証される主体.

<!-- A party whose identity is to be verified using one or more authentication protocols. -->

#### Claimed Address

ある個人 (Applicant 等) が, 自分に到達可能だと主張する物理的位置.
居住地の住所や郵便の届く住所などを含む.

<!-- The physical location asserted by an individual (e.g. an applicant) where he/she can be reached. It includes the residential street address of an individual and may also include the mailing address of the individual. -->

例えば, 外国籍のパスポートを所持している状態で米国に在住する人物であれば, Identity Proofing プロセスにおいて住所を要求されることになる.
そう言った場合の住所は, "address of record" ではなく "claimed address" となろう.

<!-- For example, a person with a foreign passport, living in the U.S., will need to give an address when going through the identity proofing process. This address would not be an “address of record” but a “claimed address.” -->

#### Credential

ある Identity (および付加的属性) を Subscriber が所有ないしは管理する Authenticator に紐付ける信頼の置けるオブジェクトもしくはデータ構造.

<!-- An object or data structure that authoritatively binds an identity (and optionally, additional attributes) to an authenticator possessed and controlled by a subscriber. -->

一般的に Credential は Subscriber に管理されることが想定されるが, 本ドキュメントでは Subscriber の Authenticator と Identity の紐付けを確立する CSP 管理下の電子レコードを指すこともある.

<!-- While common usage often assumes that the credential is maintained by the subscriber, this document also uses the term to refer to electronic records maintained by the CSP which establish a binding between the subscriber’s authenticator and identity. -->

#### Credential Service Provider (CSP)

Subscriber の Authenticator を発行もしくは登録し, Subscriber に電子的な Credential を発行する信頼された主体.
CSP は自身が運営する Verifier を内包することもある.
CSP は独立した第三者となることもあれば, 自身で発行した Credential を用いて自らサービスを提供することもある.

<!-- A trusted entity that issues or registers subscriber authenticators and issues electronic credentials to subscribers. The CSP may encompass verifiers that it operates. A CSP may be an independent third party, or may issue credentials for its own use. -->

#### Derived Credential

事前に発行済の Credential に紐づいた Authenticator を所有・管理していることを証明することで発行される Credential.
このような Credential を発行することで, 再び Identity Proofing プロセスを繰り返す必要がなくなる.

<!-- A credential issued based on proof of possession and control of an authenticator associated with a previously issued credential, so as not to duplicate the identity proofing process. -->

#### Digital Authentication

情報システムに対して, 電子的に表現されたユーザーの Identity の確からしさを確立するプロセス.
SP 800-63 では以前まで *Electronic Authentication* と呼ばれていたもの.

<!-- The process of establishing confidence in user identities electronically presented to an information system. In previous editions of SP 800-63, this was referred to as *Electronic Authentication*. -->

#### Digital Signature

秘密鍵を用いてデータに電子署名を行い, 公開鍵を用いて署名検証を行う, Asymmetric Key を用いたオペレーション.
Digital Signature は Authenticity Protection (真正性), Integrity Protection (完全性), Non-Repudication (否認防止) を提供するが, Confidentiality Protection (機密性) は提供しない.

<!-- An asymmetric key operation where the private key is used to digitally sign data and the public key is used to verify the signature. Digital signatures provide authenticity protection, integrity protection, and non-repudiation but not confidentiality protection. -->

#### Electronic Authentication (E-Authentication)

*Digital Authentication* 参照.

<!-- See *Digital Authentication*. -->

#### Enrollment

Applicant が CSP の Subscriber となるべく申し込み, RA が CSP の代理として Applicant の Identity を確認するプロセス.

<!-- The process through which an applicant applies to become a subscriber of a CSP and an RA validates the identity of the applicant on behalf of the CSP. -->

#### Identity

特定のコンテキストにおいてある人物を他と区別できるかたちで表現する属性の集合.

<!-- A set of attributes that uniquely describe a person within a given context. -->

#### Identity Proofing

CSP が Credential 発行のためにある人物に関する情報を収集および検証するプロセス.

<!-- The process by which a CSP collects and verifies information about a person for the purpose of issuing credentials to that person. -->

#### Issuing Source

身分証 (Identity Evidence) として利用可能なデータやドキュメントを責任を持って生成する Authority.

<!-- An authority that is responsible for the generation of data and/or documents that can be used as identity evidence. -->

#### Knowledge Based Verification

Private Database 内で当該個人の Claimed Identity と関連づけられている情報を知っていることを根拠とした Identity Proofing.
Knowledge Based Authentication (KBA) や Knowledge Based Proofing (KBP) とも呼ばれる.

<!-- Identity proofing of an individual based on knowledge of information associated with his or her claimed identity in private databases. This is often referred to as knowledge based authentication (KBA) or knowledge based proofing (KBP). -->

#### Network

オープンなコミュニケーションの伝達手段.
Internet がその代表例である.
Network は Claimant とその他の主体の間でメッセージを伝達するために用いられる.
特に明示されない限り, Network のセキュリティは前提とされず, オープンであり, 任意の主体 (Claimant, Verifier, CSP および RP) 間の任意の点において自発的な攻撃 (なりすまし, Man-in-the-Middle, Session Hijacking 等) や受動的な攻撃 (盗聴等) にさらされうるものと想定される.

<!-- An open communications medium, typically the Internet, that is used to transport messages between the claimant and other parties. Unless otherwise stated, no assumptions are made about the security of the network; it is assumed to be open and subject to active (i.e., impersonation, man-in-the-middle, session hijacking) and passive (i.e., eavesdropping) attack at any point between the parties (e.g., claimant, verifier, CSP or RP). -->

#### Personally Identifiable Information (PII)

OMB Circular A-130 で定義されているように, Personally Identifiable Information とは個人の Identity を識別したり追跡するために用いられる情報である.
単体の情報で個人を識別・追跡可能なものもあれば, 特定の個人に紐付け済もしくは紐付け可能なその他の情報と組み合わせることで識別・追跡可能となるものもある.

<!-- As defined by OMB Circular A-130, Personally Identifiable Information means information that can be used to distinguish or trace an individual's identity, either alone or when combined with other information that is linked or linkable to a specific individual. -->

#### Practice Statement

Authentication プロセスに関わる主体 (CSP, Verifier etc.) がプロセス実施の規範とする公式の規定.
通常, 各主体のポリシーや実施手法などが記載され, 法的拘束力を持つこともある.

<!-- A formal statement of the practices followed by the parties to an authentication process (i.e., CSP or verifier). It usually describes the policies and practices of the parties and can become legally binding. -->

#### Protected Session

2者間でやりとりされるメッセージを, Session Key と呼ばれる Shared Secret を用いて暗号化し, Integrity を保護するセッション.

<!-- A session wherein messages between two participants are encrypted and integrity is protected using a set of shared secrets called session keys. -->

当該セッション内で, ある主体が Session Key に加えて1つ以上の Authenticator を所有していることを証明し, もう一方の主体が当該 Authenticator に紐づく Identity を検証できる場合, 当該主体は *Authenticated* であると言う.
もし両主体が共に Authenticated となる場合, この Protected Session は *Mutually Authenticated* であると言える.

<!-- A participant is said to be *authenticated* if, during the session, he, she or it proves possession of one or more authenticators in addition to the session keys, and if the other party can verify the identity associated with the authenticator(s). If both participants are authenticated, the protected session is said to be *mutually authenticated*. -->

#### Pseudonym

実名 (Legal Name) 以外の名前.

<!-- A name other than a legal name. -->

#### Public Key

Asymmetric Key ペアの公開鍵.
データへの署名検証や暗号化に用いられる.

<!-- The public part of an asymmetric key pair that is used to verify signatures or encrypt data. -->

#### Remote

(*Remote Authentication や Remote Transaction といったコンテキストで*) 単一組織によるセキュリティ対策のみでは End-to-End での確実な保護が期待できないような状況下での, ネットワーク接続されたデバイス間の情報交換.

<!-- (*As in remote authentication or remote transaction*) An information exchange between network-connected devices where the information cannot be reliably protected end-to-end by a single organization’s security controls. -->

注) Internet を介した情報交換はすべて Remote とみなされる.

<!-- Note: Any information exchange across the Internet is considered remote. -->

#### Subscriber

CSP によって自身の Credential をある Authenticator に紐づけられる主体.

<!-- A party who has had their credential bound to an authenticator by a CSP. -->

#### Token

*Authenticator* 参照.

<!-- See *Authenticator*. -->

#### Token Authenticator

*Authenticator Output* 参照.

<!-- See *Authenticator Output*. -->

#### Token Secret

*Authenticator Secret* 参照.

<!-- See *Authenticator Secret*. -->

#### Trust Anchor

ハードウェアやソフトウェエアに直接埋め込まれていたり, Out-of-band な手法によりセキュアに提供されたりすることで Trust される, Public Key もしくは Symmetric Key.
他の Trusted Entity の保証を受けて Trust を得るものは Trust Anchor とは呼ばない (Public Key Certificate 等).

<!-- A public or symmetric key that is trusted because it is directly built into hardware or software, or securely provisioned via out-of-band means, rather than because it is vouched for by another trusted entity (e.g. in a public key certificate). -->

#### Valid

ある ID (身分証明書) について, それが期限切れや失効していないこと.

<!-- In reference to an ID, the quality of not being expired or revoked. -->

#### Virtual In-Person Proofing

Remote の Identity Proofing プロセスのうち, 物理的・技術的・手続き上の手段により Remote Session であっても物理的に対面 (In-person) の Identity Proofing と同等であると考えられるもの.

<!-- A remote identity person proofing process that employs physical, technical and procedural measures that provide sufficient confidence that the remote session can be considered equivalent to a physical, in-person identity proofing encounter. -->
