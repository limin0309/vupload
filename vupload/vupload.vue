<!--// vupload 组件 基于swiper 组件制作查看大图，可滑动查看全图 解决 前端图片压缩，图片颠倒问题， 图片压缩: { 宽高压缩： 以手机屏幕宽度为值，等比例压缩高度 质量宽度： canvas 压缩质量参数压缩 }

// 引入上传组件 import { upload, uploadList, uploadFile } from 'vupload'

export default { components: { upload, uploadList, uploadFile } }-->

### 上传组件使用方法
<template>
    <div class="ins-btn">
        <upload class="base remark-img" :list="option.ScaleImg">
            <upload-list
                    :data="option.ScaleImg"
                    class="list"
            />
            <upload-file :defaults="option" class="uploader"/>
        </upload>
    </div>
</template>

<script>
    export default {
        data () {
            return {
                option: {
                    ScaleImg: {
                        imgList: [],//已上传图片队列
                        imgCache: [],//缩略图队列
                        hide: true,//(ture) 点击查看大图
                        pos: 0,//当前查看大图下标
                        onDel: index => {
                            console.log(index)
                        } //删除图片回调（返回删除图片的数组下标）
                    },//查看大图参数

                    server: '/',//上传服务器地址

                    multiple: true, //是否允许多张（默认为true）

                    max: 5,//最多允许上传图片个数

                    quality: 0.5,//压缩图片质量

                    start: canvas => {
                        this.option.ScaleImg.imgCache.push(canvas)
                    }, //图片上传前回调(返回一个canvas)

                    success: jsons => {
                        this.option.ScaleImg.imgList.push(jsons.content.downloadUrl)
                    }, //图片上传成功回调（返回接口参数）

                    error: (e) => {
                        console.log(e)
                    }, //图片上传失败回调（图片上传个数超过最大值报错处理）

                    progress: num => {
                        console.log(e)
                    }//图片上传进度条回调（返回一个进度比值，该事件移动支持度不高，可忽略）
                }
            }
        }
    }
</script>
<style>
    @function turnToRem($px) {
    @return 64px * $px / 75px / 32px * 1rem;
    }


    .ins-btn {
        position: relative;
        min-height: turnToRem(45px);
        overflow: hidden;
    }

    .uploader {
        float: left;
        width: turnToRem(200px);
        height: turnToRem(200px);
    }


    .list {
    .item {
        float: left;
        width: turnToRem(198px);
        height: turnToRem(198px);
        border: 1px solid #ddd;
        margin-right: 2%;
        position: relative;
        margin-bottom: 2%;
        overflow: hidden;
    img {
        width: 100%;
        height: 100%;
    }
    .loadImg {
        width: 100%;
        height: 100%;
        position: absolute;
        opacity: .7;
        background: #eee;
        top: 0;
        left: 0;
        display: flex;
        align-items: center;
    .loading {
        margin: 0 auto;
        width: turnToRem(66px);
        height: turnToRem(6px);
        background:url('../../components/vupload/assets/loading.gif');
        background-size: turnToRem(66px) auto;
    }
    }
    .del {
        position: absolute;
        top: 0;
        right: 0;
        width: turnToRem(40px);
        height: turnToRem(40px);
        background: url('../../components/vupload/assets/del.png');
        background-size: turnToRem(40px) auto
    }
    }
    }
</style>