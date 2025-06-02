---
title: "[커널아카데미] 백엔드 부트캠프 10주차 - Spring의 내부 동작"
excerpt: "10주차 회고"

categories:
  - Reflection
tags: ["커널아카데미", "패스트캠퍼스"]

permalink: /reflection/10thweek/

toc: true
toc_sticky: true

date: 2025-05-11
last_modified_at: 2025-06-01
---

# 📜 10주차 회고
이번 주에는 Spring 프레임워크의 요청 처리 흐름과 초기화 과정에 대해 학습하였다.

우선, 클라이언트의 요청이 들어왔을 때 톰캣(Tomcat)이 이를 어떻게 처리하는지를 이해하는 것이 핵심이었다.
톰캣은 내부의 쓰레드 풀(Thread Pool)에서 하나의 쓰레드를 할당하여 요청을 처리하며, 웹 애플리케이션 초기화 시점에 다음과 같은 과정을 거친다.

**ContextLoaderListener**를 통해 Root Application Context가 생성된다. 이 과정은 web.xml의 설정에 의해 자동으로 실행된다.

이후 **DispatcherServlet**이 초기화되며, 이를 통해 Servlet Application Context가 별도로 생성된다.

클라이언트의 요청은 DispatcherServlet을 통해 Controller로 전달되고, 이 흐름 속에서 ViewResolver, HandlerMapping 등 여러 컴포넌트가 작동하여 최종적으로 응답이 반환된다.

이번 학습을 통해, Spring의 전체적인 구조와 작동 원리를 이해하는 기반이 마련되었다. 단순히 어노테이션을 사용하는 수준이 아니라, Spring이 내부적으로 어떻게 구성되고 실행되는지를 알게 되었기 때문에, 앞으로 실무 수준의 개발을 이해하고 설계하는 데 있어 중요한 전환점이 되었다.

다음 주부터는 본격적으로 스프링의 핵심 기능들을 더 깊게 학습해나갈 예정이다. 시스템의 작동 원리를 이해한 만큼, 앞으로의 학습도 더욱 명확한 방향성을 가지고 진행할 수 있을 것이다.