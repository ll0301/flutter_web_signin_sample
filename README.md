# signin_example
플러터 웹으로 개발하기
* * *
## Getting Started
[웹에서 Flutter 앱 작성]   
- https://flutter.dev/docs/get-started/codelab-web    
- 첫 번째 Flutter 웹 앱 작성 튜토리얼이다. 객체 지향 프로그래밍 및 변수, 루프 및 조건과 같은 개념에 익순한경우 이 학습서를 완료할 수 있다.    

[무엇을 만들것이가]
- 로그인 화면을 표시하는 간단한 웹 앱   
학습 목표 
- 웹에서 자연스럽게 보이는 Flutter 앱 작성방법 
- Flutter 앱의 기본 구조    
- 트윈 애니메이션을 구현하는 방법    
- 상태 저장 위젯을 구현하는 방법    
- 디버거를 사용하여 중단 지점을 설정하는 방법    
준비물   
- 플러터 SDK   
- 크롬 브라우저   
- IDE (VS CODE)   
-> Dart DevTools로 디버깅할 수 있도록 크롬에서 웹앱을 실행한다.   

[초보자용 웹앱 받기]     
-> cmd -> flutter channel beta -> flutter upgrade -> flutter config --enable-web -   
-> flutter doctor -> flutter devices (장치 설치 확인)    
-> cd FlutterProject -> flutter create signin_example -> cd signin_example -> flutter run -d chrome   
-> 크롬 브라우저 실행 확인   

[빌드]
-> flutter build web    
-> 개발 컴파일러 대신 dart2.js를 사용하여 단일 JavaScript 파일을 생성    
*기존 앱에 웹 지원 추가    
-> flutter create .    
-> 기존 프로젝트에 웹 지원을 추가    

[sign up example setting]    
-> https://flutter.dev/docs/get-started/codelab-web    
링크에 있는 예제 signup 코드를 signin_example의 lib/main.dart 에 입력한다.     
- 관찰
  - 예제의 전체 코드는 lib/main.dart 파일에 있다.    
  - Java를 알고 있다면 다트 언어는 매우 친숙하게 느껴질 것이다.     
  - 앱의 모든 UI는 다트 코드로 생성된다.    
  - UI는 시각적 디자인 언어인 Material Design을 준수한다.     
  - ios 디자인언어 cupertino 위젯 라이브러리도 제공한다.     
  - Flutter에서 대부분의 모든것은 위젯이다. 앱 자체도 위젯이다.     
  - 앱의 UI는 위젯 트리로 설명할 수 있다.    
* * *
[1. 시작화면표시]    
-> SignUpForm클래스는 상태 위젯이다. 이는 단순히 사용자 입력 또는 피드의 데이터와 같이 변경할 수 있는 정보를 저장함을 의미한다.    
-> Flutter는 상태 정보를 State Class에 저장한다.   
-> Dart 컴파일러는 밑줄이 붙은 식별자에 대해 프라이버시를 시행한다.    
-> WelcomeScreen 클래스 생성   
-> _SingUpFormState 내부에 _showWelcomeScreen 메소드 생성하고 버튼의 onPressed 속성에 해당 함수를 추가한다.   

-> SignUpApp 내부에 -> '/welcome': (context) => WelcomeScreen(), 경로를 추가한다.   

- 관찰
  - _showWelcomeScreen() 메소드는 build() 메소드에서 콜백 함수로 사용된다. (버튼을 누를 때 이 방법을 호출한다 라는 의미)   
  - 플러터에는 하나의 Navigator객체만 있다. 이 위젯은 스택 내에서 플러터의 화면을 관리한다. 새 화면을 스택으로 밀어 디스플레이가 전환된다. 이것이 _showWelcomeScreen 함수를 WelcomeScreen 클래스에서 스택으로 푸시하는 이유이다.    
