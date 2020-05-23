<template>
    <div class="mydiv">
        <div style="height: 40%;">
            <v-row>
                <v-col v-for="(bien, index) in mesBiens" :key="index" col="4">
                   <v-btn small color="primary" name="index" @click="goToPostion(13,bien.coord)">{{ bien.type }}</v-btn> 
                </v-col>
            </v-row>
    
            <p>Center: {{ mapCenter }}</p>
            <p>Zoom: {{ mapZoom }}</p>
            <p>Bounds: {{ mapBounds }}</p>
        </div>

        <l-map ref="macarte"
            :zoom="mapZoom"
            :center="mapCenter"
            :options="mapOptions"
            :zoomAnimation=true
            class="mapstyle"
            @update:center="centerUpdated"
            @update:zoom="zoomUpdated"
            @update:bounds="boundsUpdated"
        >
            <l-tile-layer
                :url="url"
                :attribution="attribution"
            />
            <l-marker v-for="(bien, i) in mesBiens" :key="i"
                :lat-lng="getPosition(bien.coord)"
                :options="{riseOnHover:true}"
                @mouseover="changeColor(true)" @mouseout="changeColor(false)">
                <l-popup>
                        popup exemple {{ bien.type }}
                </l-popup>
                <l-icon
                    :icon-anchor="staticAnchor"
                    :popupAnchor="[0,-20]"
                    >
                    <v-icon x-large :class="markerIconClass">mdi-map-marker-radius-outline</v-icon>
                </l-icon>
                <l-tooltip :options="{direction:'bottom'}">{{ bien.type }}</l-tooltip>
            </l-marker>

            <l-circle v-if="circle.show"
                :lat-lng="circle.center"
                :radius="circle.radius"
                :color="circle.color"
            />
        

        </l-map>

    </div>  
  
</template>

<script>
import { latLng } from "leaflet";
import { LMap, LTileLayer, LMarker, LPopup, LCircle, LIcon, LTooltip } from 'vue2-leaflet';


import { Icon } from 'leaflet';

delete Icon.Default.prototype._getIconUrl;
Icon.Default.mergeOptions({
  iconRetinaUrl: require('leaflet/dist/images/marker-icon-2x.png'),
  iconUrl: require('leaflet/dist/images/marker-icon.png'),
  shadowUrl: require('leaflet/dist/images/marker-shadow.png'),
});

export default {
    name : 'CarteSimple',
    components: {
        LMap,
        LTileLayer,
        LMarker,
        LPopup,
        LCircle,
        LIcon,
        LTooltip,
    },
    data: () => ({
        mapZoom: 13,
        mapCenter: latLng(48.85735, 2.44082),
        mapBounds : null,
        url: 'https://{s}.tile.openstreetmap.fr/osmfr/{z}/{x}/{y}.png',
        attribution: '&copy, <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
        withPopup: latLng(48.85735, 2.44082),
        currentZooom: 13,
        currentCenter: latLng(48.85735, 2.44082),
        showDetail: false,
        mapOptions: {
            zoomSnap: 0.5
        },
        message: " toto ",
        markerIconClass: " red--text",
        
        mesBiens : [
            {"type":"vente maison", "coord":[48.85735, 2.44082]},
            {"type":"location appretement", "coord":[48.88111, 2.393217]},
            {"type":"Gestion coop d'un immeuble", "coord":[46.14485, 6.089922]}
        ],
        circle: {
            show: false,
            center: latLng(48.85735, 2.44082),
            radius: 120,
            color: 'red'
        },
        staticAnchor: [19, 34],
    }),
    methods: {
        zoomUpdated (zoom) {
            this.mapZoom = zoom;
        },
        centerUpdated (center) {
            this.mapCenter = center;
        },
        boundsUpdated (bounds) {
            this.mapBounds = bounds;
        },
        showAllDetail() {
            this.showDetail = !this.showDetail;
        },
        goToPostion(zoom, position) {          
            this.mapZoom = zoom;
            this.mapCenter = latLng(position); 
            /* // circle
            this.circle.show = true
            this.circle.center = latLng(position); */
        },
        getPosition(point) {
            return latLng(point);
        },
        showMarkers() {

        },
        changeColor(changeIt) {
            changeIt?this.markerIconClass = "green--text":this.markerIconClass = "red--text";
        }   
    },


}
</script>

<style>
    .mapstyle {
        height: 60%;
        width: 100%;
        position: absolute;
    }
    .mydiv {
        height: 400px;
        width: 100%;
        border: 2px solid #336699;
        position: absolute;
    }
    .someExtraClass {
        background-color: aqua;
        padding: 10px;
        border: 1px solid #333;
        border-radius: 0 20px 20px 20px;
        box-shadow: 5px 3px 10px rgba(0, 0, 0, 0.2);
        text-align: center;
        width: auto !important;
        height: auto !important;
        margin: 0 !important;
    }
</style>