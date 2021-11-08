<template>

    <nav>
        <v-app-bar color="teal darken-1" dark app> <!-- 상단바 설정. dark app 사용하면 흰색글씨 나오고 안쓰면 검정글씨 나옴 -->
            <v-app-bar-nav-icon @click.stop="drawer =!drawer">

            </v-app-bar-nav-icon>
            <v-toolbar-title class="text-uppercase"> <!-- toolbar 부분 class 로 잡아서 대문자로 나오게 표시 -->
                <span class="font-weight-light">mapduck_</span> <!-- mapduck 부분은 진하게 표시 x , home 글자만 굵게 표현 -->
                <span>home</span>
            </v-toolbar-title>
            <v-spacer></v-spacer>

            <v-menu offset-y>
                <template v-slot:activator="{on}">
                    <v-btn text v-on="on">
                        <v-icon left>expand_more</v-icon>
                        <span>Menu</span>
                    </v-btn>

                </template>
                <v-list flat>
                    <v-list-item v-for="link in links" :key="link.text" router :to="link.route" active-class="border"> 
                        <!-- 상단 메뉴 생성 border 통해서 메뉴 선택시 색깔 나오게 함-->
                        <!-- to : 대상 route 객체로 이동, from : 현재 라우트로 오기전 라우트. 라우트에 대한 설명은 notion 참고-->
                        <v-list-item-title>{{link.text}}</v-list-item-title>
                    </v-list-item>
                </v-list>
            </v-menu>

            <v-btn text>
                <span>Login</span>
            </v-btn>
        

            <v-btn text>
                <span>Exit</span>
                <v-icon right>exit_to_app</v-icon>
            </v-btn>
        </v-app-bar>

        <v-navigation-drawer v-model="drawer" dark app class="teal lighten-2"> <!-- 왼쪽 메뉴 -->
            <v-layout column align-center>
                <v-flex class="mt-5">
                    <v-avater size="100">
                    </v-avater>
                    <p class="white--text subheading mt-1 text-center">Username</p> <!-- 왼쪽메뉴 맨 위에 username 표시.. 로그인 할때 이름 떴으면 좋겠음-->
                </v-flex>

                <v-flex class="mt-4 mb-4">
                    <Popup/>>
                    
                </v-flex>

                <v-flex class="mt-4 mb-4">
                    <Home/>>
                    
                </v-flex>

                
            </v-layout>

            <v-list flat>
                <v-list-item v-for="link in links" :key="link.text" router :to="link.route" active-class="border">

                    <v-list-item-action>
                        <v-icon>{{link.icon}}</v-icon>
                    </v-list-item-action>

                    <v-list-item-content>
                        <v-list-item-title>{{link.text}}</v-list-item-title>
                    </v-list-item-content>

                </v-list-item>
            </v-list>
        </v-navigation-drawer>
    </nav>
 
</template>

<script>
import Popup from './Popup.vue' // 내가 사용하고자 하는 js 문서를 import 하기
import Home from './Home.vue'

export default {
    data:() =>({
        
        drawer: true,
        links: [
            {icon: 'dashboard', text:'Dashboard', route:'/'},
            {icon: 'folder', text:'My Project', route:'/project'},
            {icon: 'person', text:'Team', route:'/team'},
            {icon: 'lock', text:'Home', route:'/home'}
        ]
    }),
    components :{
        Popup,
        Home
    }
}
</script>


<style>
.border{
    border-left: 4px solid #006064
}
</style>

