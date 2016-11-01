<a name="sec1"></a>
<!--
## 1. Purpose
-->

## 1. 目的

<!--
This recommendation and its companion documents, [SP 800-63-3](sp800-63-3.html), [SP 800-63A](sp800-63a.html), and [SP 800-63C](sp800-63c.html), provide technical guidelines to credential service providers for the implementation of digital authentication.
-->

本推奨、及び付随文書 [SP 800-63-3](sp800-63-3.html), [SP 800-63A](sp800-63a.html) 及び [SP 800-63C](sp800-63c.html) は、クレデンシャル・サービス・プロバイダがデジタル認証の実装を行う際の技術的なガイドラインを提供する。

<a name="sec2"></a>

<!--
## 2. Introduction
-->

## 2. イントロダクション

<!--
Digital authentication is the process of establishing confidence in user identities electronically presented to an information system. E-authentication presents a technical challenge when this process involves the digital authentication of individual people over a network. 
-->

デジタル認証は、情報システムにおいて電子的に表現されたユーザのアイデンティティの確かさを証明するためのプロセスである。E-authentiationは、本プロセスがネットワークを介した個々人のデジタル認証に関与する際、技術的なチャレンジを提起する。

<!--TODO E-Authentication -->

<!--
The ongoing authentication of subscribers is central to this process. Subscriber authentication is performed by verifying that the claimant controls one or more *authenticators* (called *tokens* in earlier editions of SP 800-63) associated with a given subscriber. A successful authentication results in the assertion of an identifier, either pseudonymous or non-pseudonymous, and optionally other identity information, to the relying party (RP).
-->

継続的に行われる加入者の認証が本プロセスの中心である。加入者認証は、要求者が、加入者と関連付けられた一つ以上の *認証器* (SP 800-63の以前の版では *トークン* と呼ばれていた)を制御していることを検証することによって実施される。認証が成功すると、識別子（仮名または仮名でない）及びオプションで他のアイデンティティ情報のアサーションが、リライング・パーティ(RP: Relying Party)に提示される。


<!--
This document provides guidelines on types of authentication processes, including choices of authenticators, that may be used at various *Authenticator Assurance Levels* (AAL). It also provides guidelines on the lifecycle of authenticators, including revocation in the event of loss or theft.
-->

本書は、様々な *認証器保証レベル* (AAL)の認証器の選択を含む、認証プロセスの種別の指針を提供する。また、本書は認証器の紛失・盗難に伴う廃棄を含む、認証器のライフサイクルに関する指針を提供する。

<!--
These technical guidelines apply to digital authentication of human users to IT systems over a network. They do not primarily address the authentication of a person who is physically present, for example, for access to buildings, although some credentials that are used remotely may also be used in local authentication. These technical guidelines also establish requirements that Federal IT systems and service providers participating in authentication protocols be authenticated to subscribers. However, these guidelines do not specifically address machine-to-machine (such as router-to-router) authentication, or establish specific requirements for issuing authentication credentials to machines and servers when they are used in e-authentication protocols with people.
-->

これらの技術的なガイドラインは人間のユーザがネットワークを介してITシステムに対して行うデジタル認証に適用される。これらは主として人間が物理的に存在すること ー例えばそのユーザが建物に入館できることー の認証については言及しない。しかしながら、リモートで利用されるクレデンシャルのなかにはローカルの認証でも利用するものがあるかもしれない。また、これらの技術的なガイドラインは、米国連邦のITシステムやサービスプロバイダが加入者を認証するための認証プロトコルに準拠する上での要件を規定している。しかしながら、これらのガイドラインは、(ルータ同士のような)Machine-to-machineの認証については言及していない。また、マシンやサーバに対して発行された認証クレデンシャルが、E-authenticationプロトコル中でユーザを介して利用される際の特別な要件については規定しない。

<!--TODO E-authentication-->

<!--
The strength of an authentication transaction is characterized by a categorization known as the AAL. A high-level summary of the technical requirements for each of the authenticator assurance levels is provided below; see [Section 4](#sec4) and [5](#sec5) of this document for specific normative requirements.

The strength of an authentication transaction is characterized by a categorization known as the AAL. Stronger authentication (a higher AAL) requires a higher level of capabilities and/or resources on the part of an attacker in order to successfully authenticate.  A high-level summary of the technical requirements for each of the authenticator assurance levels is provided below; see [Section 4](#sec4) and [5](#sec5) of this document for specific normative requirements.
-->

認証トランザクションの強度はAALとして知られている分類によって特徴付けられる。より強力な認証(より高度なAAL)では、攻撃者側が認証を成功させるために高度なケーパビリティ及びリソースが必要となる。個々の認証器保証レベルに求められる技術要件の高度なサマリを以下に記載する; 特別な要求規則については、本書の [Section 4](#sec4) 及び [5](#sec5) を参照。


<!--
**Authenticator Assurance Level 1** - AAL 1 provides single factor authentication, giving some assurance that the same claimant who participated in previous transactions is accessing the protected transaction or data. AAL 1 allows a wide range of available authentication technologies to be employed and requires only a single authentication factor to be used. It also permits the use of any of the authentication methods of higher authenticator assurance levels, therefore allowing CSPs to allow users to use a higher AAL authenticator to be at AAL 1. Successful authentication requires that the claimant prove through a secure authentication protocol that he or she possesses and controls the authenticator.

**Authenticator Assurance Level 1** - AAL 1 provides some assurance that the claimant controls the authenticator registered to a subscriber. AAL 1 uses single-factor authentication using a wide range of available authentication technologies. Successful authentication requires that the claimant prove through a secure authentication protocol that he or she possesses and controls the authenticator.
-->

**認証器保証レベル1** - AAL 1は加入者に対して登録された認証器を申請者が制御しているという、いくらかの確実性を持つ。AAL 1では幅広く利用可能な認証技術を利用した、単一要素の認証の利用を用いる。認証が成功するには、その要求者が、セキュアな認証プロトコルを介して、自身がその認証器を所有・制御していることを証明する必要がある。

<!--
**Authenticator Assurance Level 2** – AAL 2 provides high confidence that the claimant controls the authenticator registered to a subscriber. Two different authentication factors are required. Approved cryptographic techniques are required at AAL 2 and above.

-->

**認証器保証レベル2** - AAL 2は、加入者に対して登録されている認証器を申請者が制御しているという高い確実性を持つ。異なる2つの認証要素が必要である。AAL 2及びそれ以上では、承認済み(approved)暗号技術が必要とされる。

<!--
**Authenticator Assurance Level 3** – AAL 3 provides very high confidence that the claimant controls the authenticator registered to a subscriber. Authentication at AAL 3 is based on proof of possession of a key through a cryptographic protocol. AAL 3 is similar to AAL 2 except that a "hard" cryptographic authenticator that also provides impersonation resistance is required.

-->

**認証器保証レベル 3** - AAL 3は、加入者に対して登録されている認証器を申請者が制御しているというかなり高い確実性を持つ。AAL 3における認証は、暗号プロトコルを介した鍵の所有証明(proof of posession)に基づいたものである。AAL 3は、なりすましをも防止する「ハードウェア」暗号化認証器が必要という点を覗いて、AAL 2と同様である。


