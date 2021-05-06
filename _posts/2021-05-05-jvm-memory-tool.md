---
layout: post
title: jps, jstat
subtitle: JVM Monitoring Tools
tags: [Java, JVM]
comments: true
---

###### 목차
* [Monitoring Tools](#monitoring-tools)
* [jps](#jps)
	* [옵션](#옵션)
* [jstat](#jstat)
	* [옵션](#옵션-1)
		* [일반 옵션](#일반-옵션)
			* [`-class` : Class loader 통계](#-class--class-loader-통계)
			* [`-gc` option: GC에 의해 관리된 heap 통계 출력](#-gc-option-gc에-의해-관리된-heap-통계-출력)
			* [`-gcutil` option: garbage collection 통계를 요약하여 출력](#-gcutil-option-garbage-collection-통계를-요약하여-출력)
			* [`-gccapacity` option: Memory pool generation 과 space capacity 의 정보 출력](#-gccapacity-option-memory-pool-generation-과-space-capacity-의-정보-출력)
		* [출력 옵션](#출력-옵션)
* [참고자료](#참고자료)

---

## Monitoring Tools

JDK 가 제공하는 여러 도구 중에 Java 어플리케이션을 관찰하거나 관리할 수 있는 도구로는 **jconsole, jps, jstat, jstatd** 가 있다. 이 글에서는 jps 와 jstat에 대해 다루고자 한다.

---

## jps

`jps [-q] [-mlvV] [<hostid>]`

입력된 시스템(입력되지 않을 경우, localhost)에서 실행중인 jvm 프로세스들의 정보를 출력한다.

### 옵션
`-q`: 로컬 JVM identifier(pid) 만을 출력한다.  

`-m`: main 메서드에 전달된 인자를 출력한다. (없을 경우 출력하지 않는다.)  

`-l`: main 클래스의 full package name 이나 JAR 파일의 경로를 출력한다.  

`-v`: JVM에 전달된 인자를 출력한다.  

`-V`: Flag 파일을 통해 JVM에 전달된 인자를 출력한다.   
- 참고: [Java 11 버전 오라클 문서](https://docs.oracle.com/en/java/javase/11/tools/jps.html#GUID-6EB65B96-F9DD-4356-B825-6146E9EEC81E) 의 설명이 `-q` 로 잘못 되어있다. 7, 8 버전 문서 참고.

`hostid`: host의 identifier; `[protocol:][[//]hostname][:port][/servername]`  

---

## jstat

`jstat -<option> [-t] [-h<lines>] <vmid> [<interval> [<count>]]`

JVM 통계를 출력한다.

---
### 일반 옵션

#### `-class`: Class loader 통계

Loaded: 로드된 클래스의 개수

Bytes: 로드된 KB

Unloaded: 언로드된 클래스의 개수

Bytes: 언로드된 KB

Time: 클래스 로딩과 언로딩을 하는 데 걸린 시간

---

###### ..'C' 와 ..'U'

..'C': 어떤 영역이 현재 차지하는 용량, capacity를 의미한다. 단위는 KB.
    - 예를 들어, EC: Eden Capacity, OC: Old space Capacity

..'U': 어떤 영역에서 현재 실제로 사용 중인 용량을 말한다. 마찬가지로 단위는 KB.
    - 예를 들어, EU: Eden Utilization, OU: Old space Utilization

#### `-gc`: GC에 의해 관리된 heap 통계 출력

S0C/U: 현재 survivor 0 의 정보

S1C/U: 현재 survivor 1 의 정보

EC/U: 현재 Eden 의 정보

OC/U: 현재 Old space 정보

MC/U: 현재 Metaspace 정보

CCSC/U: Compressed class space 정보

YGC: Young Generation GC의 횟수

YGCT: Young Generation GC의 총 실행시간

FGC: Full GC의 횟수

FGCT: Full GC의 총 실행시간

CGC: Concurrent GC의 횟수

CGCT: Concurrent GC의 총 실행시간

GCT: 전체 GC의 총 실행시간 

#### `-gcutil`: garbage collection 통계를 요약하여 출력
S0: S0의 사용률, (= S0U / S0C * 100)

S1: S1의 사용률

E: Eden space 사용률

O: Old space 사용률

M: Metaspace 사용률

CCS: Compressed class space의 사용률

YGC: Young Generation GC의 횟수

YGCT: Young Generation GC의 총 실행시간

FGC: Full GC의 횟수

FGCT: Full GC의 총 실행시간

GCT: 전체 GC의 총 실행시간 

###### ..'MN' 과 ..'MX'
..'MN': 최소 용량. 단위는 KB

..'MX': 최대 용량. 단위는 KB

#### `-gccapacity`: Memory pool generation 과 space capacity 의 정보 출력

NGC(MN/MX): new generation 의 용량 정보
    - NGC: 현재 용량
    - NGCMN: 최소 용량
    - NGCMX: 최대 용량

S0C: 현재 S0의 용량

S1C: 현재 S1의 용량

EC: 현재 Eden의 용량

OGC(MN/MX): old generation 의 용량 정보

OC: 현재 Old space의 용량, OGC와 같은 값 
- Young Generation의 경우 3개의 영역으로 구분되지만, HotSpot의 old generation은 1개의 영역만 갖고 있다.
- [출처](https://stackoverflow.com/questions/11253285/jstat-difference-between-ogc-oc-pgc-pc)

MC(MN/MX): metaspace 의 용량 정보

CCSC/MN/MX: Compressed class space 의 용량 정보

YGC: Young Generation GC의 횟수

FGC: Full GC의 횟수

- 이외에도 `-gccause`, `-gcnew`, `-gcnewcapacity` 등이 있다. 자세한 설명은 하단의 공식문서 참고.

### 출력 옵션

`-t`: 실행시간을 나타내는 timestamp 열을 가장 왼쪽에 출력한다.  

`-h<lines>`: 열 이름을 lines 수 마다 출력한다.  

`vmid`: Vitrual Machine Identifier (`[protocol:][//]lvmid[@hostname[:port]/servername]`), 프로세스 아이디만 입력할 경우 현재 로컬에서 실행되고 있는 프로세스를 대상으로 한다.  

`interval`: 출력 간격, 생략할 경우 1번만 출력한다.  

`count`: 출력할 카운트, 생략할 경우 무한정 출력한다. 

---

## 참고자료
- [위키피디아: JDK](https://en.wikipedia.org/wiki/Java_Development_Kit)
- [오라클 공식문서](https://docs.oracle.com/en/java/javase/11/tools/monitoring-tools-and-commands.html)
- [CGC, CGCT](https://bugs.java.com/bugdatabase/view_bug.do?bug_id=8196862)
- [Concurrent GC](https://docs.microsoft.com/en-us/dotnet/standard/garbage-collection/background-gc#:~:text=Concurrent%20garbage%20collection%20enables%20interactive,a%20garbage%20collection%20is%20occurring.)
