<template>
    <div>
        <form @submit.prevent="saveData">
            <div :class="errors.has('name') ? 'is-danger' : 'is-success'">
                <input type="text" placeholder="Nome" name="name" v-model="userData.name" v-validate="'required|min:3|max:10'">
                <p v-if="errors.has('name')">{{ errors.first('name') }}</p>
            </div>
            <hr>
            <!-- <div :class="{'is-danger' : errors.has('email')}"> -->
            <div :class="errors.has('email') ? 'is-danger' : 'is-success'">
                <input type="text" placeholder="E-mail" name="email" v-model="userData.email" v-validate="'required|email'">
                <p v-if="errors.has('email')">{{ errors.first('email') }}</p>
            </div>
            
            <hr>
            <input type="number" placeholder="Idade" v-model.number="userData.age">
            {{userData.age}}
            <hr>
            <input type="radio" name="sex" value="M" v-model="userData.sex">Masculino
            <input type="radio" name="sex" value="F" v-model="userData.sex">Femenino
            <p v-if="userData.sex ">{{userData.sex}}</p>
            <hr>
            <select v-model="userData.state">
                <option value="">Selecione o Estado</option>
                <option value="SP">São Paulo</option>
                <option value="RJ">Rio de Janeiro</option>
                <option value="MG">Minas Gerais</option>
            </select>
            <p v-if="userData.state">{{ userData.state }}</p>
            <hr>
            <label for="agree">Concordo com os termos de uso</label>
            <input type="checkbox" id="agree" v-model="terms">
            <hr>
            <textarea cols="30" rows="10" v-model="description"></textarea>
            <pre>{{ description }}</pre>
            <hr>
            <button type="submit">Enviar</button>
        </form>

        <div v-if="isSubmited">
            {{ userData }}
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            userData: {
                name:'',
                email: '',
                age: '',
                sex: '',
                state: ''
            },
            terms: true,
            description: '',
            isSubmited: false
        }
    },
    methods: {
        saveData () {
            this.$validator.validateAll().then((result) => {
                if (result) {
                    this.isSubmited = true
                    return;
                }

                
            });
        }
    }
}
</script>

<style scoped>
.is-danger {
    border: 1px solid red;
    color: red;
}

.is-success {
    border: 1px solid green;
    color: green;
}
</style>
