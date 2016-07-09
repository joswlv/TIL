#.gitignore파일 만들기
-

|형식   |내용                |
|-------|--------------------|
|*.a    | .a인 파일 무시	 |
|!lib.a | lib.a는 무시안함   |
|/todo  | /todo 안에있는 파일 다무시 하지만 subdir는 무시안함|
|build/ | build 폴더 안에 있는 파일, 디렉토리 다무시 |
|doc/*.txt| doc 폴더 안에 있는 .txt파일 무시 하지만 subdir안에 있는  .txt는 무시안함|
