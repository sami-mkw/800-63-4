<a name="sec4"></a>

## <a name="AAL_SEC4"></a>4. 認証器保証レベル

<!--
## <a name="AAL_SEC4"></a>4. Authenticator Assurance Levels
-->

<!--
In order to satisfy the requirements of a given Authenticator Assurance Level (AAL), a claimant SHALL be authenticated with at least a given level of strength to be recognized as a subscriber. The result of an authentication process is an identifier, that MAY be pseudonymous, that SHALL be used each time that subscriber authenticates to that relying party. Optionally, other attributes that identify the subscriber as a unique person may also be provided.
-->

指定された認証器保証レベル(AAL)要件を満たすために、申請者は少なくとも自身が加入者であると認識される強度のレベルで認証するものとする(SHALL)。認証プロセスの結果は識別子である。それは仮名でもよく(MAY)、加入者がRPに対して認証するたびに使われるものとする(SHALL)。任意で、加入者を一位な人物であると識別するために、他の属性もまた提供されるかもしれない。

<!--
Detailed normative requirements for authenticators and verifiers at each AAL are provided in Section 5.
-->
各AALにおける認証器及び検証主体に対する要求規則の詳細については、5章で記載する。

<!--
FIPS 140 requirements are satisfied by [[FIPS 140-2]](#FIPS140-2) or newer revisions.
-->

FIPS 140 要求事項は、[[FIPS 140-2]](#FIPS140-2)またはより新しい版によって充足される。

<!--
[Table 4-1](#63bSec4-Table1) lists strict adherence to M-04-04 Level of Assurance, mapping the corresponding Authenticator Assurance Levels.
-->

[Table 4-1](#63bSec4-Table1)は、M-04-04 保証レベルを遵守するAALを表したもので、対応する認証器保証レベルにマッピングされている。

<a name="63bSec4-Table1"></a>

<div class="text-center" markdown="1">

<!--
**Table 4-1.  Legacy M-04-04 AAL Requirements**
-->

**Table 4-1.  レガシー M-04-04 AAL 要件**

</div>

| M-04-04保証レベル(LOA) | 認証器保証レベル(AAL) |
|:------------------:|:-----------------------------:|
| 1 | 1| 
| 2 | 2 または 3 |
| 3 | 2 または 3 |
| 4 | 3 |

<!--
| M-04-04 Level of Assurance (LOA) |  Authenticator Assurance Level (AAL) |
|:------------------:|:-----------------------------:|
| 1 |  1| 
| 2 |  2 or 3 |
| 3 |  2 or 3 |
| 4 |  3 |
-->


### 4.1. 認証器保証レベル 1(Authenticator Assurance Level 1)
<!--
### 4.1. Authenticator Assurance Level 1
-->

AAL 1は、申請者が加入者に対して登録されている認証器を制御していることにある程度の保証を与える。AAL 1は幅広く利用可能な認証技術を使った単一要素認証器を利用する。認証が成功するには、申請者が、自身が認証器を所有及び制御することを、セキュアな認証プロトコルを通して証明する必要がある。

<!--
AAL 1 provides some assurance that the claimant controls the authenticator registered to a subscriber. AAL 1 uses single-factor authentication using a wide range of available authentication technologies. Successful authentication requires that the claimant prove through a secure authentication protocol that he or she possesses and controls the authenticator.
-->

#### 4.1.1. 許可された認証器タイプ
<!--
#### 4.1.1. Permitted Authenticator Types
-->

認証器保証レベル 1では、5章で定義される以下の任意の認証器タイプの利用が許可されている。

<!--
Authenticator Assurance Level 1 permits the use of any of the following authenticator types, defined in Section 5:
-->

* 記憶シークレット
* ルックアップシークレット
* 経路外 (一部非推奨。 より詳細については [Section 5.1.3](#out-of-band) 参照のこと。)
* 単一要素 OTP デバイス
* 多要素 OTP デバイス
* 単一要素暗号ソフトウェア
* 単一要素暗号デバイス
* 多要素暗号ソフトウェア
* 多要素暗号デバイス

<!--
* Memorized Secret
* Look-up Secret
* Out of Band (Partially deprecated; see [Section 5.1.3](#out-of-band) for more details)
* Single Factor OTP Device
* Multi-Factor OTP Device
* Single Factor Cryptographic Software
* Single Factor Cryptographic Device
* Multi-Factor Cryptographic Software
* Multi-Factor Cryptographic Device
-->

#### 4.1.2. 認証器及び検証主体 要求事項
<!--
#### 4.1.2. Authenticator and Verifier Requirements
-->

AAL 1で用いられる暗号認証器は、承認済みの暗号を利用するものとする(SHALL)。汎用オペレーティング・システム環境で動作するソフトウェアベースの認証器は、実施上(例、マルウェアやJailbreakによって)それ自身が動作しているプラットフォームが改竄されていることを検出するよう試みてもよく(MAY)、そのような改竄が検出されると操作を拒否すべき(SHOULD)である。

<!--
Cryptographic authenticators used at AAL 1 SHALL use approved cryptography. Software-based authenticators that operate within the context of a general purpose operating system MAY, where practical, attempt to detect compromise of the platform in which they are running (e.g., by malware or "jailbreak") and SHOULD decline to operate when such a compromise is detected.
-->

申請者とチャネル(経路外認証器の場合はプライマリチャネル)との間の通信は、認証器出力の秘匿性と中間者攻撃に対する耐性を提供する保護された認証済みチャネルを介して行われるものとする(SHALL)。
<!--
Communication between the claimant and channel (the primary channel in the case of an Out of Band authenticator) SHALL be via an authenticated protected channel to provide confidentiality of the authenticator output and resistance to man-in-the-middle attacks.
-->

政府機関が運用する検証主体は、AAL 1において、[[FIPS 140]](#FIPS140-2) Level 1 の要求事項に適合していることを確認されるものとする(SHALL)。

<!--
Verifiers operated by government agencies at AAL 1 SHALL be validated to meet the requirements of [[FIPS 140]](#FIPS140-2) Level 1.
-->

#### 4.1.3. アサーション 要求事項
<!--
#### 4.1.3. Assertion Requirements
-->

AAL 1で正当であるために、認証器のアサーションは [SP 800-63C](sp800-63c.html) で定義されている要求事項を満たすものとする(SHALL)。無記名アサーションを利用してもよい(MAY)。

<!--
In order to be valid at AAL 1, authentication assertions SHALL meet the requirements defined in [SP 800-63C](sp800-63c.html). Bearer assertions MAY be used.
-->

#### <a name="aal1reauth"></a>4.1.4. 再認証
<!--
#### <a name="aal1reauth"></a>4.1.4. Reauthentication
-->

AAL 1では、ユーザの活動に関わらず、加入者の再認証は少なくとも30日ごとに1回は繰り返し実施すべきである(SHOULD)。

<!--
At AAL 1, reauthentication of the subscriber SHOULD be repeated at least once per 30 days, regardless of user activity.
-->

#### 4.1.5. セキュリティ統制
<!--
#### 4.1.5. Security Controls
-->

CSPは、[[SP 800-53]](#SP800-53) または等価な業界標準で定義されているセキュリティ統制の低い基準に、適切に適合したセキュリティ統制を採用すべき(SHOULD)であり、 *低い*基準に対応する確実性の要求事項を最低限を満たしていることを保証すべきである(SHOULD)。

<!--
The CSP SHOULD employ appropriately tailored security controls from the low baseline of security controls defined in [[SP 800-53]](#SP800-53) or equivalent industry standard and SHOULD ensure that the minimum assurance requirements associated with the *low* baseline are satisfied.
-->

#### 4.1.6. レコード保存
<!--
#### 4.1.6. Records Retention
-->

CSPは、準拠法及び規則の適用に合致する個別のレコード保存ポリシーに従うものとする。もしCSPが何らかの法的要件なくレコード保存をすることを選択する場合、CSPはレコードの記録期間を決定するためのプライバシリスクアセスメントを行うものとする(SHALL)。

<!--
The CSP shall comply with their respective records retention policies in accordance with applicable laws and regulations. If the CSP opts to retain records in the absence of any legal requirements, the CSP SHALL conduct a privacy risk assessment to determine how long any records should be retained.
-->

### 4.2. 認証器保証レベル2(Authenticator Assurance Level 2)
<!--
### 4.2. Authenticator Assurance Level 2
-->

AAL 2は、申請者が加入者に対して登録されている認証器を制御していることにより高い確実性を与える。2つの異なる認証要素が必要である。承認済み(approved)の暗号技術がAAL 2とそれ以上では必須である。

<!--
AAL 2 provides high confidence that the claimant controls the authenticator registered to a subscriber. Two different authentication factors are required. Approved cryptographic techniques are required at AAL 2 and above.
-->

#### 4.2.1. 許可された認証器タイプ
<!--
#### 4.2.1. Permitted Authenticator Types
-->

AAL 2では、多要素認証器の所持、または2つの単一要素認証器の組み合わせが求められる。認証器の要求事項は5章で述べられている。

<!--
At AAL 2, it is required to have (a) a multi-factor authenticator, or (b) a combination of two single-factor authenticators. Authenticator requirements are specified in Section 5.
-->

多要素認証器を利用する際、以下の任意のものを利用してよい: 

<!--
When a multi-factor authenticator is used, any of the following may be used:
-->

* 多要素 OTP デバイス
* 多要素暗号ソフトウェア
* 多要素暗号デバイス

<!--
* Multi-Factor OTP Device
* Multi-Factor Cryptographic Software
* Multi-Factor Cryptographic Device
-->

2つの単一要素認証器を組み合わせる際には、記憶シークレット認証器と、以下のリストから1つの所有ベース("something you have")の認証器を含むこととする(SHALL):

<!--
When a combination of two single-factor authenticators is used, it SHALL include a Memorized Secret authenticator and one possession-based ("something you have") authenticator from the following list:
-->

* ルックアップシークレット
* 経路外
* 単一要素OTPデバイス
* 単一要素暗号ソフトウェア
* 単一要素暗号デバイス

<!--
* Look-up Secret
* Out of Band
* Single Factor OTP Device
* Single Factor Cryptographic Software
* Single Factor Cryptographic Device
-->

<!-- > Note: The requirement for a memorized secret authenticator above derives from the need for two different types of authentication factors to be used. All biometric authenticators compliant with this specification are multi-factor, so something you know (a memorized secret) is the remaining possibility. -->

> 注記: 上記の記憶シークレット認証器の要件は、異なる2タイプの認証器要素を利用するということに由来する。本仕様に準拠した全ての生体認証器は多要素であるので、something you know (記憶シークレット)は使っても良いし使わなくても良い。

<!-- TODO remaining possibilityがわからない -->

#### 4.2.2. 認証器及び検証主体 要求事項
<!--
#### 4.2.2. Authenticator and Verifier Requirements
-->

AAL 2で用いられる暗号認証器は、承認済み(approved)暗号を使うものとする(SHALL)。政府機関によって開発された認証器は、[[FIPS 140]](#FIPS140-2) Level 1の要求事項に適合していることを確認されるものとする(SHALL)。汎用オペレーティング・システム環境で動作するソフトウェアベースの認証器は、実施上(例、マルウェアやJailbreakによって)それ自身が動作しているプラットフォームが改竄されていることを検出するよう試みてもよく(MAY)、そのような改竄が検出されると操作を拒否すべき(SHOULD)である。

<!--
Cryptographic authenticators used at AAL 2 SHALL use approved cryptography. Authenticators procured by government agencies SHALL be validated to meet the requirements of [[FIPS 140]](#FIPS140-2) Level 1. Software-based authenticators that operate within the context of a general purpose operating system MAY, where practical, attempt to detect compromise of the platform in which they are running (e.g., by malware or "jailbreak") and SHOULD decline to operate when such a compromise is detected.
-->

申請者とチャネル(経路外認証器の場合はプライマリチャネル)との間の通信は、認証器出力の秘匿性と中間者攻撃に対する耐性を提供する保護された認証済みチャネルを介して行われるものとする(SHALL)。

<!--
Communication between the claimant and channel (the primary channel in the case of an Out of Band authenticator) SHALL be via an authenticated protected channel to provide confidentiality of the authenticator output and resistance to man-in-the-middle attacks.
-->

政府機関によって運営されているAAL 2の検証主体は、[[FIPS 140]](#FIPS140-2) Level 1の要求事項に適合していることを確認されるものとする(SHALL)。

<!--
Verifiers operated by government agencies at AAL 2 SHALL be validated to meet the requirements of [[FIPS 140]](#FIPS140-2) Level 1.
-->

#### 4.2.3. アサーション要求事項
<!--
#### 4.2.3. Assertion Requirements
-->

AAL 2で正当であるために、認証器のアサーションは [SP 800-63C](sp800-63c.html) で定義されている要求事項を満たすものとする(SHALL)。無記名アサーションを利用してもよい(MAY)。

<!--
In order to be valid at AAL 2, authentication assertions SHALL meet the requirements defined in [SP 800-63C](sp800-63c.html). Bearer assertions MAY be used.
-->

#### <a name="aal2reauth"></a>4.2.4. 再認証
<!--
#### <a name="aal2reauth"></a>4.2.4. Reauthentication
-->

AAL 2では、ユーザの活動に関わらず、加入者の再認証は少なくとも12時間に1回は繰り返し実施するものとする(SHALL)。加入者の再認証はユーザが活動していない時間が30分を超えないように繰り返し実施することとする(SHALL)。CSPは、望ましい場合、ユーザが活動していないことで生じるタイムアウトの間際に、ユーザに対し活動契機となるように入力を促してもよい(MAY)。
再認証は単一認証要素を利用してよい(MAY)。

<!--
At AAL 2, authentication of the subscriber SHALL be repeated at least once per 12 hours, regardless of user activity. Reauthentication of the subscriber SHALL be repeated following no more than 30 minutes of user inactivity. The CSP MAY prompt the user to cause activity just before the inactivity timeout, if desired. Reauthentication MAY use a single authentication factor.
-->

#### 4.2.5. セキュリティ統制
<!--
#### 4.2.5. Security Controls
-->

CSPは、[[SP 800-53]](#SP800-53) または等価な業界標準で定義されているセキュリティ統制の適度な基準に、適切に適合したセキュリティ統制を採用すべき(SHOULD)であり、 *適度な*基準に対応する確実性の要求事項を最低限を満たしていることを保証すべきである(SHOULD)。

<!--
The CSP SHOULD employ appropriately tailored security controls from the moderate baseline of security controls defined in [[SP 800-53]](#SP800-53) or equivalent industry standard and SHOULD ensure that the minimum assurance requirements associated with the *moderate* baseline are satisfied.
-->

#### 4.2.6. レコード保存
<!--
#### 4.2.6. Records Retention
-->

CSPは、あらゆる法律及び規則の適用に対しても合致する個別のレコード保存ポリシーに従うものとする。もしCSPが何らかの法的要件なくレコード保存をすることを選択する場合、CSPはレコードの記録期間を決定するためのプライバシリスクアセスメントを行うものとする(SHALL)。

<!--
CSPs shall comply with their respective records retention policies in accordance with whatever laws and/or regulations apply to those entities. If the CSP opts to retain records in the absence of any legal requirements, the CSP SHALL conduct a privacy risk assessment to determine how long any records should be retained.
-->

### 4.3. 認証器保証レベル(Authenticator Assurance Level 3)
<!--
### 4.3. Authenticator Assurance Level 3
-->

AAL 3は、申請者が加入者に対して登録されている認証器を制御していることにより非常に高い確実性を与える。AAL3における認証は、暗号プロトコルを介した鍵の所持証明に基づいている。AAL 3は、さらに検証主体なりすまし耐性を持った"堅牢な"の暗号認証器を必要とする、という点を除けばAAL 2と同一である。

<!--
AAL 3 provides very high confidence that the claimant controls the authenticator registered to a subscriber. Authentication at AAL 3 is based on proof of possession of a key through a cryptographic protocol. AAL 3 is similar to AAL 2 except that a "hard" cryptographic authenticator that also provides verifier impersonation resistance is required.
-->

#### 4.3.1. 許可された認証器タイプ
<!--
#### 4.3.1. Permitted Authenticator Types
-->

認証器保証レベル 3では、3種類のハードウェアデバイスのうち、1つを利用する必要がある:

<!--
Authentication Assurance Level 3 requires the use of one of three kinds of hardware devices:
-->

* 多要素暗号デバイス
* 単一要素暗号デバイス(記憶シークレットと連動して用いられる)

<!--
* Multi-Factor Cryptographic Device
* Single-Factor Cryptographic Device used in conjunction with Memorized Secret
-->

AAL 3で用いる全ての暗号デバイス認証器は、section [5.2.5](#verifimpers)に記載されている検証主体なりすまし耐性を備えるものとする(SHALL)。

<!--
All cryptographic device authenticators used at AAL 3 SHALL be verifier impersonation resistant as described in section [5.2.5](#verifimpers).
-->

#### 4.3.2. 認証器及び検証主体 要求事項
<!--
#### 4.3.2. Authenticator and Verifier Requirements
-->

申請者とチャネルとの間の通信は、認証器出力の秘匿性と中間者攻撃に対する耐性を提供する保護された認証済みチャネルを介して行われるものとする(SHALL)。AAL 3で利用される少なくとも1つの認証器は、Section [5.2.5](#verifimpers)に記載されているように検証主体なりすまし耐性を備えるものとする(SHALL)。

<!--
Communication between the claimant and channel SHALL be via an authenticated protected channel to provide confidentiality of the authenticator output and resistance to man-in-the-middle attacks. At least one authenticator used in each AAL 3 authentication SHALL be verifier impersonation resistant as described in Section [5.2.5](#verifimpers). 
-->

AAL 3で利用される多要素認証器は、[[FIPS 140]](#FIPS140-2) Level 2、または少なくとも[[FIPS 140]](#FIPS140-2) Level 3物理セキュリティ全体よりも高度な基準で確認されたハードウェア暗号モジュールであるものとする(SHALL)。
AAL 3で利用される単一要素暗号デバイスは、[[FIPS 140]](#FIPS140-2) Level 1、または少なくとも[[FIPS 140]](#FIPS140-2) Level 3物理セキュリティ全体よりも高度な基準で確認されているものとする(SHALL)。これらの要求事項は、[[FIPS 201]](#FIPS201)準拠のPersonal Identity Verification (PIV) CardのPIV認証鍵を利用することで満たすことができる(CAN)。

<!--
Multi-factor authenticators used at AAL 3 SHALL be hardware cryptographic modules validated at [[FIPS 140]](#FIPS140-2) Level 2 or higher overall with at least [[FIPS 140]](#FIPS140-2) Level 3 physical security. Single-factor cryptographic devices used at AAL 3 SHALL be validated at [[FIPS 140]](#FIPS140-2) Level 1 or higher overall with at least [[FIPS 140]](#FIPS140-2) Level 3 physical security. These requirements CAN be met by using the PIV authentication key of a [[FIPS 201]](#FIPS201) compliant Personal Identity Verification (PIV) Card.
-->

AAL 3における検証主体は、[[FIPS 140]](#FIPS140-2) Level 1またはそれ以上の基準で確認されるものとする(SHALL)。

<!--
Verifiers at AAL 3 SHALL be validated at [[FIPS 140]](#FIPS140-2) Level 1 or higher.
-->

#### 4.3.3. アサーション要求事項
<!--
#### 4.3.3. Assertion Requirements
-->

AAL 3で正当であるために、認証器のアサーションは [SP 800-63C](sp800-63c.html) で定義されている 所持証明(proof-of-posession)アサーションの要件を満たすものとする(SHALL)。

<!--
In order to be valid at AAL 3, authentication assertions SHALL meet the requirements of proof-of-possession assertions as defined in [SP 800-63C](sp800-63c.html).
-->

#### <a name="aal2reauth"></a>4.3.4. 再認証
<!--
#### <a name="aal3reauth"></a>4.3.4. Reauthentication
-->

AAL 3では、ユーザの活動に関わらず、加入者の再認証は少なくとも12時間に1回は繰り返し実施するものとする(SHALL)。加入者の再認証はユーザが活動していない時間が15分を超えないように繰り返し実施することとする(SHALL)。再認証は両方の認証要素を利用するものとする(SHALL)。検証主体はユーザが活動していないことで生じるタイムアウトの前に、ユーザに対し活動契機となるように入力を促してもよい(MAY)。

<!--
At AAL 3, authentication of the subscriber SHALL be repeated at least once per 12 hours, regardless of user activity. Reauthentication of the subscriber SHALL be repeated following a period of no more than 15 minutes of user inactivity. Reauthentication SHALL use both authentication factors. The verifier MAY prompt the user to cause activity just before the inactivity timeout.
-->

#### 4.3.5. セキュリティ統制
<!--
#### 4.3.5. Security Controls
-->

CSPは、[[SP 800-53]](#SP800-53) または等価な業界標準で定義されているセキュリティ統制の高度な基準に、適切に適合したセキュリティ統制を採用すべき(SHOULD)であり、 *高度な*基準に対応する確実性の要求事項を最低限を満たしていることを保証すべきである(SHOULD)。

<!--
The CSP SHOULD employ appropriately tailored security controls from the high baseline of security controls defined in [[SP 800-53]](#SP800-53) or an equivalent industry standard and SHOULD ensure that the minimum assurance requirements associated with the *high* baseline are satisfied.
-->

#### 4.3.6. レコード保存
<!--
#### 4.3.6. Records Retention
-->

CSPは、あらゆる法律及び規則の適用に対しても合致する個別のレコード保存ポリシーに従うものとする。もしCSPが何らかの法的要件なくレコード保存をすることを選択する場合、CSPはレコードの記録期間を決定するためのプライバシリスクアセスメントを行うものとする(SHALL)。

<!--
The CSP SHALL comply with their respective records retention policies in accordance with whatever laws and/or regulations apply to those entities. If the CSP opts to retain records in the absence of any legal requirements, the CSP SHALL conduct a privacy risk assessment to determine how long any records should be retained.
-->

<!--
### <a name="aal_privacy"></a>4.4. Privacy Requirements
-->

### <a name="aal_privacy"></a>4.4. プライバシー要件

CSPは[[SP 800-53]](#SP800-53)で定義された適切に調整されたプライバシーコントロール、または他の等価な業界標準を採用すべきである(SHOULD)。

<!--
The CSP SHOULD employ appropriately tailored privacy controls defined in [[SP 800-53]](#SP800-53) or equivalent industry standard.
-->

CSPは、認証実施や法令遵守、法的手続き以外の目的で認証器の情報を利用・開示しないものとし、追加の用途のためには、明確な通知を提供し、加入者から承諾を得るものとする(SHALL NOT)。CSPは、サービス条件に対する同意をとらなくてもよい(MAY NOT)。情報を収集した際の元々の目的に利用が限定されていることを保証するための対策が講じられるものとする(SHALL)。このような情報の利用が、認証実施や法令遵守、法的手続きに関連する用途に該当しないのであれば、CSPは通知を行い、加入者から同意を得るものとする(SHALL)。この通知は、[SP 800-63A Section 8.2](sp800-63a.html#consent)の*Notice and Consent*に記載されているのと同じ原則に従うべき(SHOULD)であり、法律に固執し過ぎたプライバシーポリシーや一般条件に丸め込むべきではない(SHOULD not)。明示的な目的外の用途がある場合は、むしろ加入者は追加の利用目的を理解するための意味のある方法、及び承諾または辞退する機会が提供されるべきである(SHOULD)。

<!--
CSPs SHALL NOT use or disclose information about authenticators for any purpose other than conducting authentication or to comply with law or legal process, unless the CSP provides clear notice and obtains consent from the subscriber for additional uses. CSPs MAY NOT make consent a condition of the service. Care SHALL be taken to ensure that use of such information is limited to its original purpose for collection. If the use of such information does not fall within uses related to authentication or to comply with law or legal process, the CSP SHALL provide notice and obtain consent from the subscriber.  This notice SHOULD follow the same principles as described in *Notice and Consent* in [SP 800-63A Section 8.2](sp800-63a.html#consent) and SHOULD not be rolled up into a legalistic privacy policy or general terms and conditions. Rather, if there are uses outside the bounds of these explicit purposes, the subscriber SHOULD be provided with a meaningful way to understand the purpose for additional uses, and the opportunity to accept or decline.
-->

CSPが政府機関または民間のプロバイダーであるかどうかにかかわらず、次の要件が認証サービスを提供・利用する政府機関に対して適用される:

<!--
Regardless of whether the CSP is an agency or private sector provider, the following requirements apply to the agency offering or using the authentication service:
-->


1. 政府機関は、認証器の発行・維持を目的としたPersonally Identifiable Information (PII)の収集が*Privacy Act of 1974* [[PrivacyAct]](#PrivacyAct)の要件に発展するかどうか分析を実施するため、プライバシー領域の政府機関幹部と協議するものとする(SHALL)。

* 政府機関は、必要に応じてそのような収集活動を対象とするレコード通知システムを公開するものとする(SHALL)。
* 政府機関は、認証器の発行・維持を目的としたPIIの収集が*E-Government Act of 2002* [[E-Gov]](#E-Gov)の要件に発展するかどうか分析を実施するため、プライバシー領域の政府機関幹部と協議するものとする(SHALL)。
* 政府機関は、必要に応じてそのような収集活動を対象とするPrivacy Impact Assement(PIA)を公開するものとする(SHALL)。

<!--
1. The agency SHALL consult with their Senior Agency Official for Privacy to conduct an analysis to determine whether the collection of Personally Identifiable Information (PII) to issue or maintain authenticators triggers the requirements of the *Privacy Act of 1974* [[PrivacyAct]](#PrivacyAct). 
* The agency SHALL publish a System of Records Notice to cover such collections, as applicable. 
* The agency SHALL consult with their Senior Agency Official for Privacy to conduct an analysis to determine whether the collection of PII to issue or maintain authenticators triggers the requirements of the *E-Government Act of 2002* [[E-Gov]](#E-Gov). 
* The agency SHALL publish a Privacy Impact Assessment to cover such collection, as applicable.
-->

### 4.5. 要求事項要約
<!--
### 4.5. Summary of Requirements
-->

*(参考; 要求規則は前セクションを参照のこと。)*

<!--
*(Non-normative; refer to preceding sections for normative requirements)*
-->

[Table 4-3](#63bSec4-Table3)は認証器保証レベル毎の要求事項を要約したものである:

<!--
[Table 4-3](#63bSec4-Table3) summarizes the requirements for each of the authenticator assurance levels:
-->

<a name="63bSec4-Table3"></a>

<div class="text-center" markdown="1">

<!--
**Table 4-3.  AAL Summary of Requirements**
-->

**Table 4-3.  AAL要件サマリ**

</div>



要求事項 | AAL 1 | AAL 2 | AAL 3
------------|-------|-------|-------
**許可されている認証器タイプ** | 記憶シークレット;<br />ルックアップシークレット;<br />経路外;<br />単一要素OTPデバイス;<br />多要素OTPデバイス;<br />単一要素暗号ソフトウェア;<br />単一要素暗号デバイス;<br />多要素暗号ソフトウェア;<br />多要素暗号デバイス<br /> | 多要素OTPデバイス;<br />多要素暗号ソフトウェア;<br />多要素暗号デバイス;<br />または記憶シークレットと次の組み合わせ:<br />&nbsp;&bull;&nbsp;ルックアップシークレット<br />&nbsp;&bull;&nbsp;経路外<br />&nbsp;&bull;&nbsp;単一要素OTPデバイス<br />&nbsp;&bull;&nbsp;単一要素暗号ソフトウェア<br />&nbsp;&bull;&nbsp;単一要素暗号デバイス<br /> | 多要素暗号デバイス<br />単一要素暗号デバイス ＋ &nbsp;&nbsp;記憶シークレット
**FIPS 140 確認** | Level 1 (政府機関の検証主体) | Level 1 (政府機関の認証器及び検証主体) | Level 2 全体 (多要素認証器)<br />Level 1 全体 (検証主体及び単一要素暗号デバイス)<br />Level 3 物理セキュリティ (全ての認証器)
**アサーション** | 無記名または所有証明 | 無記名または所有証明 | 所有証明のみ
**再認証** | 30 日 | 12 時間または30分間活動なし; 単一認証要素を利用してもよい | 12 時間または15分間活動なし; 両方の認証要素を利用するものとする
**セキュリティ統制**|[[SP 800-53]](#SP800-53) 低い基準 (または 等価なもの)|[[SP 800-53]](#SP800-53) 適度な基準 (または等価なもの)|[[SP 800-53]](#SP800-53) 高い基準 (または等価なもの)
**中間者攻撃耐性** | 必要 | 必要 | 必要 |
**検証主体なりすまし耐性** | 不要 | 不要 | 必要 |

<!--

Requirement | AAL 1 | AAL 2 | AAL 3
------------|-------|-------|-------
**Permitted authenticator types** | Memorized Secret;<br />Look-up Secret;<br />Out of Band;<br />SF OTP Device;<br />MF OTP Device;<br />SF Crypto Software;<br />SF Crypto Device;<br />MF Crypto Software;<br />MF Crypto Device<br /> | MF OTP Device;<br />MF Crypto Software;<br />MF Crypto Device;<br />or memorized secret plus:<br />&nbsp;&bull;&nbsp;Look-up Secret<br />&nbsp;&bull;&nbsp;Out of Band<br />&nbsp;&bull;&nbsp;SF OTP Device<br />&nbsp;&bull;&nbsp;SF Crypto Software<br />&nbsp;&bull;&nbsp;SF Crypto Device<br /> | MF Crypto Device<br />SF Crypto Device plus &nbsp;&nbsp;Memorized Secret
**FIPS 140 verification** | Level 1 (Government agency verifiers) | Level 1 (Government agency authenticators and verifiers) | Level 2 overall (MF authenticators)<br />Level 1 overall (verifiers and SF Crypto Devices)<br />Level 3 physical security (all authenticators)
**Assertions** | Bearer or proof of possession | Bearer or proof of possession | Proof of possession only
**Reauthentication** | 30 days | 12 hours or 30 minutes inactivity; may use one authentication factor | 12 hours or 15 minutes inactivity; shall use both authentication factors
**Security controls**|[[SP 800-53]](#SP800-53) Low Baseline (or equivalent)|[[SP 800-53]](#SP800-53) Moderate Baseline (or equivalent)|[[SP 800-53]](#SP800-53) High Baseline (or equivalent)
**MITM resistance** | Required | Required | Required |
**Verifier impersonation resistance** | Not required | Not required | Required |
-->



