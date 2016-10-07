<a name="sec5"></a>

# <a name="ipv-section"></a> 5. Identity Resolution, Validation and Verification

本章では, それぞれのIALのセキュリティ要件を満たすよう, 身元証明においてCSPが従わなければならない (SHALL) 手順や目的を記す.
これらの要件は, 申請者により提示されたアイデンティティはCSPに登録しようとしている人物の実際のアイデンティティであり, 登録済の多くのユーザに対してスケーラブルな攻撃で影響を与えるにはかなりの時間と労力が必要であることを意図している.

<!-- The following sections list the objectives and steps a CSP SHALL follow to identity proof an individual to meet the security requirements per IAL. The requirements are intended to ensure the claimed identity is the actual identity of the person attempting to enroll with the CSP and that scalable attacks effecting a large population of enrolled individuals are difficult to execute without significant time and cost.  -->

## <a name="resolve"></a>5.2. Identity Resolution

1. ユーザ特定のプロセスにおいて複数情報の完全一致を要求することで, 攻撃の達成を困難にすることができます.
CSPは個人情報と, 信頼できる情報源や第三者などをまたがって取得されたその他複数の関連データが異なる場合を違いを考慮した最適なマッチングアルゴリズムを採用してもよい (MAY). マッチングアルゴリズム・規則は, 公開されているかあるいは何らかの方法で確認できるものを利用するべきである (SHOULD). 例えば, 上記で参照された規約や約款の一部として記載されているなど (MAY).

<!-- 1. Exact matches of information used in the proofing process may be difficult to achieve due to multiple factors. The CSP MAY employ appropriate matching algorithms to account for differences in personal information and other relevant proofing data across multiple pieces of evidence, authoritative records, and third party records. Matching algorithms/rules used SHOULD be publicly or community of interest available. For example, they MAY be included as part of the written policy or practice statement referenced above. -->

2. "知っていること"に基づいた証明 (KBV) ("知っていること"に基づいた認証 (KBA) を指すこともある) は, 公的なデータベースから取得できる情報と, 申請者に問うて得られた内容を突合して確認することで提示されているアイデンティティが正当なものであることを証明する方法である. CSPは提示されたアイデンティティを一意に識別するためにKBVを利用してもよい (MAY).

<!-- 2. Knowledge based verification  (KBV)   (sometimes referred to as knowledge based authentication  (KBA) )  is typically used to verify a claimed identity by testing the personal knowledge of the applicant against information obtained from public databases. The CSP MAY use KBV to resolve to a unique, claimed identity. -->

## <a name="validate"></a>5.3. Identity Evidence Validation

身元検証の目的は, 申請者から最も適切な身分証を取得し, その信憑性・有効性・正確性を確認することである. 身分証の検証は, 適切な身分証を取得するプロセスと, それが現存する個人と結びついているものであることを確認するプロセスの, 2つのプロセスから成る.

<!-- The goal of identity validation is to collect from the applicant the most appropriate identity evidence and determine its authenticity, validity, and accuracy.  Identity validation is made up of two process steps: collecting the appropriate identity evidence and confirming the data is valid and related to an actual, live individual. -->

### 5.3.1. Identity Evidence Characteristic Requirements

本節では, 各強度における身分証の性質および品質の要件を記す.

<!-- This section provides requirements on the properties and qualities of identity evidence at a given strength. -->

#### 5.3.1.1. Scoring of Identity Evidence

下表では, 有効なユーザとして登録するために取得された身分証の品質について, 弱い (WEAK) ものから上級 (SUPERIOR) のものまで, 記している. 特に明記されていない限り, その強度を達成するためには少なくとも記載されている全ての性質を満たさなければならない (SHALL).

<!-- The following table lists qualities, ranging from weak to superior, of identity evidence that is collected to establish a valid identity. Unless otherwise noted, to achieve a given strength the evidence SHALL, at a minimum, meet all the properties listed. -->

