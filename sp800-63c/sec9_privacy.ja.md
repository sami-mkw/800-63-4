<a name="sec9"></a>

## <a name="privacy-section-header"></a> 9. Privacy Considerations

本章の内容は参考情報である.

<!-- These privacy considerations are non-normative. -->

9.1 Minimizing Tracking and Profiling

Section 4, 4.1.4 および 5.2.5 では, Tracking および Profiling 能力の向上によりもたらされる Privacy リスクの最小化を目的とした要件をまとめた.
例えば複数の RP に対して同じ IdP を利用して認証を行う Subscriber がいた場合, IdP は Federation を行わない時は存在しえなかった Subscriber Transaction の Profile を構築することができるようになる.
そのようなデータは Subscriber が感知せず望みもしないような使い方をされる危険性を孕んでいる.
Federation は RP および Subscriber に多くの恩恵をもたらすが, Subscriber による IdP に対する信頼を必要とする.
Federation Model において Subscriber の信頼を構築するには, Subscriber のデータ利用が適切に制限され, データ収集時の目的に限定されていることが重要である.
利用目的の範囲内に収まっているかどうかが疑問な際は, Senior Agency Official for Privacy に相談のこと.

<!-- Sections 4, 4.1.4, and 5.2.5 cover a number of requirements the objective for which is to minimize privacy risks arising from increased capabilities to track and profile subscribers. For example, a subscriber using the same IdP to authenticate to multiple RPs allows the IdP to build a profile of subscriber transactions that would not have existed absent federation.  The availability of such data makes it vulnerable to uses that may not be anticipated or desired by the subscriber.  Federation offers numerous benefits to RPs and subscribers, but requires subscribers to have trust in the IdP.  Accordingly, to build subscriber trust in a federated model, it is important that uses of subscriber data are appropriately limited and scoped to the purpose for which it was originally collected. Consult your Senior Agency Official for Privacy if there are questions about whether proposed agency uses fall within the scope of these uses. -->

Section 4 は Unlinkability を提供し Subscriber Activity の Tracking と Profiling を防止する技術的対策を推奨している.
IdP のポリシーと手順は適切な利用制限および目的明確化の原則の順守のために重要な要素であるが, 4.1.4 で述べた Distributed Federation や 5.2.5 で述べた Pairwise Pseudonymous Identifier ような技術的対策は, Subscriber のデータにアクセスすることをより困難にし, IdP のポリシーをより有効なものとする.

<!-- Section 4 also encourages the use of technical measures to provide unlinkability and prevent subscriber activity tracking and profiling.  While IdP policies and procedures are important in ensuring adherence to appropriate use limitation and purpose specification principles, technical measures such as outlined in 4.1.4 for distributed federation and 5.2.5 for pairwise pseudonymous identifiers, can increase the effectiveness of these policies by making subscriber data more difficult to access. -->


9.2 Notice and Consent

Federation において Subscriber の Trust を構築するには, Subscriber に対して Transparency が確保されていなければならず, どのような情報が送信されるのか, どれが必須でどれがオプショナルなのかが Subscriber に理解され, オプショナルな属性を RP に送るかどうかの決定権が Subscriber に与えられている必要がある.
Section 6 が Subscriber に関するいかなる属性の送信に際してもその送信前に Subscriber による Positive Confirmation を要求しているのも, そのような訳である.
UX スタンダード & リサーチ, およびデータ収集に伴って発生するプライバシーリスクに関するアセスメントを考慮した, 効果的な Notice が重要となろう.
考慮すべき点は, Subscriber がデータ収集の結果として予期するであろう内容の信頼性, Subscriber から収集した上納にその他の情報を紐付けるか否かなど, 多岐にわたる.
効果的な Notice とは, 相当数の Subscriber が読みもせず理解もしないであろう複雑で法律用語に満ちた Privacy Policy や一般契約条件 (General Terms and Conditions) へのリンクではないことだけは注意すること.

<!-- To build subscriber trust in federation, transparency must be provided to the subscriber to understand what information will be transmitted, what is required versus optional, and the ability to decide whether to transmit optional attributes to the RP.  Accordingly, Section 6 requires that positive confirmation be obtained from the subscriber before any attributes about the subscriber are transmitted to any RP.  An effective notice will take into account user experience design standards and research, as well as an assessment of privacy risks that may arise from the collection. There are many factors that should be considered, including the reliability of the assumptions Subscribers may have about the collection, whether other information is being collected and appended to the information collected from the Subscriber. However, an effective notice is never only a link that leads to a complex, legalistic privacy policy or general terms and conditions that a substantial number of Subscribers do not read or understand. -->

Section 6 はどの主体が Notice を提示すべきかを指定していない.
Federation においては, Subscriber に Notice を行い Consent を得るための Subscriber への直接のコネクションを持たない主体も存在しうる.
複数の主体が Notice を行うこともありうるが, あらかじめ契約や Trust Framework Policy によってどの主体が Notice を行い Confirmation を得るかを取り決めておくことも可能である.
ただしそのような取り決めを行う際は, Subscriber が Notice に気づき, 十分な説明を受けよく考えた上での選択 (Informed Choice) を行えることを前提とすること.

