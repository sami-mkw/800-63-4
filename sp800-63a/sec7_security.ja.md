<a name="sec7"></a>

# 7. Threats and Security Considerations

登録のプロセスにおける脅威は, 2つの一般的なカテゴリのものが存在する. なりすまし, そしてインフラ (CSP) による不正あるいはインフラ (CSP) の乗っ取り. 本章における推奨事項は, なりすましの脅威への対処に焦点を当てている. インフラの脅威は, 一般的なコンピュータセキュリティ管理 (責任分離, 記録保持, 独立監査など) によって対処することとし, 本書の定める範囲外とする.

<!-- There are two general categories of threats to the enrollment process: impersonation and either compromise or malfeasance of the infrastructure (CSPs). This recommendation focuses on addressing impersonation threats. Infrastructure threats are addressed by normal computer security controls (e.g., separation of duties, record keeping, independent audits) and are outside the scope of this document. -->

なりすまし攻撃を含む登録プロセスにおける脅威は, 身元確認時の書類 (データ) 送付時, オーセンティケーターとの結合時, クレデンシャルの発行時に発生する. [Table 7-1](#63aSec7-Table1) は, 登録および身元確認における脅威のリストである.

<!-- The threats to the enrollment process include impersonation attacks and threats to the transport mechanisms for identity proofing, and authenticator binding, and credential issuance. [Table 7-1](#63aSec7-Table1) lists the threats related to enrollment and identity proofing. -->

<a name="63aSec7-Table1"></a>

<div class="text-center" markdown="1">

**Table 7-1.  登録および身元確認プロセスにおける脅威**
<!-- **Table 7-1.  Enrollment and Identity Proofing Threats** -->

</div>

| **行動**   |     **脅威/攻撃**  | **例** |
|登録 | 偽装された身分証 | 偽装した運転免許章を利用して不正な申請が行われる. |
| | 他者の証明書の不正利用 | 他人のパスポートを利用して不正な申請が行われる. |
| | 登録の否認| 登録済のユーザが, CSPに対して登録していないと主張し, 登録を否認する. |
||Social engineering|A malicious applicant manipulates an individual responsible for identity proofing in order to be enrolled as another individual.
|発行 |漏えい | CSPにより, 登録済みユーザに発行されたキーが攻撃者によってコピーされ, オーセンティケーターを発行する際にCSPからユーザにそれが渡されてしまう. |
| |改ざん | ユーザによって作成された新しいパスワードが攻撃者によって変更され, CSPでのクレデンシャル発行フェーズで登録されてしまう. |
| |不正発行 | 実際にはそのユーザではないにもかかわらずそうであると主張する攻撃者に対して, そのユーザのクレデンシャルを発行してしまう. |
||Social engineering|A malicious person manipulates an individual responsible for issuance in order to obtain a credential bound to another, valid subscriber.
|||If social engineering was successful at enrollment, obtaining a credential requires no extra effort.

<!--
|**Activity**   |     **Threat/Attack**  | **Example** |
|---------------|------------------------|------------------|
|Enrollment | Falsified identity proofing evidence | An applicant claims an incorrect identity by using a forged driver's license.|
| | Fraudulent use of another's identity | An applicant uses a passport associated with a different individual
| | Repudiation of enrollment | A subscriber denies enrollment, claiming that he or she did not enroll with the CSP.|
||Social engineering|A malicious applicant manipulates an individual responsible for identity proofing in order to be enrolled as another individual.
|Issuance|Disclosure | A key created by the CSP for a Subscriber is copied by an attacker as it is transported from the CSP to the subscriber during authenticator issuance.|
| |Tampering | A new password created by the subscriber is modified by an attacker as it is being submitted to the CSP during the credential issuance phase.
| |Unauthorized issuance | A person claiming to be the subscriber (but in reality is not the subscriber) is issued credentials for that subscriber.
||Social engineering|A malicious person manipulates an individual responsible for issuance in order to obtain a credential bound to another, valid subscriber.
|||If social engineering was successful at enrollment, obtaining a credential requires no extra effort.
-->

## 7.1. Threat Mitigation Strategies

登録プロセスにおける脅威は, なりすましでの完遂を困難にすること, 不正検出の精度を高めることによって抑制することができる. ここでの推奨事項は, 主になりすましをより困難にする方法についてである. とはいえ, 誰がなりすましを行ったのかを証明するのにも役立つ可能性のある手順や方法である. 各レベルにおいてこれらは, 申請中の人物が実在するか否か, 申請者は本当に申請中の人物として識別される権利を有するのかを決定し, 登録後に登録したことを否認できないようにするための方法としても採用される. 保証されるレベルが上がるに伴い, 簡単ななりすまし, 機械的ななりすまし, 関係者によるなりすましに対する抑制効果が高い方法が利用される. [Table 7-2](#63aSec7-Table2) は, 登録時・発行時における脅威の低減策のリストである.

<!-- Enrollment threats can be deterred by making impersonation more difficult to accomplish or by increasing the likelihood of detection. This recommendation deals primarily with methods for making impersonation more difficult; however, it does prescribe certain methods and procedures that may help to prove who carried out an impersonation. At each level, methods are employed to determine that a person with the claimed identity exists, that the Applicant is the person who is entitled to the claimed identity, and that the Applicant cannot later repudiate the enrollment. As the level of assurance increases, the methods employed provide increasing resistance to casual, systematic and
insider impersonation. [Table 7-2](#63aSec7-Table2) lists strategies for mitigating threats
to the enrollment and issuance processes. -->


<a name="63aSec7-Table2"></a>

<div class="text-center" markdown="1">

**Table 7-2.  登録時・発行時における脅威の低減策**
<!-- **Table 7-2.  Enrollment and Issuance Threat Mitigation Strategies** -->

</div>

| **行動**   |     **脅威/攻撃**  | **低減策** |
| 登録 | 偽装された身分証 | 提示された証明書の物理的なセキュリティ機能を検証する. |
| | 他者の証明書の不正利用 | 他の発行元あるいは信頼できるソースから得られた情報と突合して申請者の提示する身分証を検証する, あるいは生体情報を検証する. |
| | | Verify Applicant-provided non-government issued documentation  (e.g. electricity bills in the name of the Applicant with the current address of the Applicant printed on the bill, or a credit card bill)  to help in achieving a higher level of confidence in the identity of the applicant. |
| | 登録の否認 | Have the applicant sign a form acknowledging participation in the enrollment activity. |
||Social engineering|Duplicate records check.
| | |
| 発行 | 漏えい | Issue the authenticator in person, physically mail it in a sealed envelope to a secure location, or use a protected session to send the authenticator electronically.|
| | 改ざん | Issue credentials in person, physically mailing storage media in a sealed envelope, or through the use of a communication protocol that protects the integrity of the session data.|
| | | Establish a procedure that allows the Subscriber to authenticate the CSP as the source of any authenticator and credential data that he or she may receive.|
| | 不正発行 / Social engineering | Establish procedures to ensure that the individual who receives the authenticator is the same individual who participated in the enrollment procedure.|
| | | Implement a dual-control issuance process that ensures two independent individuals shall cooperate in order to issue an authenticator.|

<!--
| **Activity** | **Threat/Attack** | **Mitigation Strategy** |
|--------------|-------------------|-------------------------|
| Enrollment | Falsified identity proofing evidence | CSP validates physical security features of presented evidence.
| | | CSP validates personal details in the evidence with the issuer or other authoritative source.
| | Fraudulent use of another's identity | CSP verifies identity evidence or biometric of applicant against information on evidence or obtained from issuer or other authoritative source.
| | | Verify Applicant-provided non-government issued documentation (e.g. electricity bills in the name of the Applicant with the current address of the Applicant printed on the bill, or a credit card bill) to help in achieving a higher level of confidence in the identity of the applicant. |
| | Repudiation of enrollment | Have the applicant sign a form acknowledging participation in the enrollment activity. |
||Social engineering|Duplicate records check.
| |
| Issuance | Disclosure | Issue the authenticator in person, physically mail it in a sealed envelope to a secure location, or use a protected session to send the authenticator electronically.
| | Tampering | Issue credentials in person, physically mailing storage media in a sealed envelope, or through the use of a communication protocol that protects the integrity of the session data.
| | | Establish a procedure that allows the Subscriber to authenticate the CSP as the source of any authenticator and credential data that he or she may receive.
| | Unauthorized issuance/Social engineering | Establish procedures to ensure that the individual who receives the authenticator is the same individual who participated in the enrollment procedure.
| | | Implement a dual-control issuance process that ensures two independent individuals shall cooperate in order to issue an authenticator.
-->
