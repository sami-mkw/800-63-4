<a name="sec3"></a>

## 3. Definitions and Abbreviations

Authentication のエリアでは数多くの用語定義がなされている.
その多くは前リビジョンの SP 800-63 と一貫性が保たれているが, いくつかについては本リビジョンで改定がなされている.
こういった用語の多くには, 一貫した単一の定義はなく, 個々の定義に注意深く注目することが望まれる.

<!-- There are a variety of definitions used in the area of authentication. While many terms are consistent with earlier revisions version of SP 800-63, some have changed in this revision. Since there is no single, consistent definition of many of these terms, careful attention to how the terms are defined here is warranted. -->

本セクションで定義される用語は, 主に本ドキュメントで参照されるものである.
その他の定義や略語については, 他の SP 800-63 ドキュメント群を参照のこと.

<!-- The definitions in this section are primarily those that are referenced in this document. Refer to the other documents in the SP 800-63 document family for additional definitions and abbreviations specific to their content. -->

#### Assertion

Verifier から Relying Party (RP) に対して発行される Subscriber に関する Identity Information を含む Statement.
Assertion は Verified Attributes を含むこともある.

<!-- A statement from a verifier to a Relying Party (RP) that contains identity information about a subscriber. Assertions may also contain verified attributes. -->

#### Assertion Reference

Assertion と紐付けて生成されるデータオブジェクトであり, Verifier を識別するとともに, Verifier が所有する Full Assertion へのポインタとして機能する.

<!-- A data object, created in conjunction with an assertion, which identifies the verifier and includes a pointer to the full assertion held by the verifier. -->

#### Asymmetric Signature

Asymmetric Keys (Public Key と Private Key のペア) を利用して Digital Signature を付与することで Data Integrity を保護する方法.
RSA 署名や Elliptic Curve 署名などが例としてあげられる.

<!-- A means of protecting data integrity by use of a digital signature that uses asymmetric keys (a public and private key pair). Examples include RSA and Elliptic Curve signatures. -->

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

#### Authenticated Protected Channel

Connection Initiator (接続元, Client) が Recipient (接続先, Server) を認証し, 暗号化されたコミュニケーションチャネル.
Authenticated Protocol Channel は Confidentiality および Man-in-the-middle 耐性を提供するものであり, 認証プロセスの中でよく使われるものである.
TLS [[BCP 195]](#bcp195) がその例としてあげられ, TLS では Recipient が提示した Certificate を Initiator が Verify することになる.

<!-- A communication channel that uses approved encryption where the initiator of the connection (client) has authenticated the recipient (server). Authenticated protected channels provide confidentiality and man-in-the-middle protection and are frequently used in the user authentication process. TLS [[BCP 195]](#bcp195) is an example of an authenticated protected channel when the certificate presented by the recipient is verified by the initiator. -->

#### Authentication

User や情報システムの Identity について確証を得るプロセス.

<!-- The process of establishing confidence in the identity of users or information systems. -->

#### Authentication Protocol

Claimant (要求者) が自身の Identity を確立するための正当な Authenticator を保持および制御していることを示す, Claimant と Verifier の間での一連のメッセージのやりとり.
セキュアな Authentication Protocol は, Claimant が正規の Verifier とやりとりしていることも明示する.

<!-- A defined sequence of messages between a claimant and a verifier that demonstrates that the claimant has possession and control of one or more valid authenticators to establish his/her identity. Secure authentication protocols also demonstrate to the claimant that he or she is communicating with the intended verifier. -->

#### Back-Channel Communication

2つのシステム間で直接コネクションを貼って行われるコミュニケーション. (標準プロトコルレベルでのプロキシの利用を許容する)
ブラウザ等を媒介としたリダイレクトは用いない.
HTTP Request & Response により実現される.

<!-- Communication between two systems that relies on a direct connection (allowing for standard protocol-level proxies), without using redirects through an intermediary such as a browser. This can be accomplished using HTTP requests and responses. -->

#### Federation

Identity / Authentication Information を一連のネットワークシステム間でやりとりするためのプロセス.
多くの場合, 各システムは異なるネットワークおよび異なるセキュリティドメインに存在し, 異なる主体により管理・運営されている.

<!-- A process that allows for the conveyance of identity and authentication information across a set of networked systems. These systems are often run and controlled by disparate parties in different network and security domains. -->

#### Federation Proxy

IdP に対して論理的に RP として動作し, RP に対して論理的に IdP として動作する, 2つのシステムを Bridge するコンポーネント.
"Broker" と呼ばれることもある.

<!-- A component that acts as a logical RP to a set of IdPs and a logical IdP to a set of RPs, bridging the two systems with a single component. These are sometimes referred to as "brokers".  -->

#### Front-Channel Communication

ブラウザ等を媒介とし, 2つのシステム間でリダイレクトを用いて行われるコミュニケーション.
これは通常メッセージ受信者がホストする URL に HTTP Query Parameter を付与することで実現される.

<!-- Communication between two systems that relies on redirects through an intermediary such as a browser. This is normally accomplished by appending HTTP query parameters to URLs hosted by the receiver of the message. -->

#### Identity Provider (IdP)

Subscriber の Primary Authentication Credentials を管理し, Assertion を発行する主体.
本ドキュメント群においては, Credential Service Provider (CSP) とも呼ばれる.

<!-- The party that manages the subscriber's primary authentication credentials and issues assertions derived from those credentials. This is commonly the credential service provider (CSP) as discussed within this document suite. -->

#### Pairwise Pseudonymous Identifier

CSP が特定の RP に対して生成する, opaque で推測不可能な Subscriber Identifier.
この識別子は特定の CSP-RP ペア以外には知られることはなく, 当該ペア間でのみ用いられる.

<!-- An opaque unguessable subscriber identifier generated by a CSP for use at a specific individual RP. This identifier is only known to and only used by one CSP-RP pair. -->

#### Relying Party (RP)

本ドキュメントでは, Subscriber を識別する Assertion を受け取り処理する主体.

<!-- In this document, the party that receives and processes the assertion identifying the subscriber. -->

#### Symmetric Signature

Shared Key を利用して Hash や Digest を付与することで Data Integrity を保護する方法.
HMAC や KMAC などが例としてあげられる.

<!-- A means of protecting data integrity by use of a hash or digest mechanism that uses a shared key. Examples include HMAC and KMAC. -->
