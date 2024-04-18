# 🗓️ PersonalScheduler

## 🪧 목차
- [📜 프로젝트 및 개발자 소개](#-프로젝트-및-개발자-소개)
- [🕹️ 주요 기능](#%EF%B8%8F-주요-기능)
- [📱 구현 화면](#-구현-화면)
- [💡 키워드](#-키워드)
- [📁 폴더 구조](#-폴더-구조)
- [🔮 개선하고 싶은 점](#-개선하고-싶은-점)
<br>

## 📜 프로젝트 및 개발자 소개
> **소개** : 원티드 프리온보딩에서 진행한 개인 일정을 관리하는 앱 <br> **프로젝트 기간** : 2023.01.09 ~ 2023.01.13

| **App Icom** | **Judy** |
|:---:|:---:|
| <img width="282" alt="image" src="https://user-images.githubusercontent.com/102353787/212327895-0ddff3b5-ccc1-4757-bb67-a20ec46005c7.png">|<img src = "https://github.com/Judy-999/ios-BoxOffice/assets/102353787/ebd9c08c-c5ac-4b51-8dd5-795a4282e31a" width="300" height="300"> |
| |[@Judy-999](https://github.com/Judy-999)|

### ❗️ 로그인 기능을 위한 SecretKey 다운로드 
키를 보호하기 위해 `xcconfig`로 분리해뒀습니다.

[SecretKey.xcconfig 다운로드](https://drive.google.com/file/d/1WkpHBcJlr7lY3KpDiG6OIusCCBtkOgwt/view?usp=share_link)

위 링크에서 `SecretKey.xcconfig` 다운로드 후 파일을 추가한 후 테스트 부탁드립니다!


<br>

## 🕹️ 주요 기능
- 새로운 일정 추가
	- `하루종일` 선택 기능
- 일정 편집
- 카카오 및 페이스북으로 로그인
	- 자동 로그인

<br>

## 📱 구현 화면
### UI in Figma
> 앱을 구현하기 전 Figma를 통해 다음과 같이 디자인 계획을 세운 후 작업하였습니다.

![](https://i.imgur.com/GIVjhCC.png)
<br>

### 실행 예시

|**소셜 로그인** | **일정 목록 및 상세 화면** | 
| :--------: | :--------: |
| ![](https://i.imgur.com/VUG6mZA.gif)| ![](https://i.imgur.com/A895JfW.gif)| 

|**새로운 일정 등록** | **일정 삭제** | 
|:--------: | :--------: |
| ![](https://i.imgur.com/pGLFEBq.gif)| <img src = "https://i.imgur.com/Jj5myw1.gif" width="300" height="600">| 

<br>

## 💡 키워드
- [x] **Firebase-Firestore**
- [x] **FirebaseAuth**
- [x] **KakaoLogin**
- [x] **FacebookLogin**
- [x] **Observable**
- [x] **MVVM**
<br>

### 디자인 패턴
**Observable Pattern**
- MVVM 구현 시 데이터 바인딩을 위해 옵저버블 패턴으로 구현했습니다.

**Singleton Pattern**
- 데이터베이스로 사용하는 FirestoreManager와 로그인을 관리하는 LoginManager 구현 시 하나의 인스턴스를 유지하고 전역으로 사용하기 위해 싱글톤 패턴을 적용했습니다.
- **UserDefault** : 자동 로그인을 위한 정보를 저장하되 앱을 삭제할 때는 자동 로그인이 해제되어야 한다고 생각하여 `UserDefault`로 해당 기능을 구현했습니다.

**Delegate Pattern**
- 하루 종일 스위치에 따른 DatePieker의 Mode와 선택 날짜를 변경하는 작업을 대신 수행하기 위해 델리게이트 패턴을 적용했습니다.

<br>

### MVVM 
**ViewModel** 
- view에서 받은 이벤트를 가지고 데이터를 가공 및 전달

**View**
- 사용자의 입력을 받아 ViewModel에 이벤트를 전달하고 ViewModel로부터 데이터를 가져와 화면에 출력

**Model** 
- 데이터 구조를 정의
 
**Obsevable**
- MVVM 구조에서 `ViewModel`과 `View`의 데이터를 바인딩하기 위해 `Observable` 클래스를 구현하여 사용

<br>

## 📁 폴더 구조

```swift
.
├── GoogleService-Info.plist
├── Info.plist
├── PersonalScheduler.entitlements
├── Application
│	├── AppDelegate.swift
│	└── SceneDelegate.swift
├── Domain
│	├── Entity
│	│	└── Schedule.swift
│	└── UseCase
│	    └── ScheduleFirestoreUseCase.swift
├── Resources
│	├── Assets.xcassets
│	│	├── AccentColor.colorset
│	│	│	└── Contents.json
│	│	├── AppIcon.appiconset
│	│	│	└── Contents.json
│	│	├── Contents.json
│	│	└── kakao_login_medium_wide.imageset
│	│		├── Contents.json
│	│		└── kakao_login_medium_wide.png
│	└── Base.lproj
│	    └── LaunchScreen.storyboard
├── Scene
│	├── LoginScene
│	│	└── LoginViewController.swift
│	├── Namespace
│	│	├── AlertPhrase.swift
│	│	├── ScheduleImage.swift
│	│	└── ScheduleInfo.swift
│	├── ScheduleDetailScene
│	│	├── ScheduleDetailViewController.swift
│	│	└── SubViews
│	│		├── DetailViewMode.swift
│	│		├── ScheduleDatePickerView.swift
│	│		└── ScheduleSwitchView.swift
│	└── ScheduleListScene
│	 	├── ScheduleListViewController.swift
│	 	├── ScheduleViewModel.swift
│	 	└── SubViews
│			└── ScheduleListTableViewCell.swift
├── Service
│	└── Firestore
│		├── FirebaseError.swift
│		└── FirestoreManager.swift
└── Utility
	├── Extension
	│	├── Date+toString.swift
	│	├── String+toDate.swift
	│	└── UIViewController+Alert.swift
	├── LoginManager
	│	└── LoginManager.swift
	└── Observable
	 	└── Observable.swift
```
<br>

## 🔮 개선하고 싶은 점
### Apple Login 및 Remote 알림
해당 기능은 Apple Developer Membership을 소유하지 않아 구현 불가능했습니다. 이후 조건이 갖춰지면 구현해보고 싶습니다.

### 로그아웃
현재는 앱을 삭제하지 않는 이상 로그인 정보를 변경할 수 없습니다. 로그아웃 기능을 추가하고 현재 로그인 기능도 효율적으로 개선해보고 싶습니다.
또한 소셜 로그인을 사용하지 않고 `이메일-비밀번호`로 회원가입하는 기능을 추가하면 좋을 것 같습니다.

<br><br> 
