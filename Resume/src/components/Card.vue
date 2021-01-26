<template>
    <div class="container">
        <p>
        <button class="btn primary" @click="Upload()">Загрузить комментарии</button>
        </p>
        <div class="loader" v-if="loading"></div>
        <div v-else-if="lists.length > 0" class="card">
            <h2>Комментарии</h2>
            <ul class="list">
                <li class="list-item"
                    v-for="list in lists"
                    :key="list.id"
                >
                    <div>
                        <p><strong>{{ list.email }}</strong></p>
                        <small>{{ list.body }}</small>
                    </div>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data: () => ({
        loading: false,
        lists: [],
        url: 'https://jsonplaceholder.typicode.com/comments?_limit=42',
    }),
    methods: {
        Upload() {
            this.loading = true;
            axios.get(this.url)
                .then((res) => {
                    this.loading = false;
                    console.log(res.data);
                    this.lists = res.data;
                })
        }
    },
}
</script>