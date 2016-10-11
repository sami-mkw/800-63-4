<a name="sec5"></a>

## 5. <a name="AAL_SEC5"></a>認証器及び検証主体の要求事項
<!--## 5. <a name="AAL_SEC5"></a>Authenticator and Verifier Requirements-->

本章では、各認証器タイプごとの要求仕様詳細について明らかにする。4章で指定されたバリデーション要求事項の例外とともに、各認証器タイプごとの技術的要求事項が、それが利用されるAALとは関係なく、同じである。

<!--
This section provides the detailed requirements specific for each of the authenticator types. With the exception of validation requirements specified in Section 4, the technical requirements for each of the authenticator types is the same regardless of the AAL at which it is used.
-->

### 5.1. 認証器タイプ毎の要求事項
<!--### 5.1. Requirements by Authenticator Type-->

#### 5.1.1. 記憶シークレット
<!--#### 5.1.1. Memorized Secrets-->

<div class="text-left" markdown="1">
<table style="width:100%">
  <tr>
    <td><img src="sp800-63b/media/Memorized-secret.png" alt="authenticator" style="width: 100px;height: 100px"/></td>
    <td>記憶シークレット認証器(一般的にはパスワードや、数字ならばPinとして表されているもの) は、ユーザによって決められ、記憶されるシークレットである。記憶シークレットは攻撃者が正しい値を推測したり特定できないように、十分な複雑かつ秘密の状態にしておく必要がある。   
    </td>
    <!--
    <td>A Memorized Secret authenticator (commonly referred to as a <i>password</i> or <i>PIN</i> if it is numeric) is a secret value that is intended to be chosen and memorizable by the user. Memorized secrets need to be of sufficient complexity and secrecy that it would be impractical for an attacker to guess or otherwise discover the correct secret value.</td> 
    -->
  </tr>
  </table>
  </div>

##### 5.1.1.1. 記憶シークレット認証器
<!--##### 5.1.1.1. Memorized Secret Authenticators-->

