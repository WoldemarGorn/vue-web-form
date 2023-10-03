<template>
    <form @submit.prevent="handleSubmit">
        <label>Email :</label>
        <input type="email" required v-model="email">

        <label>Password :</label>
        <input type="password" required v-model="password">
        <div v-if="passwordError" class="error">{{ passwordError }}</div>

        <label>Role :</label>
        <select v-model="role">
            <option value="developer">Web developer</option>
            <option value="designer">Web designer</option>
        </select>

        <label>Skills :</label>
        <input type="text" v-model="tempSkill" @keyup="addSkill">

        <div v-for="skill in skills" :key="skill" class="pill">
            <span @click="deleteSkill(skill)">{{ skill }}</span>
        </div>

        <div class="terms">
            <input type="checkbox" v-model="terms" required>
            <label>Accept terms</label>
        </div>

        <div class="submit">
            <button>Accept data</button>
        </div>
    </form>
</template>


<script>
export default {
    data() {
        return {
            email: '',
            password: '',
            role: 'developer',
            terms: false,
            tempSkill: '',
            skills: [],
            passwordError: ''
        }
    },
    methods: {
        addSkill(e) {
            if (e.key === ',' || e.key === 'Enter' && this.tempSkill) {
                if (!this.skills.includes(this.tempSkill)) {
                    this.skills.push(this.tempSkill.replace(',', ''))
                }
                this.tempSkill = ''
            }
        },
        deleteSkill(skill) {
            this.skills = this.skills.filter((item) => {
                return skill !== item
            })
        },
        handleSubmit() {
            this.passwordError = this.password.length > 5 ? '' : 'Password musst be > 5 chars'
            if (!this.passwordError) {
                console.log('form submit')
            }
        }
    }
}
</script>

<style>
form {
    max-width: 400px;
    margin: 20px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}

label {
    color: grey;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.8em;
    font-weight: bold;
}

input,
select {
    display: block;
    padding: 10px 5px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
}

input[type="checkbox"] {
    display: inline-block;
    max-width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
}

.pill {
    display: inline-block;
    margin: 20px 10px 0 0;
    padding: 6px 12px;
    background: #eee;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    cursor: pointer;
}

button {
    background: green;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;

}

.submit {
    text-align: center;
}

.error {
    color: red;
    font-size: 0.8em;
    font-weight: bold;
    margin-top: 10px;
}
</style>