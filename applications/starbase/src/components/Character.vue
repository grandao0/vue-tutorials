<template>
<div class="col-md-4">
    <div class="character-card" @click="switchCharacter">
        <div class="card-block">
            <h4 class="card-title">{{character.name}}</h4>
            <p class="card-text">Heigth: {{character.heigth}}</p>
            <p class="card-text">Mass: {{character.mass}}</p>
            <p class="card-text">Hair Color: {{character.hair_color}}</p>
            <p class="card-text">Eye Color: {{character.eye_color}}</p>
        </div>
    </div>
    <br>
    <button class="btn btn-primary" @click="revertCharacter">Revert</button>
</div>
</template>

<script>
export default {
    props: ['id'],
    data () {
        return {
            character: {
            },
            last: null
        }
    },
    created() {
        this.fetchCharacter(this.id);
    },
    methods: {
        fetchCharacter (id) {
            fetch(`https://swapi.co/api/people/${id}`, {
                method: 'GET'
            }).then(response => response.json())
            .then(json => this.character = json);
        },
        switchCharacter () {
            this.last = this.id;
            let randomId = Math.floor(Math.random() * 83)  + 1;
            this.fetchCharacter(randomId);
        },
        revertCharacter () {
            this.fetchCharacter(this.last);
        }
    }
}
</script>
