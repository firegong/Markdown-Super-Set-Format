# 마크다운 수퍼 포맷 (Markdown Super Format)

> **기준:** MultiMarkdown 6(MMD)을 기본으로 한다. MMD가 지원하지 않는 문법은 **Pandoc Markdown → markdown-it → Obsidian** 순으로 가져온다.
> 같은 기능이 여러 곳에 있으면 앞 순서의 문법을 쓴다.
>
> **출처 표기:** 출처 열에는 해당 문법을 지원하는 **모든** 표준을 적는다. `(플러그인)`은 markdown-it에서 확장 플러그인으로만 지원함을 뜻한다.
> 약어: CM = CommonMark, GFM = GitHub Flavored Markdown, MMD = MultiMarkdown 6, PD = Pandoc Markdown, MI = markdown-it, OB = Obsidian

## 0. 설계 원칙

1. **MMD 우선**: MMD 문법으로 표현 가능하면 MMD 문법만 쓴다.
2. **출처 순서**: MMD → Pandoc → markdown-it(GFM 계열) → Obsidian.
3. **충돌 금지**: 같은 기호가 두 의미를 갖지 않도록 아래 "충돌 해결" 규칙을 따른다.
4. **렌더링 안전성**: 가져온 문법은 해당 도구가 없어도 읽기 쉬운 원문이 남도록 쓴다.
5. **입력 편의성**: 기호 한 글자로 동작을 바꾸지 않는다. 실행·렌더링 여부는 키워드(`run`, `render`)로 명시한다.

(전체 사양은 영어 버전 README.md를 참조하세요. 한글 전체 본문은 이 파일에 제공됩니다.)

## 지원 범위 요약

| 출처 | 가져온 항목 |
|---|---|
| MultiMarkdown | 기본 문법 전체, 정의 목록, 아래·위첨자, 제목 ID, 표 캡션, 그림·표 상호 참조, 수식, 각주, 메타데이터 |
| Pandoc Markdown | 취소선, 밑줄 span, 작업 목록, 예제 목록, 코드 속성·캡션, 원시 블록, 이미지 크기, 그리드 표, 인용 참조, YAML 메타데이터 |
| markdown-it | GFM 계열 기능과 알림 블록(Obsidian과 동일 문법으로 통합). 별도 문법은 추가하지 않음 |
| Obsidian | 위키링크, 임베드, 하이라이트, 주석, 태그, 블록 참조, 콜아웃, 이미지 크기 임베드 |

## 주의

- 이 문서는 **설계안**이다. 실제 렌더러마다 동작이 다르므로, 출력 도구에 맞춰 일부 문법을 바꿔야 할 수 있다.
- Pandoc YAML과 MMD 메타데이터는 동시에 쓰지 않는다.
- 공식 명세와 다른 부분이 있을 수 있으니 최종 사용 전 각 도구에서 샘플로 검증한다.

## License

MIT License. See the SuperMark project for full license details.