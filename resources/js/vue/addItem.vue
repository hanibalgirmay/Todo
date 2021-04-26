<template>
    <div class="addItem">
        <input type="text" v-model="item.name" />
        <button
            @click="addItem"
            class="btn"
            :class="[item.name ? 'active' : 'inactive']"
        >
            Save
        </button>
    </div>
</template>

<script>
export default {
    data() {
        return {
            item: {
                name: ""
            }
        };
    },
    methods: {
        addItem() {
            if (this.item.name !== "") {
                axios
                    .post("api/item/store", {
                        item: this.item
                    })
                    .then(res => {
                        if (res.status == 201) {
                            this.item.name = "";
                            this.$emit('reloadlist')
                        }
                        // alert("New Item added");
                    })
                    .catch(err => console.error(err));
            } else {
                return;
            }
        }
    }
};
</script>

<style>
.addItem {
    display: flex;
    justify-content: center;
    align-items: center;
}
input {
    background: #ffffff;
    border: 2px;
    outline: none;
    padding: 5px;
    margin-right: 10px;
}
.active {
    color: #00c26e;
}
.inactive {
    color: #999999;
}
</style>
