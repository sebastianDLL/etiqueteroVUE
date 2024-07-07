<script >
export default{
    emits:["onTagsChange"],
    data(){
        return{
            CurretValue: "",
            tags: []  
        };
    },

    methods:{
        handleKeydown(e){
            if(e.key === "Backspace" && this.CurretValue === "") {
                this.tags.pop();
                //this.onTagsChange(this.tags);
                this.$emit("onTagsChange", this.tags);
            }
        },
        handleSubmit(){
            if(this.CurretValue !== ""){
                const exist = this.tags.some((item) => item === this.CurretValue);
                if(!exist){
                    this.tags.push(this.CurretValue);
                    this.CurretValue = "";
                    //this.onTagsChange(this.tags);
                    this.$emit("onTagsChange", this.tags);
                }else{
                    alert("Tag already exists");
                }
            }
        },
        deleteTag(tag){
            this.tags = this.tags.filter((item) => item !== tag);
            //this.onTagsChange(this.tags);
            this.$emit("onTagsChange", this.tags);
        }
    }
};
</script>

<template>
    <div class="inputTag">
        <h1>Esto es un etiquetero</h1>
        <div class="tags">
            <div class="tag" v-for="(tag,index) in tags" :key="index">
                {{tag}} <button @click="deleteTag(tag)">X</button>
            </div>
        </div>
        <form @submit.prevent="handleSubmit">
            <input class="input" type="text" v-model="CurretValue" @keydown="handleKeydown" />
        </form>
    </div>
</template>

<style scoped>
.inputTag {
    display: inline-flex;
    border: 1px solid #0000;
    border-radius: 3px;
    height: 43px;
}

.tags{
    display: flex;
    flex-wrap: wrap;
    gap: 3px;
    padding: 5px;
}

.tags .tag{
    display: flex;
    gap: 3px;
    padding: 5px;
    border:solid 1px #ccc;
    align-content: center;
    border-radius: 3px;
}

.inputTag form{
    display: inline-flex;
}

.inputTag .input{
    border: none;
    outline: none;
    padding: 0 5px;
}

.tag button{
    border: none;
    background-color: transparent;
    border-radius: 3px;
    cursor: pointer;
}

.tag button:hover{
    background-color: #ccc;
}
</style>
