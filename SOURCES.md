# VADTree 발표 자료의 출처와 해석 범위

## 기준 원문

Wenlong Li, Yifei Xu, Yuan Rao, Zhenhua Wang, Shuiguang Deng, *VADTree: Explainable Training-Free Video Anomaly Detection via Hierarchical Granularity-Aware Tree*, NeurIPS 2025. 제공된 [논문 PDF](NeurIPS-2025-vadtree-explainable-training-free-video-anomaly-detection-via-hierarchical-granularity-aware-tree-Paper-Conference.pdf)를 기준으로 작성했다. 논문 보고값을 해설한 자료이며 모델 재실행이나 성능 재현 결과가 아니다.

`src/fig1.png`–`fig3.png`, `src/table1.png`–`table6.png`, `src/fx1.png`–`fx10.png`는 제공된 원문 이미지다. `assets/`의 figure/table/algorithm 이미지는 같은 PDF를 고해상도로 렌더한 것이며, `table1_training_free.png`와 `table2_training_free.png`는 원문 표의 표시 범위를 좁힌 이미지다. 확대 버튼은 전체 원문 표를 연다. 수치나 선을 새로 그린 그림은 발표자의 계산·도식임을 별도로 표시한다.

## 본편 슬라이드별 근거와 읽는 방법

| 장 | 원문 | 발표에서 설명할 핵심과 해석 범위 |
|---|---|---|
| 1–2 | 논문 표지; 발표 구성 | 제목과 목차. 논문 실험의 증거가 아니다. |
| 3 | Sec. 1–2 | LAVAD의 고정 창, EventVAD의 사건 경계 활용에서 이어지는 질문. 각 완성 시스템의 차이를 트리 하나의 인과 효과로 읽지 않는다. |
| 4 | Fig. 1 A–B, PDF p.2 | 빨간 GT 9.0–14.6초와 고정 창의 불일치, coarse/fine의 서로 다른 길이. 한 사례의 동기다. |
| 5 | Fig. 1 C, PDF p.2; Table 14 | x축은 GT 사건 길이, y축은 후보 구간과 GT의 mIoU. Fig. 1의 UCF 평균 0.52는 중복 노드를 유지한 구성이고 최종 트리 값은 0.47. |
| 6 | Fig. 2, Sec. 3 | 왼쪽 트리 생성과 오른쪽 구간 판단·두 단계 보정. GEBD 경계 신뢰도와 이상 점수를 구별한다. |
| 7 | Eqs. (1)–(3), PDF p.5 | 10초 겹침 창은 GEBD 입력; 중앙 절반을 시간축에 이어 붙인 뒤 국소 최대를 경계 후보로 선택. |
| 8 | Algorithm 1, Appendix A.1, PDF p.23 | 현 구간의 최고 경계 신뢰도에서 재귀 분할, 후보가 없거나 최대값이 γ_min=0.4보다 작으면 중단. 부모 노드도 남는다. |
| 9 | Fig. 2 왼쪽; Eq. (4); Appendix A.2 | 경계 신뢰도의 K-means 두 집합에서 coarse/fine 노드 선택. 고정 트리 깊이가 아니다. RemoveDup과 Complete는 중복과 시간 커버리지를 다룬다. |
| 10 | Fig. 2 오른쪽; Eqs. (5)–(7); Appendix B.1 | 노드별 사전 지식·VLM 설명·LLM 초기 이상 점수. 분할 기준은 앞 단계에서 이미 결정됐다. 초기 점수는 보정된 확률이라는 증거가 없다. |
| 11 | Eq. (8); Appendix C.3, C.9 | 같은 coarse 또는 fine 집합의 시각적 유사 노드 K개를 이용한 첫 보정. 시간상 인접 구간만을 뜻하지 않는다. |
| 12 | Eqs. (9)–(10); Appendix C.4 | 자식 점수 분산에 따른 부모·자식 결합. β=0.4에서 분산 0이면 0.5/0.5, 분산 1이면 0.3/0.7. |
| 13 | Eq. (10) | 부모 0.3, 자식 0.9, 정규화 분산 0.5의 0.66 계산은 발표자 예시이며 논문 실험값이 아니다. |
| 14 | Sec. 4 | 성능표는 완성 시스템 비교, 구성요소 표는 내부 변화, Fig. 3은 개별 사례라는 검증 질문. |
| 15 | Table 1, PDF p.7 | UCF 프레임 ROC-AUC. 잘라낸 회색 training-free 행의 EventVAD 82.03과 VADTree 84.74를 비교. 전체 표의 fine-tuning 행까지 최고라는 뜻이 아니다. |
| 16 | Table 2, PDF p.7 | XD의 숫자 열은 AP 다음 AUC. 시각 전용 VADTree AUC 90.44와 EventVAD 87.51; AP는 VADTree 67.82가 SUVAD 70.10보다 낮다. 별표는 음향 입력 추가. |
| 17 | Table 3, PDF p.8 | MSAD 전체 AUC/AP에서 VADTree 89.32/71.41. 이상 특화 AUC_a/AP_a는 π-VAD 71.25/77.86이 VADTree 67.85/75.49보다 높다. |
| 18 | Table 5, PDF p.8; Table 13, Appendix | UCF 누적 AUC 71.57→75.67→83.05→84.74. 가장 큰 상승은 군집 내 보정이 추가될 때다. 누적 차이를 독립적인 모듈 효과로 단정하지 않는다. |
| 19 | Table 14, Appendix C.6, PDF p.30 | NoS는 생성 구간 수. 촘촘한 10초 창 69,634개와 최종 트리 8,613개, mIoU 0.51/0.47, AUC 82.87/84.74를 함께 읽는다. 중복 유지 행의 mIoU 0.52는 별도 구성. |
| 20 | Table 16, Appendix C.7, PDF p.31 | 총 GPU 시간: VADTree 기본 Think 62.3, LAVAD 55.9, no-Think 44.5 GPU·h. 구간 수 감소가 총 GPU 시간 감소와 같지 않다. 일부 LAVAD 비용은 논문의 추정치. |
| 21–22 | Fig. 3, PDF p.10; Sec. 4.3 | 청록 coarse, 분홍 fine, 빨간 GT, 파란 최종 점수. UCF의 절도/정상 매장과 XD의 행동 변화/장면 전환 사례. 사례 그림만으로 평균 성능이나 설명 충실도를 입증하지 않는다. |
| 23 | Appendix D; Tables 14, 16 | 작은 이상 단서를 VLM이 놓치는 문제는 원문 한계. 설명 충실도·온라인 확정·비용 비교는 표와 방법 범위에서 도출한 발표자의 후속 질문. |
| 24 | 위 근거의 종합 | 문제·방법·근거 범위를 요약한 발표자 해석. |

