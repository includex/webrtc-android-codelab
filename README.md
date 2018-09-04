# webrtc-android-codelab
An attempt to provide a codelab for Webrtc in Android - Similar to codelab for web at https://codelabs.developers.google.com/codelabs/webrtc-web/

More at : https://vivekc.xyz/getting-started-with-webrtc-for-android-daab1e268ff4

참 좋은 글이지만 Setp3 예제가 현재는 아래 이유로 잘 동작하지 않는다.
1. gradle dependency의 버전을 +로 설정하여, 최신 webrtc를 import하지만 셈플코드는 예전 코드이다 보니 예전 인터페이스를 사용한다.
2. ice서버의 인터페이스가 변경되어 STURN, TURE 정보를 얻어오는 부분이 동작하지 못한다.
3. 빌드에 성공하더라도 빠진 코드가 있어, 이를 알지 못하는 사용자는 NullPointException를 경험하게 된다.
4. 시그널서버에 대한 가이드 부재

따라서 아래와 같이 동작하도록 수정한 코드를 적용했다.
1. 샘플코드가 사용하는 버전을 찾아 명시한다. 
  implementation 'org.webrtc:google-webrtc:1.0.22672'
2. ice서버의 인터페이스에 영향 받지 않도록 서버설정을 직접 기입하도록 수정한다.
3. 빠진 코드를 추가한다.
        sdpConstraints = new MediaConstraints();
        sdpConstraints.mandatory.add(new MediaConstraints.KeyValuePair("offerToReceiveAudio", "true"));
        sdpConstraints.mandatory.add(new MediaConstraints.KeyValuePair("offerToReceiveVideo", "true"));
4. 시그널서버용 코드를 쉽게 설정할 수 있도록 수정
