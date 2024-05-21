---
title: 210502 Front-end Side Project Report 1/2일차
date: 2021-05-02 18:01:00
tags:
  - Self-Development
  - React
  - Test-Scenario
  - Side-Project-Diary
categories:
  - Side-Project-Diary
hidden: true
secret: true
---

<div>
  <img src="/images/post_images/210502_side_project.jpeg" alt="나의 사이트 프로젝트 기록"/>
</div>

## **Front-end Side Project Report 1/2일차**

오늘은 본격적으로 사이드 프로젝트를 시작한지 2일차가 되는 날이다.
이전에도 간단하게 사이드 프로젝틑를 진행했지만, 매번 프로젝트를 할때마다 뭔가 애매하게 알고 있는 개념들이 많았다. 그래서 우선적으로 내가 확실하게 알고 있는 것과 모르고 있는 것을 구분하는 것을 시작으로 부족했던 부분을 추가적으로 학습하였다.

아직 완전히 알고 있다고 할 수는 없지만, 이전과 비교했을때 애매하다고 생각되는 개념들이 어느정도 개념이 잡혀서 이제는 공부했던 개념들을 하나씩 적용시켜가면서 프로젝트를 하나씩 완성시켜 나가려고 한다.

이번 사이드 프로젝트는 ReactJS를 활용한 영화 컨텐츠 검색 어플리케이션 개발이다. 이번 사이드 프로젝트는 테스트 주도 개발(TDD)방식으로 진행을 하고, 어제 저녁부터 오늘까지 header와 page 컴포넌트의 틀을 만들었다.
이번 어플리케이션이 비교적 간단한 어플리케이션이기 때문에 TDD방식으로 `실패하는 테스트 코드의 작성부터 테스트 코드를 통과하기 위한 코드 작성, 코드 refactoring을 적용`하는데 좋은 연습이 될 것 같다는 생각이 든다.

테스트 코드를 작성하기 전에 간단하게 `시각적 요소에 대한 테스트`와 `외부 입력에 따른 상태변경에 대한 테스트`로 나눠서 시나리오를 구성해보았다. 이 부분에 대해서는 이전에 네이버의 프론트엔드 개발자 분이 올려주신 프론트엔드 개발에 있어서의 테스트 코드 작성이라는 주제의 블로그 포스팅이 많은 도움이 되었다.

  <!-- more -->

그리고 이번 프로젝트는 CRA(create-react-app)를 사용하지 않고 직접 React프로젝트를 위한 webpack을 만들어서 프로젝트를 진행하였다. 그 이유는 실제 실무에서는 webpack을 직접 커스터마이징해서 사용해야 되는 부분이 많을 것이기 때문이고, CRA를 통해 프로젝트를 생성하게 되면, 내가 프로젝트에서 사용하는 것 외에도 많은 파일들이 자동생성되기 때문이다.

이번 사이드 프로젝트는 `프로젝트의 기본 구성`부터 `프로젝트의 진행방향` 그리고 `작성한 코드`에 대해서 누군가가 물어본다면 제대로 대답할 수 있도록 하는 것이 목표이다.
현재 프로젝트에서 사용되는 기술 스택으로 프로젝트를 진행하면서 개선되어야 한다고 느꼈던 부분들과 어떤 방식으로 해결할 수 있을지에 대한 고민과 해결책은 틈틈이 프로젝트의 README 파일에 정리해두도록 하겠다.
그리고 이번 프로젝트가 자바스크립트로 완성이 되면 (v1.0.0), TypeScript로 기존 프로젝트에 적용(v2.0.0)을 해볼 것이다. 또한 렌더링 최적화를 위한 처리도 꼼꼼하게 적용을 할 것이다.