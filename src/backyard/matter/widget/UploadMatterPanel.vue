<template>
  <div class="upload-matter-panel">
    <NbExpanding>
      <div class="huge-block clearfix"
           v-if="matter.loading">
        <div class="media">
          <div class="pull-right">
            <i class="btn-action f16 fa fa-trash text-danger" v-if="false" @click.stop.prevent="del()"></i>
          </div>
          <div class="media-body">{{matter.file.name}}</div>
        </div>
        <div class="progress" :class="{'progress-striped active' : matter.loading}">
          <div :style="'width: '+(matter.progress*100)+'%'" class="progress-bar progress-bar-primary">
            <span>已上传 {{(matter.progress * 100).toFixed(1)}}%</span>
          </div>
        </div>
        <div>
          已上传:{{ (matter.file.size * matter.progress).toFixed(0) | humanFileSize }}/{{ matter.file.size |
          humanFileSize}}
          速度:{{matter.speed | humanFileSize}}/s

        </div>
      </div>
    </NbExpanding>

  </div>
</template>
<script>
  import Matter from '../../../common/model/matter/Matter'
  import NbExpanding from "../../../common/widget/NbExpanding"
  import Vue from "vue"
  import $ from "jquery"
  import Director from "./Director";
  import {Message, MessageBox, Notification} from 'element-ui'
  import {setInputSelection} from "../../../common/util/Utils";

  export default {
    data() {
      return {}
    },
    components: {

      NbExpanding
    },
    props: {
      matter: {
        type: Matter,
        required: true
      }
    },
    methods: {
      del() {
        let that = this
        that.matter.clear()
      }
    },
    created() {
    },
    mounted() {

    }
  }

</script>
<style lang="less" rel="stylesheet/less">
  .upload-matter-panel {

    .huge-block {
      background-color: white;
      border-radius: 5px;
      padding: 10px;
      border: 1px solid #eeeeee;
      margin-bottom: 10px;

      .progress {
        margin-bottom: 10px;
      }

      .media {
        margin-bottom: 5px;
        .media-body {
          cursor: pointer;
          color: #555;
          font-size: 15px;
          font-weight: bold;
          white-space: nowrap;
          text-overflow: ellipsis;
        }
      }

    }

  }
</style>
