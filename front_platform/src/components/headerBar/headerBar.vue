<template>
    <div class="headerBar">
        <div class="layout">
            <!-- <div class="logo"><h1 @click="$router.push({name: 'home'})">MEIZU</h1></div> -->
            <div class="logo"><img @click="$router.push({name: 'home'})" src="@/static/image/logo.jpg" alt="" ></div>
             <div class="zhuce">
              <Button type="primary"  @click="$router.push({name:'regist'})">立即注册</Button>
            </div>
            <div class="person">
              <span><Icon  type="md-person"/>
                <h2 v-if="hasLogin == undefined"  @click="$router.push({name:'login'})">登录</h2>
                <h2 v-else @click="logout">退出</h2>
              </span>
              <!-- <span  class="carIcon" @click="goToCart">
                <Badge :count="1" type="error" :offset="[20,-3]">
                  <Icon type="md-cart" />
                </Badge>
              </span> -->
            </div>
          
            <div class="nav">
               <Menu mode="horizontal" :theme="'light'" :active-name="$route.name">
                    <MenuItem name="phoneList" :to="{name:'phoneList'}" >
                        <Icon type="ios-paper" />
                        手机
                    </MenuItem>
                    <MenuItem name="headsetList" :to="{name:'headsetList'}">
                        <Icon type="ios-stats" />
                        声学
                    </MenuItem>
                    <MenuItem name="partList" :to="{name:'partList'}">
                        <Icon type="ios-people" />
                        配件
                    </MenuItem>
                    <MenuItem name="lifeRoundList" :to="{name:'lifeRoundList'}">
                        <Icon type="ios-people" />
                        生活周边
                    </MenuItem>
                    <MenuItem name="5">
                        <Icon type="ios-people" />
                        Flyme
                    </MenuItem>
                    <MenuItem name="6">
                        <Icon type="ios-people" />
                        服务
                    </MenuItem>
                    <MenuItem name="7">
                        <Icon type="ios-people" />
                        专卖店
                    </MenuItem>
                </Menu>
            </div>
        </div>
    </div>
</template>
<script>
import {loginOut } from "@/api/user"; 
export default {
    name:'headerBar',
    data(){
      return{
        hasLogin:'',
      }
    },
    mounted(){
      this.hasLogin = localStorage.getItem('userId')
    },
    methods:{
      goToCart(){
        this.$router.push({name:"cart"})
      },
      async logout(){
        const res = await loginOut()  
        if(res.status == 0){
          localStorage.clear()
          this.$router.push({name:'login'})
        }
      }
    }
}
</script>
<style lang="scss" scoped>
.headerBar{
    width: 100%;
    background: #fff;
    position:fixed;
    border-bottom: 1px solid #eee;
    z-index: 999;
    .layout{
        overflow: hidden;
        width: 1240px;
        margin: 0 auto;
        .logo{
          height: 60px;
          float: left;
          line-height: 60px;
          img{
            height: 40px;
            margin-top: 15%;
            display: block;
            &:hover{
            transition: all 0.8s linear;
            cursor: pointer;
            }
          }
          h1{
            font-size: 40px;
            letter-spacing: 1px;
            color:#2d8cf0;
            &:hover{
              color:#333;
              transition: all 0.8s linear;
              cursor: pointer;
            }
          }
        }
        .person{
          float: right;
          height: 60px;
          font-size: 24px;
          line-height: 60px;
          width: 85px;
          .carIcon:hover{
            color: #2d8cf0;
            cursor: pointer;
          }
          h2{
            display: inline-block;
            font-size: 14px;
            color:#333;
            margin-right:30px;
            &:hover{
              cursor: pointer;
              color: #2d8cf0;
            }
          }
        }
        .zhuce{
          float: right;
          height: 60px;
          font-size: 24px;
          line-height: 60px;
          width: 120px;
        }
        .nav{
          margin-left: 10%;
          float: left;
          height: 60px; 
        }
    }
}
</style>

