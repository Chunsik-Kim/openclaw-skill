# OpenClaw Skills

OpenClaw 에이전트(엘라/토니/니봇)가 사용하는 스킬 백업 및 관리 레포.

## 설치된 스킬 목록

| 스킬 | 버전 | 용도 | 사용자 | 설치일 | API 키 필요 |
|------|------|------|--------|--------|------------|
| firecrawl-search | 1.0.0 | 웹 리서치 + 크롤링 (JS 페이지 포함) | 엘라 | 2026-04-18 | FIRECRAWL_API_KEY |
| memory-hygiene | 1.0.0 (수정) | 메모리 청소·최적화 (백업 단계 추가) | 니봇 | 2026-04-18 | 없음 |
| ai-image-prompts | 1.0.9 | 이미지 생성 프롬프트 추천 (10,000+ 라이브러리) | 엘라 | 2026-04-18 | 없음 |
| self-improving | 1.2.16 | 자기 반성 + 학습 + 메모리 관리 | 전체 | 2026-04-18 | 없음 |

## 설치 경로

컨테이너 내: `/home/node/.openclaw/workspace/skills/`

## 설치 방법

```bash
# 컨테이너 안에서
openclaw skills install <skill-name>
```

## 커스텀 수정 시

1. 이 레포에서 수정
2. 컨테이너에 반영: `docker cp` 또는 직접 편집
3. 변경 사항 commit + push

## 관련 문서

- [엘라 TOOLS.md](https://github.com/Chunsik-Kim/ella-studio) — Git/Vercel 배포 정보
- OpenClaw v2026.4.5
