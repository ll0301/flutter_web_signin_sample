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
   
-> lib/main.dart 파일의 WelcomScreen위젯에 다음 클래스 정의를 추가한다.   
   class WelcomeScreen extends StatelessWidget {
     @override
     Widget build(BuildContext context) {
       return Scaffold(
         body: Center(
           child: Text('Welcome!', style: Theme.of(context).textTheme.headline2),
         ),
       );
     }
   }   
-> 클래스 (_SignUpFormState)   
  -> SignUp 버튼을 만드는 코드의 일부이다.   
  -> 파란색 배경에 흰색 텍스트이며 누르면 아무것도 수행되지 않는다.   
  -> 내부에 있는 FlatButton의 onPressed 속성에 _showWelcomeScreen 을 추가한다.   
  -> onPressed: _showWelcomeScreen,   
   
-> 클래스 내부에 showWelcomeScreen 메소드 추가    
   void _showWelcomeScreen() {
     Navigator.of(context).pushNamed('/welcome');
   }
   
-> 클래스 (SignUpApp) 의 routes에 다음을 추가한다.   
-> '/welcome': (context) => WelcomeScreen(),   
-> 앱을 실행하고 SignUp 버튼을 클릭하고 Welcome 화면이 보이면 성공    
- 관찰   
* _showWelcomeScreen() 메소드는 build() 메소드에서 콜백 함수로 사용된다. (버튼을 누를 때 이 방법을 호출한다 라는 의미)   
* 플러터에는 하나의 Navigator객체만 있다. 이 위젯은 스택 내에서 플러터의 화면을 관리한다. 새 화면을 스택으로 밀어 디스플레이가 전환된다. 이것이 _showWelcomeScreen 함수를 WelcomeScreen 클래스에서 스택으로 푸시하는 이유이다.     
* * *
[2. 로그인 진행상황 progress tracking]    
* * *
This project is a starting point for a Flutter application.

A few resources to get you started if this is your first Flutter project:

- [Lab: Write your first Flutter app](https://flutter.dev/docs/get-started/codelab)
- [Cookbook: Useful Flutter samples](https://flutter.dev/docs/cookbook)

For help getting started with Flutter, view our
[online documentation](https://flutter.dev/docs), which offers tutorials,
samples, guidance on mobile development, and a full API reference.
