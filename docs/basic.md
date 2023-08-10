# 문제 정의

- 범용 목적의 프로토콜이나 구현체들은 스케일이 쉽지 않다.
    - 대용량 파일 전송, 이메일 메시지, 실시간성을 요구하는 금융 데이터나, 게임 데이터가 HTTP 서버를 사용하지 않는 것과 같다.
- 따라서 특수 목적에 맞는 최적화 프로토콜을 구현할 필요가 있다.
    - 채팅이나 스트리밍, 대용량 파일 전송을 위한 HTTP 서버를 최적화
    - 레거시 독점 프로토콜과의 상호 운용성 보장

__중요한 것은 안정성과 성능을 포기하지 않으면서 얼마나 빠르게 구현할수 있는가의 문제이다.__


# 문제 해결

Netty는 쉽고 빠르게 네트워크 애플리케이션을 구현할 수 있도록 하는 NIO 클라이언트 서버 프레임워크이다.

Netty는 FTP, SMTP, HTTP를 비롯한 여러 프로토콜로부터의 경험을 기초로 잘 설계되었다.    
따라서 쉬운 개발, 성능, 안정성, 유연성을 달성할 수 있다.

Netty가 다른 비슷한 프레임워크와 차별화되는 것은 철학이다.    
Netty는 API와 구현 측면에서 가장 편한 경험을 할 수 있도록 설계되었다.


# 아키텍처

![](https://user-images.githubusercontent.com/140141048/258360135-bf1a564a-f410-457d-861f-1cc3cec8a218.png)

Netty는 3가지 코어 컴포넌트를 가진다.
- Buffer
- Channel
- Event Model

이 컴포넌트 간의 협업을 바탕으로 다양한 feature가 구현되었다.

## Buffer
JDK에서 제공하는 API(ByteBuffer) 대신에 자체 buffer API를 가진다.(ChannelBuffer)
- own buffer type
- zero-copy
- dynamic buffer (capacity)
- fatster

데이터를 전송할 때 decoding 과 같은 작업 등을 위해 보통은 새로운 buffer에 복사하는 패턴이 많으나,     
Channel Buffer는 복사하지 않고, pointing 한다.

![](https://user-images.githubusercontent.com/140141048/258360487-95c9608d-d512-4733-a952-09544d537421.png)

## Channel 클래스를 통한 비동기 API 통합

Java에서 제공하는 IO API는 서로 호환이 안된다.     
이는 불필요한 노력을 수반하기도 하고,
더 심각하게는, 구현단계에 들어서기도 전에 어떤 API를 사용해야하는 지 강제로 결정해야 한다.

Netty는 Channel 클래스를 퉁화 모든 기능을 추상화하여 제공한다.     
ChannelFactory 구현체를 통해 전환 가능하다.

## Interceptor Chain 패턴 기반 Event Model

## 빠른 개발을 위한 확장된 컴포넌트

core 컴포넌트만으로도 구현가능하지만, 빠른 구현을 위해 몇가지 컴포넌트를 제공한다.

```Codec framework```    
```SSL / TLS Support```
```HTTP Implementation```        
```WebSocket```    
```Google Protocol Buffer```    



