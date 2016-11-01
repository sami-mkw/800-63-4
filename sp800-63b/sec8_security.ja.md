<a name="sec8"></a>

<!-- ## 8. Threats and Security Considerations -->
## 8. 脅威とセキュリティに関する考慮事項

<!-- *This section is non-normative.* -->
*このセクションは non-normative である。*

<!-- ### 8.1. Authenticator Threats -->
### 8.1. Authenticator に対する脅威

<!-- An attacker who can gain control of an authenticator will often be able to masquerade as the authenticator's owner. Threats to authenticators can be categorized based on attacks on the types of authentication factors that comprise the authenticator: -->
Authenticator を制御できる攻撃者は Authenticator の所有者のように偽装することができる。 認証システムを構成する認証ファクターの種類ごとの攻撃に基づいて Authenticator への脅威を分類できる。

<!-- - *Something you have* may be lost, damaged, stolen from the owner or cloned by an attacker. For example, an attacker who gains access to the owner’s computer might copy a software authenticator. A hardware authenticator might be stolen, tampered with, or duplicated. -->
- *Something you have* は紛失、破損、所有者から盗難される、または攻撃者によって複製されることがある。 たとえば、所有者のコンピューターへのアクセスを取得した攻撃者は、ソフトウェアの Authenticator をコピーするかもしれない。 ハードウェアの Authenticator は、盗難されたり、いじられたり、複製されるかもしれない。

<!-- - *Something you know* may be disclosed to an attacker. The attacker might guess a memorized secret. Where the authenticator is a shared secret, the attacker could gain access to the CSP or verifier and obtain the secret value or perform a dictionary attack on a hash of that value. An attacker may observe the entry of a PIN or passcode, find a written record or journal entry of a PIN or passcode, or may install malicious software (e.g., a keyboard logger) to capture the secret. Additionally, an attacker may determine the secret through offline attacks on a hashed password database maintained by the verifier. -->
- *Something you know* は攻撃者に開示されることがある。 攻撃者は、記憶の中のシークレットを推測するかもしれない。 Authenticator が共有シークレットである場合、攻撃者は CSP または検証者へのアクセス権を得てシークレットの値を入手する、または、その値のハッシュに対して辞書アタックを行うかもしれない。 攻撃者は、PIN やパスコードの入力を観察したり、書き写された記録やジャーナル見つけたり、またはシークレットをキャプチャーするために不正なソフトウェア (例：キーボードロガー) をインストールしたりするかもしれない。 さらに、攻撃者は、検証者によってメンテナンスされているハッシュされたパスワード データベースに対するオフライン攻撃からシークレットを特定するかもしれない。

<!-- - *Something you are* may be replicated. An attacker may obtain a copy of the subscriber’s fingerprint and construct a replica - assuming that the biometric system(s) employed do not block such attacks by employing robust liveness detection techniques. -->
- *Something you are* は複製されるかもしれない。 攻撃者は、認証されるべき者 (サブスクライバー) の指紋のコピーを取得し、レプリカを作成するかもしれない (堅牢な生体検知技術によってこのような攻撃を検知しない生体認証システムが採用されていることを前提として) 。

<!-- - *Out of band* secrets may be intercepted. An attacker may receive a challenge or response by eavesdropping on the primary or secondary communications channel. The attacker might then authenticate their own channel or save the message for later replay. -->
- *Out of band* のシークレットは傍受されるかもしれない。 攻撃者は、プライマリまたはセカンダリの通信チャネルで、盗聴によってチャレンジまたはレスポンスを受信するかもしれない。 攻撃者は、独自のチャネルを認証させたり、後でリプレイするためにメッセージを保存したりするかもしれない。

