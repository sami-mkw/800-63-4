<a name="sec4"></a>

# <a name="ial-section"></a> 4. Identity Assurance Level Requirements

本書で扱うパラダイムは, 個人 (この段階では申請者) が, 身元確認を行われて登録されるプロセスである. この段階において, 申請者の身元証明となる書類と属性情報が集められ, 一意に特定されるようなレコードとして登録され, 検証され, 有効になる. これらの属性情報は次に, [SP 800-63B](#800-63b) に記載されている Authenticator に紐づけられる.

<!-- The paradigm of this document is that individuals (referred to as applicants at this stage) undergo an identity proofing and enrollment process, in which their identity evidence and attributes are collected, uniquely resolved to a single identity record, then validated and verified. These attributes are then bound to an authenticator (described in [SP 800-63B](#800-63b)). -->

身元確認が必要な唯一の理由は, 身元確認をを行うことで, 申請者が彼/彼女自身が主張する通りの人物であることを確実にするということである. これには身元確認を達成するのに必要となる最低限の属性情報についての, 証明情報の提示, 妥当性の確認, そして検証が含まれている. このような核となる属性情報はこれらを含む (最低限必要な場合はその他の情報も含む):

<!-- The only outcome of identity proofing is to ensure that the applicant is who he/she claims to be. This includes presentation, validation and verification of the minimum attributes necessary to accomplish identity proofing.  Such core attributes, to the extent they are the minimum necessary, could include:  -->

1. フルネーム
2. 生年月日
3. 住所

<!--
1. Full name
2. Date of birth
3. Home address
-->

本書に明記される要件に従い妥当性確認および検証が行われ, かつ, そのCSPがその属性情報を収集し保存することに対して, 個々に対して明示的な同意を得た場合については, 身元確認の段階で, 個別にその他の追加情報を集めることも可能である.

<!-- It is possible that additional information could be collected in the process of identity proofing an individual, provided validation and verification follow the requirements contained herein, and the individual explicitly consents to the CSP collecting and storing the attributes. -->

## 4.1. Process Flow

[Figure 4-1](#63aSec4-Figure1) は「身元証明」と「登録」についての流れの概要を, 基本的な要件に対応するように記したものである.

<!-- [Figure 4-1](#63aSec4-Figure1) outlines the basic flow for Identity Proofing and Enrollment, to include the corresponding sections with normative requirements. -->

<a name="63aSec4-Figure1"></a>

<div class="text-center" markdown="1">

![](sp800-63a/media/ProofingProcess.png)

**Figure 4-1.  The Identity Proofing Process**

</div>

## 4.2. General Requirements

[Table 4-1](#63aSec4-Table1) は, M-04-04 の保証レベル (LOA) を忠実に厳守した場合, 身元保証レベル (IAL) のどのレベルに対応するかを記している.

<!-- [Table 4-1](#63aSec4-Table1) lists strict adherence to M-04-04 Level of Assurance, mapping the corresponding Identity Assurance Levels.  -->

<a name="63aSec4-Table1"></a>

<div class="text-center" markdown="1">

**Table 4-1.  Legacy M-04-04 IAL Requirements**

</div>

| M-04-04 Level of Assurance (LOA) | Identity Assurance Level (IAL)|
|:------------------:|:-----------------------------:|
| 1 | 1 |
| 2 | 2 |
| 3 | 2 |
| 4 | 3 |

[Table 4-2](#63aSec4-Table2) は, M-04-04 の保証レベル (LOA) を満たすことが許容されている身元保証レベル (IAL) の拡張セットを記している. 各機関は, M-04-04の保証レベル (LOA) に基づいて, 対応するIALを選択する必要がある (SHALL). また, 各機関は, より強固な身元確認を行うことにおけるプライバシーリスクを考慮するべきであり (SHOULD), 事業目的を敏感に考慮して必要以上に高いIALを選択してはならない (SHOULD NOT).

<!-- However, [Table 4-2](#63aSec4-Table2) shows the expanded set of IAL's that are allowable to meet M-04-04 Level of Assurance. Agencies SHALL select the corresponding IAL based on the assessed M-04-04 LOA. Agencies SHOULD consider the privacy risks of stronger identity proofing and SHOULD NOT select an IAL that is higher than necessary considering the sensitivity of the business purpose. -->

<a name="63aSec4-Table2"></a>

<div class="text-center" markdown="1">

**Table 4-2.  Recommended M-04-04 IAL Requirements**

</div>

| M-04-04 Level of Assurance | Identity Assurance Level
|:------------------:|:-----------------------------:
| 1 | 1
| 2 | 1 or 2
| 3 | 1 or 2
| 4 | 1, 2 or 3


以下は, いかなるCSPにおいても, IAL2 もしくは IAL3 の身元確認を行う場合に必要な要件である.

<!-- The following requirements apply to any CSP performing identity proofing at IAL 2 or 3. -->

1. 身元確認は, サービスや利益を享受するのに適切である/権利があるか否かの決定ために行うのは好ましくない (SHALL NOT).
<!-- 1. Identity proofing SHALL NOT be performed to determine suitability/entitlement to gain access to services or benefits. -->

2. CSP は, 他のいかなる属性情報をもってしても, ユーザを一意に特定することができない場合を除き, を SSN を集めるべきではない (SHALL NOT).
<!-- 2. The CSP SHALL NOT collect the SSN unless it is necessary for performing identity resolution and cannot be accomplished by collection of another attribute or combination of attributes. -->

2. 個人を特定できる情報 (PII) の収集は, 申請者の主張する内容が実在して有効であることを確認するため, また, 最善策に基づいて, ユーザを適切に一意に特定し, 検証し, 有効性確認を行うために必要な最低限に限定されるべきである (SHALL).
<!-- 2. Collection of personally identifiable information (PII) SHALL be limited to the minimum necessary to validate the existence of the claimed identity and associate the claimed identity to the applicant providing identity evidence based on best available practices for appropriate identity resolution, validation, and verification. -->

3. 身元確認のために必要な属性情報を収集し, 記録・維持する目的について, CSP は, 申請者に対して情報を収集する際に明示的に通知を行わなければならない (SHALL). その属性情報が任意な情報の場合はもちろん, 身元確認を行うために必須な場合でも, また, その結果属性情報を提示しないという結果に至ったとしても, 通知を行う必要がある (SHALL).
<!-- 3. The CSP SHALL provide explicit notice at the time of collection to the applicant regarding the purpose for collecting and maintaining a record of the attributes necessary for identity proofing, including whether the such attributes are voluntary or mandatory in order to complete the identity proofing transactions and the consequences for not providing the attributes. -->

5. CSP は, いかなる目的でも次にあげる目的以外に身元確認時に収集し保存した属性情報を利用する際は, ユーザの明示的な同意を得なければならない (SHALL NOT): 身元確認, 認証, 認可, 属性情報の証明, その他法律または法的手続きを遵守するもの.   
<!-- 5.     The CSP SHALL NOT use attributes collected and maintained in the identity proofing process for any purpose other than identity proofing, authentication, authorization or attribute assertions, or to comply with law or legal process unless the CSP provides clear notice and obtains consent from the subscriber for additional uses. -->

6. CSP は, 申請者の公平を保つ補償や身元確認で発生する問題に対応するための効果的な手段を提供しなければならない (SHALL). これれの手段は, 申請者からアクセスしやすく見つけやすいところに配置しなければならない (SHALL).
<!-- 6.    The CSP SHALL provide effective mechanisms for redress of applicant complaints or problems arising from the identity proofing. These mechanisms SHALL be easy for applicants to find and access. -->

7. 身元確認ならびに登録のプロセスは, 適切に記述されたポリシー, あるいは, ID 発行時の一般的な段階が仕様化された *practice statement* に従って行われるべきである (SHALL).
<!-- 7. The identity proofing and enrollment processes SHALL be performed according to an applicable written policy or *practice statement* that specifies the particular steps taken to verify identities. -->

3. CSP は申請者への ID 発行時に行った全ての手順の記録を維持しなければならない (SHALL). また, 身元確認時に提示された身分証の種類についても記録しておく必要がある (SHALL). CSP は次のことを決定するために, プライバシーのリスク評価を実施しなければならない (SHALL):  
<!-- 3. The CSP SHALL maintain a record of all steps taken to verify the identity of the applicant and SHALL record the types of identity evidence presented in the proofing process. The CSP SHALL conduct a privacy risk assessment to determine: -->

    a) 申請者の ID を発行するために, 本仕様に記載されている必須要件を超える手順を必要とするか否か.
    <!-- a) Any steps that it will take to verify the identity of the applicant beyond any mandatory requirements specified herein; -->

    b) CSP が, PII (身分証の画像やスキャンデータ, その他のコピー情報を含む) を身元確認時に登録し維持する必要があるか否か. 注) 特定の国家要件が適用される場合もある.
    <!-- b) the PII, including any images, scans, or other copies of the identity evidence that the CSP will maintain as a record of identity proofing. Note: Specific federal requirements may apply; and -->

    c) それらの記録の維持期間. 注) 特定の国立公文書記録管理局 (NARA: Specific National Archives and Records Administration) の記録はその維持期間が適用される.
    <!-- c) the schedule of retention for these records. Note: Specific National Archives and Records Administration (NARA) records retention schedules may apply. -->

6. 登録プロセスにて収集された全ての個人を特定できる情報 (PII) は, 機密性, 完全性, 情報源の帰属を確実にするため, 保護されるべきである (SHALL).   
<!-- 6. All personally identifiable information (PII) collected as part of the enrollment process SHALL be protected to ensure confidentiality, integrity, and attribution of the information source. -->

13. 全ての身元確認のトランザクション (第三者とのトランザクションも含む) は, 認証済みで保護されたチャンネル上 (Authenticated Protected Channel) で行われるべきである (SHALL).
<!-- 13. The entire proofing transaction, including transactions that involve a third party, SHALL occur over an Authenticated Protected Channel. -->

13. <a name="gr13"></a>CSP は, 本書に記載されている必須要件の代わりとして追対策を利用しない限り, 詐称に対する対策を適用することで, CSP はリモートでの身元確認に対して追加の信頼情報を得ることができる (MAY). 例えば, geolocation の調査, 申請者のデバイス特性の調査, 行動特性の評価, あるいは [Death Master File](http://www.ntis.gov/products/ssa-dmf/#) などの重要な統計リポジトリをチェックするなど. そして, それらの対策はプライバシーリスク評価を実施されなければならない (SHALL).
<!-- 13. <a name="gr13"></a>The CSP MAY obtain additional confidence in remote identity proofing using fraud mitigation measures, for example inspecting geolocation, examining the device characteristics of the applicant, evaluating behavioral characteristics, or checking vital statistic repositories such as the [Death Master File](http://www.ntis.gov/products/ssa-dmf/#), so long as any additional mitigations do not substitute for the mandatory requirements contained herein and the CSP SHALL conduct a privacy risk assessment of these mitigation measures. Such assessments SHOULD include any privacy risk mitigations (e.g., limited retention, use limitations, notice, etc.) or other technological mitigations (e.g.,cryptography). -->

12. CSP は, 身元確認および登録プロセス実施しなくなった場合には, CSP は PII を含む機微データの完全な破棄, および, 保管期間中の認められていない不正アクセスからの保護について責任を負わなければならない (SHALL).
<!-- 12. In the event a CSP ceases to conduct identity proofing and enrollment processes, the CSP SHALL be responsible for fully disposing of or destroying any sensitive data including PII, or its protection from unauthorized access for the duration of retention. -->

13. CSP が公的機関であるか民間機関であるかにかかわらず, 身元認証サービスとして提供され利用される機関は次に挙げる要件が適用される:
<!-- 13. Regardless of whether the CSP is an agency or private sector provider, the following requirements apply to the agency offering or using the proofing service: -->

    a) プライバシー保護法や個人情報保護法に基づいて, 身元確認を行うためにPIIの取得が必要であるか否かを決定するため, 公的高等機関に相談するべきである (SHALL).
    <!-- a) The agency SHALL consult with their Senior Agency Official for Privacy to conduct an analysis to determine whether the collection of PII to conduct identity proofing triggers the requirements of the Privacy Act. -->

    b) その結果PIIの取得が必要である場合, 収集し保存する目的についてを公表するべきである (SHALL).
    <!-- b) The agency SHALL publish a System of Records Notice to cover such collections, as applicable. -->

    c) 2002年施行の電子政府法 (the E-Government Act of 2002) に基づいて, 身元確認を行うためにPIIの取得が必要であるか否かを決定するため, 公的高等機関に相談するべきである (SHALL).
    <!-- c) The agency SHALL consult with their Senior Agency Official for Privacy to conduct an analysis to determine whether the collection of PII to conduct identity proofing triggers the requirements of the E-Government Act of 2002. -->

    d) その結果PIIの取得が必要である場合, プライバシーインパクトの評価結果を公表するべきである (SHALL).
    <!-- d) The agency SHALL publish a Privacy Impact Assessment to cover such collections, as applicable. -->

