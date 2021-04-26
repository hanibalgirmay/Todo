<template>
    <div class="item">
        <input type="checkbox" @change="updateItem" v-model="item.completed" />
        <span :class="[item.completed ? 'completed' : 'itemText']">{{
            item.name
        }}</span>
        <button @click="removeItem" class="btn">Remove</button>
    </div>
</template>

<script>
export default {
    props: ["item"],
    methods: {
      updateItem(){
        try {
          axios.put('api/item/'+ this.item.id,{
            item:this.item
          }).then((res) => {
            if(res.status == 200){
              this.$emit('itemchanged')
            }
          }).catch(err => console.error(err))
        } catch (error) {
          console.error(error);
        }
      },
      removeItem(){
          try {
              axios.delete('api/item/'+ this.item.id)
                .then((res) => {
                    if(res.status == 200){
                        this.$emit('itemchanged')
                    }
                }).catch(err => console.error(err))
          } catch (error) {
              console.error(error)
          }
      }
    },
};
</script>

<style>
.completed {
    text-decoration: line-through;
    color: #999;
}
.itemText {
    width: 100%;
    margin-left: 20px;
}
.item {
    display: flex;
    justify-content: center;
    align-items: center;
}
.btn {
    background: #b83a3a;
    border: none;
    outline: none;
}
</style>