<!-- This document assumes that the subscriber is not colluding with the attacker who is attempting to falsely authenticate to the verifier. With this assumption in mind, the threats to the authenticator(s) used for e-authentication are listed in [Table 8-1](#63bSec8-Table1), along with some examples. -->
このドキュメントは、サブスクライバーが検証者に対して虚偽の認証を行おうとしている攻撃者と共謀してないことを前提としている。 この前提に立って、電子認証用の Authenticator への脅威は [Table 8-1](#63bSec8-Table1) について、いくつかの例とともにリストする。


<a name="63bSec8-Table1"></a>

<div class="text-center" markdown="1">

**Table 8-1.  Authenticator に対する脅威**
<!-- **Table 8-1.  Authenticator Threats** -->

</div>

<!--
| **Authenticator Threats/Attacks**  | **Description**  | **Examples** |
|------------------------------------|------------------|--------------|
| Theft | A physical authenticator is stolen by an Attacker. | A hardware cryptographic device is stolen. |
| | | A One-Time Password device is stolen. |
| | | A look-up secret authenticator is stolen. |
| | | A cell phone is stolen. |
| Duplication | The subscriber’s authenticator has been copied with or without their knowledge. | Passwords written on paper are disclosed.
| | | Passwords stored in an electronic file are copied. |
| | | Software PKI authenticator (private key) copied. |
| | | Look-up secret authenticator copied. |
| Eavesdropping | The authenticator secret or authenticator output is revealed to the attacker as the subscriber is authenticating. | Memorized secrets are obtained by watching keyboard entry. |
| | | Memorized secrets or authenticator outputs are intercepted by keystroke logging software. |
| | | A PIN is captured from PIN pad device. |
| | | A hashed password is obtained and used by an attacker for another authentication (*pass-the-hash attack*) |
| | An out of band secret is intercepted by the attacker by compromising the communication channel. | An out of band secret is transmitted via unencrypted wifi and received by the attacker. |
| Offline cracking | The authenticator is exposed using analytical methods outside the authentication mechanism. | A software PKI authenticator is subjected to dictionary attack to identify the correct password to use to decrypt the private key. |
| Side channel attack | The authenticator secret is exposed using physical characteristics of the authenticator. | A key is extracted by differential power analysis on a hardware cryptographic authenticator. |
| | | A cryptographic authenticator secret is extracted by analysis of the response time of the authenticator over a number of attempts. |
| Phishing or pharming | The authenticator output is captured by fooling the subscriber into thinking the attacker is a verifier or RP. | A password is revealed by subscriber to a website impersonating the verifier.
| | | A memorized secret is revealed by a bank subscriber in response to an email inquiry from a phisher pretending to represent the bank. |
| | | A memorized secret is revealed by the subscriber at a bogus verifier website reached through DNS spoofing.
| Social engineering | The attacker establishes a level of trust with a subscriber in order to convince the subscriber to reveal his or her authenticator secret or authenticator output. | A memorized secret is revealed by the subscriber to an officemate asking for the password on behalf of the subscriber’s boss. |
| | | A memorized secret is revealed by a subscriber in a telephone inquiry from an attacker masquerading as a system administrator. |
| | | An out of band secret sent via SMS is received by an attacker who has convinced the mobile operator to redirect the victim's mobile phone to the attacker. |
| Online guessing | The attacker connects to the verifier online and attempts to guess a valid authenticator output in the context of that verifier. | Online dictionary attacks are used to guess memorized secrets. |
| | | Online guessing is used to guess authenticator outputs for a one-time password device registered to a legitimate claimant. |
| Endpoint compromise | Malicious code on the endpoint proxies remote access to a connected authenticator without user consent. | A cryptographic authenticator connected to the endpoint is used to authenticate remote attackers. |
| | Malicious code on the endpoint causes authentication to other than the intended verifier. | Authentication is performed on behalf of an attacker rather than the subscriber.
| | | A malicious app on the endpoint reads an out of band secret sent via SMS; the attacker uses the secret to authenticate.
| | Malicious code on the endpoint compromises a multi-factor software cryptographic authenticator. | Malicious code proxies authentication or exports authenticator keys from the endpoint.
-->

| **Authenticator に対する脅威/攻撃** | **説明** | **例** |
|------------------------------------|------------------|--------------|
| 盗難 | 物理的な Authenticator が攻撃者によって盗まれる。 | ハードウェア暗号化デバイスが盗まれる。 |
| | | ワンタイム パスワード デバイスが盗まれる。 |
| | | look-up secret authenticator が盗まれる。 |
| | | 携帯電話が盗まれる。 |
| 複製 | サブスクライバーの Authenticator が、本人の知識なしに複製される。 | パスワードが書かれた紙が開示される。 |
| | | 電子ファイルに格納されているパスワードがコピーされる。 |
| | | Software PKI authenticator (private key) がコピーされる。 |
| | | look-up secret authenticator がコピーされる。 |
| 盗聴 | サブスクライバーが認証を行ったときに、 Authenticator シークレットまたは Authenticator の出力が攻撃者に暴露される。 | キーボードエントリーを監視して記憶されたシークレットを取得する。 |
| | | キーストロークをロギングするソフトウェアによって、記憶されたシークレットまたは Authenticator の出力を横取りする。 |
| | | PIN パッド デバイスからPINをキャプチャする。 |
| | | ハッシュ化されたパスワードが攻撃者の手に渡り, それを他の認証に使われる。(*pass-the-hash attack*) |
| | Out of band シークレットが、通信チャネルの危殆化によって攻撃者に横取りされる。 | Out of band シークレットが暗号化されていないWi-Fiで送信され、攻撃者に受信される。 |
| オフライン クラッキング | Authenticator が、認証メカニズムの外で、解析メソッドによって明らかにされる。 | Software PKI authenticator が、秘密鍵の復号に使用する正しいパスワードを識別するために辞書攻撃を受ける。 |
| サイドチャネル攻撃 | Authenticator シークレットが、 Authenticator の物理的特性によって明らかにされる。 | キーが hardware cryptographic authenticator の差分電力解析によって明らかにされる。 |
| | | 無数の試行の応答時間の解析によって、 cryptographic authenticator secret が抽出される。 |
| フィッシングやファーミング | 攻撃者が検証者や RP であるようにサブスクライバーをだまし、Authenticator の出力をキャプチャする。 | サブスクライバーが検証者を偽装した web サイトに入力することで、パスワードが明らかにされる。 |
| | | 記憶されたシークレットが、銀行からの問い合わせに見せかけたメールに返信することで明らかにされる。 |
| | | サブスクライバーがDNS スプーフィングを介して偽の検証者 Webサイトにアクセスしてしまうことで、記憶されたシークレットが明らかにされる。 |
| ソーシャルエンジニア リング | 攻撃者が、サブスクライバーとの間に願いに応じるだけの信頼関係を構築し、サブスクライバー自身が Authenticator シークレット、または Authenticator の出力を明らかにする。 | サブスクライバーが、サブスクライバーの上司に代わってパスワードを聞いてきた同僚に対して記憶されたシークレットを明らかにする。 |
| | | 記憶されたシークレットが、システム管理者を装った攻撃者からの電話によって明らかにされる。 |
| | | 攻撃者が被害者の携帯電話を攻撃者にリダイレクトするようにモバイルオペレーターを信じさせることで、SMS経由のOut of band シークレットが攻撃者に受信される。 |
| オンラインでの推測 | 攻撃者が、検証者にオンラインで接続し、その検証のコンテキストで有効な Authenticator の出力を推測しようと試行する。 | オンライン辞書攻撃によって、記憶されたシークレットを推測する。 |
| | | オンラインでの推測によって、正当な要求者に登録されたワンタイム パスワード デバイスとしての Authenticator の出力が推測される。 |
| エンドポイントの危殆化 | エンドポイント上の不正なコードがユーザー同意なしの Authenticator へのリモートアクセス接続をプロキシする。 | エンドポイントに接続された暗号化 Authenticator が、リモートから攻撃者の認証に利用される。 |
| | エンドポイント上の不正なコードが、検証者が意図していない認証の原因となる。 | サブスクライバーではなく攻撃者に代わって認証が行われる。 |
| | | エンドポイント上の不正なアプリが SMS 経由で送信された Out of band シークレットを読みだし、攻撃者がシークレットを認証に使用する。 |
| | エンドポイント上の不正なコードが、 multi-factor software cryptographic authenticator を危殆化させる。 | 不正なコードが認証をプロキシする、またはエンドポイントから Authenticator 鍵をエクスポートする。 |

<!-- ### 8.2. Threat Mitigation Strategies -->
### 8.2. 脅威を軽減するストラテジー

<!-- Related mechanisms that assist in mitigating the threats identified above are summarized in [Table 8-2](#63bSec8-Table2). -->
[Table 8-2](#63bSec8-Table2) は、上記で説明された脅威の軽減を支援するメカニズムをまとめたものである。

<a name="63bSec8-Table2"></a>

<div class="text-center" markdown="1">

**Table 8-2 - Authenticator に対する脅威の軽減**
<!-- **Table 8-2 - Mitigating Authenticator Threats** -->

</div>

<!--
| **Authenticator Threat/Attack** | **Threat Mitigation Mechanisms** |
|---------------------------------|----------------------------------|
| Theft | Use multi-factor authenticators which need to be activated through a memorized secret or biometric.|
| Duplication |  Use authenticators from which it is difficult to extract and duplicate long-term authentication secrets. |
| Eavesdropping | Ensure the security of the endpoint, especially with respect to freedom from malware such as key loggers, prior to use.
| | Maintain situational awareness when entering memorized secrets and one-time passwords to ensure that they cannot be observed by others.
| | Authenticate over authenticated protected channels (observe lock icon in browser window, for example)
| | Use authentication protocols that are resistant to replay attacks such as *pass-the-hash*
| Offline cracking | Use an authenticator with a high entropy authenticator secret.
| | Store memorized secrets in a salted, hashed form to raise the cost of dictionary attacks; use a keyed hash.
| Side channel attack | Use authenticator algorithms that are designed to maintain constant power consumption and timing regardless of secret values.
| Phishing or pharming | Use authenticators that provide verifier impersonation resistance.
| | Be alert for unexpected hostnames in URLs.
| | Do not click on links in email messages; instead, enter the URL manually or through a trusted bookmark.
| Social engineering | Do not reveal authentication secrets to others, regardless of their story.
| | Avoid use of authenticators that present a risk of social engineering of third parties such as customer service agents.
| Online guessing | Use authenticators that generate high entropy output.
| | Use an authenticator that locks up after a number of repeated failed activation attempts.
| Endpoint compromise | Use hardware authenticators that require physical action by the subscriber.
| | Provide secure display of identity of verifier and relying party.
| | Maintain software-based keys in restricted-access storage.
-->

| **Authenticator に対する脅威/攻撃** | **脅威を軽減するメカニズム** |
|---------------------------------|----------------------------------|
| 盗難 | 記憶されたシークレットまたは生体認証をアクティブにするときには、多要素認証を使用する。 |
| 複製 | 認証シークレットの複製や抽出が長期的に困難な Authenticator を使用する。 |
| 盗聴 | 特にキーロガーなどのマルウェアに感染していないか、使用する前にエンドポイントがセキュリティを確保できているか確かめる。 |
| | 記憶されたシークレットやワンタイムパスワードを入力するときは、他の人がそれを観察できない環境であるか、常に気を配る。 |
| | 認証され、保護されたチャネル経由で認証を行う。 (たとえば、ブラウザーウィンドウにあるロック アイコンを確認する。) |
| | _pass-the-hash_ のようなリプレイ攻撃に耐性のある認証プロトコルを使用する。 |
| オフライン クラッキング | 高エントロピーの Authenticator シークレットを使用する。 |
| | 辞書攻撃のコストを高めるために、記憶されたシークレットをソルトを用いたハッシュ形式で保存する。鍵付きハッシュを使用する。 |
| サイドチャネル攻撃 | シークレットの値に関係なく消費電力とタイミングが一定に保たれるように設計された Authenticator アルゴリズムを使用する。 |
| フィッシングやファーミング | なりすましの検証を行うことができる Authenticator を使用する。 |
| | 意図しないホストネームがURLの中にあれば警告する。 |
| | 電子メールメッセージ内のリンクをクリックしない。代わりに、URLを手動で入力するか、信頼するブックマークからアクセスする。 |
| ソーシャルエンジニア リング | 誰に何を言われても、他人に対して認証シークレットを明らかにしない。 |
| | カスタマーサービスエージェントなどの第三者によるソーシャルエンジニアリングの危険性がある Authenticator の使用を避ける。 |
| オンラインでの推測 | 高エントロピーの出力を生成する Authenticator を使用する。 |
| | アクティベーションの試行に繰り返し失敗した後は Authenticator をロックアップする。 |
| エンドポイントの危殆化 | サブスクライバーの物理的なアクションを必要とするハードウェア Authenticator を使用する。 |
| | 検証者と RP のセキュリティで保護された ID 表示を提供する。 |
| | ソフトウェアベースの鍵はアクセス制限つきストレージで管理する。 |

<!-- There are several other strategies that may be applied to mitigate the threats described in Table 5: -->
他にも、表 5 に記載されている脅威を軽減するために適用できるいくつかのストラテジーがある。

<!-- - *Multiple factors* make successful attacks more difficult to accomplish. If an attacker needs to both steal a cryptographic authenticator and guess a memorized secret, then the work to discover both factors may be too high. -->
- *複数の要素* があると、攻撃が成功しにくくなる。 もし攻撃者が cryptographic authenticator を盗むことと記憶されたシークレットの推定の両方を必要とするなら、その両方を達成することはとても困難になり得る。

<!-- - *Physical security mechanisms* may be employed to protect a stolen authenticator from duplication. Physical security mechanisms can provide tamper evidence, detection, and response. -->
- *物理的なセキュリティメカニズム* は複製による Authenticator の盗難を防ぐために採用されることがある。物理的なセキュリティメカニズムは、耐タンパー性の確保、検出、および対応を可能にする。

<!-- - *Requiring the use of long memorized secrets* that don’t appear in common dictionaries may force attackers to try every possible value. -->
- 共有されている辞書に現れない *長い 記憶されたシークレット の使用を要求する* ことは、攻撃者にすべての入力可能な値を試させる。

<!-- - *System and network security controls* may be employed to prevent an attacker from gaining access to a system or installing malicious software. -->
- *システムとネットワークのセキュリティコントロール* は、攻撃者がシステムへのアクセスを得ることや、不正なソフトウェアのインストールを防ぐために用いられる。

<!-- - *Periodic training* may be performed to ensure subscribers understand when and how to report compromise (or suspicion of compromise) or otherwise recognize patterns of behavior that may signify an attacker attempting to compromise the authentication process. -->
- *定期的なトレーニング* を行うことで、いつ、どのように危殆化 (または危殆化の疑い) を報告するか、サブスクライバーの理解を促す。または、振る舞いのパターンを認識することで、攻撃者の認証プロセスを破るための試行であることを知る。

<!-- - *Out of band techniques* may be employed to verify proof of possession of registered devices (e.g., cell phones). -->
- *Out of band テクニック* は、登録されたデバイス (例: 携帯電話) を所有していることの検証に使用される。

<!-- ### 8.3. Authenticator Recovery -->
### 8.3. Authenticator の復旧

<!-- The weak point in many authentication mechanisms is the process followed when a subscriber loses control of one or more authenticators and needs to replace them. In many cases, the options remaining available to authenticate the subscriber are limited, and economic concerns (cost of maintaining call centers, etc.) motivate the use of inexpensive, and frequently less secure, backup authentication methods. To the extent that authenticator recovery is human-assisted, there is also the risk of social engineering attacks. -->
多くの認証メカニズムの弱点は、サブスクライバーが 1 つまたは複数の Authenticator のコントロールを失い、それらを交換する必要がある場合の手続きである。 多くの場合、サブスクライバーを認証できる残りの選択肢は限られている。経済的な心配 (コールセンター運営のコストなど) から、安価であったり、あまりセキュアでないものや、バックアップの認証方法を使用したいと考えさせる。 Authenticator の復旧は、人の手を借りるという点で、ソーシャルエンジニア リング攻撃の危険性がある。

<!-- In order to maintain the integrity of the authentication factors, it is essential that it not be possible to leverage an authentication involving one factor to obtain an authenticator of a different factor. For example, a memorized secret must not be usable to obtain a new list of look-up secrets. -->
認証要素の完全性を維持するためには、 1 つの要素によって異なる要素の Authenticator を取得するなど、不正に活用できないことが必要不可欠である。 たとえば、記憶されたシークレットは新しい look-up secret のリストに含まれていない必要がある。
