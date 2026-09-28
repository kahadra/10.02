# VADTree 발표자료 출처와 해석 범위

## 기준 자료

- Wenlong Li, Yifei Xu, Yuan Rao, Zhenhua Wang, Shuiguang Deng. *VADTree: Explainable Training-Free Video Anomaly Detection via Hierarchical Granularity-Aware Tree*. NeurIPS 2025.
- 사용자 제공 `NeurIPS-2025-vadtree-explainable-training-free-video-anomaly-detection-via-hierarchical-granularity-aware-tree-Paper-Conference.pdf`, 총 33쪽. 본문 pp.1–10, 참고문헌 pp.10–14, 체크리스트 pp.15–22, 부록 pp.23–33.
- 사용자 제공 이미지 19개: `src/fig1.png`–`fig3.png`, `src/table1.png`–`table6.png`, `src/fx1.png`–`fx10.png`.
- 형식: `../09.11/index.html`의 1280×720 레이아웃·색상·글꼴·탐색·대본 표시를 계승. `../.agents/agent.md`의 제목/목차 선행, 명사구 제목, 원문 그림 설명 규칙 적용.
- 발표자·소속은 기존 자료의 박천웅·IRV_Lab을 유지. 날짜는 2026.10.02.

이번 자료는 제공된 PDF를 내용의 기준으로 삼았습니다. 외부 최신 버전이나 공개 코드의 현재 상태를 검증한 작업이 아닙니다. 원문 성능을 직접 재현하지 않았습니다. 본편의 일반화·실시간 적용·설명 신뢰성에 대한 논의는 명시된 실험 범위를 읽고 제시한 발표자의 해석입니다.

## 이전 세미나 인용

| 이전 자료 | 실제 인용한 내용 | 이번 연결 |
|---|---|---|
| `../07.29/index.html`, 4장; `EventVAD_presentation_script.md`, Slides 4–6 | MLLM의 시간 단위 불일치; 프레임·전체·고정 클립 한계; 사건 단위 입력 | 본편 3·4·21장, 부록 38장 |
| `../08.12/index.html`, 4장; `MemoVAD_presentation_script.md`, Slides 4·11·12 | 선택적 VLM 질의와 확인된 의미의 재사용 | 본편 3·16·21장, 부록 39장 |
| `../09.11/index.html`, 11장; `presentation_script.md`, Slide 11 | 배경 유사도에 기반한 검출 confidence 재점수화 | 본편 3·21장, 부록 40장 |

기존 HTML을 숨김 Edge에서 직접 렌더링해 `assets/prior_eventvad.png`, `prior_memovad.png`, `prior_bem.png`로 캡처했습니다. 원래 파일은 수정하지 않았습니다. `assets/previous_seminars.json`에 경로·장 번호·렌더링된 텍스트를 기록했습니다.

기존 발표 인용은 당시 설명을 복기하기 위한 것입니다. 이전 논문의 현재 출판 상태나 논문별 성능표를 재검증한 결과로 사용하지 않았습니다. MemoVAD의 약지도·엣지/클라우드 설정과 BEM의 객체 검출 과제는 VADTree의 training-free VAD와 구별했습니다.

## 본편과 원문 대응

| 장 | 내용 | 근거 |
|---|---|---|
| 1–2 | 표지·20분 구성 | 표지, 발표자 시간 설계 |
| 3 | 이전 발표 복기 | 위 기존 세미나 원본 |
| 4 | 고정 창과 사건 길이 | Fig.1 A–B, p.2 |
| 5 | 사건 길이별 구간 정합 | Fig.1 C, p.2; Table14, p.30 |
| 6 | 전체 구조 | Fig.2, p.4 |
| 7 | 경계 신뢰도와 이진 트리 | Eqs.1–3, p.5; Algorithm1, p.23 |
| 8 | 두 군집·중복 제거·완성 | Eq.4, p.5; Appendix A.2, pp.23–24 |
| 9 | 사전 지식·설명·점수 | Eqs.5–7, p.6; Appendix B.1, pp.24–27 |
| 10 | 군집 내 점수 보정 | Eq.8, p.6; C.3, p.28; C.9, p.31 |
| 11 | 부모·자식 융합 | Eqs.9–10, pp.6–7; C.4, p.29 |
| 12 | 모델과 평가 | Sec.4, p.8; Table6; B.1 |
| 13 | UCF·XD 결과 | Tables1–2, p.7 |
| 14 | MSAD 결과 | Table3, p.8; Sec.4.1, p.9 |
| 15 | 모듈 기여 | Table5, p.8; Table13, p.29 |
| 16 | 샘플 수·GPU 시간 | Tables14,16, pp.30–31; C.6–C.7 |
| 17–19 | 정성 결과 전체·행별 확대 | Fig.3, p.10; Sec.4.3 |
| 20 | 적용 한계 | Appendix D, pp.31–32; B.1, Sec.3; 발표자 해석 |
| 21–22 | 기존 발표 연결·결론 | 위 자료의 구조적 비교와 종합 |

세부 장 번호·시간·근거·대본은 `assets/slide_manifest.json`에 함께 저장했습니다.

## 그림·표·수식

사용자 제공 `src/`의 원본 바이트를 유지했습니다. 작은 추출 이미지의 글자 가독성을 위해 같은 PDF의 그림과 표 영역을 4배 배율로 렌더링해 `assets/`에 저장했습니다. 색상·점수·곡선·문장을 새로 생성하지 않았습니다.

