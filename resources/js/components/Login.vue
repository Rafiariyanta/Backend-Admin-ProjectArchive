<template>
    <div>
        <div class="form-group">
            <label for="exampleInputEmail1">Username</label>
            <input type="email" class="form-control" v-model="user.username" id="exampleInputEmail1" aria-describedby="emailHelp">
        </div>
        <div class="form-group">
            <label for="exampleInputPassword1">Password</label>
            <input type="password" class="form-control" v-model="user.password" id="exampleInputPassword1">
        </div>
        <button type="submit" @click="login" class="btn btn-primary">Submit</button>
    </div>   
</template>

<script>
export default {
    data: () => ({
        user: {
            username: '',
            password: '',
        }
    }),
    methods: {
        login(){
            console.log(this.user);
            this.$store.dispatch('currentUser/loginUser', this.user)        
        }
    },
}
</script>