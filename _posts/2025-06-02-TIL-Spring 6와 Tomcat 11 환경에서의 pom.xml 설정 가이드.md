---
title: "[Spring] Spring 6와 Tomcat 11 환경에서의 pom.xml 설정 가이드"
excerpt: "Spring 6, Tomcat 11 설정"

categories:
  - ETC
tags: ["Spring", "Tomcat"]

permalink: /etc/spring6_tomcat11_config/

toc: true
toc_sticky: true

date: 2025-06-02
last_modified_at: 2025-06-02
---

# 📜Spring 6와 Tomcat 11 환경에서의 pom.xml 설정 가이드
Spring 프레임워크 6 버전부터 Jakarta EE 10을 기반으로 하기 때문에 기존의 `javax.*` 패키지들이 모두 `jakarta.*`로 변경되었다. 이로 인해 톰캣도 10 이상, 특히 Tomcat 11을 사용하는 경우에는 반드시 Jakarta 기반의 API들을 사용해야 한다. 본 포스트에서는 Spring 6.1.4와 Tomcat 11, Java 24 환경에서 WAR 프로젝트를 구성할 때 필요한 `pom.xml` 설정을 정리한다.

---

## 1. 환경 정보

- Java: 24
- Spring Framework: 6.1.4
- Tomcat: 11
- Maven: 3.8 이상
- 프로젝트 타입: WAR

---

## 2. 주요 고려사항

### ✅ Spring 6 이상은 Jakarta EE 10을 사용

Spring 6부터는 다음과 같은 변화가 있다:

| 기존 패키지         | 변경된 패키지            |
|--------------------|--------------------------|
| `javax.servlet.*`  | `jakarta.servlet.*`      |
| `javax.inject.*`   | 그대로 유지 가능         |
| `javax.jsp.*`      | `jakarta.servlet.jsp.*`  |
| `javax.jstl.*`     | `jakarta.servlet.jsp.jstl.*` |

---

### ✅ JSP와 JSTL 설정도 Jakarta로 전환 필요

JSP와 JSTL도 Jakarta EE 10 호환 라이브러리를 사용해야 Tomcat 11에서 정상 동작한다. Maven에서 제공하는 `jakarta.servlet.jsp.*` 및 `jakarta.servlet.jsp.jstl.*` 그룹 ID를 사용하는 것이 핵심이다.

---

### ✅ Maven Compiler Plugin 버전 주의

Java 21 이상부터는 `maven-compiler-plugin`을 **3.10 이상**으로 설정해야 빌드 오류 없이 사용할 수 있다. Java 24를 사용하는 경우에도 동일하다.

---