<!-- Section 6.0 does not specify which party should provide the notice.  In some cases, a party in a federation may not have a direct connection to the subscriber to provide notice and obtain consent. Although multiple parties may elect to provide notice, it is permissible for parties to determine in advance either contractually or through trust framework policies which party will provide the notice and obtain confirmation, as long as the determination is being based upon factors that center on enabling the subscriber to pay attention to the notice and make an informed choice. -->



9.3 Data Minimization

IdP が RP の要求以上の追加属性を収集することもあるが, 送信する属性は RP が明示的に要求したものに限定すること.
場合によっては, RP がある属性についての完全な値を必要としないこともありうる.
Subscriber が13歳以上かどうかを知りたいが, 完全な生年月日は必要としない場合などが例として挙げられる.
潜在的にセンシティブな PII の収集を最小化するため, RP は "Subscriber は13歳以上か? (Y/N)" などの Attribute Claim を要求することもできる.
そうすることで RP はセンシティブかつ不要な PII の収集を最小化できる.
このようなことから, Section 6.4 では RP に可能な限り完全な Attribute Value ではなく Attribute Claim を要求するよう求めている.

<!-- Although an IdP may collect additional attributes beyond what the RP requires for its use case, only those attributes that were explicitly requested by the RP are to be transmitted by the IdP. In some instances, an RP does not require a full value of an attribute is not necessary; for example an RP may need to know whether the subscriber is over 13 years old, but has no need for the full date of birth. To minimize the collection of potentially sensitive PII, the RP may request an attribute claim (e.g., is the subscriber over 13 years old? Y/N, Pass/Fail).  This minimizes the RPs collection of potentially sensitive and unnecessary PII.  Accordingly, Section 6.4 requires the RP to, where feasible, request attribute claims rather than full attribute values.  To support this RP requirement, IdPs are in turn, required to support attribute claims. -->


9.4 Agency Specific Privacy Compliance

Section 4 では Privacy Compliance Requirements 策定のため SAOP (Senior Agency Official for Privacy) と協議すべき要件について定めている.
各機関は Digital Authentication システム構築の早い段階から担当 SAOP を関与させること.
Privacy リスクの評価と対策, Privacy Act of 1974 や E-Government Act of 2002 に定められた Privacy Impact Assesment 実施義務の有無などについて, 早期の段階から SAOP の意見を聞くことは非常に重要である.
例えばある機関が Federation において Credential Service Provider を提供している場合, RP となる機関の代理で Credential を管理することになるため, Privacy Act 要件を求められ, 新規もしくは既存の Privacy Act System of Records の対象となるだろう.
しかしながらある機関が Relying Party であり 3rd party の IdP を使って Digital Authentication を実現している場合は, どのようなデータが RP に渡り RP がどのような管理を行うかによって Privacy Act 要件を求められないこともある.
(そのような場合は当該機関は当該データをカバーするより広くプログラマティックな SORN (System of Records Notices) を提出することになろう)
SAOP は同時に PIA の要・不要についても当該機関をサポートできる.
これらの Considerations は Privacy Act System of Records Notice や PIA を Federated Credential の利用のためだけに要求するものではない.
多くの場合は, Digital Authentication プロセス全体を網羅した PIA や SORN を記述したり, 当該機関がオンラインアクセスを提供するプログラムやベネフィットについて検討する広範囲の PIA の一部として Digital Authentication プロセスを位置付けるのが良いだろう.

<!-- Section 4.0 identifies agency requirements to consult their SAOP to determine privacy compliance requirements. It is critical to involve your agency’s SAOP in the earliest stages of digital authentication system development to assess and mitigate privacy risks and as advise the agency on compliance obligations such as whether the federation triggers the Privacy Act of 1974 or the E-Government Act of 2002 requirement to conduct a Privacy Impact Assessment.  For example, if the Agency is serving as a Credential Service Provider in a federation, it is likely that the Privacy Act requirements will be triggered and require coverage by either a new or existing Privacy Act system of records since credentials would be maintained on behalf of the agency RP.  If, however, the agency is a Relying Party and using a 3rd party IdP digital authentication may not trigger the requirements of the Privacy Act depending on what data passed from the RP are maintained by the agency as the RP (in such instances the agency may have a broader programmatic SORN that covers such data).  The SAOP can similarly assist the agency in determining whether a PIA is required.  These considerations should not be read as a requirement to develop a Privacy Act System of Records Notice or PIA for use of a federated credential alone; in many cases it will make the most sense to draft a PIA and SORN that encompasses the entire digital authentication process or include the digital authentication process as part of a larger programmatic PIA that discusses the program or benefit the agency is establishing online access. -->

Digital Authentication の要素は多岐にわたるため, SAOP は各個別要素の認識と理解を持ち, どのようなコンプライアンス要件が必要かを適切に助言することが重要である.
さらに言えば, SOAP が Digital Authentication の個別要素に関して綿密に理解することによって, コンプライアンスプロセス等を通じたプライバシーリスクの正確な評価と対策が可能になるのである.

<!-- Due to the many components of digital authentication, it is important for the SAOP to have an awareness and understanding of each individual component so as to advise appropriately on what compliance requirements apply. Moreover a thorough understanding of the individual components of digital authentication will enable the SAOP to thoroughly assess and mitigate privacy risks either through compliance processes or by other means. -->