## 4.4. Identity Assurance Level 1

CSPは申請者の身元確認を行ってはならない (SHALL NOT). 申請者がCSPに申請する属性情報の内容は自己申告でよい (MAY).

<!-- The CSP SHALL NOT proof applicants.  Applicants MAY self-assert zero or more attributes to the CSP. -->

## 4.5. Identity Assurance Level 2

IAL2 では, 対面での他リモートでの身元確認も許容されている. このレベルでは, より多くのユーザが対象となるように, 正常な申請者が身元確認を完遂できないといった偽陰性 (false negative) を減らすように, そして悪意のある申請者による不正な身分証の提示は可能な限り検出できるように, 幅広い身元確認方法に対応する. CSP はこれらの要件以上の要件を設定してもよい (MAY).

<!-- IAL 2 allows for remote or in-person identity proofing.  IAL supports a wide range of acceptable identity proofing techniques in order to increase user adoption, decrease false negatives (legitimate applicants that cannot successfully complete identity proofing), and detect to the best extent possible the presentation of fraudulent identities by a malicious applicant. A CSP MAY exceed these requirements. -->

CSP は [Section 4.5.1](#normal) にしたがって身元確認を実装すべきである (SHOULD).
CSP がサービスを提供する対象によっては, CSP は [Section 4.5.2](#antecedent) や [Section 4.5.3](#referee) にしたがった身元確認を実装しても良い (MAY).

<!-- A CSP SHOULD implement identity proofing in accordance with [Section 4.5.1](#normal). Depending on the population the CSP serves, the CSP MAY implement identity proofing in accordance with [Section 4.5.2](#antecedent) or [Section 4.5.3](#referee). -->

### <a name="normal"></a>4.5.1. IAL2 Conventional Proofing Requirements

#### 4.5.1.1. Resolution Requirements

PII の取得は, ユーザを一意に識別するために必要な最低限に限定されるべきである (SHALL). 一般的な要件は [Section 5.2](#resolve) を参照のこと.

<!-- Collection of PII SHALL be limited to the minimum necessary to resolve to a unique identity record.  See [Section 5.2](#resolve) for general resolution requirements. -->

#### 4.5.1.2. Evidence Requirements

利用可能な身分証について, 詳細の情報は [Section 5.3, Identity Evidence Validation](#validate) を参照のこと.

<!-- See [Section 5.3, Identity Evidence Validation](#validate) for more information on acceptable identity evidence. -->

- 上級 (SUPERIOR) 証明書あるいは強力な (STRONG) 証明書を1つ. **その証明証の発行元が身元確認を行う場合**, 申請者の自己申告が正しいか確認を行うため, 上級 (SUPERIOR) 証明書あるいは強力な (STRONG) 証明書を2つ以上必要とする **あるいは**
<!-- - One (1) piece of SUPERIOR or STRONG evidence **if** the issuing source of the evidence, during its identity proofing event, confirmed the claimed identity by collecting two (2) or more forms of SUPERIOR or STRONG evidence; **OR** -->

- 強力な (STRONG) 証明書を2つ **あるいは**
<!-- - Two (2) pieces of STRONG evidence; **OR** -->

- 強力な (STRONG) 証明書1つに加えて, 適切な (ADEQUATE) 証明書2つ
<!-- - One (1) piece of STRONG evidence plus two (2) pieces of ADEQUATE evidence. -->

#### 4.5.1.3. Validation Requirements

利用可能な身分証について, 詳細の情報は [Section 5.3, Identity Evidence Validation](#validate) を参照のこと.
<!-- See [Section 5.3, Identity Evidence Validation](#validate) for more information on acceptable identity evidence. -->

- 各身分証の項目は, 提示されている身分証と同じ強度になるような手順で検証されなければならない. 例えば, 2つの強力な (STRONG) 身分証が提示された場合, それぞれ強力な (STRONG) 強度における検証がなされる.   
<!-- - Each piece of evidence must be validated with a process that is able to achieve the same strength as the evidence presented; For example, if two forms of STRONG identity evidence are presented, each evidence will be validated at a strength of STRONG. -->

- 第三者のデータサービスに対しての検証は, 提示された身分証のうちの片方のみが利用される (SHALL).
<!-- - Validation against a third party data service SHALL only be used for one piece of presented identity evidence. -->

#### 4.5.1.4. Verification Requirements

利用可能な身分証について, 詳細の情報は [Section 5.4, Identity Verification](#verify) を参照のこと.

<!-- See [Section 5.4, Identity Verification](#verify) for more information on acceptable identity evidence. -->

最低限, 強力な (STRONG) 強度を達成するプロセスにて申請者は証明されなければならない.

<!-- At a minimum, the applicant must be verified by a process that is able to achieve a strength of STRONG. -->

#### 4.5.1.5. Presence Requirements

CSPは対面での身元確認を行うべきである (SHOULD) が, リモートで行ってもよい (MAY). 対面とリモートの両方での身元確認を勧めるすべきである (SHOULD).

<!-- The CSP SHOULD perform identity proofing in-person. The CSP MAY perform remote identity proofing. The CSP SHOULD offer both in-person and remote proofing. -->

#### 4.5.1.6. Address Confirmation

- CSP は提示された何らかの正規の身分証に含まれる住所を検証することで, 住所レコードの確認を行うべきである (SHALL).
- Self-asserted な住所データは住所確認のために用いるべきではない (SHALL NOT).

<!--
- The CSP SHALL confirm address of record through validation of the address contained on any supplied, valid piece of identity evidence.
- Self-asserted address data that has not been confirmed in records SHALL NOT be used for confirmation.
-->

- **CSP が対面での Proofing を行う場合**
<!-- - **If CSP performed in-person proofing:**   -->

    - CSP は確認された住所レコードに対して Proofing 通知を送付すること (SHALL).
    <!-- - The CSP SHALL send a notification of proofing to the confirmed address of record. -->
    - Authenticator への紐づけが後日起こりうる場合, CSP は Subscriber に登録コード (Enrollment Code) を直接提供しても良い (MAY).
    <!-- - The CSP MAY provide an enrollment code directly to the subscriber if binding to an authenticator will occur at a later time. -->
    - 登録コードの有効期限は最大7日間とする (SHALL).
    <!-- - The enrollment code SHALL be valid for a maximum of 7 days -->

- **CSP がリモートでの Proofing を行う場合**
<!-- - **If the CSP performed remote proofing:**   -->

    - CSP は登録コードを, 申請者の連絡先に送付すること (SHALL).
    <!-- - A CSP SHALL send an enrollment code to an address of record of the applicant. -->
    - 申請者は身元確認プロセスを完遂するため, 有効な登録コードを提示すること (SHALL).
    <!-- - The applicant SHALL present a valid enrollment code to complete the identity proofing process.     -->
    - CSP は登録コードを検証済みの住所に送るべきである (SHOULD). CSP は登録コードの送信に, 検証済みの携帯電話 (SMS / 音声), 固定電話, Email アドレスなどを利用しても良い (MAY).
    <!-- - The CSP SHOULD send the enrollment code to the physical mailing address that has been verified in records.  The CSP MAY send the enrollment code to a mobile telephone (SMS or voice), landline telephone, or email that has been verified in records. -->
    - 登録コードが認証の要素として利用される場合, 初回利用時にリセットすること (SHALL).
    <!-- - If the enrollment code is also intended to be an authentication factor, it SHALL be reset upon first use. -->
    - 物理的ではない方法で登録コードを送る場合, 有効期間は最大でも10分とする (SHALL). 郵送での送付の場合は, 最大7日とする (SHALL). ただし, 例外として, 米国の郵便サービスが直接配送できる範囲外への郵送により確認する場合, 21日まで有効期間を延ばしてもよい (MAY).
    <!-- - Enrollment codes sent by means other than physical mail SHALL be valid for a maximum of 10 minutes; those sent to a postal address of record SHALL be valid for a maximum of 7 days but MAY be made valid up to 21 days via an exception process to accommodate addresses outside the direct reach of the U.S. postal service.   -->
    - 登録コードが住所に郵送されない場合, CSP は登録コード送付先とは別の宛先に Proofing 通知を送ること (SHALL). 例えば登録コードを携帯電話に送付した場合, Proofing 通知は免許書の住所に送付するなどが考えられる.
    <!-- - If delivery of the enrollment code was sent to an address of record that is not physical mail, the CSP SHALL send notification of proofing to a different address of record than the destination of the enrollment code. For example, if the CSP sends an enrollment code to a mobile phone of record, a notification of proofing will be sent to the postal address in records or obtained from validated and verified evidence, like a drivers license. -->

#### 4.5.1.7. Biometric Collection

[TODO: これ以降最新追随]

CSPはいかなる理由においても, 生体情報を取得するべきではない (SHALL NOT).

<!-- The CSP SHALL NOT collect biometrics for any reason. -->

## <a name="ial3-requirements"></a> 4.6. Identity Assurance Level 3

IAL3では, IAL2で必須なものに加えて, より強度の高い身分証の提示を必要とするなど, さらに厳しい要件が課せられる. 偽装や詐欺, その他影響の大きい損害からRPを守るため, 生体認証の利用を含む特定の追加プロセスが必要となる. 加えて, IAL3における身元確認では対面での確認, あるいは仮想的な対面での確認が必須となる. 詳細は [Section 5.4.3](#vip) を参照のこと. CSPはこれらの要件を満たしているべきである (MAY).

<!-- IAL 3 adds additional rigor to the steps required at IAL 2, to include providing further evidence of superior strength, and is subjected to additional and specific processes, including the use of biometrics, to further protect the identity and RP from impersonation, fraud, or other significantly harmful damages.  In addition, identity proofing at IAL 3 is either performed in-person or via a valid virtual in-person proofing process. See [Section 5.4.3](#vip) for more details. A CSP MAY exceed these requirements. -->

### 4.6.1. Resolution Requirements

PIIの取得は, ユーザを一意に識別するために必要な最低限に限定されるべきである (SHALL). 一般的な要件は [Section 5.2](#resolve) を参照のこと.

<!-- Collection of PII SHALL be limited to the minimum necessary to resolve to a unique identity record.  See [Section 5.2](#resolve) for general resolution requirements. -->

### 4.6.2. Evidence Requirements

利用可能な身分証について, 詳細の情報は [Section 5.3, Identity Evidence Validation](#validate) を参照のこと.   

<!-- See [Section 5.3, Identity Evidence Validation](#validate) for more information on acceptable identity evidence. -->

- 上級 (SUPERIOR) 証明書2つ以上.  **あるいは**  
- 上級 (SUPERIOR) 証明書1つと強力な (STROG) 証明書1つ. **その証明証の発行元が身元確認を行う場合**, 申請者の自己申告が正しいか確認を行うため, 上級 (SUPERIOR) 証明書あるいは強力な (STRONG) 証明書を2つ以上必要とする **あるいは**  
- 強力な (STRONG) 証明書2つと, 適切な(ADEQUATE)証明書1つ.

<!--
- Two (2) or more pieces of SUPERIOR evidence; **OR**
- One (1) piece of SUPERIOR evidence and one (1) piece of STRONG evidence **if** the issuing source of the evidence, during its identity proofing event, confirmed the claimed identity by collecting two (2) or more forms of SUPERIOR or STRONG evidence; **OR**
- Two (2) pieces of STRONG evidence plus one (1) piece of ADEQUATE evidence
-->

### 4.6.3. Validation Requirements  

利用可能な身分証について, 詳細の情報は [Section 5.3, Identity Evidence Validation](#validate) を参照のこと.

<!-- See [Section 5.3, Identity Evidence Validation](#validate) for more information on acceptable identity evidence. -->

- 各身分証の項目は, 提示されている身分証と同じ強度になるような手順で検証されなければならない. 例えば, 2つの強力な (STRONG) 身分証が提示された場合, それぞれ強力な (STRONG) 強度における検証がなされる.   
- 第三者のデータサービスに対しての検証は, 提示された身分証のうちの片方のみが利用される (SHALL).   

<!--
- Each piece of evidence must be validated with a process that is able to achieve the same strength as the evidence presented; For example, if two forms of STRONG identity evidence are presented, each evidence will be validated at a strength of STRONG.
- Validation against a third party data service SHALL only be used for one piece of presented identity evidence.
-->

### 4.6.4. Verification Requirements

利用可能な身分証について, 詳細の情報は [Section 5.4, Identity Verification](#verify) を参照のこと.

<!-- See [Section 5.4, Identity Verification](#verify) for more information on acceptable identity evidence. -->

最低限, 上級 (SUPERIOR) 強度を達成するプロセスにて申請者は証明されなければならない.

<!-- - At a minimum, the applicant must be verified by a process that is able to achieve a strength of SUPERIOR. -->

### 4.6.5. Presence Requirements

全ての身元確認は対面で行われるべきである (SHOULD).

<!-- All identity proofing steps SHOULD be performed in person. -->

[Section 5.4.3](#vip) で示される対面での身元確認の全ての要件と同等な要件を満たせる場合に限り, 仮想的な対面での身元確認を行ってもよい (MAY).

<!-- Virtual in-person identity proofing MAY be employed by a CSP as an equivalent process to in-person identity proofing provided all requirements specified in [Section 5.4.3](#vip) are met. -->

リモートでの身元確認は許容されていない (SHALL NOT).

<!-- Remote proofing SHALL NOT be allowed. -->

### 4.6.6 Address Confirmation

- CSPは身分証 (任意提示のもの含む) から取得した有効な連絡先に対して, 連絡先の確認を行うべきである (SHALL).
- 申請者による自己申告である連絡先は, 確認のために使うべきではない (SHALL NOT).   
- 身元確認完了の通知は, 確認済みの連絡先に対して行うべきである (SHALL).

<!--
- The CSP SHALL confirm address of record through validation of the address contained on any supplied, valid piece of identity evidence.
- Self-asserted address data SHALL NOT be used for confirmation.
- A notification of proofing SHALL be sent to the confirmed address of record.
-->

### 4.6.7. Biometric Collection

CSPは身元確認時, 申請者が登録したことを否認しることを避けるため, 証明写真データや指紋など生体情報を取得する (SHALL). 生体情報の取得についての詳細は, SP 800-63Bの [Section 5.2.3](#biometric_use) を参照のこと.

<!-- The CSP SHALL collect and record a biometric sample at the time of proofing (e.g., facial image or fingerprints) to ensure that the applicant cannot repudiate application.  See [Section 5.2.3](#biometric_use) of SP 800-63B for more detail on biometric collection. -->

## 4.7. Enrollment Code

登録コードにより, CSPはその連絡先が申請者の所有するものであることを確実にすることができる. また, 登録レコードによって, 申請者は登録済みの情報との紐付けをリフレッシュする権限を得られる. 登録レコードとの紐付けは, 身元確認のトランザクションと同じセッションで完遂されるとは限らない.   

<!-- An enrollment code allows the CSP to confirm that the applicant controls an address of record, as well as offers the applicant the ability to reestablish binding to their enrollment record.  Binding is not always completed in the same session as the original identity proofing transaction.   -->

登録レコードは下記のいずれかにより構成されなければならない (SHALL):

<!-- An enrollment code SHALL be comprised of one of the following: -->

* 最低でも, 6文字以上のランダムな英数字により構成  
* 6文字以上のランダム英数字と同様のエントロピーが確保可能な, 機械が読み取り可能なラベル (QRコードなど).

<!--
* Minimually, a random six (6) character alphanumeric.
* A machine readable optical label, such as a QR Code, that contains data of similar or higher entropy as a random six (6) character alphanumeric.
-->

## 4.8. Summary of Requirements
*(Non-normative; refer to preceding sections for normative requirements)*

The following table summarizes the requirements for each of the authenticator assurance levels:

Requirement | IAL 1 | IAL 2 | IAL 3
------------|-------|-------|-------
Presence|No requirements|In-person and remote|In-person or virtual in-person
Resolution|No requirements|The minimum attributes necessary to accomplish identity resolution. KBV may be used for added confidence.||
Evidence|Identity evidence is not required|Two (2) pieces of STRONG evidence<br>**OR**<br>One (1) piece of STRONG evidence plus two (2) pieces of ADEQUATE evidence|One (1) piece of SUPERIOR evidence plus one (1) piece of STRONG evidence<br>**OR**<br>Two (2) pieces of STRONG evidence plus one (1) piece of ADEQUATE evidence
Validation|No validation of evidence is required|- Each piece of evidence must be validated with a process that is able to achieve the same strength as the evidence presented; For example, if two forms of STRONG identity evidence are presented, each evidence will be validated at a strength of STRONG.<br><br>- Validation against a third party data service SHALL only be used for one piece of presented identity evidence.|Same as IAL 2.
Verification| No verification of identity is required |- At a minimum, the applicant must be verified by a process that is able to achieve a strength of STRONG.|- At a minimum, the applicant must be verified by a process that is able to achieve a strength of SUPERIOR.<br>
Address Confirmation|No requirements for address confirmation|- Self-asserted address data SHALL NOT be used for confirmation.<br>- An enrollment code consisting of at least 6 random digits SHALL be included in address confirmation.<br>- May be sent to a mobile telephone (SMS or voice), landline telephone, email, or physical mailing address obtained from records.<br>- If the enrollment code is also intended to be an authentication factor, it SHALL be reset upon first use.<br>- Enrollment codes sent by means other than physical mail SHALL be valid for a maximum of 10 minutes; those sent to a postal address of record SHALL be valid for a maximum of 7 days but MAY be made valid up to 21 days via an exception process to accommodate addresses outside the direct reach of the U.S. postal service.  <br> - A notification of proofing SHALL be sent via a different address of record than the destination of the enrollment code|- The CSP SHALL confirm address of record through validation of the address contained on any supplied, valid piece of identity evidence. - Self-asserted address data SHALL NOT be used for confirmation. - A notification of proofing SHALL be sent to the confirmed address of record.
Biometric Collection|No|No|Yes|


