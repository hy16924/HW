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
      ##### 사칙연산
      
      `awk '{print $1 * $2 + $3;}' matirx`  명령어를 실행하면 아래와 같이 계산되어 출력된다.
      
      ```
      5
      26
      65
      ```
      `awk '{sum+=$1}END{print sum}' matrix` 명령어를 실행하면 첫번째 열들을 더한 값인 12가 출력된다.
      
      여기서 END를 입력하지 않으면 더해질때마다 출력이 되서 아래처럼 출력된다.
      ```
      1
      5
      12
      ```
      여기에 `{print sum}`을 `{print sum/NR}`로 바꿔주면 첫 번째 열의 평균값을 구할 수 있다.
      
      ##### 구분자 지정
      
      기존 matirx 파일에 숫자와 숫자 사이에 공백을 지우고 ","나 "."와 같은 문자를 넣고 `cat matrix | awk '{print $1;}'`를 
      
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
      
      ##### 특정 문자열, 특정 패턴이 있는 행 출력
       ```
       a b c
       d e f
       g h i
       ```
       문자 a가 있는 행만 출력하고 싶을 때 `awk '$1=="a" matrix'를 입력하면 첫 번째 열에 a가 있는 행만 출력되고,
       
       첫 번째 열에 a가 있는 행만 제외하고 출력하고 싶으면 `awk '$1=="a"'를 `awk '$1!="a"'로 바꿔서 입력하면 된다.
       
       특정 패턴이 있는 행을 출력하는 것도 위 예시들과 비슷한데,
       
       `awk '/e/' matrix`는 "e"가 들어있는 행을 출력하고,
       
       `awk '/^d/' matrix`는 "d"로 시작하는 행을 출력한다. 
       
       `awk '$2~/e/' matrix`는 두 번째 열에서 "e"로 시작하는 행을 출력한다. 
       
       따라서 위 세개의 입력 모두 `d e f`가 출력된다.
      
      ---
      
2) **getopts** 명령어, **getopt** 명령어
   
   #### getopts
      * 쉘에서 명령을 사용할 때 함께 사용하는 옵션을 스크립트 파일이나 함수를 실행할 때에도 사용할 수 있다.
      * 스크립트 내에서 직접 옵션을 해석해서 사용해야 하는데, 그 때 사용하는 것이 바로 getopts 명령어다.
      * 인자가 있는 실행옵션은 옵션 뒤에 ":"를 붙여주고, 인지가 필요 없는 옵션은 그냥 써주면 된다.
      * 만약 옵션들을 붙여 쓸 경우(-bch), bch를 각각 하나의 옵션 `-b`, `-c`, `-h`으로 보기 때문에 getopts 명령어로 short옵션과 long 옵션을 동시에 처리하긴 어렵다.

      ###### 아래 파일 이름을 This.sh 이라 하자
      
      ```bash
      #!/bin/bash

      while getopts "a:bch" opt; do # a는 인자를 필요로 하고, bch는 인자가 필요X
      case $opt in
      a)
        echo "You choose option a, OPTARG = $OPTARG" # -a 뒤에 입력된 인자는 $OPTARG에 저장된다.
        ;;
      b)
        echo "You choose option b"
        ;;
      c)
        echo "You choose option c"
        ;;
      h)
        echo "You can choose option between a, b, c"
        ;;
     esac
    done
    shift $(( OPTIND - 1 )) # getopts에 의해 분석된 모든 옵션을 제거하고, 첫 번째로 전달된 비옵션 인수 참조
    echo "$@"
    ```
    `./test.sh -a 123 -b -c hello'를 입력하면 
    ```
    You choose option a, OPTARG = 123
    You choose option b
    You choose option c 
    hello
    ```
    만약 -a 옵션 뒤에 인자를 함께 입력해주지 않으면 `./This.sh: option requires an argument --a`라는 에러 메세지가 뜬다.
    
    이런 에러 메세지를 받고 싶지 않다면, silent mode를 이용하면 되는데, slient mode는 옵션 앞에 ":"를 붙여주면 된다.
    
    그러면 에러 메세지가 출력되지 않는다.
    ```sh
    #!/bin/bash
    
    while getopts ":a:bch" opt; do # a옵션 앞에 ":"추가
    case $opt in
      a)
        echo "You choose option a, OPTARG = $OPTARG"
        ;;
      b)
        echo "You choose option b"
        ;;
      c)
        echo "You choose option c"
        ;;
      h)
        echo "You can choose option between a, b, c"
        ;;
    esac
   done
   shift $(( OPTIND - 1 ))
   echo "$@"
   ```
   
   
   
   
   #### getopt
      * getopt 명령어는 getopts 명령어와 비슷하지만 명령어와 비슷한데 `/usr/bin/getopt/`에 위치한 외부 명령어이다.
      * getopt 명령어는 short옵션과 long 옵션을 모두 처리할 수 있다.
      * short 옵션은 -o와 함께, long 옵션은 -l을 써준다.
      
        