|強度|身分証の性質|
|:---:|:------------------------------|
|受入不可 (UNACCEPTABLE) |身元確認を行わずに発行されたもの |
|弱い (WEAK) |- 身元確認を行わずに発行されたもの<br><br>- 申請者の所有する連絡先に送付されたと合理的に認めることができるもの<br><br>- 対象者を一意に特定するための番号を1つ以上含んでいるもの|
|適切 (ADEQUATE) |- 身元確認を行って発行されたもの<br><br>- 対象者の所有する連絡先に送付されたと合理的に認めることができるもの<br><br>- 対象者を一意に特定するための番号を1つ以上含んでいるもの<br>**あるいは**<br>対象者の写真, 画像, 生体情報のいずれかを含んでいるもの<br><br>- 所有権をKBVで認することができるもの<br><br>- 電子情報を含む場合, 暗号化 または/かつ 適切な方法で保護されており, 情報の完全性が保証され, 発行元の信頼性が確認できるもの <br><br>- 物理的なセキュリティ機能を有する場合, それを複製するには特殊な技術が必要となるもの<br><br>- 有効期限切れでないもの|
|強力 (STRONG) |- 対象者の正しいアイデンティティであることを合理的に証明できるよう設計されてた手順書に従って確認されたもの. その際に利用される手順書は, 公的機関あるいは認定機関により定期的に監査を受けるなければならない. 例えば, 2001年の米国愛国者法 (USA PATRIOT Act) や[Red Flags Rule] (#rfr), 2003年の公正及び正確信用取引法 (FACT Act) の114章に従って設立された顧客識別プログラムのガイドライン (ustomer Identification Program guidelines) など. <br><br>- 対象者の所有する連絡先に送付されたと合理的に認めることができるもの<br><br>- 対象者を一意に特定するための番号を1つ以上含んでいるもの<br><br>- 身分証に記載されてい申請者の名前が, 発行時に公式にに知られているものであるもの. 偽名や, 名と姓のエイリアスやイニシャル, などは許容されない. <br><br>- 対象者の写真, 画像, 生体情報のいずれかを含んでいるもの<br><br>- 電子情報を含む場合, 暗号化 または/かつ 適切な方法で保護されており, 情報の完全性が保証され, 発行元の信頼性が確認できるもの <br><br>- 物理的なセキュリティ機能を有する場合, それを複製するには特殊な技術が必要となるもの<br><br>- 有効期限切れでないもの|
|上級 (SUPERIOR) |- 対象者の正しいアイデンティティであることを合理的に証明できるよう設計されてた手順書に従って確認されたもの. その際に利用される手順書は, 公的機関あるいは認定機関により定期的に監査を受けるなければならない. <br><br>- 視覚的に申請者のアイデンティティが正しいことを確認され, されに実在確認がおこなわれたもの. <br><br>- 対象者の所有する連絡先に送付されたと合理的に認めることができるもの<br><br>- 対象者を一意に特定するための番号を1つ以上含んでいるもの<br><br>- 身分証に記載されてい申請者の名前が, 発行時に公式にに知られているものであるもの. 偽名や, 名と姓のエイリアスやイニシャル, などは許容されない. <br><br>- 対象者の写真, 画像のいずれかを含んでいるもの<br><br>- 対象者の生体情報を含んでいるもの<br><br>- 電子情報を含む場合, 暗号化 または/かつ 適切な方法で保護されており, 情報の完全性が保証され, 発行元の信頼性が確認できるもの <br><br>- 物理的なセキュリティ機能を有する場合, それを複製するには特殊な技術が必要となるもの<br><br>- 有効期限切れでないもの|

<!--
|Strength|Properties of Identity Evidence|
|:---:|:------------------------------|
|Unacceptable|The issuing source did not perform identity proofing |
|Weak|- The issuing source of the evidence did not perform identity proofing.<br><br>- The issuing process for the evidence means that it can reasonably be assumed to have been delivered into the possession of an individual.<br><br>- The evidence contains at least one reference number that uniquely identifies the person to whom it relates.|
|Adequate|- The issuing source of the evidence confirmed the claimed identity through an identity proofing process.<br><br>- The issuing process for the evidence means that it can reasonably be assumed to have been delivered into the possession of the person to whom it relates.<br><br>- The evidence contains at least one reference number that uniquely identifies the person to whom it relates. <br>**OR**<br> the evidence contains a photograph, image, or biometric of the person to whom it relates.<br><br>- Ownership of the evidence can be confirmed through KBV.<br><br>- Where the evidence includes digital information, that information is protected using cryptographic and/or proprietary methods and those methods ensure the integrity of the information and enable the authenticity of the claimed issuing source to be confirmed. <br><br>- Where the evidence includes physical security features, it requires proprietary knowledge to be able to reproduce it.<br><br> -The issued evidence is unexpired.|
Strong|- The issuing source of the evidence confirmed the claimed identity through written procedures designed to enable it to form a reasonable belief that it knows the true identity of the individual. Such procedures shall be subject to recurring oversight by regulatory or publicly accountable institutions. For example, the Customer Identification Program guidelines established in response to the USA PATRIOT Act of 2001 or the [Red Flags Rule] (#rfr), under Section 114 of the Fair and Accurate Credit Transaction Act of 2003  (FACT Act) <br><br>- The issuing process for the evidence ensured that it was delivered into the possession of the person to whom it relates.<br><br>  -The issued evidence contains at least one reference number that uniquely identifies the person to whom it relates.<br><br>- The applicant's name on the issued evidence must be the name that the identity was officially known at the time of issuance. Pseudonyms, aliases and initials for last name and at least one first name are not permitted.<br><br>- The issued evidence contains a photograph/image/biometric of the person to whom it relates.<br><br>- Where the issued evidence includes digital information, that information is protected using cryptographic and/or proprietary methods and those methods ensure the integrity of the information and enable the authenticity of the claimed issuing source to be confirmed.<br><br>  -Where the issued evidence contains physical security features, it requires proprietary knowledge and proprietary equipment to be able to reproduce it.<br><br>- The evidence is unexpired.|
|Superior|- The issuing source of the evidence confirmed the claimed identity through written procedures designed to enable it to have high confidence it knows the true identity of the individual. Such procedures shall be subject to recurring oversight by regulatory or publicly accountable institutions.<br><br>- The issuing source visually identified the applicant and performed further checks to confirm the existence of that identity.<br><br>- The issuing process for the evidence ensured that it was delivered into the possession of the person to whom it relates.<br><br>- The evidence contains at least one reference number that uniquely identifies person to whom it relates.<br><br>- The applicant's name on the evidence must be the name that the identity was officially known at the time of issuance. Pseudonyms, aliases and initials for first and last names are not permitted.<br><br>- The evidence contains a photograph/image of the person to whom it relates.<br><br>- The evidence contains a biometric of the person to whom it relates.<br><br>- The evidence includes digital information, the information is protected using cryptographic and/or proprietary methods and those methods ensure the integrity of the information and enable the authenticity of the issuing source to be confirmed.<br><br>- The evidence includes physical security features that requires proprietary knowledge and proprietary equipment to be able to reproduce it.<br><br>- The evidence is unexpired.|
-->

### 5.3.2. Validating Identity Evidence

CSPが情報を収集際には, 下記のことが決定できる証明書が提示されていることを決定するため, 正確性・信憑性、関連情報と突合した結果の完全性を信頼出来るソースに対してチェックを行う.

<!-- Once identity evidence is obtained by the CSP, the accuracy, authenticity, and integrity of the evidence and related information is checked against authoritative sources in order to determine that the presented evidence is: -->

* 純正の本物であり, 偽装物や模倣物, 捏造されたものでないこと.
* 記載されている情報が正しいこと.
* 実在する対象者に紐付いている情報であること.

<!--
* Genuine, authentic, and not a counterfeit, fake, or forgery.
* The information is correct.
* The information relates to a real individual.
-->

#### 5.3.2.1. Methods to Perform Identity Evidence Validation

次の表は, 身分証とそこに含まれる情報を検証するために, 許容不可 (UNACCEPTABLE) から上級 (SUPERIOR) までの品質を表示している.

<!-- The following table lists qualities, ranging from unacceptable to superior, of identity validation that is performed to validate evidence and the information contained therein. -->

|強度|方法|
|:---:|:------------------------------|
|受入不可 (UNACCEPTABLE) |検証失敗|
|弱い (WEAK) |All personal details from the evidence have been confirmed as valid by comparison with information held or published by an authoritative source.|
|適切 (ADEQUATE) |- All personal and evidence details have been confirmed as valid by comparison with information held/published by the issuing source.<br>**OR**<br> - The evidence has been confirmed as genuine using appropriate equipment, confirming the integrity of physical security features and lack of fraudulent modification.<br> **OR** <br>- The evidence has been confirmed as genuine by trained personnel. <br> **OR** <br>- The issued evidence has been confirmed as genuine by confirmation of the integrity of cryptographic security features.|
|強力 (STRONG) |- The evidence has been confirmed as genuine using appropriate equipment, confirming the integrity of physical security features and lack of fraudulent modification. **OR** The evidence has been confirmed as genuine by trained personnel and appropriate equipment, confirming the integrity of the physical security features  and lack of fraudulent modification **OR** The evidence has been confirmed as genuine by confirmation of the integrity of cryptographic security features.<br>**AND**<br> - All personal details and evidence details have been confirmed as valid by comparison with information held/published by the issuing source **OR** evidence details have been confirmed as valid by comparison with information held/published by the issuing source.|
|上級 (SUPERIOR) |- The evidence has been confirmed as genuine by trained personnel and appropriate equipment including the integrity of any physical and cryptographic security features.<br>**AND**<br>- All personal details and evidence details from the evidence have been confirmed as valid by comparison with information held/published by the issuing source.|

<!--
|Strength|Method (s) |
|:---:|:------------------------------|
|Unacceptable|Validation of the evidence failed.|
|Weak|All personal details from the evidence have been confirmed as valid by comparison with information held or published by an authoritative source.|
|Adequate|- All personal and evidence details have been confirmed as valid by comparison with information held/published by the issuing source.<br>**OR**<br> - The evidence has been confirmed as genuine using appropriate equipment, confirming the integrity of physical security features and lack of fraudulent modification.<br> **OR** <br>- The evidence has been confirmed as genuine by trained personnel. <br> **OR** <br>- The issued evidence has been confirmed as genuine by confirmation of the integrity of cryptographic security features.|
|Strong|- The evidence has been confirmed as genuine using appropriate equipment, confirming the integrity of physical security features and lack of fraudulent modification. **OR** The evidence has been confirmed as genuine by trained personnel and appropriate equipment, confirming the integrity of the physical security features  and lack of fraudulent modification **OR** The evidence has been confirmed as genuine by confirmation of the integrity of cryptographic security features.<br>**AND**<br> - All personal details and evidence details have been confirmed as valid by comparison with information held/published by the issuing source **OR** evidence details have been confirmed as valid by comparison with information held/published by the issuing source.|
|Superior|- The evidence has been confirmed as genuine by trained personnel and appropriate equipment including the integrity of any physical and cryptographic security features.<br>**AND**<br>- All personal details and evidence details from the evidence have been confirmed as valid by comparison with information held/published by the issuing source.|
-->

## 5.4. <a name="verify"></a> Identity Verification

身元検証の目標は, 提示された物理的に現存しているアイデンティティと, それらを提示している実際の人物を紐付けることである.

<!-- The goal of identity validation is to establish a linkage to the physical, live existence of the claimed identity to the person actually presenting the evidence. -->

### 5.4.1. Identity Verification Methods

The following table details the verification methods necessary to achieve a given identity verification strength.  

|Strength|Identity Verification Methods|
|:---:|:------------------------------|
|Unacceptable|Unable to confirm that the applicant is the owner of the claimed identity.|
|Weak|The applicant has been confirmed as having access to the evidence provided to support the claimed identity.|
|Adequate|- The applicant’s ownership of the claimed identity has been confirmed by Knowledge Based Verification.  See [Section 5.3.2] (#kbv)   for more details.<br>**OR**<br>- The applicant’s ownership of the claimed identity has been confirmed by a physical **OR** biometric comparison of the applicant to the strongest piece of evidence provided.|
|Strong|- The applicant’s ownership of the claimed identity has been confirmed by physical comparison using a photograph/image **OR** Biometric comparison of the Applicant to the strongest piece of evidence provided to support the claimed identity.<br>**OR**<br>- A trusted referee confirms the identity of the applicant.|
|Superior|- The applicant’s ownership of the claimed identity has been confirmed by biometric comparison of the applicant to the strongest piece of evidence provided to support the claimed identity.<br>**AND**<br>- The applicant’s ownership of the claimed identity has been confirmed by an interaction with the applicant via the postal address of record.|

The CSP MAY use KBV to verify the identity of an applicant provided the requirements in Section [Knowledge Based Verification Requirements] (#kbv)  are met.

### <a name="kbv"></a>5.4.2. Knowledge Based Verification Requirements

The following requirements apply to the identity verification steps for IAL 2 and 3. There are no restrictions for the use of KBV for identity resolution.

- KBV SHALL NOT be used if the CSP is not, or does not maintain a relationship with, an authoritative source.
- KBV SHALL NOT be based on data held by the issuing source of an applicant's supplied identity evidence.
- The CSP SHALL only use information that is expected to be known only to the applicant, to include any information that in needed to trigger KBV processes. Information accessible freely or for any fee in the public domain SHALL NOT be used.
- The CSP SHALL allow a resolved, validated, or verified identity to opt-out of KBV.

- The CSP SHOULD verify knowledge of recent transactional history that the CSP is a participant to.  The CSP SHALL ensure transaction information meets the minimum entropy for a Memorized Secret. For example, verification of amount and confirmation number of a micro-deposit to a claimed and valid bank account.

- The CSP MAY perform KBV by asking questions of the claimed identity to demonstrate they are the owner of the claimed information.
	- The CSP SHALL require a minimum of four  (4)  KBV questions each requiring a correct answer to successfully complete the KBV step.
	- The CSP SHOULD require a free form response to a KBV question.  The CSP MAY allow multiple choice answers, however, the CSP SHALL require a minimum of four  (4)  multiple choice KBV answers per question.
	- The CSP SHOULD allow two  (2)  attempts for an applicant to complete the KBV.  A CSP MAY allow no more than three  (3)  attempts to complete the KBV.
	- The CSP MAY use KBV to verify an applicant's identity against one  (1)  piece of validated identity evidence.  
	- The CSP SHALL NOT present diversionary KBV questions.  The CSP SHALL NOT allow answers to KBV questions be 'None of the Above', 'Not Applicable  (N/A) ', or similar to be regarded as correct.
	- The CSP SHALL NOT ask the same KBV questions in subsequent attempts.
	- The CSP SHALL NOT ask a KBV question that effectively answers any future KBV question, either in the current session or subsequent attempts.
	- The CSP SHALL NOT use data that does not change regularly over a period of time.
	- The CSP SHALL ensure that any KBV approach does not reveal PII that the applicant has not already provided.
	- The CSP SHALL time out KBV sessions after 2 minutes of inactivity per question.  In cases of session timeout, the CSP SHALL restart the entire KBV process.


### <a name="vip"></a>5.4.3. Virtual In-person Proofing Requirements

Virtual in-person identity proofing and enrollment transaction SHALL meet the following requirements, in addition to the IAL 3 validation and verification requirements specified in [Section 4.6] (#ial3-requirements) :

1. The CSP SHALL monitor the entire identity proofing transaction, from which the applicant SHALL NOT depart during the identity proofing session.  For example, by a continuous high-resolution video transmission of the applicant.
2. The CSP SHALL require all actions taken by the applicant during the enrollment and identity proofing process are visible.
4. All digital verification of evidence  (e.g., via chip or wireless technologies)  SHALL be performed by scanners and sensors that are integrated into the solution and in the entire field of view of the camera and the remote, live operator.
5. Collection of biometrics SHALL be done in such a way that ensures that the biometric is collected from the applicant, and not another individual. All biometric requirements in [SP 800-63B, Section 5.2.3 Biometric Considerations] (sp800-63b.html/#biometric_use)  apply.
6. The CSP SHALL have an operator participate remotely with the applicant for the entirety of the enrollment and identity proofing session.
7. A CSP SHOULD have an operator participate in-person, at the same physical location as the applicant, for the entirety of the enrollment and identity proofing session.
8. The CSP SHALL have the live operator view the biometric source  (e.g., fingers or face)  for presence of non-natural materials.
6. The CSP SHALL require operators to have undergone a training program to detect potential fraud.
7. The CSP SHALL employ tamper detection and resistance features appropriate for the environment in which it is located. For example, a kiosk located in a restricted area or one where it is monitored by a trusted individual requires less tamper detection than one that is located in a semi-public area such as a retail store.
8. All communications CSP SHALL take place over a mutually authenticated encrypted session.



### 5.4.4. Trusted Referee Requirements

The CSP MAY determine to utilize trusted referees, such as notaries, legal guardian, or some other form of certified individual that can legally vouch for and/or act on behalf of the individual.  CSP MAY use a trusted referee for both remote and in-person processes.  

In addition, antecedent in-person identity proofing MAY be allowed at IAL2.  See [The Federal Bridge Certification Authority  (FBCA)  Certificate Policy  (CP) ] (#fbcacp), Section 3.2.3.1 Authentication of Human Subscribers for Medium Assurance _and_ [FBCA Supplementary Antecedent, In-Person Definition] (#fbcasup)  for more details.

In some instances, the CSP MAY allow an individual that has successfully completed identity proofing with the same CSP to act as a trusted referee for another individual.  The CSP SHALL not accept this type of trusted referee verification at IAL3.

### 5.4.5. Considerations for Minors and People with Unique Needs
Enrollment of minors under age 18, unable to meet the evidence requirements of identity proofing SHOULD involve a parent or legal adult guardian as a trusted referee as described in Section 5.3.4. Minors under age 13 require special consideration to ensure compliance with the Children's Online Privacy Protection Act of 1998, 15 USC 6501-6505 and 16 CFR Part 312.

Other individuals may have difficulty completing the identity proofing process based on various circumstances, such as not possessing the complete set of evidence requirements at a given IAL.  In these circumstances, the CSP SHOULD allow the applicant to be enrolled by a conservator or other person with power of attorney.

## 5.5. Binding Requirements

ユーザにオーセンティケーターを紐付ける手順については, [800-63B, Section 6.1, Authenticator Binding] (#binding)  を参照のこと.