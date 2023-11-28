[TOC]

------

## 개발환경

```js
/*
테스트서버 주소: https://kodsdev.koscom.co.kr:7443/
​
디폴트
단말번호: 125
지점번호: 001
직원사번: KOSCOMB230142 심재훈 이사님 145동일씨
비번    :패스워드1
         123456
ip     : 010098020190
고객번호 : 1111111234567
​
업무개시 pb: 7609
​
계좌: 1004, 0728
​
폼메이커
service01
service01@
​
USB: zxcv/8520
​
쿼리관련
PB 비번: 1q2w3e4r@@
1. PB결합테스트 (이용자번호 086, 000 확인)
2. 담당자 검색 -> 서비스ID 검색
3. 서비스 우클릭 후 빌더에서 열기 or AUP빌더(결합테스트)에서 csv파일 저장
4. chiron에서 converter를 이용하여 변환
5. NAS서버에 업로드 tomcat9/webapps/Root/WEB_INF/PB_QRY에 변환된 쿼리 txt파일 저장
6. 5. 폴더내에 list.txt에서 QRY명을 명시해줘야 인식 가는ㅇ
6. WAS서버에 업로드 tomcat9_7447 ~ 
*/
```



## 서버

------

스파이더젠

1. `Template ~ Source` 폴더를 모두 드래그로 영역 설정을 하여 우클릭
   `WebDeploymentDlg`에서 update File Version 클릭 후 종료

2. `Build`에서 `update index version` 클릭
   `Update index version`을 클릭하여 모두 우측으로 이동
   disable cache the index.html 체크
   index.html버전 업데이트 클릭

3. bin폴더를 압축하여 USB에 저장

내부망 서버

윈도우 비번: 1q2w3e4r!! 

1. `tomcat9_7443 > webApp > root > bin` 에 USB에 압축했던 파일들을 복붙
   주의: webinf, include 폴더는 건드리면 안됨

## 전자문서 만들기

---

> `"3".padStart(3, "0");` 반환값 : "003";

```js
let wnd = new BaseWindow();
		
const clientInfo = theApp.loginManager.getClientInfo();

const sData = {
    prevViewId: 'OSC11003',	
    accNum: this.accNumber,
    clientName: clientInfo.D1고객명,
    tradeQuantity: this.tradeQuantity.getText(),
    stockName: this.stockName.getText(),
    isDeliberation: chkGrade < bondGrade ? true:false,
    bondInfo: this.bondInfo,		// 채권매수신청을 위해 데이터 통째로도 넘김
    accInfo:{
        "D1계좌번호":theApp.accManager.getSelectAcc()["D1계좌번호"],
        "D1입력비밀번호":theApp.accManager.getSelectAcc()["D1입력비밀번호"]
    },
}

wnd.setData(sData);

wnd.setWindowOption(
    {
        isFocusLostClose: false,
        isModal: true,
        modalBgOption: 'dark'	
    }
);
wnd.openCenter('Source/OSC/wins/OSC11000_W01.lay', this.getContainer(), 320, "auto");

//전자문서순서: 가입신청서(008) -> 신종자본 투자위험고지서(022) -> 가입설명서(021)
wnd.setResultCallback(async (result) => {
    if(result == 1) {
        // 매수신청
        let idData = null;
        
        if(theApp.loginManager.getOcrInfo()){
            idData = theApp.loginManager.getOcrInfo().id_card ? 
                theApp.loginManager.getOcrInfo().id_card.id_card_image : null;
				}
				
            const timeStamp = new Date();
            const timeArr = [timeStamp.getHours(), timeStamp.getMinutes(), timeStamp.getSeconds()];
            const time = timeArr.map((value) => String(value).padStart(2, "0")).join(":");

            let docData = {
                D1계좌번호:Utils.accMake(theApp.accManager.getSelectAcc()["D1계좌번호"]),
                D1고객명:theApp.userInfo.clientInfo.D1고객명,
                D1연락처: ADataMask.customMsk.phoneNum.func(theApp.loginManager.getClientInfo('D1연락전화번호')),
                D1기존정보동일:"1",
                D1종목명:this.stockName.getText(),
                D1주문금액:this.tradeQuantity.getText(),
                D1매매구분_0:"1",
                D1과세구분_0:"1",
                D1예금자보호:"1",
                D1만기사항:"1",
                enableFieldList: [
                    'D1RP거래동의1,D1RP거래동의2,D1RP거래동의3,',
                    'D1집합투자증권1,D1집합투자증권2,D1집합투자증권3,',
                    'D1계열사채권1,D1비계열사권유펀드명,',
                    '대리인성명,대리인생년월일,대리인관계,대리인주소,대리인연락처,',
                    '녹취일,녹취시간,녹취_유선통화자,녹취_비고,투자자체크1,투자자체크2',
                ].join(''),
                stampFieldList:"서명인_1",
                신분증이미지: idData ? "data:image/png;base64,"+ idData : "",
            }
            
        // 전문투자가 아니면서 고령자 or 부적합이면
            if((this.isBujukhab == "1" ||  Utils.isOldAge()) && this.userInvestInfo['D1개인법인구분'] == '1'){
                docData = {
                    ...docData, 
                    "녹취일": Utils.fnGetToday(),
                    "녹취시간": time,
                    "녹취_유선통화자": theApp.loginManager.getLoginInfo('D1사용자명'),
                    "녹취_비고": "",
                }
				}
				
            let result008 = await this.getContainer().view.ecsManager.open('086_008', docData);
        
            if(result008.result != "OK") return;
```



# 구글어널리틱스 적용하기

---

구글 어널리틱스 적용 방법

1. 구글에 어널리틱스의 추적 코드는 2개의 스크립트 부분으로 아래와 같이 구성되어 있습니다.
    ⓐ <script async src=~~~~"></script>
    ⓑ <script>
          ~~~
       </script>

2. 첫번째 src 링크 부분은 스파이더젠 File > Properties... > Project Prop 탭의 Build 화면에서 
    Script Tag & Link Tag 영역에 ⓐ 부분을 카피해서 넣습니다.

3. ⓑ 부분은 원하는 파일명(예:googleanaly.js)으로 스크립트에 해당되는 부분만 복사해서 Assets 원하는 위치(예:Assets/js)에 저장합니다.

4. MainView.cls에 onInitDone 에 맨마지막에 afc.loadScript('Assets/js/googleanaly.js'); 추가합니다.

5. 실행하고 제대로 적용이 되는지 구글 어널리틱스 페이지에서 확인합니다.