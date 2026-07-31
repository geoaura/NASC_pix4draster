# NASC_pix4draster
[드론영상 밴드중첩 및 식생지수 산출 QGIS plugin]
- 밴드중첩(Layer stack)
  *Pix4dmapper 소프트웨어를 통해 처리된 개별 드론영상의 밴드중첩 수행
  *지원 센서: rededge-mx (remx, 5bands)
                  rededge-mx dual (dual, 10bands)
                  rededge-P (redp, 5bands)
                  phantom 4 multispectral (p4mc, 5bands)
                  mavic 3 multispectral (m3mc, 4bands)
                  rgb camera (rgbc, RGB 3bands, alpha 제외)
- 식생지수(Vegetation index) 계산
  *Green, Red, Red-edge, NIR 밴드 활용
  *NDVI, GNDVI, NDRE


[히스토리]
v1.2.0 (2026.07.31., Jae-Hyun Ryu)
[구조 개선]
- 센서별 개별 모듈(drone_remx/dual/redp/p4mc/m3mc, util) 통합
  -> sensors.py 설정 기반 단일 처리 (센서 추가 시 설정 항목만 등록)
- Plugin Builder 생성 잔여 파일 정리 (미사용 dialog/.ui, Makefile, pb_tool.cfg,
  pylintrc, plugin_upload.py, README, i18n, 컴파일 리소스 제거)

[기능 추가]
- rgb camera 지원: 정사모자이크(3_dsm_ortho/2_mosaic)에서 Alpha 밴드 제외 후
  RGB 3밴드(Byte) 저장, 선택 시 식생지수 체크박스 자동 해제·비활성화
- 실행 시 report 폴더 내 기존 GeoTIFF 삭제 후 재생성
- 처리 과정을 텍스트 파일로 report 폴더에 저장 ({프로젝트명}_log_날짜_시각.txt)
  *오류로 중단된 경우에도 저장, report 폴더가 없으면 프로젝트 폴더에 저장
- 실행 상태표시등 추가 (실행 전 붉은색 / 진행 중 주황색 / 완료 녹색 / 오류 붉은색)
- 창 제목에 플러그인 버전 표시, 폴더 선택 즉시 입력 자료 점검 및 추천 센서 안내
- int16 산출물에 Scale(0.0001)/Offset(0) 메타데이터 기록

[오류 수정]
- 모듈 처리 로그가 QGIS 창에 표시되지 않던 문제 수정 (표준출력 연결)
- 식생지수 밴드 인덱스를 파장 기준 자동 결정 (p4mc 밴드 매핑 오류 수정)
- 산출물 파일명을 폴더명 길이 기반 슬라이싱에서 파일명 내 프로젝트명 추출로 변경
  (폴더명과 프로젝트명이 다를 때 글자 잘림 오류 수정)
- 반사도 int16 변환 시 상한(3.2767) 초과분 오버플로 수정
- 파일 생성 직후 'no such file' 오류 수정: 복사·저장한 파일이 열릴 때까지 대기
  (기본 1초 대기 후 최대 15초까지 재확인, 인식되면 즉시 진행)

[진단 및 표시]
- 오류 상황별 원인·조치 안내 (폴더/입력자료 누락, 센서 불일치, 밴드 누락,
  파일 잠김·권한, 좌표계 누락, 유효화소 없음, 메모리 부족, 백신·네트워크 지연 등)
- 밴드 격자(크기·해상도·원점·좌표계) 불일치 및 공통 유효영역 점검 안내
  (영상은 변형하지 않으며, 격자 정합은 Pix4D Mapper에서 처리)
- 진행 상황 정보 강화: 단계 표시, 영상 제원, 밴드별 유효화소·반사도 통계,
  식생지수 통계, 산출물 목록 및 소요 시간 요약
- 식생지수(NDVI, GNDVI, NDRE) 평균을 0~1 구간 화소만 대상으로 산출
  *수체·그림자 등 음수 구간이 평균을 왜곡하지 않도록 변경, 최소·최대는 전체 범위 표시
- 반사도 이상값 [주의] 기준 2.0 적용

v1.1.0 (2026.03.03., Jae-Hyun Ryu)
- 반사도, 식생지수 값에 10,000 scale factor 값 적용
- 파일형식: Float32 → int16

v1.0.1 (2025.12.15., Jae-Hyun Ryu)
- QGIS plugin 설명자료 내용 수정
v1.0.0 (2025.09.01., Jae-Hyun Ryu)
- 정식버전


v0.3.0 (2024.06.05., Jae-Hyun Ryu)
- 센서를 선택할 수 있는 콤보박스 추가
v0.2.0 (2024.06.04., Jae-Hyun Ryu)
- 버전관리 탭 추가
v0.1.0 (2024.05.23., Jae-Hyun Ryu)
- 초기버전
