<template>
    <template v-if="entry">
        <div class="entry-title d-flex justify-content-between p-2">
            <div>
                <span class="text-success fs-3 fw-bold">{{ day }}</span>
                <span class="text-success fs-3 fw-bold">{{ month }}</span>
                <span class="text-success fs-4 fw-light">{{ year }}</span>
            </div>

            <div>
                <button class="btn btn-danger mx-2">
                    borrar
                    <i class="fa fa-trash-alt"></i>
                </button>
                <button class="btn btn-primary">
                    Subir foto
                    <i class="fa fa-upload"></i>
                </button>
            </div>

        </div>

        <hr>
        <div class="d-flex flex-column px-3 h-75">
            <textarea placeholder="¿Que sucedió hoy?" v-model="entry.text"></textarea>
        </div>

        <img 
            src="https://images.pexels.com/photos/1619317/pexels-photo-1619317.jpeg?auto=compress&cs=tinysrgb&dpr=1&w=500"
            alt="Entry Picture"
            class="img-thumbnail" >
    </template>
        <Fab icon="fa-save"/>
</template>

<script>
import { defineAsyncComponent } from 'vue'
import { mapGetters } from 'vuex';
import getDayMonthYear from "../helpers/getDayMonthYear";

export default {
    props: {
        id: {
            type: String,
            required: true,
        }
    },
    components: {
        Fab: defineAsyncComponent(() => import('../components/Fab.vue'))
    },
    data() {
        return {
            entry: null,
        }
    },
    methods: {
        loadEntry() {
            const entry = this.getEntriesById( this.id)
            if ( !entry ) return  this.$router.push({ name: 'no-entry' })
            
            this.entry = entry
        }
    },
    computed: {
        ...mapGetters('journal', ['getEntriesById']),
        day() {
            const { day } = getDayMonthYear( this.entry.date )
            return day
        },
        month() {
            const { month } = getDayMonthYear( this.entry.date )
            return month
        },
        year() {
            const { year } = getDayMonthYear( this.entry.date )
            return year
        },
    },
    watch: {
        id() {
            this.loadEntry()
        }
    },
    created() {
        this.loadEntry()
    },
}
</script>

<style lang="scss" scoped>

textarea {
    font-size: 20px;
    border: none;
    height: 100%;

    &:focus {
        outline: none;
    }
}

img {
    width: 200px;
    position: fixed;
    bottom: 150px;
    right: 20px;
    box-shadow: 0px 5px 10px rgba($color: #000000, $alpha: 0.2);
}

</style>