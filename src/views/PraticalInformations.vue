import VueSimpleAccordion from 'vue-simple-accordion';


<template>

  <div class="PraticalInformations">
    <div class="container-fluid">
    <h1>Informations pratiques et FAQ</h1>
    
    <h2 class="titlefind">Venir</h2>

  <p class="adress">Le festival est situé Parc du Port-Mulon à Nort-sur-Erdre (44 390) en Loire-Atlantique à environ 25 km au nord de Nantes.</p>

  <div class="maps">
    <div>
      <span v-if="loading">Loading...</span>
      <!-- <label for="checkbox">GeoJSON Visibility</label>
      <input
        id="checkbox"
        v-model="show"
        type="checkbox"
      >
      <label for="checkboxTooltip">Enable tooltip</label>
      <input
        id="checkboxTooltip"
        v-model="enableTooltip"
        type="checkbox"
      >
      <input
        v-model="fillColor"
        type="color"
      > -->
      <br>
    </div>
    <l-map
      :zoom="zoom"
      :center="center"
      style="height: 200px; width: 70%; margin:15%"
    >
      <l-tile-layer
        :url="url"
        :attribution="attribution"
      />
      <l-geo-json
        v-if="show"
        :geojson="geojson"
        :options="options"
        :options-style="styleFunction"
      />
      <l-marker :lat-lng="marker" />
    </l-map>
  </div>

<div class="faq">
  <h2 class="titlefaq">FAQ</h2>
<div class="PraticalInformationsArcordion">
        <div :key="index" v-for="(item,index) in questions" role="tablist">
            <b-card no-body class="mb-1">
            <b-card-header header-tag="header" class="p-1" role="tab">
                <b-button block href="#" v-b-toggle="'accordion-' + index" variant="info">{{item.title}}</b-button>
            </b-card-header>
            <b-collapse :id="'accordion-' + index" accordion="my-accordion" role="tabpanel">
                <b-card-body>
                <b-card-text>{{ item.content }}</b-card-text>
                </b-card-body>
            </b-collapse>
            </b-card>
        </div>  
    </div>
</div>

  </div>
  </div>
</template>

<style lang="scss">
.PraticalInformations{
padding-bottom: 15%;
.btn-info{
   background-color: var(--yellow)!important ; 
   border-color: var(--yellow)!important;
   font-weight: 700;
   color:black;
}

.btn-info:hover {
  background-color: var(--blue)!important ; 
   border-color: var(--blue)!important;
   font-weight: 700;
   color:black;
}
.adress{
  text-align: justify;
  margin-left:1.5em;
  margin-right:1.5em;
}

.PraticalInformationsArcordion{
margin-top: 8.5vh;
}

.card{
  height: auto;
}

h2.titlefind{
  text-align: left;
  margin-top: 1.5em;
  margin-left:1.5em;
}

p.adress{
  display: flex;
  float: left;
}

.maps l-map{
  margin-left: 20%;
}

h2.titlefaq{
  text-align: left;
  margin-top: 1.5em;
  margin-left:1.5em;
}

.PraticalInformationsArcordion{
    margin-left:1.5em;
    margin-right:1.5em;
    background: none;
}

.card-header {
background-color: none!important;
border: none!important;
}
.card{
  border: none;
}



} 
</style>




<script>
import { latLng } from "leaflet";
import { LMap, LTileLayer, LMarker, LGeoJson } from "vue2-leaflet";

export default {
  name: "Pratical",
  components: {
    LMap,
    LTileLayer,
    LGeoJson,
    LMarker


  },
  data() {
    return {
      loading: false,
      show: false,
      enableTooltip: true,
      zoom: 5,
      center: [48, -1.219482],
      geojson: null,
      fillColor: "#e4ce7f",
      url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
      attribution:
        '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
      marker: latLng(47.20638734052255, -1.5393574567593957),
    
      questions:[
                {
                    title: 'Comment devenir Bénévole ?',
                    content: 'Le festival m’intéresse, je souhaite y postuler. Il n’y a aucun poste à pourvoir pour le moment (stages compris). Les inscriptions bénévoles sont actuellement fermées. Vous souhaitez proposer votre offre de restauration pour le festival ? Toute la restauration du festival est assurée par les équipes bénévoles. Nous ne recherchons pas de prestataires ou de foodtrucks.'
                },
                {
                    title: 'Comment me faire rembourser ?',
                    content: 'Si vous avez acheté plusieurs billets, il vous faut faire une demande par billet. Les frais de location (montant s’ajoutant au coût des billets) restent au bénéfice du prestataire de billetterie, comme lors de l’achat du billet. Par exemple, sur un billet journalier à 41 € (42,05 € si on ajoute les frais de location), le remboursement sera de 41 €.'
                },    
                {
                    title: 'Stand Prévention',
                    content: 'Pour limiter et sensibiliser sur les comportements liés à l’excès d’alcool, à la consommation de drogues ou les risques auditifs, un stand de prévention est accessible à tous. Des bénévoles dispensent informations et conseils auprès du public. Des bouchons d’oreille, casques, préservatifs, éthylotests et autres sont à disposition durant le festival.'
                },      
                {
                    title: 'Que faire en cas de vol ou de perte ?',
                    content: 'Les objets de valeur ? Nous vous conseillons vivement de laisser vos objets de valeur (bijoux, portefeuilles, appareils photos ect.) à votre domicile. Dans la foule, vous risquez de les perdre. Ne prenez avec vous que le strict nécessaire. J’ai perdu un objet durant le festival, à qui puis-je m’adresser pour le récupérer ? Après la fin de chaque soirée, une équipe de bénévoles ratisse le terrain afin de récupérer tous les objets perdus. Ils sont rassemblés au point infos. Après le festival, rendez-vous à la Mairie de Nort-sur-Erdre pour récupérer les objets trouvés.'
                },
                  {
                    title: 'Comment accéder ou festival ?',
                    content: 'Le festival est situé Parc du Port-Mulon à Nort-sur-Erdre (44 390) en Loire-Atlantique à environ 25 km au nord de Nantes.'
                },
                
            ]

  }
  },

  computed: {
    options() {
      return {
        onEachFeature: this.onEachFeatureFunction
      };
    },
    styleFunction() {
      const fillColor = this.fillColor; // important! need touch fillColor in computed for re-calculate when change fillColor
      return () => {
        return {
          weight: 2,
          color: "#ECEFF1",
          opacity: 1,
          fillColor: fillColor,
          fillOpacity: 1
        };
      };
    },
    onEachFeatureFunction() {
      if (!this.enableTooltip) {
        return () => {};
      }
      return (feature, layer) => {
        layer.bindTooltip(
          "<div>code:" +
            feature.properties.code +
            "</div><div>nom: " +
            feature.properties.nom +
            "</div>",
          { permanent: false, sticky: true }
        );
      };
    }
  },
  async created() {
    this.loading = true;
    const response = await fetch("https://rawgit.com/gregoiredavid/france-geojson/master/regions/pays-de-la-loire/communes-pays-de-la-loire.geojson")
    const data = await response.json();
    this.geojson = data;
    this.loading = false;
  }


};



</script>