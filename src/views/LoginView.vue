<template>

   

    <div class="container">
        <div class="loginForm">
            <img src="@/assets/CCF.jpg" class="rounded mx-auto d-block" alt="Bootstrap" width="300" height="300">
        <form @submit.prevent="login()">
            <div class="mb-3">
                <label for="exampleInputEmail1" class="form-label">Username</label>
                <input type="text" class="form-control" v-model="credential.username" aria-describedby="emailHelp">
            </div>
            <div class="mb-3">
                <label for="exampleInputPassword1" class="form-label">Password</label>
                <input type="password" class="form-control" v-model="credential.password">
            </div>

            <div class="d-flex justify-content-center">
                <button type="submit" class="pink baseButton">Login<font-awesome-icon icon="fa-solid fa-right-to-bracket " bounce/></button>
            </div>

        </form>
    </div>
    </div>

</template>
  
<script>
import { ref } from "vue";
import jwt_decode from "jwt-decode";

export default {
    name: 'LoginView',
    components: {
    },
    setup() {
        const credential = ref({});

        const login = async function () {

            var response = await fetch("/api/user/login", {
                method: "post",
                headers: {
                    "content-type": "application/json"
                },
                body: JSON.stringify(credential.value)
            });

            if (response.ok) {
                var data = await response.json()
                localStorage.setItem("user", data.token);

                var decoded = jwt_decode(data.token);
                alert(JSON.stringify(decoded))
                // alert(JSON.stringify(data))
                alert("login Successfully.")
                location.assign("/")
            } else {
                alert(response.statusText)
            }
            
        }

        return {
            credential, login
        }
    }
}
</script>

<style scoped>
#app {
    font-family: Arial, Helvetica, sans-serif;
    color: #2c3e50;
}

.baseButton{
    padding: 6px;
    border: none;
    border-radius: 4px;
}

.pink {
background-color: palevioletred;
color: white;
/* border: 1px solid gray; */
}

.container{
    border-radius: 100%;
    display: flex;
  flex-direction: column;
  background-image: url("@/assets/BG2.jpg");
  background-size: 100% 100%;
  background-attachment: fixed;
 
  width: 100%;
  height: 100%;
  min-width: 900px;
  min-height: 1000px;
 
  justify-content: center;
  align-items: center;

}

.loginForm {
    border-radius: 80%;
  background-color: #fff;
  min-width: 800px;
  box-shadow: rgba(0, 0, 0, 0.1) 0px 15px 30px;
  padding: 30px 20px;
}

input{
    margin-left: 270px;
    width: fit-content;
    border: 1px solid gray;
    border-radius: 4px;
}
label{
    margin-left: 330px;
    width: fit-content;

}
</style>