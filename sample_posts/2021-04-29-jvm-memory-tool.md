---
layout: post
title: JVM Monitoring Tools
subtitle: jps, jstat
tags: [Java, JVM]
comments: true
---

###### 목차

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

### 옵션

#### 일반 옵션

##### `-class` : Class loader 통계

Loaded: 로드된 클래스의 개수

Bytes: 로드된 KB

Unloaded: 언로드된 클래스의 개수

Bytes: 언로드된 KB

Time: 클래스 로딩과 언로딩을 하는 데 걸린 시간

##### `-gc` option: GC에 의해 관리된 heap 통계

S0C: 현재 survivor 0 용량 (KB)

S1C: 현재 survivor 1 용량 (KB). 

S0U: survivor 0에서 사용 중인 용량 (KB).

S1U: Survivor space 1 utilization (KB).

EC: Current eden space capacity (KB).

EU: Eden space utilization (KB).

OC: Current old space capacity (KB).

OU: Old space utilization (KB).

MC: Metaspace Committed Size (KB).

MU: Metaspace utilization (KB).

CCSC: Compressed class committed size (KB).

CCSU: Compressed class space used (KB).

YGC: Number of young generation garbage collection (GC) events.

YGCT: Young generation garbage collection time.

FGC: Number of full GC events.

FGCT: Full garbage collection time.

GCT: Total garbage collection time.

##### -gcutil option
Summary of garbage collection statistics.

S0: Survivor space 0 utilization as a percentage of the space's current capacity.

S1: Survivor space 1 utilization as a percentage of the space's current capacity.

E: Eden space utilization as a percentage of the space's current capacity.

O: Old space utilization as a percentage of the space's current capacity.

M: Metaspace utilization as a percentage of the space's current capacity.

CCS: Compressed class space utilization as a percentage.

YGC: Number of young generation GC events.

YGCT: Young generation garbage collection time.

FGC: Number of full GC events.

FGCT: Full garbage collection time.

GCT: Total garbage collection time.

##### -gccapacity option
Memory pool generation and space capacities.

NGCMN: Minimum new generation capacity (KB).

NGCMX: Maximum new generation capacity (KB).

NGC: Current new generation capacity (KB).

S0C: Current survivor space 0 capacity (KB).

S1C: Current survivor space 1 capacity (KB).

EC: Current eden space capacity (KB).

OGCMN: Minimum old generation capacity (KB).

OGCMX: Maximum old generation capacity (KB).

OGC: Current old generation capacity (KB).

OC: Current old space capacity (KB).

MCMN: Minimum metaspace capacity (KB).

MCMX: Maximum metaspace capacity (KB).

MC: Metaspace Committed Size (KB).

CCSMN: Compressed class space minimum capacity (KB).

CCSMX: Compressed class space maximum capacity (KB).

CCSC: Compressed class committed size (KB).

YGC: Number of young generation GC events.

FGC: Number of full GC events.

- 이외에도 `-gccause`, `-gcnew`, `-gcnewcapacity` 등이 있다. 자세한 설명은 하단의 공식문서 참고.

#### 출력 옵션

`-t`: 실행시간을 나타내는 timestamp 열을 가장 왼쪽에 출력한다.  

`-h<lines>`: 열 이름을 lines 수 마다 출력한다.  

`vmid`: Vitrual Machine Identifier (`[protocol:][//]lvmid[@hostname[:port]/servername]`), 프로세스 아이디만 입력할 경우 현재 로컬에서 실행되고 있는 프로세스를 대상으로 한다.  

`interval`: 출력 간격, 생략할 경우 1번만 출력한다.  

`count`: 출력할 카운트, 생략할 경우 무한정 출력한다. 

---

## 참고자료
- [위키피디아: JDK](https://en.wikipedia.org/wiki/Java_Development_Kit)
- [오라클 공식문서](https://docs.oracle.com/en/java/javase/11/tools/monitoring-tools-and-commands.html)
