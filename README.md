# AntBuildEx04_ASM_API_TEST

## 1.	목표

shell을 통해 암호화 및 복호화를 해보자.

## 2.	build.xml 코드

```
<project name="ShellScriptBuilder" default="buildShellScript">

    <property name="jar.dir" value="libs"/>
    <property name="jdbc.url" value="jdbc:mysql://*.*.*.*:3306/exampledb"/>
    <property name="jdbc.user" value="user2"/>
    <property name="jdbc.password" value="password"/>

    <!-- Build shell script -->
    <target name="buildShellScript">
        
        <echo file="example_script.sh"><![CDATA[
            #!/bin/bash

            # Get current directory of the script
            DIR="$( cd "$( dirname "${BASH_SOURCE[0]}" )" &> /dev/null && pwd )"                             

            MY_HOME=$DIR
            MY_LIB_PATH=$MY_HOME/lib
            MY_CLASSPATH=""

            export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$MY_LIB_PATH
            for LIB_NAME in `ls $MY_LIB_PATH | grep jar`; do
                MY_CLASSPATH=$MY_CLASSPATH$MY_LIB_PATH"/"$LIB_NAME
            done


            javac -cp ".:$MY_CLASSPATH" Test.java

            java  -cp ".:$MY_CLASSPATH" Test


            echo "MY_HOME :: "$MY_HOME
            echo "MY_CLASSPATH :: "$MY_CLASSPATH
            echo "MY_LIB_PATH :: "$MY_LIB_PATH

            # Changing permission
            chmod 755 example_script.sh

            echo "Shell script created successfully."
        ]]></echo>
    </target>

</project>
```
## 3.	java code
```
import *;

public class Test {
  public static void main(String[] paramArrayOfString) {
    try {
      String str1 = *.encrypt("subwaypolicy", "123123123");
      System.out.println(str1);
      String str2 = *.decrypt("subwaypolicy", str1);
      System.out.println(str2);
    } catch (Exception exception) {
      exception.printStackTrace();
    }
  }
}
```
## 4.	코드 설명 
-	<property>엔트를 통해 라이브러리 디렉토리, jdbc url, 사용자 이름, 비밀번호를 설정한다.
-	<target> 엔트를 통해 실행할 작업을 정의한다. 
-	<echo>엔트를 통해 파일로 출력하도록 정의한다. 
-	스크립트 파일은 bash에서 실행될 수 있도록한다.
-	스크립트는 현재 스크립트 파일의 디렉토리를 찾아 MY_HOME에 저장한다.
-	LD_LIBRARY_PATH에 MY_LIB_PATH를 추가한다.
-	java code를 실행하여 암복호화를 수행한다.

## 5.	실행결과
 
![image](https://github.com/auspicious0/AntBuildEx04_ASM_API_TEST/assets/108572025/f190b4c5-daac-4196-aa52-5f60d9c58380)

