<template>
    <div>
        <a-layout id="my-layout">
            <a-layout-sider class="first-sider-color" v-model="collapsed" :trigger="null" collapsible>
                <!-- <div class="logo" /> -->
                <a-layout-header class="first-sider-color" style=" padding: 0">
                    <a-icon class="trigger" :type="collapsed ? 'menu-unfold' : 'menu-fold'"
                        @click="() => (collapsed = !collapsed)" />
                </a-layout-header>

                <a-menu class="first-sider-color" theme="dark" mode="inline" :default-selected-keys="['2']">
                    <!-- <a-menu-item key="1" @click="ClickMenu(1)">
                        <a-icon type="team" />
                        <span>角色界面</span>
                    </a-menu-item> -->

                    <a-menu-item key="2" @click="ClickMenu(2)">
                        <a-icon type="area-chart" />
                        <span>快捷地图</span>
                    </a-menu-item>
                    <a-menu-item key="3" @click="ClickMenu(3)">
                        <a-icon type="search" />
                        <span>用户查询</span>
                    </a-menu-item>
                    <a-menu-item key="4" @click="ClickMenu(4)">
                        <a-icon type="eye" />
                        <span>圣遗物导出</span>
                    </a-menu-item>
                    <a-menu-item key="5" @click="ClickMenu(5)">
                        <a-icon type="calculator" />
                        <span>莫娜占卜铺</span>
                    </a-menu-item>
                    <a-menu-item key="6" @click="ClickMenu(6)">
                        <a-icon type="setting" />
                        <span>程序设置</span>
                    </a-menu-item>
                </a-menu>

                <a-button type="primary" icon="menu" id="pop-up-menu-button" size="large" @click="clickPopUpMenu"
                    />

                <transition name="slide-fade">
                    <div id="pop-up-menu-wrapper" v-show="ifPopUpMenu" >
                        <a-menu style="width: 180px" mode="vertical" @click="handlePopUpMenuClick" id="pop-up-menu">
                            <a-menu-item key="1">
                                <a-icon type="project" class="menu-icon" />
                                项目地址
                            </a-menu-item>

                            <a-sub-menu key="sub1" class="pop-up-sub-menu">
                                <span slot="title">
                                    <a-icon type="question-circle" class="menu-icon" /> 问题反馈</span>
                                <a-menu-item key="2">
                                    <a-icon type="github" />
                                    GitHub

                                </a-menu-item>
                                <a-menu-item key="3">
                                    <a-icon type="coffee" />
                                    NGA

                                </a-menu-item>
                            </a-sub-menu>


                            <a-menu-item key="4">
                                <a-icon type="close" class="menu-icon" />
                                退出程序

                            </a-menu-item>
                        </a-menu>
                    </div>
                </transition>
            </a-layout-sider>
            <a-layout>

                <a-layout-content id="second-content"
                    :style="{ margin: '0', padding: '0', background: '#fff', minHeight: '280px'}">
                    <router-view>Content</router-view>
                </a-layout-content>
            </a-layout>
        </a-layout>
    </div>

</template>
<script>
    const shell = require('electron').shell

    const {
        ipcRenderer
    } = window.require("electron");

    export default {
        data() {
            return {
                collapsed: true,
                ifPopUpMenu: false,
                clickedPopUpMenu: false

            };
        },
        mounted() {
            this.hidePopUpMenu()
        },
        methods: {
            ClickMenu(num) {
                switch (num) {
                    default:
                        break;
                    case 1:
                        // this.$router.push('/roleindex')
                        break;

                    case 2:
                        this.$router.push('/gamemap')
                        break;
                    case 3:
                        this.$router.push('/infoquery')
                        break;
                    case 4:
                        this.$router.push('/artifactsexport')
                        break
                    case 5:
                        this.$router.push('/calculation')
                        break;
                    case 6:
                        this.$router.push('/setting')
                }
            },
            clickPopUpMenu() {
                this.clickedPopUpMenu = true
                this.ifPopUpMenu = !this.ifPopUpMenu
            },
            handlePopUpMenuClick(e) {
                console.log('click ', e)
                if (e.key == 1) {
                    shell.openExternal('https://github.com/ChanIok/JumpyDumpty')
                } else if (e.key == 2) {
                    shell.openExternal('https://github.com/ChanIok/JumpyDumpty/issues')
                } else if (e.key == 3) {
                    shell.openExternal('https://bbs.nga.cn/read.php?tid=25647353')
                } else if (e.key == 4) {
                    ipcRenderer.send("exitProcess")
                }
                this.ifPopUpMenu = false
            },

            hidePopUpMenu() {
                document.addEventListener('click', (e) => {
                        let sp1 = document.getElementById("pop-up-menu-wrapper")
                        let sp2 = document.getElementById("pop-up-menu-button")
                        if (sp2) {
                            if (!sp2.contains(event.target)&&!sp1.contains(event.target)) {
                                this.ifPopUpMenu = false;
                            }
                        }


                        })
                }
            }
        };
</script>
<style scoped>
    .first-sider-color {
        background-color: #ce3c3c;
    }

    #my-layout {
        height: 100%;
        position: relative;
    }

    #my-layout .trigger {
        font-size: 18px;
        line-height: 64px;
        padding: 0 24px;
        cursor: pointer;
        transition: color 0.3s;
        color: #ffe0e0;
    }

    #my-layout .trigger:hover {
        color: #ffefef;
    }

    #my-layout .logo {
        height: 32px;
        background: rgba(255, 255, 255, 0.2);
        margin: 16px;
    }

    #pop-up-menu-button {
        /* width: 100%; */
        background-color: #ce3c3c;
        border: 0;
        position: absolute;
        left: calc(50% - 20px);
        bottom: 20px;
    }

    #pop-up-menu-wrapper {
        left: calc(50% + 40px);
        position: absolute;
        bottom: 20px;
        box-shadow: 0 4px 12px rgba(0, 0, 0, .15);
        z-index: 996;
    }

    #pop-up-menu span {
        z-index: 997;
    }

    .slide-fade-enter-active {
        transition: all .15s ease;
    }

    .slide-fade-leave-active {
        transition: all .15s cubic-bezier(1.0, 0.5, 0.8, 1.0);
    }

    .slide-fade-enter,
    .slide-fade-leave-to {
        opacity: 0;
    }

    .menu-icon {
        margin-right: 10px !important;
    }
</style>
<style>
    .pop-up-sub-menu .ant-menu-submenu-arrow {
        display: inline-block !important;
    }
</style>