* * *
[2. 로그인 진행상황 progress tracking]   
-> 로그인 화면에 3개의 필드가 있고 필드에 사용자가 입력할 때 진행 상황을 추적하고 완료되면 앱의 ui를 업데이트 하도록한다.   
-> _SignUpFormState클래스 내부에 _updateFormProgress() 메소드를 추가한다.   
-> _SignUpFormState클래스 return form() 내부에  -> onChanged: _updateFormProgress, // NEW 코드를 추가한다.   
-> FlatButton의 onPressed 속성을 다음과 같이 변경 -> _formProgress == 1 ? _showWelcomeScreen : null, // UPDATED    
-> 앱을 실행하면 세개의 필드가 모두 텍스트를 포함할 때 활성화된다.   

- 관찰
  - 위젯의 setState() 메소드를 호출하면 flutter에게 위젯을 화면에서 업데이트해야 한다고 알린다. 그 다음 프레임 워크는 이전의 위젯을 처리하고, 하위 위젯트리와 함께 새 위젯을 작성하여 화면에 렌더링 한다. 새로운 위젯 트리는 1/60th 이내에 화면에 렌더링되어 애니메이션을 구현한다. Flutter는 빠르다.   
  - 세개의 필드가 모두 채워지면 _formProgress가 1.0으로 설정된다. 1.0으로 설정되면 onPress 인수가 null 이 아니게 되어 _showWelcomeScreen을 띄울 수 있다. onPressed 에 Dart의 조건부를 사용하여 구현하였다.   
* * *
[2.5 Dart Dev Tools 시작]   
-> Dart Dev Tools을 활용하면 웹앱의 디버깅을 할 수 있다.   
-> cmd -> 프로젝트 디렉토리 이동 -> flutter run -d chrome -> DevTools에 대한 웹 소켓 정보를 가져옴   
-> 디버그 서비스 주소를 복사한다.//127.0.0.1:57187/************   
-> Dev Tools 설치 확인 (각자의 ide에 맞게 공식 문서에 설치법 나와있음)   
-> View/Commen Palette -> Dart: Open DevTools 입력   
-> 활성화 , 업그레이드 하여 패키지 활성화 시킨다. (DevTools가 브라우저에서 시작되어 자동으로 디버그 세션에 연결됨)   
-> 안됨.. 그럴땐 cmd 창에서 실행 -> flutter pub global activate devtools //설치 -> flutter pub global run devtools // 실행   
-> Serving DevTools at http://127.0.0.1:9100 표시되면 성공   
-> 크롬 브라우저에서 표시된 url 입력 하면 dart devtools 창이 뜸   
-> 앱을 실행하고 디버그 서비스 주소를 복사하여 dart devtools connect에 입력하여 dev tools와 실행중인 앱을 연결   
-> dev tools 에서 main.dart 활성화하고 원하는 곳에 중단점을 설정할 수 있다. 후에 앱에서 활동을 시작하면 중단점에서 앱이 중지된다.   
-> 디버깅 결과를 확인할 수 있다.   
* * *
[3 로그인 진행을 위한 애니메이션 추가]   
-> 로그인영역 맨 위에 LinearProgressIndicator 애니메이션을 생성한다.   
-> 파일 맨 아래에 AnimatedProgressIndicator를 추가   
-> _SignUpFormState의 form()에 AnimatedProgressIndicator(value: _formProgress), 를 추가한다.   
-> 앱을 실행하면 세개의 필드에 아무것도 임력하지 않았을 때 빨간색, 1개 주황색, 2개 노란색, 3개 초록색으로 애니메이션이 적용된 것을 확인할 수 있다.   
* * *
This project is a starting point for a Flutter application.

A few resources to get you started if this is your first Flutter project:

- [Lab: Write your first Flutter app](https://flutter.dev/docs/get-started/codelab)
- [Cookbook: Useful Flutter samples](https://flutter.dev/docs/cookbook)

For help getting started with Flutter, view our
[online documentation](https://flutter.dev/docs), which offers tutorials,
samples, guidance on mobile development, and a full API reference.
