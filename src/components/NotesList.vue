@<template>
  <div class="notes">
        <div class="note" :class="{full: !grid}" v-for="(note,index) in notes" :key="index">
            <div class="note-header" :class="{full: !grid}">
                <p> {{note.title}} </p>
                <p style="cursor: pointer; color: grey" @click="removeNote(index)">x</p>
            </div>
            <div class="note-body">
                <p> {{note.descrip}} </p>
                <p> {{note.date}} </p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        notes: {
            type: Array,
            requierd: true
        },
        grid: {
            type: Boolean,
            requierd: true
        }
    },
    methods: {
        removeNote(index){
            this.notes.splice(index, 1)
            console.log(`Note id ${index} - removed`);
        }
    }
}
</script>

<style lang="scss">
    .notes{
        display: flex;
        align-items: center;
        justify-content: space-between;
        flex-wrap: wrap;
        // padding: 40px 0;
  }

    .note{
        width: 48%;
        padding: 18px 20px;
        margin-bottom: 20px;
        background: #ffffff;
        box-shadow: 0 30px 30px rgba(0,0,0,.2);
        transition: all .25s cubic-bezier(.02,.01,.47,1);
        &:hover{
            box-shadow: 0 30px 30px rgba(0,0,0,.4);
            transform: translate(0,-6px);
            transition-delay: 0s !important;
        }
        &.full{
            width: 100%;
            text-align: center;
        }
  }

  .note-header{
    display: flex;
    align-items: center;
    justify-content: space-between;
    h1{
        font-size: 32px;
    }
    p{
        font-size: 20px;
        color: #402caf;
    }
    svg{
        color: #999999;
        margin-right: 12px;
        &.active{
            color: #402caf;
        }
        &:last-child{
        margin-right: 0;    
        }
    }
    &.full{
        justify-content: center;
        p {
            margin-right: 16px;
            &:last-child {
                margin-right: 0;
            }
        }
    }
  }

  .note-body{
    p {
        margin: 20px 0;
    }

    span{
        font-size: 14px;
        color: #999999;
    }
  }
</style>