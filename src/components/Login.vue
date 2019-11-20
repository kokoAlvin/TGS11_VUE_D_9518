<template>
    <v-app>
        <v-content>
            <v-container class="fill-height" fluid>
                <v-row align="center" justify="center">
                    <v-col cols="8" md="8">
                        <v-card>
                            <v-row>
                                <v-col cols="6">
                                    <div class="header">
                                        <div id="title"> Login Tugas 11 Kelas D</div>
                                        <div id="tagline">
                                            Vinson Alvindi (170709518)
                                        </div>
                                    </div>
                                    <div class="form">
                                        <v-text-field v-model="form.email" label="Email" outlined height=50>

                                        </v-text-field>

                                        <v-text-field v-model="form.password" label="Password" type="password" outlined height=50>

                                        </v-text-field>
                                    <v-btn @click="loginUser()" rounded block class="elevation-0" color="primary" height=50 dark>Masuk </v-btn>
                                    </div>
                                </v-col>
                            </v-row>
                        </v-card>
                    </v-col>
                </v-row>
            </v-container>
        </v-content>
    </v-app>
</template>

<script>
export default {
    data () {
        return {
            checkbox: false,
            form : {
                email : null,
                password : null,
            },

            user: new FormData,
        }
    },
    methods :
    {
        loginUser(){
            var url = this.$apiUrl + '/auth'
            this.user = new FormData()
            this.user.append('email', this.form.email)
            this.user.append('password', this.form.password)
            this.$http.post(url,this.user).then(response =>{
                if(response.data.token)
                {
                    localStorage.setItem("token", response.data.token)
                    this.$router.push({name : 'UserController'})
                }
                else
                {
                    alert('Anda gagal masuk, harap coba kembali...')
                }
            })
        }
    },
}
</script>

<style>
    .header
    {
        margin-left: 30px;
        margin-top: 30px;
    }

    .form{
        margin-top: 35px;
        margin-left: 35px;
        margin-bottom: 35px;
        margin-right: 20px;
    }

    #title
    {
        font-family: 'Courier New', Courier, monospace;
        font-style: normal;
        font-weight: bold;
        font-size: 30px;
        line-height: 50px;
    }
    #tagline
    {
        font-family: 'Times New Roman', Times, serif;
        font-style: normal;
        font-weight: bold;
        font-size: 15px;
        line-height: 50px;
    }

</style>