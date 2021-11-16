### 오픈소스 HW
1) **sed**명령어, **awk**명령어

    * sed 
      * sed 명령어는 코드를 직접 수정하지 않고 명령행에서 파일을 인자로 받아 출력 결과를 화면에서만 볼 수 있는 명령어이다.
      *  **sed 명령어를 사용해서 수정된 파일 내용이 출력되어도 원본 파일은 변경사항이 없다.**
      ###### 아래는 예시를 위해 만든 test 파일이다
      
        <img src="https://user-images.githubusercontent.com/66362763/142018133-e53ffbf6-6dba-49fa-b155-eafefb15edad.png" width="80%" height="40%"/>
       
        `$ sed -n '3p' test`를 명령행에 입력하면 파일의 3번째 줄인 *For ever if I'm far away I hold you in my heart*만 출력이 되고
        
        `$ sed -n '3d' test`를 명령행에 입력하면 파일의 3번째 줄이 삭제되어 출력된다.
        
        여기서 -n 옵션은 변경이 일어난 행만 출력하도록 한다.
        
        `$ sed '/me/d' test`는 me가 포함된 행들만 삭제한 후 출력한다.
        
        하지만 아래 이미지처럼 원본 파일에는 변경사항이 없다.    
        
          
        `$ sed 's/Remember me/Hello world!' test`를 명령행에 입력하면 Remember me가 Hello world!로 바뀐 채로 출력된다.
        
        `$ sed '/me/w outfile' test`를 입력하면 test 파일에서 me가 들어간 행을 찾아 outfile에 저장한다.
    * awd
     
      * awd 명령어는 하나 이상의 공백으로 구분된 여러 열의 텍스트를 처리할 때 유용하게 사용된다.
      * 사칙연산도 awd 명령어를 이용하여 할 수 있다.           
        
