
# 데이터 청년 캠퍼스 프로젝트 - 널뛰기
+ 개인별 달리기 경로 및 크루 추천 서비스

## 첨부할 데이터셋 + 실행 파일(ipynb)
> [명소_경로_최종.zip](https://github.com/YoungGenuineLee/-/files/7071114/_._.zip)

> [nature_GA.zip](https://github.com/YoungGenuineLee/-/files/7072817/nature_GA.zip)

> [안전경로 모듈화 + 추천.zip](https://github.com/YoungGenuineLee/-/files/7071117/%2B.zip)

##### -> (필요한 경우 seoul 전체의 데이터 셋을 이용하셔도 됩니다.)

#### 필요 라이브러리(모듈)

    pip install folium
    pip install numpy
    pip install pandas
    pip install matplotlib
    pip install selenium
    pip install haversine
    pip install json
    pip install requests
    pip install sklearn
    conda install osmnx
    conda install networkx
    conda install geopandas
    conda install geopy
    
    

#### 1. 데이터 셋 설명
> ##### A.명소_경로_최종.zip
> > + 서울시 관광 명소(서울열린데이터광장, csv)
> > + 서울시 관광거리 정보(서울열린데이터광장, csv)
> > + 서울 두드림길 계절별 추천코스 정보(서울열린데이터광장, csv)
> > + '대한민국 구석구석'사이트를 크롤링으로 명소 정보 획득 후 위도, 경도 좌표계 반환한 데이터(대한민국 구석구석, csv)
> > + OSMNX 패키지 내부에 있는 노드 추출(파이썬 OSMNX패키지, csv)
> > > ##### 모든 데이터 셋은 OSMNX 패키지 내부에 있는 노드에 점수를 부여하는 용도로 각 데이터 셋의 위도, 경도(lat, lon)을 추출해 사용하였습니다. 필요한 경유 좌표를 EPSG : 4326으로 변경해 사용하였습니다.


> ##### B.nature_GA.zip
> > + OSMNX 패키지 내부에 있는 노드 추출(파이썬 OSMNX패키지, csv)
> > + 서울시 가로수 위치 정보 데이터(서울열린데이터광장, csv)
> > + 서울시 주요 공원현황 데이터(서울열린데이터광장, csv)
> > + 서울시 녹지대 위치정보데이터(서울열린데이터광장, csv)
> > + 서울시 도시공원정보(공공데이터포털, csv)
> > + 서울시 격자파일 (서울열린데이터광장, json)
> > > ##### 모든 데이터 셋은 OSMNX 패키지 내부에 있는 노드에 점수를 부여하는 용도로 각 데이터 셋의 위도, 경도(lat, lon)을 추출해 사용하였습니다. 필요한 경유 좌표를 EPSG : 4326으로 변경해 사용하였습니다.

> > 

> >  지정코스_GeneticAI.ipynb 파일의 순서는 원형코스와 같은 과정을 거치며 출발지를 포함해 총 6개의 노드를 추출합니다.

> ##### C.안전경로_모듈화 + 추천.zip
> > + OSMNX 패키지 내부에 있는 노드 추출(파이썬 OSMNX패키지, csv)
> > + 각 구별 cctv(안심이)데이터(서울열린데이터광장, csv), 전처리 후 합친 중구_용산구_성동구 cctv데이터
> > + 각 구별 보안등데이터(서울열린데이터광장, csv), 전처리 후 합친 중구_용산구_성동구 보안등데이터
> > + 서울시구경계.shp(https://blog.naver.com/rackhunson/222398821837) -> 전처리로 저장한 성동구 횡단보도, 중구 횡단보도, 종로구 횡단보도 데이터
> > + item.csv는 추천알고리즘 적용을 위해 임의로 만든 dummy data입니다. 용도에 맞게 변경하셔서 사용하시면 더 좋은 synergy를 낼 수 있습니다.
> > > ##### 추천 알고리즘을 제외한 모든 데이터 셋은 OSMNX 패키지 내부에 있는 노드에 점수를 부여하는 용도로 각 데이터 셋의 위도, 경도(lat, lon)을 추출해 사용하였습니다. 필요한 경유 좌표를 EPSG : 4326으로 변경해 사용하였습니다.

> > 안전경로 모듈화.ipynb 

#### 2. 실행파일(ipynb) 설명
> ##### A.명소_경로_최종.zip
> > 명소_경로찾기_최종(중구, 성동구, 종로구).ipynb는 다익스트라 알고리즘을 이용해 경로를 구성하였으며 파일의 진행순서는 OSMNX패키지 내 노드 추출 -> Google geocoding API를 활용한 '대한민국 구석구석'사이트 크롤링한 명소들 데이터 위도, 경도 반환 -> csv파일을 입력 후 OSMNX 패키지 노드별 점수 부여 -> 노드와 노드사이 edge를 추출후 거점별 점수 부여 -> 다익스트라 알고리즘 기반 부여된 점수를 기준으로 (목표거리/3) +- 5%인 지점을 경유지로 설정 후 출발지, 경유지, 도착지점을 이어 경로를 설정 하는 방식으로 구현이 되어 있습니다.
> > ##### + 직접실행을 위한 함수 설명
> > > make_2d_list -> Series객체를 2차원 리스트 형태로 반환합니다.

> > > score_by_distance -> 입력한 2개의 리스트의 위도, 경도를 기준으로 거리를 측정하고, 측정된 거리에 따라 노드별 점수와 노드를 반환합니다.

> > > nearest_node -> OSMNX패키지내 노드중 입력한 (위도, 경도)와 가장 가까운 노드를 반환합니다.

> > > node_to_node_distance -> 입력한 노드와 노드 사이의 거리를 계산합니다.

> > > make_waypoint_list -> 출발지, 목표거리를 입력하면 (목표거리/3) +- 5%의 거리를 기준으로 경유지 노드를 탐색합니다.

> > > make_way_to_way_list -> make_waypoint_list에 의해 추출된 노드들 사이의 거리를 계산하여 노드 사이의 거리가 (목표거리/3) +- 5%에 해당하는 경유지쌍들을 반환합니다.

> > > best_route -> make_way_to_way_list에 의해 만들어지 경유지쌍을 이용하여 출발지->경유지1->경유지2->출발지로 돌아오는 다양한 원형코스를 생성하고 가중치를 'sights'(명소)로 설정하여 가장 명소와 적합한 하나의 경로를 반환합니다.

> > > route_distance -> 경로의 거리를 측정합니다.

> > > make_graph -> 원형코스의 경로를 시각화 합니다.

> > > make_direct_graph -> 직선코스의 경로를 시각화 합니다.

> > > search_node -> 무작위로 받은 출발지와 도착지의 위도,경도와 가장 유사한 노드를 탐색합니다.


> ##### B.genetic_final.zip
> > 자연코스.ipynb (A) 파트는 위치 기준 자동 경로 추천 부분이며
> > > 1. 출발지 및 원하는 dist(km, 거리)를 입력하며, 네이버 api를 통해 출발지의 위경도 반환
> > > 2. 출발지 기준 일정 반경(1 or 1.5km) 내 데이터 필터링
> > > 3. 필터링 된 데이터 중 상위 50%에서 9개의 노드 랜덤 추출 후 출발지 데이터 추가
> > > 4. 유전 알고리즘 (tsp) 적용
> > > 5. 4번을 통해 검출된 거리가 dist - (dist/30) ~ dist+(dist/30)에 만족할 때까지 반복하는 순서 입니다.

> > (B) 파트는 입력 구간 경로 추천하는 부분이며
> > > 1. 출발지, 도착지를 입력하며, 네이버 api를 통해 각 입력에 대해 위경도 반환
> > > 2. 두 좌표로 사각형을 정의하고 범위 내 데이터를 필터링
> > > 3. 필터링 된 데이터 중 상위 50%에서 8개의 노드 랜덤 추출
> > > 4. 유전 알고리즘 (tsp) 적용
> > > 5. 4의 결과에 출발지와 도착지를 추가하여 경로 생성 하는 순서입니다.

> > ##### + 직접실행을 위한 함수 설명
> > > 전처리를 위한 함수

> > > make_2d_list -> Series객체를 2차원 리스트 형태로 반환합니다.

> > > make_short_distance_dataframe -> OSMNX노드와 데이터 셋의 위치, 경도를 기준으로 직선거리중 가장 작은 노드를 추출합니다.

> > > 좌표 주위 데이터 필터링을 위한 클래스, 메소드

> > > (Class) Mapping -> 필터링에 필요한 메소드가 저장된 클래스입니다.

> > > filter_by_rectangle -> 사각형 범위 내 조건에 맞는 데이터 갯수를 추출합니다.

> > > filter_by_radius -> 사각형 범위내 데이터를 입력한 거리에 맞는 조건으로 필터링 합니다.

> > > show_rectangle -> 위 함수의 결과를 html파일로 시각화합니다.

> > > random_select_node -> 추출된 노드중 상위 50%내 노드를 9개 랜덤으로 추출합니다.

> > > 유전알고리즘 결과 시각화를 위한 함수

> > > find_nearest_node -> 추출된 노드와 가장 가까운 OSMNX노드를 찾아 반환합니다.

> > > running_route_distance -> 추출된 노드를 이어 완성된 경로의 거리를 반환합니다.

> > > make_running_route -> 추출된 노드를 이어 경로를 완성후 경로를 반환합니다.

> > > show_running_route -> 완성된 경로를 folium으로 시각화 합니다.

> > > 유전알고리즘 클래스, 메소드

> > > (Class) Point -> 방문할 노드의 위치를 생성하는 클래스입니다.

> > > (Class) Point_info -> 모든 지점의 정보를 저장하는 클래스입니다.

> > > (Class) Route -> 경로를 생성하는 클래스입니다. 초기화, 무작위 생성, 거리계산, 경로크기 계산를 지원합니다.

> > > getFitness -> 거리가 짧은수록 높은 점수를 주기위해 조정하는 메소드입니다.

> > > getDistance -> 생성된 경로의 길이를 계산하는 메소드입니다.

> > > (Class) GA -> 유전알고리즘 객체를 생성하는 클래스입니다.

> > > (Class) Population -> 최적의 값을 계산하며, 최적의 값과 최적의 경로를 탐색합니다.

> > > evolvePopulation -> 가장 좋은값(경로)와 랜덤으로 추출한 값(경로)를 비교해 높은 값을 반환(유전자)하는 메소드입니다.

> > > crossover (교배) -> 높은 적합도의 노드 유전자(노드)를 저장하며 빈 위치는 윗세대의 값을 저장하는 메소드입니다.

> > > mutate -> 입력된 두 값의 위치를 변경해 돌변변이를 생성하는 메소드입니다.

> ##### C.안전경로 모듈화 + 추천.zip
> > 데이터 전처리.ipynb는 OSMNX패키지 노드 추출과정과, cctv데이터, 보안등데이터를 전처리 및 concat하는 과정이 있으며 shp파일을 활용해 원하는 구역의 횡단보도 데이터를 추출하는 과정이 있습니다.
> > 안전경로 모듈화.ipynb는 A-star 알고리즘을 이용해 경로를 구성하였으며 파일의 진행순서는 데이터 셋 호출 -> 각 데이터 셋 전처리 -> 전처리 결과 얻은 위도, 경도 기준 OSMNX 노드 점수 부여 -> 출발지, 운동거리 입력 -> 출발지와 가장 가까운 노드 탐색 후 입력한 거리에 맞게 노드를 계속적으로 탐색 -> 입력한 거리의 오차범위내에 진입시 출발지와 마지막노드를 이어 탐색을 종료합니다.
> > 안전경로 모듈화.ipynb가 도착지가 설정되어 있는 경우에는 위와 같은 과정으로 진행하되 -> OSMNX 노드 dataframe의 위도, 경도 추출 -> 출발지와 도착지기준 가장 가까운 OSMNX노드 탐색 -> 출발지와 도착지를 사이의 위도, 경도를 기준으로 5x5 matrix를 생성후 각 요소들의 제일 낮은 값을 장애물로 지정후 maze 생성 -> A-star알고리즘을 따라 경로를 탐색 후 경로의 위도와 원본 OSMNX노드의 위도를 비교해 ID를 추출 후 노드를 이어 경로를 생성합니다.

> > ##### + 직접실행을 위한 함수 설명
> > > make_2d_list -> Series객체를 2차원 리스트 형태로 반환합니다.

> > > make_short_distance_dataframe -> OSMNX노드와 데이터 셋의 위치, 경도를 기준으로 직선거리중 가장 작은 노드를 추출합니다.

> > > find_next_node -> 현재 노드를 기준으로 550m내 제일 높은 점수의 노드를 탐색합니다.

> > > find_orig_id -> 원본 OSMNX노드 ID를 비교후 index를 반환합니다.

> > > make_route_distance -> 반환된 index를 넣어 경로의 길이를 계산하고, 경로를 완성합니다.

> > > make_auto_route -> 완성된 경로를 시각화하며 지나온 노드들의 위도, 경도를 시각화합니다.

> > > find_similar_node -> 출발지, 도착지와 가장 가까운 노드를 탐색하고 위치와 index를 반환합니다.

> > > make_maze -> 출발지와 도착지를 5x5matrix로 만든 후 각 요소별 제일 높은 점수의 노드를 반환 후 각 행에서 제일 점수가 작은 노드를 장애물로 설정합니다.

> > > heuristic -> Diagonal Distance기법을 이용해 현재 노드에서 도착지까지의 삼각거리를 계산합니다.

> > > aStar -> 현재 위치를 저장하며 다음 진행할 노드에서 가장 거리가 짧은 노드를 탐색합니다.

> > > astar_main -> maze, 시작점, 도착점을 설정하면 직접 경로를 생성합니다.

> > > find_orig_node_id -> 경로내 노드들의 원본 OSMNX ID를 반환합니다.

> > > find_destination -> 경로를 시각화하며 경로의 거리를 계산합니다.

> > 아이템 기반 협업필터링 추천.ipynb파일은 아이템 기반 인접이웃 협업필터링을 이용해 추천기능을 사용했습니다. 파일의 구성 순서는 데이터 셋 호출 -> 코스간 cosine 유사도를 계산 -> 코스간 유사도, 성별, 총 이용횟수를 기준으로 비슷한 러닝 성향의 유저를 추천 -> 원하는 추천 갯수 설정 후 MSE로 예측한 사용하지 않은 코스 추천의 순서입니다.
> > ##### + 직접실행을 위한 함수 설명
> > > predict_course -> 코스간 코사인 유사도 계산값을 내적후 평균내도록 계산후 반환

> > > get_mse -> Nan 값 제외 가중치를 부여 후 MSE계산

> > > predict_item_topsim -> 원하는 추천 갯수 설정 뒤 예측 값을 계산

> > > get_unused_route -> 유저가 이미 이용해본 길은 추천대상에서 제외하도록함.

> > > recommend_route_by_userid -> 유저별 이용하지 않은 길을 높은 값부터 추천

감사합니다.