- Fig.1: 전체 보존, A–B와 C를 분리하여 본편 4·5장에 사용.
- Fig.2: 전체와 트리 구성 영역을 본편 6·8장에 사용.
- Fig.3: 전체와 위/아래 행을 본편 17–19장에 사용. 각 그래프의 축·색·GT·모델 설명 의미를 대본과 화면에 설명.
- Table1–6: 원문 이미지를 부록에 수록. 본편의 선별 행과 차이값은 HTML로 전사·계산.
- Eq.1–10: 제공된 `src/fx*.png`를 부록에 모두 수록. 본편 10·11장은 기호를 줄인 동치 설명식 사용.
- 추가 Table13·14·16·17: 제공 PDF 부록에서 직접 렌더링. 핵심 비용·안정성 주장 확인에 사용.
- 트리 시간 예시, 융합 슬라이더: 발표자의 계산 예시. 논문 실험값과 구분.
- `assets/manifest.json`: PDF SHA-256, 렌더 페이지·영역(PDF point)·배율·해시, 제공 이미지 해시.

## 수치 비교와 해석

- UCF AUC: VADTree 84.74 − EventVAD 82.03 = **+2.71%p**.
- XD AUC: 90.44 − 87.51 = **+2.93%p**; XD AP: 67.82 − 64.04 = **+3.78%p**.
- XD AP의 VADTree 67.82는 SUVAD 70.10보다 낮음. `VADTree*`는 음향을 추가하므로 별도 행으로 유지.
- MSAD 전체 AP 차이: 71.41 − π-VAD 71.26 = **+0.15%p**. AUCₐ·APₐ는 π-VAD가 더 높음. 본문은 a를 anomaly-specific으로 지칭하며, 상세 산정 범위는 충분히 명세하지 않으므로 전체 AUC/AP와 구별하는 수준으로 설명.
- Table5 누적 증가: **+4.10 / +7.38 / +1.69%p**. 순서 의존적인 차이이며 독립 효과로 해석하지 않음.
- Table14 dense TW 대비 NoS: 69,634 → 8,613 = **87.63% 감소**, **약 8.08배 적은 구간**. 비중첩 10초 창은 3,852개로 더 적음.
- Table14의 dense TW 비교는 sampling variant 비교. Table16은 LAVAD 전체 시스템과의 비교이며 서로 같은 실험으로 합치지 않음.
- Table16: 기본 Think 62.3 GPU·h > LAVAD 55.9 GPU·h. no-Think 44.5 / t5gemma 41.5. C.7에서 LAVAD caption·summary·scoring 시간은 추정이라고 명시함. GPU·h를 FPS나 프레임 지연시간으로 환산하지 않음.
- Eq.10: β=0.4, ŵ=0일 때 부모/자식 0.5/0.5; ŵ=1일 때 0.3/0.7. 슬라이더의 부모=0.3, 자식=0.9, ŵ=0.5이면 0.66.

## 원문 내 구분·불일치

1. **Fig.1과 Table14의 UCF mIoU:** Fig.1의 0.52는 Table14의 `VADTree + Redundant`와 일치. 최종 `VADTree` 행은 0.47. 구성 구분 없이 두 값을 섞지 않았음.
2. **낮은 분산에서 부모 지배라는 서술:** Eq.10에서 β≥0, ŵ∈[0,1]이면 부모 비중은 최대 0.5. 본편은 실제 수식을 기준으로 설명.
3. **정규화:** ŵ에 대한 정규화 동작을 서술하지만 구체 식·상수 분산 처리 등을 명시하지 않음. 임의 구현을 원문 설정으로 단정하지 않음.
4. **VLM 명칭:** p.8 구현 설명은 `LLaVA-Video-7B-Qwen2`, Table6과 비교 설명은 `LLaVA-NeXT-Video-7B`. Appendix B.1의 URL은 전자를 가리킴. 정확한 체크포인트는 코드 대조 대상.
5. **Fine 기준값:** Table4 Fine 82.81 vs. Tables10·12 Fine 83.05. Table5 사전 지식 이후 75.67 vs. Table10 Fine K=0의 73.17. 표 사이 중간 행을 하나의 실험으로 이어 붙이지 않음.
6. **온도 τ=100:** Table11 Fine 값은 83.02, C.3 서술은 82.43. 부록에서 차이를 기록.
7. **Table17 δ:** VADTree 세 회 84.74/84.49/84.73의 δ=0.25는 범위와 일치. 표준편차로 부르지 않음. 반복 3회만으로 방법 간 통계적 유의성을 주장하지 않음.
8. **설명 출력:** B.1.4의 최종 출력 프롬프트는 숫자 리스트 하나를 요구함. Fig.3·6의 설명 문장과 최종 숫자가 어떻게 분리·저장되는지는 재현 시 대조 필요.

## 검증 범위

HTML의 로컬 파일 참조, 41장 화면 렌더, 그림 표시, 화면 경계, 탐색·확대·대본, 20분 타이머, 본편 종료 동작, 반응형 캔버스, 오프라인 로컬 자산, 대본과 화면 노트 동기화를 확인합니다. 실제 결과는 `validation.json`을 참조하세요.

계획 시간 19:00은 합산 검증 대상이며, 사람의 실제 발표시간 측정과 구분합니다. 20분 준수는 제공된 체크포인트와 축약 대본을 사용해 리허설해야 합니다.
