<template>
  <div class="cm_main2">
    <div class="cm_main cm_pr">
      <m-title :title="title"></m-title>
      <div class="cm_pc_12 cm_mt3 cm_mb8">
              <ul class="cm_pc_12">
              	<li class="cm_pc_12 cm_prl05 cm_lh105 cm_ti2 cm_mtb05">
              	   <span class="">{{indexData.desc}}</span>
                  </li>
              	<li class="cm_pc_12 cm_prl05 cm_tc cm_mb05">
              		<div class="cm_pc_6 cm_hl2" :class="{'cm_c1b cm_cf':dnid==k,'cm_be':dnid!=k}" @click="tsDnid(k)" v-for="(v,k) in indexData.dnarr" v-bind:key="k">{{v.name}}</div>
              	</li>
                  <li class="cm_pc_12 cm_mb05" v-for="(v2,k2) in indexData.dnarr" v-bind:key="k2">
  		                <img class="cm_h17 cm_bs100 cm_fc" :src="v2.img" v-if="dnid==k2"/>
                  </li>
                  <li class="cm_pc_12 cm_prl05 cm_lh1 cm_ti2 cm_mb05">
                   <span class="cm_fs08 cm_c1c">{{indexData.about}}</span>
                  </li>
              </ul>
          </div>
      <m-footer></m-footer>
    </div>
  </div>
</template>
<script>
import mTitle from 'components/aiplat/header1';
import mFooter from 'components/aiplat/footer1';
export default {
  data() {
    return {
      title: window.thisPage.title,
      indexData: {
        desc:'非常感谢各位对ai智能空间的无偿捐赠,ai智能空间将会持续开发更多更好的应用。',
        about:'特别说明:以下收款二维码仅在全球唯一网站aiplat.com有效,对于全球其他地方或网站出现的均是假冒的。',
        dnid: window.store.getters.getDnid,
        dnarr: [
          {
            name: '微信收款',
            img: require('assets/images/aiplat/index/donateWX.png')
          },
          {
            name: '支付宝收款',
            img: require('assets/images/aiplat/index/donateZFB.png')
          }
        ]
      }
    };
  },
  methods: {
    tsDnid: function(id) {
      window.store.dispatch('tsone',id);
    }
  },
  computed: {
      dnid() {
          return window.store.getters.getDnid
      }
  },
  mounted() {
    window.store.dispatch('pushToBaidu');
    window.cm.setWXH();
  },
  components: { mTitle, mFooter },
  activated: function() {
    window.cm.sli2(0, 1);
  },
  deactivated: function() {}
};
</script>