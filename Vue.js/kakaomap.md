# 카카오맵 이용해서 마커 찍기   
> 건물명을 이용하여 그 위치 찍기
```javascript
initMap() {
            const vue = this;
            var mapContainer = document.getElementById('map'), // 지도를 표시할 div 
        
            mapOption = {
                center: new kakao.maps.LatLng(33.450701, 126.570667), // 지도의 중심좌표
                level: 3 // 지도의 확대 레벨
            };  

            // 지도를 생성합니다    
            var map = new kakao.maps.Map(mapContainer, mapOption); 

            // 주소-좌표 변환 객체를 생성합니다
            let ps = new kakao.maps.services.Places();
            ps.keywordSearch(vue.exhibit.location, (data)=>{
                console.log(data);

                for(let arr of data){
                    if(arr.category_group_name==="문화시설"){
                        var coords = new kakao.maps.LatLng(Number(arr.y), Number(arr.x));

                        var marker = new kakao.maps.Marker({
                            map: map, // 마커를 표시할 지도
                            position: new kakao.maps.LatLng(Number(arr.y), Number(arr.x)), // 마커를 표시할 위치
                            title : vue.exhibit.location, // 마커의 타이틀, 마커에 마우스를 올리면 타이틀이 표시됩니다
                            // image : markerImage // 마커 이미지 
                        });
                        break;
                    }
                }
                map.setCenter(coords);
            });
        }
```   
