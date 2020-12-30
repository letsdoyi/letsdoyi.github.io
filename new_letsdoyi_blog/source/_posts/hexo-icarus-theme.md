---
title: "Hexo Icarus Theme 커스터 마이징"
date: 2020-03-23 00:41:04
tags: hexo
categories:
- Playground
---
Hexo는 블로그 프레임워크이며, 다양한 테마를 제공합니다. 그 테마 중 현재 사용 중인 Icarus라는 테마를 어떻게 커스터 마이징 하였는지 정리하고자 합니다. Icarus 테마는 다양한 위젯을 제공하며, 이 위젯을 켜고 끌 수 있습니다. `themes/icarus/_config.yml` 파일에서 커스터마이징을 할 수 있습니다.

## 화면 분할 (위젯 설정)
```
# Widget name
type: recent_posts
# Where should the widget be placed, left or right
position: {right}
```
현재 이 블로그처럼 article 공간을 좀더 크게 활용하고 싶다면 위젯을 한쪽으로 몰아 배치하면, 자동으로 article 부분의 공간이 넓어집니다.

## post 내용을 일정 부분 숨기기
`READ MORE`을 표시하려면 자신이 작성한 post에 `<!-- more -->` 을 넣어주면 됩니다. 이 태그가 들어간 글의 앞부분은 Home 페이지에 노출이 됩니다.

## thumbnail 넣기
자신이 작성한 post에 `thumbnail:{이미지 주소}`를 넣어 설정 가능 합니다.
저는 깔끔하고 차분한 분위기 블로그를 위해 thumbnail을 숨겨놓았는 데, 어떻게 해야 할지는 현재도 고민 중입니다.

<참고>
https://github.com/ppoffice/hexo-theme-icarus/issues/60