<script>
import { actions } from '../store';

export default {
    vuex: {
        actions: actions
    },
    data () {
        return {
            content: ''
        };
    },
    methods: {
        onKeyup (e) {
            e = e || window.event;
            let keyCode = e.keyCode || e.which || e.charCode;
            let ctrlKey = e.ctrlKey || e.metaKey;
            if (ctrlKey && keyCode === 13) {
                this.content += '\n';
            } else if (keyCode === 13 && this.content.length) {
                e.preventDefault();
                this.sendMessage(this.content);
                this.content = '';
            }
        },
        sendMsg:function () {
            let chatTa = document.getElementById('chatTa');
            this.sendMessage(chatTa.value);
            chatTa.value = '';
        }
    }
};
</script>

<template>
    <div class="text">
        <textarea id="chatTa" placeholder="按 Enter 发送" v-model="content" @keyup="onKeyup"></textarea>
        <div class="action">
            <span class="info">按 Ctrl + Enter 换行</span>
            <a href="javascript:;" @click="sendMsg">发送</a>
        </div>
    </div>
</template>

<style lang="less" scoped>
    .text {
        height: 160px;
        border-top: solid 1px #ddd;
        textarea {
            padding: 10px;
            height: 120px;
            width: 100%;
            border: none;
            outline: none;
            font-family: "Micrsofot Yahei";
            resize: none;
        }
        .action {
            height: 40px;
            margin-top: -5px;
            background: #fff;
            text-align: right;
            padding-right: 15px;
            .info {
                color: #c3c3c3;
                font-size: 12px;
                margin-left: 10px;
                margin-right: 7px;
            }
            a {
                text-decoration: none;
                color: #4d4d4d;
                background: #fff;
                display: inline-block;
                border: 1px solid #c1c1c1;
                border-radius: 4px;
                -moz-border-radius: 4px;
                -webkit-border-radius: 4px;
                padding: 3px 30px;
                font-size: 14px;
            }
        }
    }
</style>