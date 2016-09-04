<a name="sec4"></a>

<!--
## <a name="AAL_SEC4"></a>4. Authenticator Assurance Levels
-->

## <a name="AAL_SEC4"></a>4. 認証器保証レベル

指定された認証器保証レベル(AAL)要件を満たすために、申請者は少なくとも自身が加入者であると認識される強度のレベルで認証するものとする(SHALL)。認証プロセスの結果は識別子である。それは仮名でもよく(MAY)、加入者がRPに対して認証するたびに使われるものとする(SHALL)。任意で、加入者を一位な人物であると識別するために、他の属性もまた提供されるかもしれない。

<!--
In order to satisfy the requirements of a given Authenticator Assurance Level (AAL), a claimant SHALL authenticate themselves with at least a given level of strength to be recognized as a subscriber. The result of an authentication process is an identifier, that MAY be pseudonymous, that SHALL be used each time that subscriber authenticates to that relying party. Optionally, other attributes that identify the subscriber as a unique person may also be provided.
-->

各AALにおける認証器及び検証主体に対する要求規則の詳細については、5章で記載する。

<!--
Detailed normative requirements for authenticators and verifiers at each AAL are provided in Section 5.
-->

FIPS 140 要求事項は、[[FIPS 140-2]](#FIPS140-2)またはより新しい版によって充足される。

<!--
FIPS 140 requirements are satisfied by [[FIPS 140-2]](#FIPS140-2) or newer revisions.
-->

以下の表は、M-04-04 保証レベル毎に求められるAALを表したものである。機関は、 評価済みの M-04-04 LOA に基づいて、対応するAALを選択するものとする(SHALL)。

<!--
The following table shows the required AAL per M-04-04 Level of Assurance. Agencies SHALL select the corresponding AAL based on the assessed M-04-04 LOA.
-->

| 保証レベル | 認証器保証レベル
|:------------------:|:-----------------------------:
| 1 | 1, 2 または 3 
| 2 | 2 または 3
| 3 | 2 または 3 
| 4 | 3 

<!--
| Level of Assurance | Authenticator Assurance Level
|:------------------:|:-----------------------------:
| 1 | 1, 2 or 3 
| 2 | 2 or 3
| 3 | 2 or 3 
| 4 | 3 
-->


### 4.1. 認証器保証レベル 1(Authenticator Assurance Level 1)
<!--
### 4.1. Authenticator Assurance Level 1
-->

AAL 1は、以前のトランザクションに関わったのと同一の申請者が、保護されたトランザクションやデータにアクセスしようとしていることにある程度の確実性を与える、単一要素のネットワーク認証を規定する。AAL 1は幅広く利用可能な認証技術を採用することを認めており、単一の認証要素を利用することだけを要求する。AAL 1は、より高い認証器保証レベルの任意の認証方式の利用も認めている。認証が成功するには、申請者が、自身が認証器を所有及び制御することを、セキュアな認証プロトコルを通して証明する必要がある。

<!--
AAL 1 provides single factor remote network authentication, giving some assurance that the same Claimant who participated in previous transactions is accessing the protected transaction or data. AAL 1 allows a wide range of available authentication technologies to be employed and requires only a single authentication factor to be used. It also permits the use of any of the authentication methods of higher authenticator assurance levels. Successful authentication requires that the Claimant prove through a secure authentication protocol that he or she possesses and controls the authenticator.
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
* 単一要素暗号デバイス
* 多要素ソフトウェア暗号認証器
* 多要素暗号デバイス

<!--
* Memorized Secret
* Look-up Secret
* Out of Band (Partially deprecated; see [Section 5.1.3](#out-of-band) for more details)
* Single Factor OTP Device
* Multi-Factor OTP Device
* Single Factor Cryptographic Device
* Multi-Factor Software Cryptographic Authenticator
* Multi-Factor Cryptographic Device
-->

#### 4.1.2. 認証器及び検証主体 要求事項
<!--#### 4.1.2. Authenticator and Verifier Requirements-->

AAL 1で用いられる暗号認証器は、承認済みの暗号を利用するものとする(SHALL)。

<!--
Cryptographic authenticators used at AAL 1 SHALL use approved cryptography.
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

CSPは、あらゆる法律及び規則の適用に対しても合致する個別のレコード保存ポリシーに従うものとする。さもなければ保存期間に関する要件はない。

<!--
The CSP shall comply with their respective records retention policies in accordance with whatever laws and/or regulations apply. Otherwise, no retention period is required.
-->

### 4.2. 認証器保証レベル2(Authenticator Assurance Level 2)
<!--
### 4.2. Authenticator Assurance Level 2
-->

AAL 2は、以前のトランザクションに関わったのと同一の申請者が、保護されたトランザクションやデータにアクセスしようとしていることに、より高い確実性を規定する。少なくとも2つの異なる認証要素が必要である。多要素ソフトウェア暗号認証器を含む、前述の様々なタイプの認証器を利用してもよい。AAL 2は、AAL 3の任意の認証方式を認めている。AAL 2認証は、検証主体なりすまし攻撃同様、AAL 1における全ての脅威に対するプロトコル上の脅威によるセキュリティ侵害から、一次認証器を保護する暗号メカニズムを必要とする。承認済みの暗号技術がAAL 2とそれ以上では必須である。

<!--
AAL 2 provides higher assurance that the same claimant who participated in previous transactions is accessing the protected transaction or data. At least two different authentication factors are required. Various types of authenticators, including multi-factor software cryptographic authenticators, may be used as described below. AAL 2 also permits any of the authentication methods of AAL 3. AAL 2 authentication requires cryptographic mechanisms that protect the primary authenticator against compromise by the protocol threats for all threats at AAL 1 as well as against verifier impersonation attacks. Approved cryptographic techniques are required at AAL 2 and above.
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
* 多要素ソフトウェア暗号認証器
* 多要素暗号デバイス

<!--
* Multi-Factor OTP Device
* Multi-Factor Software Cryptographic Authenticator
* Multi-Factor Cryptographic Device
-->

2つの単一要素認証器を組み合わせる際には、記憶シークレット認証器と、以下のリストから1つの所有ベース("something you have")の認証器を含むこととする(SHALL):

<!--
When a combination of two single-factor authenticators is used, it SHALL include a Memorized Secret authenticator and one possession-based ("something you have") authenticator from the following list:
-->

* ルックアップシークレット
* 経路外
* 単一要素 OTP デバイス
* 単一要素暗号デバイス

<!--
* Look-up Secret
* Out of Band
* Single Factor OTP Device
* Single Factor Cryptographic Device
-->

<!-- > Note: The requirement for a memorized secret authenticator above derives from the need for two different types of authentication factors to be used. All biometric authenticators compliant with this specification are multi-factor, so something you know (a memorized secret) is the remaining possibility. -->

> 注記: 上記の記憶シークレット認証器の要件は、異なる2タイプの認証器要素を利用するということに由来する。本仕様に準拠した全ての生体認証器は多要素であるので、something you know (記憶シークレット)は使っても良いし使わなくても良い。

<!-- TODO remaining possibilityがわからない -->

#### 4.2.2. 認証器及び検証主体 要求事項
<!--
#### 4.2.2. Authenticator and Verifier Requirements
-->

AAL 2で用いられる暗号認証器は、承認された暗号を使うものとする(SHALL)。政府機関によって開発された認証器は、[[FIPS 140]](#FIPS140-2) Level 1の要求事項に適合していることを確認されるものとする(SHALL)。

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

CSPは、あらゆる法律及び規則の適用に対しても合致する個別のレコード保存ポリシーに従うものとする。さもなけれレコードは７年6ヶ月保存しなければならない。

<!--
CSPs shall comply with their respective records retention policies in accordance with whatever laws and/or regulations apply to those entities. Otherwise, retention of records is required for seven years and 6 months.
-->

### 4.3. 認証器保証レベル(Authenticator Assurance Level 3)
<!--
### 4.3. Authenticator Assurance Level 3
-->

AAL 3は、もっとも高い実用的なリモートネットワーク認証の確実性を規定する。AAL3における認証は、暗号プロトコルを通した鍵の所持の証明に基づいている。AAL 3は、"堅牢な"の暗号認証器のみを認めているという点を除けばAAL 2と同一である。

<!--
AAL 3 is intended to provide the highest practical remote network authentication assurance. Authentication at AAL 3 is based on proof of possession of a key through a cryptographic protocol. AAL 3 is similar to AAL 2 except that only “hard” cryptographic authenticators are allowed.
-->

#### 4.3.1. 許可された認証器タイプ
<!--
#### 4.3.1. Permitted Authenticator Types
-->

認証器保証レベル 3では、3種類のハードウェアデバイスのうち、1つを利用する必要がある:

<!--
Authentication Assurance Level 3 requires the use of one of three kinds of hardware devices:
-->

* 多要素 OTP デバイス
* 多要素暗号デバイス
* 単一要素暗号デバイス(記憶シークレットと連動して用いられる)

<!--
* Multi-Factor OTP Device
* Multi-Factor Cryptographic Device
* Single-Factor Cryptographic Device used in conjunction with Memorized Secret
-->




#### 4.3.2. 認証器及び検証主体 要求事項
<!--
#### 4.3.2. Authenticator and Verifier Requirements
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

AAL 3では、ユーザの活動に関わらず、加入者の再認証は少なくとも12時間に1回は繰り返し実施するものとする(SHALL)。加入者の再認証はユーザが活動していない時間が15分を超えないように繰り返し実施することとする(SHALL)。CSPは、望ましい場合、ユーザが活動していないことで生じるタイムアウトの間際に、ユーザに対し活動契機となるように入力を促してもよい(MAY)。

<!--
At AAL 3, authentication of the subscriber SHALL be repeated at least once per 12 hours, regardless of user activity. Reauthentication of the subscriber SHALL be repeated following a period of no more than 15 minutes of user inactivity. It is permissible to prompt the user to cause activity just before the inactivity timeout, if desired.
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

CSPは、あらゆる法律及び規則の適用に対しても合致する個別のレコード保存ポリシーに従うものとする。さもなけれレコードは10年6ヶ月保存しなければならない。

<!--
The CSP shall comply with their respective records retention policies in accordance with whatever laws and/or regulations apply to those entities. Otherwise, retention of records is required for ten years and 6 months.
-->

### 4.4. 要求事項要約
<!--
### 4.4. Summary of Requirements
-->

*(参考; 要求規則は前セクションを参照のこと。)*

<!--
*(Non-normative; refer to preceding sections for normative requirements)*
-->

以下の表は認証器保証レベル毎の要求事項を要約したものである:

<!--
The following table summarizes the requirements for each of the authenticator assurance levels:
-->

要求事項 | AAL 1 | AAL 2 | AAL 3
------------|-------|-------|-------
**許可されている認証器タイプ** | 記憶シークレット<br />ルックアップシークレット<br />経路外<br />単一要素OTPデバイス<br />多要素OTPデバイス<br />単一要素暗号デバイス<br />多要素ソフトウェア暗号認証器<br />多要素暗号デバイス<br /> | 多要素OTPデバイス<br />多要素ソフトウェア暗号認証器<br />多要素暗号デバイス<br />または記憶シークレット(追加):<br />&nbsp;ルックアップシークレット<br />&nbsp;経路外<br />&nbsp;単一要素OTPデバイス<br />&nbsp;単一要素暗号デバイス<br /> | 多要素OTPデバイス<br />多要素暗号デバイス<br />単一要素暗号デバイス ＋ 記憶シークレット
**FIPS 140 確認** | Level 1 (政府機関の検証主体) | Level 1 (政府機関の認証器及び検証主体) | Level 2 全体 (多要素認証器)<br />Level 1 全体 (検証主体及び単一要素暗号デバイス)<br />Level 3 物理セキュリティ (全ての認証器)
**アサーション** | 無記名または所有証明 | 無記名または所有証明 | 所有証明のみ
**再認証** | 30 日 | 12 時間または30分間活動なし; 単一認証要素を利用してもよい | 12 時間または15分間活動なし; 両方の認証要素を利用するものとする
**セキュリティ統制**|[[SP 800-53]](#SP800-53) 低い基準 (または 等価なもの)|[[SP 800-53]](#SP800-53) 適度な基準 (または等価なもの)|[[SP 800-53]](#SP800-53) 高い基準 (または等価なもの)
**レコード保存**|要求なし|7年6ヶ月|10年6ヶ月

<!--

Requirement | AAL 1 | AAL 2 | AAL 3
------------|-------|-------|-------
**Permitted authenticator types** | Memorized Secret<br />Look-up Secret<br />Out of Band<br />SF OTP Device<br />MF OTP Device<br />SF Cryptographic Device<br />MF Software Cryptographic Authenticator<br />MF Cryptographic Device<br /> | MF OTP Device<br />MF Software Cryptographic Authenticator<br />MF Cryptographic Device<br />or memorized secret plus:<br />&nbsp;Look-up Secret<br />&nbsp;Out of Band<br />&nbsp;SF OTP Device<br />&nbsp;SF Cryptographic Device<br /> | MF OTP Device<br />MF Cryptographic Device<br />SF Cryptographic Device plus Memorized Secret
**FIPS 140 verification** | Level 1 (Government agency verifiers) | Level 1 (Government agency authenticators and verifiers) | Level 2 overall (MF authenticators)<br />Level 1 overall (verifiers and SF Crypto Devices)<br />Level 3 physical security (all authenticators)
**Assertions** | Bearer or proof of possession | Bearer or proof of possession | Proof of possession only
**Reauthentication** | 30 days | 12 hours or 30 minutes inactivity; may use one authentication factor | 12 hours or 15 minutes inactivity; shall use both authentication factors
**Security Controls**|[[SP 800-53]](#SP800-53) Low Baseline (or equivalent)|[[SP 800-53]](#SP800-53) Moderate Baseline (or equivalent)|[[SP 800-53]](#SP800-53) High Baseline (or equivalent)
**Records Retention**|Not required|7 years, 6 months|10 years, 6 months
-->



