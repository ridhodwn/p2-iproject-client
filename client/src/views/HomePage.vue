<script>
import { mapActions, mapWritableState } from 'pinia';
import { useCounterStore } from '../stores/counter';
import SongCard from "../components/SongCard.vue";
export default {
    components: {
        SongCard
    },
    methods: {
        ...mapActions(useCounterStore, ["getParams", "fetchNewReleases", "fetchUser"]),
    },
    computed: {
        ...mapWritableState(useCounterStore, ['songs'])
    },
    created() {
        if(!localStorage.getItem("access_token")) {
            this.getParams();
            this.fetchUser();
        }
        this.fetchNewReleases();
    }
}
</script>
    
<template>
    <section class="col-md-9 ms-sm-auto col-lg-10 px-md-4">
        <div class="row">

            <div class="col-12">
                <h2 class="mb-3 mt-4"><b>NEW RELEASES</b></h2>
                <div class="row row-cols-1 row-cols-md-5 g-2 d-flex col-12 ms-1 me-3">
                    <SongCard v-for="song in songs" :key="songs.id" :song="song" />
                </div>
            </div>

        </div>
    </section>
</template>