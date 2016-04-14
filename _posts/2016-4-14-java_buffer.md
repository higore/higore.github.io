---
layout: post
title: nio ByteBuffer
tag : [java]
---

### 내용
프로젝트를 수행하다보면 버퍼 자료형을 사용할 일이 종종 생깁니다.  
어떤 특징이 있고 활용하는 방버에 대해서 알아보겠습니다.

#### java.nio
nio 패키지는 jdk 1.3에서 부터 사용 할수 있고 기존 io에서 부족한 부분을 채워서 추가 되었습니다.
또한 jdk 1.7 에서는 nio2라고 하며 nio 패키지에 파일관련된 기능이 강화되었습니다.  
이번에 다뤄볼 내용은 nio의 BytyBuffer 입니다.  


#### ByteBuffer
java.nio 의 ByteBuffer는 allocateDirect와 allocate 메소드를 활용하여 선언할 수 있습니다.  
allocateDirect를 통해 사용할때 시스템 메모리를 사용하므로 allocateDirect를 사용하면 더 좋은 퍼포먼스를 기대할 수 있습니다.  
allocate를 쓸경우 jvm의 가상메모리를 사용한 후 가비지 컬렉터가 메모리를 회수 해야 하므로 더 자주 가비지 컬랙팅이 일어나게 하여 시스템 성능을 떨어립니다.하지만 초기 할당 속도는 allocate가 allocateDirect보다 빠르므로 자주 할당 해야 하는 경우 버퍼풀을 구현해서 성능면에서 손해보는 일이 없도록 해야 할 것 입니다.  

#### buffer  
buffer의 인덱스를 다루는데 있어서 알아야할 용어는 아래와 같습니다.
 - capacity : 버퍼의 크기이며 마지막 인덱스를 의미한다.
 - position : 버퍼에서 현재 인덱스를 가르키며 사용하기 전에는 0 이다.
 - limit : 버퍼가 만들어졌을때는 capacity와 같은 값이다.
 - clear() : 버퍼를 초기화 한다. 이름과 달리 실제 데이터를 지우지는 않고 위의 3개 값을 초기화 한다.
 - flip() :  읽기/쓰기 모드를 변경한다. 버퍼에 데이터슷 쓰고 flip() 하면 position은 0으로 돌아가고 limit는 입력데이터 다음 인덱스(즉 limit인덱스공간에는 값이 없다.) capacity는 변경되지 않는다.
 - compact() :  버퍼의 남은 공간을 앞으로 당기고 사용한 공간을 뒤로 이동시킨다. 즉, 서로 스왑한다.