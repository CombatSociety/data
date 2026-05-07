# Combat Society Data

Combat Society 가 발행한 기사의 **메타·출처·이미지 라이선스** 데이터셋.

> Train. Study. Prepare.
> 군사안보 전문 미디어 — combatsociety.kr

## 구조

```
data/
├── index.csv             # 모든 기사 ↔ 데이터셋 매핑
├── articles/
│   └── YYYY-MM/
│       └── {slug}/
│           ├── meta.json     # 기사 메타 (title·summary·category·tags·priority·content_type·published_at·image_caption·image_credit)
│           ├── sources.json  # multi-source 교차 (Type B 합성 시)
│           └── README.md     # 자동 생성 요약
└── briefs/               # (예정) Daily/Weekly/Monthly/Quarterly digest
```

본문(body) 은 미러하지 않습니다. 사이트(combatsociety.kr) 에서 읽어주세요.

## 콘텐츠 타입

| `content_type` | 설명 | 출처 표기 |
|---|---|---|
| `original` | Type B 자체 합성 — 2+ 매체 교차 후 자체 분석 | sources.json 에 매체 명단 |
| `wire` | Type A 단신 — 단일 외부 매체 출처 | meta.json 의 `source_url`/`source_name` |

## 우선순위

| `priority` | 의미 |
|---|---|
| `P1` | 속보 |
| `P2` | TOP — 주요 이슈 |
| `P3` | NEWS — 일반 |
| `P4` | BRIEF — 요약 |

## 인용 가이드

학술 논문·다른 매체에서 인용 시:

```
Combat Society dataset, "{기사 제목}", combatsociety.kr/news/{slug},
mirrored at github.com/CombatSociety/data, accessed YYYY-MM-DD.
```

## 라이선스

- **데이터** (`*.json`, `*.csv`, `*.md` 자동 생성분): [CC-BY-4.0](LICENSE)
  저작자 표시 시 자유 이용·재배포 가능.
- **미러 에이전트 코드**: MIT (`pipeline/agents/data_mirror.py` in main repo).

## 갱신 주기

매시 정각 자동 갱신 (KST). launchd cron + Supabase pull + git push.
