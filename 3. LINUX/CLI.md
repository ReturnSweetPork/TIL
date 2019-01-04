# CLI

- CLI - 커맨드 라인 인터페이스, 키보드 안으로  컴퓨터를 조작함.
- GUI- 그래픽 유저 인터페이스, 키보드와 마우스로 조작함.





# WITCH OS

- Unix based os(Linux, Mac OS 등)
- Unix => 서버를 관리하는 시점에서 무조건 사용하게 됩니다.



# prompt

- 컴퓨터가 명령을 받을 준비가 됨. => $
- 뭔가 막혔을땐 => ctrl + c를 통해서 탈출함.



# 명령어

| 명령어          | 설명                        | 사용법       |
| --------------- | --------------------------- | ------------ |
| echo            | 다음에 들어오는 내용을 리턴 | echo "hello" |
| ctrl + c        | 정지                        | ctrl + c     |
| ↑, ↓            | 이전명령어, 다음명령어      | ↑, ↓         |
| clear, ctrl + l | 터미널 깔끔하게 정리        | clear        |



# 파일조작



| 명령어               | 설명어                                          | 사용법                      |
| -------------------- | ----------------------------------------------- | --------------------------- |
| `>`                  | 왼쪽의 출력물을 오른쪽파일로 전송e              | echo "hello" > hello.txt    |
| `>>`                 | 왼쪽의 출력물을 오른쪽 파일로 붙이기            | echo "hihi" > hello.txt     |
| `cat` `<file>`       | <file>의 내용을 화면에 출력                     | cat hello.txt               |
| `ls`                 | 파일/디렉토리 들의 목록을 보여줌                | ls                          |
| ls - a               | 숨김 파일으 포함해서 모록을 보여줌              | ls -a                       |
| `mv` `<old>` `<new>` | <old>의 이름을 <new>로 변경(나중에 이동도 시킴) | mv hihi hihi.txt            |
| `cp` `<old>` `<new>` | <old>를 <new>로 복사                            | cp hello.txt copy_hello.txt |
| rm <file>            | <file> 지우기                                   | rm hello.txt                |
| rm -r <dir>          | <dir>과 그 하위 폴더와 파일까지 전부 지우기     | rm -f.git                   |
| 탭                   | 자동완성                                        |                             |
| 두번탭               | 목록을 출력                                     |                             |

# 파일검사



| 명령어        | 설명                      | 실행                                                         |
| ------------- | ------------------------- | ------------------------------------------------------------ |
| curl          | url과 상호작용            | curl -O `https://educhang.github.io/test/bohemian.txt                                                                                   ` |
| head '<file>' | 파일의 앞부분 출력        | head bohemian.txt                                            |
| tail '<file>' | 파일의 뒷부분 출력        | tail bohemian.txt                                            |
| wc '<file>'   | 줄, 단어, 바이트를 카운트 | wc bohemian.txt                                              |



# 디렉토리



| 명령어     | 설명                    | 실행 |
| ---------- | :---------------------- | ---- |
| ls         | 파일/폴더 내용을 출력   | ls   |
| pwd        | print working dirctorty | pwd  |
| cd `<dir>` | dir 위치로 이동         |      |

- / : 최상위 루트
- ~ : 홈 디렉토리
- 