---
title: 'Tinymce demo'
date: 2021-01-27 13:43:36
tags: [editor]
published: true
hideInList: false
feature: 
isTop: false
---
```js
<template>
  <div class="editor">
    <TinymceEditor id="editor-tinymce" ref="ZEditor" v-model="myValue" :init="completeSetting" :disabled="disabled" />
  </div>
</template>

<script>
import tinymce from 'tinymce/tinymce'
import TinymceEditor from '@tinymce/tinymce-vue'
// 样式
// import 'tinymce/skins/content/default/content.min.css'
// import 'tinymce/skins/ui/oxide/skin.min.css'
// import 'tinymce/skins/ui/oxide/content.min.css'

// 主题
import 'tinymce/themes/silver/theme'
import 'tinymce/icons/default/icons'

import 'tinymce/plugins/advlist'
import 'tinymce/plugins/anchor'
import 'tinymce/plugins/autolink'
import 'tinymce/plugins/autosave'
import 'tinymce/plugins/autoresize'

import 'tinymce/plugins/charmap'
import 'tinymce/plugins/code'
import 'tinymce/plugins/codesample'
import 'tinymce/plugins/colorpicker'
import 'tinymce/plugins/contextmenu'
import 'tinymce/plugins/directionality'
import 'tinymce/plugins/emoticons'
import 'tinymce/plugins/fullscreen' // 全屏插件
import 'tinymce/plugins/help'
import 'tinymce/plugins/hr'

import 'tinymce/plugins/image' // 图片插件
import 'tinymce/plugins/imagetools'
import 'tinymce/plugins/insertdatetime'

import 'tinymce/plugins/link' // 链接插件
import 'tinymce/plugins/lists'
import 'tinymce/plugins/media' // 媒体插件
import 'tinymce/plugins/noneditable'
import 'tinymce/plugins/nonbreaking'
import 'tinymce/plugins/quickbars' // 快速栏插件

import 'tinymce/plugins/table' // 表格插件
import 'tinymce/plugins/template'
import 'tinymce/plugins/textcolor'
import 'tinymce/plugins/textpattern'
import 'tinymce/plugins/wordcount'
import 'tinymce/plugins/searchreplace'

import 'tinymce/plugins/pagebreak'
import 'tinymce/plugins/paste'
import 'tinymce/plugins/preview'
import 'tinymce/plugins/print'
import 'tinymce/plugins/visualblocks'
import 'tinymce/plugins/visualchars'

import 'tinymce/plugins/importword'
import 'tinymce/plugins/indent2em'
import 'tinymce/plugins/formatpainter'

export default {
  name: 'ZEditor',
  components: {
    TinymceEditor
  },
  props: {
    value: {
      type: String,
      default: ''
    },
    setting: {
      type: Object,
      default: () => {}
    },
    disabled: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      defaultSetting: {
        language_url: '/admin_jzm/tinymce/langs/zh_CN.js',
        language: 'zh_CN',
        // theme: 'silver',
        // theme_url: '/admin_jzm/tinymce/mytheme.js',
        // skin: 'oxide',
        skin_url: 'http://127.0.0.1:8001/admin_jzm/tinymce/skins/ui/oxide',
        // skin_url: '/admin_jzm/tinymce/skins/ui/oxide',
        min_height: 250,
        max_height: 600,
        selector: 'textarea',
        plugins:
          'print preview searchreplace autolink directionality visualblocks visualchars fullscreen image link media template code codesample table charmap hr pagebreak nonbreaking anchor insertdatetime advlist lists wordcount imagetools textpattern help noneditable autosave indent2em autoresize formatpainter importword quickbars paste',

        toolbar: `code undo redo restoredraft | cut copy paste pastetext | forecolor backcolor bold italic underline strikethrough link anchor | alignleft aligncenter alignright alignjustify outdent indent | \
        styleselect formatselect fontselect fontsizeselect | bullist numlist | blockquote subscript superscript removeformat | \
        table image media charmap hr pagebreak insertdatetime print preview | codesample fullscreen | indent2em lineheight formatpainter importword restoredraft`,
        toolbar_sticky: false, // 粘性工具栏
        quickbars_insert_toolbar: '', // quickimage quicktable
        quickbars_selection_toolbar:
          'removeformat | bold italic underline strikethrough | fontsizeselect forecolor backcolor',
        branding: false, // 隐藏右下角技术支持
        menubar: true, // 隐藏最上方menu
        statusbar: false, // 隐藏编辑器底部的状态栏
        convert_urls: false,
        toolbar_mode: 'wrap', // sliding & wrap
        // 字号
        // fontsize_formats: '12px 14px 16px 18px 24px 36px 48px 56px 72px',
        // 字体
        font_formats:
          '微软雅黑=Microsoft YaHei,Helvetica Neue,PingFang SC,sans-serif;苹果苹方=PingFang SC,Microsoft YaHei,sans-serif;宋体=simsun,serif;仿宋体=FangSong,serif;黑体=SimHei,sans-serif;Arial=arial,helvetica,sans-serif;Arial Black=arial black,avant garde;Book Antiqua=book antiqua,palatino;',
        link_list: [{ title: '预置链接1', value: 'http://www.baidu.com' }],
        image_list: [{ title: '预置图片1', value: 'https://www.baidu.com/img/bd_logo1.png' }],
        // importcss_append: true, // 配合插件 importcss
        // content_security_policy: "script-src *;", //内容安全策略
        // extended_valid_elements: 'script[src]', // 扩展有效元素
        // 为内容模板插件提供预置模板
        templates: [
          {
            title: '模板文档',
            description: '介绍文字',
            content:
              '<div class="mceTmpl"><span class="cdate">CDATE</span>，<span class="mdate">MDATE</span>，我的内容</div>'
          }
        ],
        insertdatetime_formats: ['%Y年%m月%d日', '%H点%M分%S秒', '%Y-%m-%d', '%H:%M:%S'],
        paste_data_images: true, // 配合插件 paste 允许粘贴图像
        autosave_ask_before_unload: true, // 当关闭或跳转URL时，弹出提示框提醒用户仍未保存变更内容。默认开启提示。
        // images_upload_base_path: '/', // 给返回的相对路径指定它所相对的基本路径。
        images_upload_handler: (blobInfo, success, failFun) => {
          const img = 'data:image/jpeg;base64,' + blobInfo.base64()
          success(img)
        }
      },
      myValue: this.value
    }
  },
  computed: {
    completeSetting () {
      return Object.assign(this.defaultSetting, this.setting)
    }
  },
  watch: {
    myValue (newValue) {
      this.$emit('input', newValue)
    },
    value (newValue) {
      this.myValue = newValue
    }
  },
  mounted () {
    // tinymce.init({})
  },
  beforeDestroy () {
    tinymce.get('editor-tinymce').destroy()
  }
}
</script>

<style lang="less" scoped>
::v-deep .tox-tinymce {
  border: 1px solid #dcdfe6;
  border-radius: 4px;
}
</style>
```