記憶シークレットは、加入者が指定する場合少なくとも8文字とするものとする(SHALL)。記憶シークレットがCSPまたは検証主体によってランダムに選択されたものである場合は、少なくとも6文字であるものとし(SHALL)、全て数字でもよい(MAY)。
CSPや検証主体は、指定された記憶シークレットがセキュリティ侵害を受けたブラックリストに出現するかどうかに基づいて拒否するかもしれず、そのような場合に加入者は、別の記憶シークレット値を選ぶものとする(SHALL)。
その他、記憶シークレットに課される複雑さに関する要求事項はあるべきではない(SHOULD)。このことについての根拠は[Appendix A](#appA)に記載されている。

<!--
Memorized secrets SHALL be at least 8 characters in length if chosen by the subscriber; memorized secrets chosen randomly by the CSP or verifier SHALL be at least 6 characters in length and MAY be entirely numeric. Since the CSP or verifier may disallow some choices of memorized secrets based on their appearance on a blacklist of compromised values, the subscriber SHALL choose a different memorized secret if a choice is rejected. No other complexity requirements for memorized secrets SHOULD be imposed; a rationale for this is presented in [Appendix A](#appA).
-->

##### 5.1.1.2. 記憶シークレット検証主体
<!--##### 5.1.1.2. Memorized Secret Verifiers-->

検証主体は加入者が指定した、最低8文字の記憶シークレットを要求するものとする(SHALL)。検証主体はユーザが決定した記憶シークレットの場合は最低でも64文字とすべきである(SHOULD)。すべての印字可能なASCII [[RFC 20]](#RFC20) 文字(スペースも同様)は記憶シークレットとして許容されるべきである(SHOULD)。Unicode[[ISO/ISC 10646:2014]](#ISOIEC10646)文字も同様に許容されるべきである(SHOULD)。検証主体は、最低8文字以上であることの検証に先立って、連続した複数のスペースまたは全てのスペースを除去してもよい(MAY)。シークレット文字列の前後の切り詰めについては実施しないものとする(SHALL NOT)。前述の長さ要求を満たす目的で、それぞれのUnicode符号位置は単一文字としてカウントされるものとする(SHALL)。

<!--
Verifiers SHALL require subscriber-chosen memorized secrets to be at least 8 characters in length. Verifiers SHOULD permit user-chosen memorized secrets to be at least 64 characters in length. All printing ASCII [[RFC 20]](#RFC20) characters as well as the space character SHOULD be acceptable in memorized secrets; Unicode [[ISO/ISC 10646:2014]](#ISOIEC10646) characters SHOULD be accepted as well. Verifiers MAY remove multiple consecutive space characters, or all space characters, prior to verification provided that the result is at least 8 characters in length. Truncation of the secret SHALL NOT be performed. For purposes of the above length requirements, each Unicode code point SHALL be counted as a single character.
-->

記憶シークレットは、CSP(例えばエンロールメント時など)また検証主体(ユーザが新しいPINを要求した時など)によりランダムに決定されるもので、最低6文字であるものとし(SHALL)、承認済み(approved)乱数生成器を利用して生成されるものとする(SHALL)。

<!--
Memorized secrets that are randomly chosen by the CSP (e.g., at enrollment) or by the verifier (e.g., when a user requests a new PIN) SHALL be at least 6 characters in length and SHALL be generated using an approved random number generator.
-->

記憶シークレット検証主体は、加入者に対して、未認証の申請者が簡単に手に入れることができる「ヒント」を記録しないものとする(SHALL NOT)。
記憶シークレットを選択する際、検証主体は加入者に対して特別なタイプの情報（例えば、あなたの最初のペットの名前はなんですか？といったもの）の入力を求めないものとする(SHALL)。

<!--
Memorized secret verifiers SHALL NOT permit the subscriber to store a "hint" that is accessible to an unauthenticated claimant. Verifiers also SHALL NOT prompt subscribers to use specific types of information (e.g., "What was the name of your first pet?") when choosing memorized secrets.
-->

記憶シークレットの設定、変更の要求を処理する際、検証主体はシークレットの値を、一般的に利用されている値、予想できる値、セキュリティ侵害を受けた値と比較するものとする(SHALL)。例えば、以下のリスト(に限定するものではない)が含んでいるものでよい(MAY):

* 過去にセキュリティ侵害にあったパスワード集
* 辞書に含まれる言葉
* サービス名や、ユーザ名、そこから派生するようなものなど、文脈によって特定可能な単語

<!--
When processing requests to establish and change memorized secrets, verifiers SHALL compare the prospective secrets against a list of known commonly-used, expected, and/or compromised values. For example, the list MAY include (but is not limited to):

* Passwords obtained from previous breach corpuses
* Dictionary words
* Context specific words, such as the name of the service, the username, and derivates thereof
-->

もし選択したシークレットがリスト中に存在したら、加入者は、それが一般的に使われているため異なるシークレット値を選び直す必要があるということを知らされ、異なる値の選択を求められるものとする(SHALL)。

<!--
If the chosen secret is found in the list, the subscriber SHALL be advised that they need to select a different secret because their previous choice was commonly used, and be required to choose a different value.
-->

検証主体は、攻撃者が加入者のアカウント乗っ取りのために試みた認証失敗の回数を有効に制限するスロットリングの仕組み[Section 5.2.2](#throttle)を実装するものとする(SHALL)。

<!--
Verifiers SHALL implement a throttling mechanism that effectively limits the number of failed authentication attempts an attacker can make on the subscriber’s account as described in [Section 5.2.2](#throttle).
-->

検証主体は他の構成ルール(例えば、異なる文字種の組み合わせ)を記憶シークレットに課すべきではない(SHOULD NOT)。検証主体は、認証器が侵害されている、または加入者が変更要求を行った証拠がない限りは、記憶シークレットを任意で(例えば、定期的に)変更するよう要求すべきではない(SHOULD NOT)。

<!--
Verifiers SHOULD NOT impose other composition rules (mixtures of different character types, for example) on memorized secrets. Verifiers SHOULD NOT require memorized secrets to be changed arbitrarily (e.g., periodically) unless there is evidence of compromise of the authenticator or a subscriber requests a change.
-->

申請者が記憶シークレットを正しく入力することを支援するために、検証主体は(典型的なドットやアスタリスク表示ではなく)シークレットを表示するオプションを提供すべき(SHOULD)である。検証主体は、申告者が入力文字を確認するのに十分な時間表示したあとは、文字を非表示にするものとする(SHALL)。これにより、申請者は彼らのスクリーンが盗み見られている可能性が高くない場所にいるとき、自身で入力を検証することができる。

<!--
In order to assist the claimant in entering a memorized secret successfully, the verifier SHOULD offer an option to display the secret (rather than a series of dots or asterisks, typically) as it is typed. The verifier SHALL hide the character after it is displayed for a time sufficient for the claimant to see the character. This allows the claimant to verify their entry if they are in a location where their screen is unlikely to be observed.
-->

検証者は承認済み(approved)暗号化を利用するものとし(SHALL)、記憶シークレットを要求する際には、盗聴やフィッシングを防止する目的で、記憶シークレットを要求する自身の申請者に対して(例えば、申請者が受け入れ可能な、承認された暗号化を用いたX.509証明書の利用を通じて)自身の真正性を証明するものとする(SHALL)。

<!--
Verifiers SHALL use approved encryption and SHALL authenticate themselves to the claimant (e.g., through the use of a X.509 certificate using approved encryption that is acceptable to the claimant) when requesting memorized secrets in order to provide resistance to eavesdropping and phishing attacks.
-->

検証主体は、オフライン攻撃へ対策するため、フォームに記憶シークレットを保存するものとする(SHALL)。シークレットは、 *ソルト*値と一緒に、例えば[[SP800-132]](#SP800-132)で記載されているPBKDF2のような承認済み(approved)のハッシュを用いてハッシュ化されるものとする(SHALL)。
ソルト値は32ビット以上のランダム値で、承認済み(approved)の乱数生成器を用いて生成され、ハッシュ結果とともに記録される。少なくとも繰り返し10000回のハッシュ関数を適用すべきである(SHOULD)。ハッシュ認証器から分離されて記録される鍵(例:ハードウェアセキュリティモジュール中)を用いる鍵付ハッシュ関数(例:HMAC)は、記録済みハッシュ化認証器に対する辞書攻撃に対する更なる対抗方法として利用されるべきである(SHOULD)。

<!--
Verifiers SHALL store memorized secrets in a form that is resistant to offline attacks. Secrets SHALL be hashed with a *salt* value using an approved hash function such as PBKDF2 as described in [[SP800-132]](#SP800-132). The salt value SHALL be a 32 bit (or longer) random value generated by an approved random number generator and is stored along with the hash result. At least 10,000 iterations of the hash function SHOULD be performed. A keyed hash function (e.g., HMAC), with the key stored separately from the hashed authenticators (e.g., in a hardware security module) SHOULD be used to further resist dictionary attacks against the stored hashed authenticators.
-->

#### 5.1.2. ルックアップシークレット

<!--
#### 5.1.2. Look-up Secrets
-->

<div class="text-left" markdown="1">
<table style="width:100%">
  <tr>
    <td><img src="sp800-63b/media/Look-up-secrets.png" alt="authenticator" style="width: 100px;height: 100px"/></td>
    <td>ルックアップシークレット認証器は物理的または電子的なレコードであり、申請者とCSPとの間で共有されているシークレット一式を記録するものである。申請者は、検証主体からの入力要求に答えるために必要とされる適切なシークレットを検索するために認証器を利用する。例えば、申請者は検証主体によって、カード上に印字された表形式の数字または文字列のうち特定の一部を提示するよう求められるかもしれない。
    </td>
    <!--
    <td>A look-up secret authenticator is a physical or electronic record that stores a set of secrets shared between the claimant and the CSP. The claimant uses the authenticator to look up the appropriate secret(s) needed to respond to a prompt from the verifier. For example, a claimant may be asked by the verifier to provide a specific subset of the numeric or character strings printed on a card in table format.</td> 
    -->
  </tr>
  </table>
  </div>

##### 5.1.2.1 ルックアップシークレット認証器

<!--
##### 5.1.2.1 Look-up Secret Authenticators
-->

CSPがルックアップシークレット認証器を生成する際、承認済み(approved)乱数生成器を用いてシークレットのリストを生成するものとし(SHALL)、加入者に対して認証器を安全に届けるものとする(SHALL)。ルックアップシークレットは最低64ビットのエントロピーを持つものとする(SHALL)か、[Section 5.2.2](#throttle)に記載があるように認証失敗回数の制限を行ったうえで最低20ビットのエントロピーを持つものとする(SHALL)。

<!--
CSPs creating look-up secret authenticators SHALL use an approved random number generator to generate the list of secrets, and SHALL deliver the authenticator securely to the subscriber. Look-up secrets SHALL have at least 64 bits of entropy, or SHALL have at least 20 bits of entropy if the number of failed authentication attempts is limited as described in [Section 5.2.2](#throttle).
-->

もし認証機がルックアップシークレットを連続してリストから利用する場合、加入者は一度認証に成功した場合に限ってシークレットを破棄してもよい(MAY)。

<!--
If the authenticator uses look-up secrets sequentially from a list, the subscriber MAY dispose of used secrets, but only after a successful authentication.
-->

##### 5.1.2.2. ルックアップシークレット検証主体
<!--
##### 5.1.2.2. Look-up Secret Verifiers
-->

ルックアップシークレットの検証主体は申請者に対して、彼らの認証器から得られる次のシークレット、または特定の(例:付番された)シークレットの入力を促すものとする(SHALL)。認証器から得られたシークレットは1度しか正常に利用できないものとする(SHALL)。従って、ある認証器は有限の回数に限り認証を成功させるために利用することができる。もしルックアップシークレットが格子状のカードから得られる場合、格子の各セルは1度だけ利用するものとする(SHALL)。

<!--
Verifiers of look-up secrets SHALL prompt the claimant for the next secret from their authenticator or for a specific (i.e., numbered) secret. A given secret from an authenticator SHALL be used successfully only once; therefore, a given authenticator can only be used for a finite number of successful authentications. If the look-up secret is derived from a grid card, each cell of the grid SHALL be used only once.
-->

検証主体は、オフライン攻撃へ対策するため、フォームにルックアップシークレットを保存するものとする(SHALL)。シークレットは、*ソルト*値と一緒に、[[SP800-132]](#SP800-132)で記載されている承認済み(approved)のハッシュ関数を用いてハッシュ化されるものとする(SHALL)。
ソルト値は32ビット以上のランダム値で、承認済み(approved)の乱数生成器を用いて生成され、ハッシュ結果とともに記録される。ハッシュ認証器から分離されて記録される鍵(例:ハードウェアセキュリティモジュール中)を用いる鍵付ハッシュ関数(例:HMAC [[FIPS198-1]](#FIPS198-1))は、記録済みハッシュ化認証器に対する辞書攻撃に対する更なる対抗方法として利用されるべきである(SHOULD)。

<!--
Verifiers SHALL store look-up secrets in a form that is resistant to offline attacks. Secrets SHALL be hashed with a "salt" value using an approved hash function as described in [[SP 800-132]](#SP800-132). The "salt" value SHALL be a 32 bit (or longer) random value generated by an approved random number generator that is stored along with the hash result. A keyed hash function (e.g., HMAC [[FIPS198-1]](#FIPS198-1)), with the key stored separately from the hashed authenticators (e.g., in a hardware security module) SHOULD be used to further resist dictionary attacks against the stored hashed authenticators.
-->

ルックアップシークレットは、承認済み(approved)乱数生成器を用いてシークレットのリストを生成するものとし(SHALL)、最低20ビットのエントロピーを持つものとする(SHALL)。ルックアップシークレットが64ビット未満のエントロピーを持つような場合、検証主体は[Section 5.2.2](#throttle)に記載があるように、攻撃者が加入者のアカウント乗っ取りのために試みた認証失敗の回数を有効に制限するスロットリングの仕組みを実装するものとする(SHALL)。

<!--
Look-up secrets SHALL be generated using an approved random number generator and SHALL have at least 20 bits of entropy. When look-up secrets have less than 64 bits of entropy, the verifier SHALL implement a throttling mechanism that effectively limits the number of failed authentication attempts an attacker can make on the subscriber’s account as described in [Section 5.2.2](#throttle).
-->

検証者は承認済み(approved)暗号化を利用するものとし(SHALL)、ルックアップシークレットを要求する際には、盗聴やフィッシングを防止する目的で、申請者に対して(例えば、申請者が受け入れ可能な、承認された暗号化を用いたX.509証明書の利用を通じて)自身の真正性を証明するものとする(SHALL)。

<!--
Verifiers SHALL use approved encryption and SHALL authenticate themselves to the claimant (e.g., through the use of a X.509 certificate using approved encryption that is acceptable to the claimant) when requesting look-up secrets in order to provide resistance to eavesdropping and phishing attacks.
-->

#### <a name="out-of-band"></a>5.1.3. 経路外(Out-of-Band)デバイス

<!--
#### <a name="out-of-band"></a>5.1.3. Out-of-Band Devices
-->

<div class="text-left" markdown="1">
<table style="width:100%">
  <tr>
    <td><img src="sp800-63b/media/Out-of-band-OOB.png" alt="authenticator" style="width: 100px;height: 100px"/></td>
    <td>経路外認証器は、一意にアドレス可能、かつセカンダリチャネルと呼ばれる異なる通信チャネルを介して検証主体と安全に通信することができる物理デバイスである。デバイスは申請者によって所有と制御されており、電子的認証のためのプライマリチャネルと分離されたセカンダリチャネルを介したプライベートな通信をサポートしている。経路外認証器は以下の方法の1つで動作することができる。<br><br>
    
- 申請者は経路外デバイスによってセカンダリチャネルを介して受け取ったシークレットを、プライマリチャネルを使って検証主体に送信する。例えば、申請者は自身のモバイルデバイス上でシークレットを受信し、それ(典型的には数字6桁のコード)を自身の認証セッションに対して打ち込むかもしれない。<br><br>

- 申請者はプライマリチャネルを介して受け取ったシークレットを、経路外デバイスに対して送信し、セカンダリチャネルを介して検証主体に対して送信する。例えば、申請者は自身の認証セッション上で確認したシークレットを、モバイルデバイス上のアプリケーション対して入力したり、バーコード・QRコードといった技術を利用して送信を達成する。<br><br>

- 申請者はプライマリチャネルとセカンダリチャネルから得たシークレットを比較し、セカンダリチャネルを介した認証の裏付け行う。<br><br>

シークレットの目的は安全に認証操作をプライマリとセカンダリのチャネルに結びつけることである。プライマリ通信チャネルを介してレスポンスをする場合、シークレットは経路外デバイスを申請者が制御していることもまた証明していることになる。</td> 
  </tr>
  </table>
  </div>

<!--
<div class="text-left" markdown="1">
<table style="width:100%">
  <tr>
    <td><img src="sp800-63b/media/Out-of-band-OOB.png" alt="authenticator" style="width: 100px;height: 100px"/></td>
    <td>An out-of-band authenticator is a physical device that is uniquely addressable and can communicate securely with the verifier over a distinct communications channel, referred to as the secondary channel. The device is possessed and controlled by the claimant and supports private communication over this secondary channel that is separate from the primary channel for e-authentication. The out-of-band authenticator can operate in one of the following ways:<br><br>
-->

<!--
- The claimant transfers a secret received by the out-of-band device via the secondary channel to the verifier using the primary channel. For example, the claimant may receive the secret on their mobile device and type it (typically a 6 digit code) into their authentication session.<br><br>
-->

<!--
- The claimant transfers a secret received via the primary channel to the out-of-band device for transmission to the verifier via the secondary channel. For example, the claimant may view the secret on their authentication session and either type it into an app on their mobile device or use a technology such as a barcode or QR code to effect the transfer.<br><br>
-->

<!--
- The claimant compares secrets received from the primary channel and the secondary channel and confirms the authentication via the secondary channel.<br><br>
-->

<!--
The purpose of the secret is to securely bind the authentication operation on the primary and secondary channel. When the response is via the primary communication channel, the secret also establishes the claimant's control of the out-of-band device.</td> 
  </tr>
  </table>
  </div>
-->

##### 5.1.3.1. 経路外認証器

<!--
##### 5.1.3.1. Out-of-Band Authenticators
-->

経路外認証器は経路外シークレットや認証リクエストを取得するために検証主体との分離された通信チャネルを確立するものとする(SHALL)。このチャネルはプライマリ通信チャネルとの関係において経路外(out-of-band)であるとし、同じデバイス上で終端されている場合でさえも、申請者の認可なしに一方から他方に対して情報が漏洩することがないようなデイバイスであることを前提とする。

<!--
The out-of-band authenticator SHALL establish a separate channel with the verifier in order to retrieve the out-of-band secret or authentication request. This channel is considered to be out-of-band with respect to the primary communication channel, even if it terminates on the same device, provided the device does not leak information from one to the other without the authorization of the claimant.
-->

経路外デバイスは一意にアドレス可能であるとし(SHALL)、セカンダリチャネルを介した通信はプライベートであるものとする(SHALL)。VoIP(voice-over-IP)電話サービスの中にはテキストメッセージや音声コールを、物理デバイスの所持なしに配信することができるものがあり、これらは経路外認証で利用しないものとする(SHALL NOT)。Emailメッセージや他の種類のインスタントメッセージを受け取ることができる能力は、一般的には特別なデバイスを所持していることの証明にはならないため、経路外認証方式では利用されないものとする(SHALL NOT)。スマートフォンアプリケーションのようなセキュアな通信プロトコルを用いて一意に経路外デバイスを特定する仕組みが、経路外認証に用いられるべきである(SHOULD)。

<!--
The out-of-band device SHALL be uniquely addressable and communication over the secondary channel SHALL be private. Some voice-over-IP telephone services can deliver text messages and voice calls without the need for possession of a physical device; these SHALL NOT be used for out-of-band authentication. Ability to receive email messages or other types of instant message does not generally prove the possession of a specific device, and therefore SHALL NOT be used as out-of-band authentication methods. Mechanisms such as smartphone applications that employ secure communications protocols and uniquely identify the out-of-band device SHOULD be used for out-of-band authentication.
-->

経路外認証器は、検証主体との通信において以下に記載する方法の1つを用いて、一意に自身の真正性を証明するものとする(SHALL):

<!--
The out-of-band authenticator SHALL uniquely authenticate itself in one of the following ways in communicating with the verifier:
-->

- 承認済み(approved)暗号理論を利用して検証主体に対する保護された認証済みチャネルを確立する。利用する鍵はデバイス上で最もセキュアなストレージ(例:キーチェーン、Trusted Platform Module、可能ならばTrusted Execution Environment)に記録されるものとする(SHALL)。

<!--
- Establish an authenticated protected channel to the verifier using approved cryptography. The key used SHALL be stored in the most secure storage available on the device (e.g., keychain storage, trusted platform module, or trusted execution environment if available).
-->

- SIMカードまたはデバイスを一意に識別する等価な方法を用いて公衆携帯電話網に対して認証する。この方法は電話網(SMSまたは音声)を介して経路外デバイスに対して検証主体からシークレットが送信される場合に限り用いるものとする(SHALL)。

<!--
- Authenticate to a public mobile telephone network using a SIM card or equivalent that uniquely identifies the device. This method SHALL only be used if a secret is being sent from the verifier to the out-of-band device via the telephone network (SMS or voice).
-->

もし検証主体から経路外デバイスに対してシークレットが送信されるならば、デバイスは所有者によってデバイスがロックされている(例:PINやパスコード入力を求める)間は認証シークレットを表示すべきではない(SHOULD NOT)。しかしながら認証器はロックされたデバイス上で認証シークレットを受信したことは表示してもよい(MAY)。

<!--
If a secret is sent by the verifier to the out-of-band device, the device SHOULD NOT display the authentication secret on a device while it is locked by the owner (i.e., requires an entry of a PIN or passcode). However, authenticators MAY indicate the receipt of an authentication secret on a locked device.
-->

もし経路外認証機がセカンダリ通信チャネルを介して承認メッセージを送信するならば(申請者がプライマリ通信チャネルに対して受け取ったシークレットを送信するよりもむしろ)、次のうち1つを実施するものとする(SHALL):

<!--
If the out-of-band authenticator sends an approval message over the secondary communication channel (rather than by the claimant transferring a received secret to the primary communication channel), it SHALL do one of the following:
-->

* 認証器はプライマリチャネルから得たシークレットを転送することを許容するものとし(SHALL)、認証トランザクションに対する承認と関連付けるために、セカンダリチャネルを介して検証主体に対して送信するものとする(SHALL)。申請者は送信を手動で実施、またはバーコード・QRコードといった技術を利用して送信を達成してもよい(MAY)。

<!--
* The authenticator SHALL accept transfer of the secret from the primary channel which it SHALL send to the verifier over the secondary channel to associate the approval with the authentication transaction. The claimant MAY perform the transfer manually or use a technology such as a barcode or QR code to effect the transfer.
-->

* 認証器はセカンダリチャネルを介して検証主体から受け取ったシークレットを提示し、申請者に対してプライマリチャネルのシークレットとの一貫性を検証するよう促した上で、申請者から「はい/いいえ」の応答を受け入れるものとする(SHALL)。

<!--
* The authenticator SHALL present a secret received via the secondary channel from the verifier and prompt the claimant to verify the consistency of that secret with the primary channel, prior to accepting a yes/no response from the claimant. It SHALL then send that response to the verifier.
-->

##### 5.1.3.2. 経路外検証主体
<!--
##### 5.1.3.2. Out-of-Band Verifiers
-->

SMSメッセージや音声コールが傍受されたりリダイレクトされたりするかもしれないというリスクに起因し、新システムの実装者は代替となる認証器を注意深く検討すべきである(SHOULD)。もし経路外検証が公衆交換電話網(PSTN:public switched telephone network)を用いて行われるならば、検証主体は事前登録された電話番号がVoIP(または他のソフトウェアベースの)サービスと関連付けられていないことを検証することとする(SHALL)。そのうえでSMSや音声メッセージは事前登録された電話番号に対して送信される。事前登録された電話番号の変更が、変更時に2要素認証なしで可能となっていないものとする(SHALL NOT)。 **公衆交換電話網(PSTN)を用いた経路外(OOB)は非推奨**であり、このガイドラインの将来のリリースではもはや許可されなくなるかもしれない。

<!--
Due to the risk that SMS messages or voice calls may be intercepted or redirected, implementers of new systems SHOULD carefully consider alternative authenticators. If the out-of-band verification is to be made using the public switched telephone network (PSTN), the verifier SHALL verify that the pre-registered telephone number being used is not associated with a VoIP (or other software-based) service. It then sends the SMS or voice message to the pre-registered telephone number. Changing the pre-registered telephone number SHALL NOT be possible without two-factor authentication at the time of the change.  **OOB using the PSTN (SMS or voice) is deprecated**, and may no longer be allowed in future releases of this guidance.
-->

経路外検証がセキュアなアプリケーション(例:スマートフォン上)を利用して行われる場合、検証主体はデバイスに対してPush通知を行ってもよい(MAY)。検証主体は保護された認証済みチャネルの確立を待ち、認証器の識別キーを検証する。認証器は識別キー自身を記録しないものとする(SHALL NOT)が、承認済み(approved)のハッシュ関数を用いたハッシュのような検証方法を用いるか、認証器を一意に識別するための識別キーの所持証明をおこなうものとする(SHALL)。認証すると、検証主体は認証シークレットを認証器に対して送信する。

<!--
If out-of-band verification is to be made using a secure application (e.g., on a smart phone), the verifier MAY send a push notification to that device. The verifier then waits for a establishment of an authenticated protected channel and verifies the authenticator's identifying key. The verifier SHALL NOT store the identifying key itself, but SHALL use a verification method such as hashing (using an approved hash function) or proof of possession of the identifying key to uniquely identify the authenticator. Once authenticated, the verifier transmits the authentication secret to the authenticator.
-->

経路外認証器の種別に応じて、以下のうち1つを行うものとする(SHALL):

<!--
Depending on the type of out-of-band authenticator, one of the following SHALL take place:
-->

* シークレットをプライマリチャネルに送出: 検証主体は加入者の認証器を持つデバイスに対して認証の準備を示すシグナルを送信してもよい(MAY)。そのうえで、経路外認証器に対してランダムなシークレットを送信するものとする(SHALL)。検証主体はプライマリ通信チャネル上でシークレットが返却されるのを待つものとする(SHALL)。

<!--
* Transfer of secret to primary channel: The verifier MAY signal the device containing the subscriber's authenticator to indicate readiness to authenticate. It SHALL then transmit a random secret to the out-of-band authenticator. The verifier SHALL then wait for the secret to be returned on the primary communication channel.
-->

* シークレットをセカンダリチャネルに送出: 検証主体はランダムな認証シークレットをプライマリチャネル経由で申請者に対して表示するものとする(SHALL)。そのうえで、セカンダリチャネル上で申請者の経路外認証器からシークレットが返却されるのを待つものとする(SHALL)。

<!--
* Transfer of secret to secondary channel: The verifier SHALL display a random authentication secret to the claimant via the primary channel. It SHALL then wait for the secret to be returned on the secondary channel from the claimant's out-of-band authenticator.
-->

* 申告者によるシークレットの検証主体: 検証主体はランダムな認証シークレットをプライマリチャネル経由で申請者に対して表示するものとし(SHALL)、セカンダリチャネルを介して経路外認証器に対して同じシークレットを送信し申請者に提示するものとする(SHALL)。そのうえで、セカンダリチャネルを介した承認(非承認)メッセージを待つものとする(SHALL)。

<!--
* Verification of secrets by claimant: The verifier SHALL display a random authentication secret to the claimant via the primary channel, and SHALL send the same secret to the out-of-band authenticator via the secondary channel for presentation to the claimant. It SHALL then wait for an approval (or disapproval) message via the secondary channel.
-->

全てのケースにおいて、5分以内に完了しない認証は不正とみなすものとする(SHALL)。

<!--
In all cases, the authentication SHALL be considered invalid if not completed within 5 minutes.
-->

検証主体は、承認済み(approved)乱数生成器を用いて最低20ビットのエントロピーでランダムな認証シークレットを生成するものとする(SHALL)。もし認証シークレットが64ビット未満のエントロピーを持つような場合、検証主体は[Section 5.2.2](#throttle)に記載があるように、攻撃者が加入者のアカウント乗っ取りのために試みた認証失敗の回数を有効に制限するスロットリングの仕組みを実装するものとする(SHALL)。

<!--
The verifier SHALL generate random authentication secrets with at least 20 bits of entropy using an approved random number generator. If the authentication secret has less than 64 bits of entropy, the verifier SHALL implement a throttling mechanism that effectively limits the number of failed authentication attempts an attacker can make on the subscriber’s account as described in [Section 5.2.2](#throttle).
-->

#### 5.1.4. 単一要素OTPデバイス
<!--
#### 5.1.4. Single Factor OTP Device
-->

<div class="text-left" markdown="1">
<table style="width:100%">
  <tr>
    <td><img src="sp800-63b/media/Single-factor-otp-device.png" alt="authenticator" style="width: 100px;height: 100px"/></td>
    <td>単一要素OTPデバイスは時間ベースのワンタイムパスワードの生成をサポートするハードウェアデバイスである。単一要素OTPデバイスは、携帯電話などにインストールされたソフトウェアのOTP生成器も含んでいる。このデバイスは、ワンタイムパスワードの生成のシードとして利用される組み込みのシークレットを保持しており、二要素目によるアクティベーションを必要としない。認証は、認証プロトコル中で認証器出力(例:ワンタイムパスワード)を用いて達成され、そのことによりデバイスの所持と制御を証明している。ワンタイムパスワードデバイスは例えば一度に6文字の表示を行うかもしれない。<br><br>

単一要素OTPデバイスはルックアップシークレット認証器と同様、暗号理論に基づいて認証器と検証主体がシークレットを生成し、検証主体によって比較されるという例外の面で似ている。シークレットは、時間ベースまたは認証器と検証主体のカウンタから生じるノンスに基づいて計算される。</td> 
  </tr>
  </table>
  </div>

<!--
<div class="text-left" markdown="1">
<table style="width:100%">
  <tr>
    <td><img src="sp800-63b/media/Single-factor-otp-device.png" alt="authenticator" style="width: 100px;height: 100px"/></td>  
-->
    
<!--
    <td>A single factor OTP device is a hardware device that supports the time-based generation of one-time passwords. This includes software-based OTP generators installed on devices such as mobile phones. This device has an embedded secret that is used as the seed for generation of one-time passwords and does not require activation through a second factor. Authentication is accomplished by using the authenticator output (i.e., the one-time password) in an authentication protocol, thereby proving possession and control of the device. A one-time password device may, for example, display 6 characters at a time.<br><br>

Single factor OTP devices are similar to look-up secret authenticators with the exception that the secrets are cryptographically generated by the authenticator and verifier and compared by the verifier. The secret is computed based on a nonce that may be time-based or from a counter on the authenticator and verifier.</td> 
-->

<!--
  </tr>  
  </table>
  </div>
-->

##### <a name="sfotpa"></a>5.1.4.1. 単一要素OTP認証器

<!--
##### <a name="sfotpa"></a>5.1.4.1. Single Factor OTP Authenticators
-->

単一要素OTP認証器は2つの永続的な値を保持する。1つ目はデバイスの生存期間の間保持し続ける対象鍵である。2つ目は認証機が使われる都度変化する、またはリアルタイムクロックに基づいているノンスである。

<!--
Single factor OTP authenticators contain two persistent values. The first is a symmetric key that persists for the lifetime of the device. The second is a nonce that is changed each time the authenticator is used or is based on a real-time clock.
-->

シークレットは最低でも[[SP 800-131A]](#SP800-131A)の最新版で定義された承認済み(approved)の長さ(現在は112ビット)であるものとする(SHALL)。ノンスは、デバイスの生存期間に渡りデバイスが操作される都度一意であることを保証するために十分長いこととする(SHALL)。

<!--
The secret key SHALL be of at least the minimum approved length as defined in the latest revision of [[SP 800-131A]](#SP800-131A) (currently 112 bits). The nonce SHALL be of sufficient length to ensure that it is unique for each operation of the device over its lifetime.
-->

認証器出力は、鍵とノンスとを安全な方法で結合し、承認済み(approved)ブロック暗号またはハッシュ関数を施して得られる。認証器出力は少なくとも(約20ビットのエントロピーの)6桁の数字になるよう切り詰めてもよい(MAY)。

<!--
The authenticator output is obtained by using an approved block cipher or hash function to combine the key and nonce in a secure manner. The authenticator output MAY be truncated to as few as 6 decimal digits (approximately 20 bits of entropy).
-->

もし認証器出力を生成するために利用されるノンスがリアルタイムクロックをベースとしている場合、ノンスは少なくとも2分毎に変化するものとする(SHALL)。与えられたノンスと結び付けられているOTP値は一度だけ受け入れられるものとする(SHALL)。

<!--
If the nonce used to generate the authenticator output is based on a real-time clock, the nonce SHALL be changed at least once every 2 minutes. The OTP value associated with a given nonce SHALL be accepted only once.
-->

もし認証器がその出力をUSBなどの電子的なインタフェースを介して供給する場合、認証器はワンタイムパスワードを生成するきっかけとなる物理的な入力(例:デバイスのボタンを押す)を求めるべきである(SHOULD)。

<!--
If the authenticator supplies its output via an electronic interface such as USB, it SHOULD require a physical input (e.g., pressing a button on the device) to cause a one-time password to be generated.
-->

##### 5.1.4.2. 単一要素OTP検証主体
<!--
##### 5.1.4.2. Single Factor OTP Verifiers
-->

単一要素OTP検証主体は、認証器によるOTPの生成プロセスを実質的に再現する。検証主体は、認証器が使う対象鍵を所持しており、セキュリティ侵害に対して強力な防御が行われているものとする(SHALL)。

<!--
Single factor OTP verifiers effectively duplicate the process of generating the OTP used by the authenticator. As such, the symmetric keys used by authenticators are also present in the verifier, and SHALL be strongly protected against compromise.
-->

申請者からOTPを収集する過程で、検証者は承認済み(approved)暗号化を行うものとし(SHALL)、申告者に対して自身の真正性を証明するものとする(SHALL)。

<!--
In collecting the OTP from the claimant, the verifier SHALL use approved encryption and SHALL authenticate itself to the claimant. 
-->

もし認証器出力が64ビット未満のエントロピーしか持ち得なければ、検証主体は[Section 5.2.2](#throttle)に記載があるように、攻撃者が加入者のアカウント乗っ取りのために試みた認証失敗の回数を有効に制限するスロットリングの仕組みを実装するものとする(SHALL)。

<!--
If the authenticator output has less than 64 bits of entropy, the verifier SHALL implement a throttling mechanism that effectively limits the number of failed authentication attempts an attacker can make on the subscriber’s account as described in [Section 5.2.2](#throttle).
-->

#### 5.1.5. Multi-Factor OTP Devices

<div class="text-left" markdown="1">
<table style="width:100%">
  <tr>
    <td><img src="sp800-63b/media/Multi-factor-otp-device.png" alt="authenticator" style="width: 100px;height: 100px"/></td>
    <td>A multi-factor (MF) OTP device hardware device generates one-time passwords for use in authentication and requires activation through a second factor of authentication. The second factor of authentication may be achieved through some kind of integral entry pad, an integral biometric (e.g., fingerprint) reader or a direct computer interface (e.g., USB port). The one-time password is typically displayed on the device and manually input to the verifier, although direct electronic output from the device as input to a computer is also allowed. For example, a one-time password device may display 6 characters at a time. The MF OTP device is <i>something you have</i>, and it SHALL be activated by either <i>something you know</i> or <i>something you are</i>.</td> 
  </tr>
  </table>
  </div>


##### 5.1.5.1. Multi-Factor OTP Authenticators

Multi-factor OTP authenticators operate in a similar manner to single-factor OTP authenticators (see [Section 5.1.4.1](#sfotpa)), except that they require the entry of either a memorized secret or use of a biometric to obtain a password from the authenticator. Each use of the authenticator SHALL require the input of the additional factor.

The authenticator output SHALL have at least 6 decimal digits (approximately 20 bits) of entropy. The output SHALL be generated by using an approved block cipher or hash function to combine a symmetric key stored on a personal hardware device with a nonce to generate a one-time password. The nonce MAY be based on the date and time or on a counter generated on the device. 

Any memorized secret used by the authenticator for activation SHALL be at least 6 decimal digits (approximately 20 bits) in length or of equivalent complexity. A biometric activation factor SHALL meet the requirements of [Section 5.2.3](#biometric_use), including limits on number of successive authentication failures.

The unencrypted key and activation secret or biometric sample (and any biometric data derived from the biometric sample such as a probe produced through signal processing) SHALL be immediately erased from storage immediately after a password has been generated.

##### 5.1.5.2. Multi-Factor OTP Verifiers

Multi-factor OTP verifiers effectively duplicate the process of generating the OTP used by the authenticator, but without the requirement that a second factor be provided. As such, the symmetric keys used by authenticators SHALL be strongly protected against compromise.

In collecting the OTP from the claimant, the verifier SHALL use approved encryption and SHALL authenticate itself to the claimant. Time-based one-time passwords SHALL have a lifetime of less than 2 minutes.

If the authenticator output or activation secret has less than 64 bits of entropy, the verifier SHALL implement a throttling mechanism that effectively limits the number of failed authentication attempts an attacker can make on the subscriber’s account as described in [Section 5.2.2](#throttle). A biometric activation factor SHALL meet the requirements of [Section 5.2.3](#biometric_use), including limits on number of successive authentication failures.
    
#### 5.1.6. Single Factor Cryptographic Devices

<div class="text-left" markdown="1">
<table style="width:100%">
  <tr>
    <td><img src="sp800-63b/media/Single-factor-crypto.png" alt="authenticator" style="width: 100px;height: 100px"/></td>
    <td>A single-factor cryptographic device is a hardware device that performs cryptographic operations on input provided to the device. This device does not require activation through a second factor of authentication. This device uses embedded symmetric or asymmetric cryptographic keys. Authentication is accomplished by proving possession of the device. The authenticator output is highly dependent on the specific cryptographic device and protocol, but it is generally some type of signed message.</td> 
  </tr>
  </table>
  </div>

##### 5.1.6.1. Single Factor Cryptographic Device Authenticators

Single-factor cryptographic device authenticators encapsulate a secret key that is unique to the device and SHALL NOT be exportable (removed from the device). They operate by signing a challenge nonce, usually presented through a direct computer interface such as a USB port.

The secret key SHALL be of at least the minimum approved length as defined in the latest revision of [[SP 800-131A]](#SP800-131A) (currently 112 bits). The challenge nonce SHALL be at least 64 bits in length. The authenticator output is normally provided via a computer interface (usually the same one from which the challenge value was received).

Single-factor cryptographic device authenticators SHOULD require a physical input such as the pressing of a button in order to operate. This provides defense against unintended operation of the device, which might occur if the device to which it is connected is compromised.

##### 5.1.6.2. Single Factor Cryptographic Device Verifiers

Single-factor cryptographic device verifiers generate a challenge nonce, send it to the corresponding authenticator, and use the authenticator output to verify possession of the device. The authenticator output is highly dependent on the specific cryptographic device and protocol, but it is generally some type of signed message.

The verifier contains either symmetric or asymmetric public keys corresponding to each authenticator. While both types of keys SHALL be protected against modification, symmetric keys SHALL additionally be strongly protected against unauthorized disclosure.

The challenge nonce SHALL be at least 64 bits in length, and SHALL either be unique over the lifetime of the authenticator or statistically unique (generated using an approved random number generator).
    
#### 5.1.7. Multi-Factor Cryptographic Software

<div class="text-left" markdown="1">
<table style="width:100%">
  <tr>
    <td><img src="sp800-63b/media/Multi-factor-software-crypto.png" alt="authenticator" style="width: 100px;height: 100px"/></td>
    <td>A multi-factor software cryptographic authenticator is a cryptographic key is stored on disk or some other “soft” media that requires activation through a second factor of authentication. Authentication is accomplished by proving possession and control of the key. The authenticator output is highly dependent on the specific cryptographic protocol, but it is generally some type of signed message. The MF software cryptographic authenticator is <i>something you have</i>, and it SHALL be activated by either <i>something you know</i> or <i>something you are</i>.</td> 
  </tr>
  </table>
  </div>



##### 5.1.7.1. Multi-Factor Cryptographic Software Authenticators

Multi-factor software cryptographic authenticators encapsulate a secret key that is unique to the authenticator and is accessible only through the input of an additional factor, either a memorized secret or a biometric. The key SHOULD be stored in the most secure storage available on the device (e.g., keychain storage, trusted platform module, or trusted execution environment if available).

Each authentication operation using the authenticator SHALL require the input of the additional factor.

Any memorized secret used by the authenticator for activation SHALL be at least 6 decimal digits (approximately 20 bits) in length or of equivalent complexity. A biometric activation factor SHALL meet the requirements of [Section 5.2.3](#biometric_use), including limits on number of successive authentication failures.

The unencrypted key and activation secret or biometric sample (and any biometric data derived from the biometric sample such as a probe produced through signal processing) SHALL be immediately erased from storage immediately after an authentication transaction has taken place.

##### 5.1.7.2. Multi-Factor Cryptographic Software Verifiers

The requirements for a multi-factor cryptographic software verifier are identical to those for a multi-factor cryptographic device verifier, described in [Section 5.1.8.2](#mfcdv).

#### 5.1.8. Multi-Factor Cryptographic Devices

<div class="text-left" markdown="1">
<table style="width:100%">
  <tr>
    <td><img src="sp800-63b/media/Multi-factor-crypto-device.png" alt="authenticator" style="width: 100px;height: 100px"/></td>
    <td>A multi-factor cryptographic device is a hardware device that contains a protected cryptographic key that requires activation through a second authentication factor. Authentication is accomplished by proving possession of the device and control of the key. The authenticator output is highly dependent on the specific cryptographic device and protocol, but it is generally some type of signed message. The MF Cryptographic device is <i>something you have</i>, and it SHALL be activated by either <i>something you know</i> or <i>something you are</i>.</td> 
  </tr>
  </table>
  </div>


##### 5.1.8.1. Multi-Factor Cryptographic Device Authenticators

Multi-factor cryptographic device authenticators use tamper-resistant hardware to encapsulate a secret key that is unique to the authenticator and is accessible only through the input of an additional factor, either a memorized secret or a biometric.

Each authentication operation using the authenticator SHOULD require the input of the additional factor. Input of the additional factor MAY be accomplished via either direct input on the device or via a hardware connection (e.g., USB or smartcard).

Any memorized secret used by the authenticator for activation SHALL be at least 6 decimal digits (approximately 20 bits) in length or of equivalent complexity. A biometric activation factor SHALL meet the requirements of [Section 5.2.3](#biometric_use), including limits on number of successive authentication failures.

The unencrypted key and activation secret or biometric sample (and any biometric data derived from the biometric sample such as a probe produced through signal processing) SHALL be immediately erased from storage immediately after an authentication transaction has taken place.

##### <a name="mfcdv"></a>5.1.8.2 Multi-Factor Cryptographic Device Verifiers

Multi-factor cryptographic device verifiers generate a challenge nonce, send it to the corresponding authenticator, and use the authenticator output to verify possession of the device and activation factor. The authenticator output is highly dependent on the specific cryptographic device and protocol, but it is generally some type of signed message.

The verifier contains either symmetric or asymmetric public keys corresponding to each authenticator. While both types of keys SHALL be protected against modification, symmetric keys SHALL additionally be strongly protected against unauthorized disclosure.

The challenge nonce SHALL be at least 64 bits in length, and SHALL either be unique over the lifetime of the authenticator or statistically unique (generated using an approved random number generator). The verification operation SHALL use approved cryptography.

#### 5.2. General Authenticator Requirements

#### 5.2.1. Physical Authenticators

CSPs SHALL provide subscriber instructions on how to appropriately  protect the authenticator against theft or loss. The CSP SHALL provide a mechanism to revoke or suspend the authenticator immediately upon notification from subscriber that loss or theft of the authenticator is suspected.

#### <a name="throttle"></a>5.2.2. Rate Limiting (Throttling)

*cf. 800-63-2 sec 8.2.3, p.75*

When the authenticator output or activation secret does not have sufficient entropy, the verifier SHALL implement controls to protect against online guessing attacks. Unless otherwise specified in the description of a given authenticator, the verifier SHALL effectively limit online attackers to 100 consecutive failed attempts on a single account in any 30 day period.

Additional techniques MAY be used to prioritize authentication attempts that are likely to come from the subscriber over those that are more likely to come from an attacker:

- Requiring the claimant to complete a Completely Automated Public Turing test to tell Computers and Humans Apart (CAPTCHA) before attempting authentication

- Requiring the claimant to wait for a short period of time (anything from 30 seconds to an hour, depending on how close the system is to its maximum allowance for failed attempts) before attempting Authentication following a failed attempt

- Only accepting authentication requests from a white list of IP addresses at which the subscriber has been successfully authenticated before

- Leveraging other risk-based or adaptive authentication techniques to identify user behavior that falls within, or out of, typical norms.

Since these measures often create user inconvenience, the verifier SHOULD allow a certain number of failed authentication attempts before employing the above techniques. 

When the subscriber successfully authenticates, the verifier SHOULD disregard any previous failed attempts from the same IP address.

#### <a name="biometric_use"></a>5.2.3. Use of Biometrics

For a variety of reasons, this document supports only limited use of biometrics for authentication. These include:

- Biometric False Match Rates (FMR) and False Non-Match Rates (FNMR) do not provide confidence in the authentication of the subscriber by themselves. In addition, FMR and FNMR do not account for spoofing attacks.
- Biometric matching is probabilistic, whereas the other authentication factors are deterministic.
- Biometric template protection schemes provide a method for revoking biometric credentials that are comparable to other authentication factors (e.g., PKI certificates and passwords). However, the availability of such solutions is limited, and standards for testing these methods are under development.
- Biometric characteristics do not constitute secrets.  They can be obtained online or by taking a picture of someone with a camera phone (e.g. facial images) with or without their knowledge, lifted from through objects someone touches (e.g., latent fingerprints), or captured  with high resolution images (e.g., iris patterns for blue eyes). While presentation attack detection (PAD) technologies such as liveness detection can mitigate the risk of these types of attacks, additional trust in the sensor is required to ensure that PAD is operating properly in accordance with the needs of the CSP and the subscriber.

Therefore, the use of biometrics for authentication is supported, with the following requirements and guidelines:

Biometrics SHALL be used with another authentication factor (something you know or something you have).

Empirical testing of the biometric system to be deployed SHALL demonstrate an equal error rate of **1 in 1000** or better with respect to matching performance. The biometric system SHALL operate with a false match rate of **1 in 1000** or better.

When the biometric sensor and subsequent processing are not part of an integral unit that resists replacement of the sensor, the sensor SHALL demonstrate that it is a certified or qualified sensor meeting these requirements by authenticating itself to the processing element.

Testing of the biometric system to be deployed SHALL demonstrate at least 90% resistance to presentation attacks for each relevant attack type (aka species), where resistance is defined as the number of thwarted presentation attacks divided by the number of trial presentation attacks. The biometric system SHALL implement presentation attack protection (PAD).

The biometric system SHALL allow no more than 10 consecutive failed authentication attempts. Once that limit has been reached, the claimant SHALL be required to use a different authenticator or to activate their authenticator with a different factor such as a memorized secret.

Biometric matching SHOULD be performed locally on claimant's device or MAY be performed at a central verifier. 

If matching is performed centrally:

* Use of the biometric SHALL be bound tightly to a single, specific device that is identified using approved cryptography.
* Biometric revocation SHALL be implemented.
* An authenticated protected channel between sensor and central verifier SHALL be established, and the sensor authenticated, **prior** to capturing the biometric sample from the claimant.
* All transmission of biometrics shall be over the authenticated protected channel.

Biometric samples collected in the authentication process MAY be used to train matching algorithms or, with user consent, for other research purposes. Biometric samples (and any biometric data derived from the biometric sample such as a probe produced through signal processing) SHALL be immediately erased from storage immediately after a password has been generated.

Biometrics are also used in some cases to prevent repudiation of registration and to verify that the same individual participates in all phases of the registration process as described in SP 800-63A.

#### <a name="attestation"></a>5.2.4 Attestation

Authenticators that are directly connected to or embedded in endpoints MAY convey attestation information such as the provenance or health and integrity of the authenticator (and possibly the endpoint as well) to the verifier as part of the authentication protocol. If this attestation is signed, the verifier SHOULD validate its signature. This information MAY be used as part of a risk-based authentication decision.

When federated authentication is being performed as described in [SP 800-63C](sp800-63c.html), the verifier SHOULD include any such attestation information in the assertion it provides to the relying party.