부록 25–43장은 원문 수식 1–10, 표와 그림을 확대해 볼 수 있도록 둔 참고 자료다. 각 장의 원문 위치와 발화 대본은 `assets/slide_manifest.json` 및 `presentation_script.md`에 기록했다.

## 수치와 원문 표현의 주의점

- UCF Table 1의 +2.71%p와 XD Table 2 AUC의 +2.93%p는 EventVAD와 VADTree의 **완성 시스템** 차이다. 트리 구조만의 격리된 효과가 아니다.
- Table 5는 누적 순서의 실험이다. 75.67→83.05의 +7.38%p가 가장 크지만 모듈별 독립 효과를 그대로 뜻하지 않는다.
- Table 14에서 조밀한 10초 창의 69,634개보다 최종 VADTree의 8,613개가 적다. 겹치지 않는 10초 창 3,852개보다는 많다. mIoU와 AUC의 방향도 다르므로 '정합이 높아서 AUC가 높다'는 단일 설명은 성립하지 않는다.
- Eq. (10)의 β=0.4는 부모 가중치를 최대 0.5로 만든다. 원문의 '낮은 분산에서 부모가 지배한다'는 문구와 수식의 수치적 의미 사이에는 차이가 있어 발표에서는 수식을 기준으로 설명한다. 정규화 분산의 구체적 구현은 원문만으로 확정하기 어렵다.
- 과제용 가중치 학습이 없다는 training-free 주장과, 사전학습 GEBD·VLM·LLM 및 데이터셋 이상 유형 사전 지식을 쓰는 사실을 함께 말한다.
- LAVAD의 시간은 Table 16의 비교값이며 Appendix C.7이 일부 단계를 추정으로 기술한다. GPU·h를 FPS나 실시간 처리 보장으로 바꾸어 말하지 않는다.
- 원문의 VLM 명칭은 구현 설명과 비교 표 사이에 일치하지 않는 부분이 있다. 모델 정체를 하나로 확정해 발표하지 않는다.

## 검증 범위

`validation.json`은 HTML의 파일 참조, 슬라이드 개수, 화면 경계, 탐색·확대·발표자 노트·타이머, PDF 내보내기 결과를 기록한다. 계획 시간 19:00은 대본의 합계다. 실제 발표 시간, 모델 실행, 논문 수치의 독립 재현, 생성 설명의 충실도는 이 검증에 포함되지 않는다.