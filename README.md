# 오픈소스 HW
 1) **sed**명령어, **awk**명령어

    * sed  
   
      * sed 명령어는 코드를 직접 수정하지 않고 명령행에서 파일을 인자로 받아 출력 결과를 화면에서만 볼 수 있는 명령어이다.
      *  **sed 명령어를 사용해서 수정된 파일 내용이 출력되어도 원본 파일은 변경사항이 없다.**
      
      ###### 아래는 예시를 위해 만든 test 파일이다
      
        <img src="https://user-images.githubusercontent.com/66362763/142018133-e53ffbf6-6dba-49fa-b155-eafefb15edad.png" width="80%" height="40%"/>
       
        `$ sed -n '3p' test`를 명령행에 입력하면 파일의 3번째 줄인 *For ever if I'm far away I hold you in my heart*만 출력이 되고
        
        `$ sed '3d' test`를 명령행에 입력하면 파일의 3번째 줄이 삭제되어 출력된다.
        
        여기서 -n 옵션은 변경이 일어난 행만 출력하도록 한다.
        
        `$ sed '/me/d' test`는 me가 포함된 행들만 삭제한 후 출력한다.
       
        ![sed test](https://user-images.githubusercontent.com/66362763/142557940-742f69d0-0369-4f37-b203-817fc3925afc.png)
        
        ![cat test](https://user-images.githubusercontent.com/66362763/142557977-64ef75b2-4b4a-41a7-bbfa-ccb89e8339e6.png)

        
        하지만 아래 이미지처럼 원본 파일에는 변경사항이 없다.    
        
        ![cat no change](https://user-images.githubusercontent.com/66362763/142558052-3c24ba49-b47f-41ea-98a7-320189549b95.png)
          
        `$ sed 's/Remember me/Hello world!/' test`를 명령행에 입력하면 Remember me가 Hello world!로 바뀐 채로 출력된다.
        
        ![Remeber me change Hello World!](https://user-images.githubusercontent.com/66362763/142558345-82b4a4e6-9098-49f8-a741-115edc1329e2.png)
        
        `$ sed '/me/w outfile' test`를 입력하면 test 파일에서 me가 들어간 행을 찾아 outfile에 저장한다.
        
        ![nano outfile](https://user-images.githubusercontent.com/66362763/142558476-e97ecb75-e339-4293-a583-4c2bf9680836.png)
        
               

    #### awk
     
      * awd 명령어는 하나 이상의 공백으로 구분된 여러 열의 텍스트를 처리할 때 유용하게 사용된다.
      * 사칙연산도 awd 명령어를 이용하여 할 수 있다.
      ###### 아래와 같은 새로운 matrix 파일을 만들었다고 하자
      ```
      1 2 3
      4 5 6 
      7 8 9
      ```
      ##### 기본 출력
      
      `cat matrix | awk '{print $1 * $2 + $3;}'`  명령어를 실행하면 아래와 같이 계산되어 출력된다.
      
      ```
      5
      26
      65
      ```
      ##### 구분자 지정
      
      기존 matirx 파일에 숫자와 숫자 사이에 공백을 지우고 ,나 .와 같은 문자를 넣고 `cat matrix | awk '{print $1;}'`를 
      
      명령행에 입력하면 문자로 구분이 되지 않고 출력이 되는데,
      ```
      1,2,3 
      4,5,6 
      7,8,9
      ```
      여기서 -F 옵션으로 구분자를 지정해주고 `cat matrix | awk -F, '{print $1;}'`를 입력하면 첫 번째 열만 출력이 된다.
      ```
      1
      4
      7
      ```
      추가로 `cat matrix | awk -F, '{print $1, $2;}'`를 입력하면 첫번째 열과 두 번째 열이 스페이스로 띄어서 출력이 되고, ','가 없으면 두 열이 붙어서 출력이 된다.
      
      ##### 행번호 출력
      
      awk를 이용한 출력에도 행 앞에 행번호를 붙일 수가 있는데, -NR 옵션을 추가하여 `cat matrix | awk '{print NR " " $0;}'`를 명령행에 입력하면
      ```
      1 1,2,3
      2 4,5,6
      3 7,8,9
      ```
      위처럼 행 번호가 앞에 붙여져서 출력이 된다. $0은 전체 열을 출력한다는 의미이다.
      
      ---
      
2) **getopts** 명령어, **getopt** 명령어
   
   #### getopts
      * 쉘에서 명령을 사용할 때 함께 사용하는 옵션을 스크립트 파일이나 함수를 실행할 때에도 사용할 수 있다.
      * 스크립트 내에서 직접 옵션을 해석해서 사용해야 하는데, 그 때 사용하는 것이 바로 getopts 명령어다.
      * getopts 명령어는 short 옵션을 처리한다. (-n, -al과 같이 '-' 하나와 사용하는 옵션)
   
   #### getopt
      * getopt 명령어는 getopts 명령어와 비슷하지만 명령어와 비슷한데 `/usr/bin/getopt/`에 위치한 외부 명령어이다.
      * getopt는 short 옵션, long 옵션 모두를 지원한다.
      
        
