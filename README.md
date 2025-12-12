# NASC_pix4draster
'Pix4d Mapper' 프로그램을 이용하여 드론 다중분광영상 매핑 후 밴드중첩 및 식생지수를 산출하는 QGIS 플러그인
- 밴드중첩(Layer stack)
  *pix4d 프로그램을 통해 전처리된 다중분광영상 밴드중첩 수행
  *지원 센서: rededge-mx (remx, 5bands)
             rededge-mx dual (dual, 10bands)
             rededge-P (redp, 5bands)
             phantom 4 multispectral (p4mc, 4bands)
             mavic 3 multispectral (m3mc, 4bands)
- 식생지수(Vegetation index) 계산
  *Green, Red, Red-edge, NIR 밴드 활용
  *NDVI, GNDVI, NDRE
