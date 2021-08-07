# Vue.js Kakao 지도 API 사용







![image-20210806041634988](C:\Users\multicampus\AppData\Roaming\Typora\typora-user-images\image-20210806041634988.png)

```javascript
<script>
export default {
  data() {
    return{
      form: {
        title: '',
        name: '',
        Type: null,
        checked: [],
        num:Number,
        date: Date,
        time: TimeRanges
      },
      Types: [{ text: 'Select One', value: null }, 'Game', 'Study', 'Travel', 'Restaurant'],
      show: true,
      promiseTime:Date,
      lat:Number,
      lon:Number,
      // "kakao": false
    }
  },
  mounted() {
    if (window.kakao && window.kakao.maps) {
      this.initMap();
    } else {
      const script = document.createElement('script')
      script.onload = () => kakao.maps.load(this.initMap)
      script.src =
        `http://dapi.kakao.com/v2/maps/sdk.js?autoload=false&appkey=${process.env.VUE_APP_MAP_API}&libraries=services,clusterer`
      document.head.appendChild(script)
    }
    console.log(`${process.env.VUE_APP_MAP_API}`)
  },
  methods: {
    initMap() {
      var mapContainer = document.getElementById('map'), // 지도를 표시할 div
          mapOption = {
            center: new kakao.maps.LatLng(37.564343, 126.947613), // 지도의 중심좌표
            level: 3, // 지도의 확대 레벨
          }
      var map = new kakao.maps.Map(mapContainer, mapOption)
      var marker = new kakao.maps.Marker({ 
          // 지도 중심좌표에 마커를 생성합니다 
          position: map.getCenter() 
      });
      var geocoder = new kakao.maps.services.Geocoder();
      // 주소-좌표 변환 객체를 생성합니다

      marker.setMap(map); // 지도에 마커를 표시합니다
      kakao.maps.event.addListener(map, 'click', function(mouseEvent) {
        // 클릭한 위도, 경도 정보를 가져옵니다 
        var latlng = mouseEvent.latLng;
        marker.setPosition(latlng);
        marker.setMap(map);

        var message = '클릭한 위치의 위도는 ' + latlng.getLat() + ' 이고, ';
        message += '경도는 ' + latlng.getLng() + ' 입니다';
        console.log(message)

        geocoder.coord2Address(latlng.getLng(), latlng.getLat(), function(result, status) {
          if (status === kakao.maps.services.Status.OK) {
            var detailAddr = result[0].address.address_name;
            console.log(detailAddr)
          }   
        });
      });
    },
  },
}
</script>
```



힘들게 했는데... 바꿔야 된다.....ㅠ



검색도 하면 나죽어