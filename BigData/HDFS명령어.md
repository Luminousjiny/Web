# HDFS 명령어(하둡2)

```
./bin/hdfs dfs-cmd [args]
```

### HDFS내에 사용자 홈 디렉터리

```
**/user/사용자명**
```

```
ex> ./bin/hdfs dfs -ls data   -> /user/hadoop/data 디엑터리 조회
```

### 자주 사용하는 HDFS 명령어

```
mkdir : 디렉터리 생성
ls : 파일 목록 보기
get, copyToLocal : HDFS -> 로컬 디스크 파일 이동
put, copyFromLocal : 로컬디스트 -> HDFS로 파일이동
cat : 파일보기
mv : 이동
cp : 복사
```
