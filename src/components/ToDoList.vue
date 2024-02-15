<script >   
import {setTimeout} from 'timers';
export default {
    data :() => {
        return {
            entry:"",
            entryFavorite: false,
            todoList:[],
            completedToDoList:[],
            showCompletedList:false,
 }
    },

    methods : {
        addEntry() {
            if(this.entry != "")
            {
                let date = new Date;
                let newEntry = {
                    id : date.fetTime(),
                    title: this.entry,
                    favorite: this.entryFavorite,
                    complete: false,
                    show:false,
                }

                if(newEntry.favorite) {
                    this.todoList.push(newEntry);
                }

                setTimeout(() => {
                    this.todoList.find(element => element.id === newEntry.id).show = true; 
                    },10);
                }

                this.entry = "";
                this.entryfavorite = false;
            },
            setFavoriteItem(item) {
                item.favorite = !item.favorite;
                item.show = false;

                setTimeout(() => {
                    let index = this.todoList.findIndex(element => element.id === item.id);
                    this.todoList.splice(0, 0, item );
                    item.show = true;
                }, 500);
            },
            uncompleteItem(item) {
                item.complete = !item.complete;
                item.show = false;

                setTimeout(() => {
                    if(item.favorite) {
                        this.todoList.splice(0, 0, item);
                    }
                    else {
                        this.todoList.push(item);
                    }
                    let index = this.completedToDoList.findIndex(element => element.id === item.id);
                        this.completedToDoList.slice(index, 1);
                    item.show = true;
                }, 500);
                        
                    }
                }
            }
        

                    
                </script>





<template>
  <div class ="container">
    <div class ="add-item">
      <div class ="add-icon">
        <i class ="fas fa-plus"></i>
  </div>
  <form action ="">
    <input 
    type ="text" 
    placeholder ="Add To-Do...">
  </form>

  <div class ="feature-icon">
    <i class ="far fa-star"></i>
  </div>
  </div>
  </div>
  
</template>


<style lang="scss" scoped>
.container {
  padding :10px;
  widht:calc(100% - 20px);
  min-height: calc(100% - 20px);

  .add-item {
    display:grid;
    grid-template-columns: 70px auto 70px;
    grid-template-rows: 60px;
    width: 100%;
    height: 60px;
    background: rgba($color: #000000, $alpha: .3, );
    border-radius: 5px;
    overflow: hidden;


    .add.icon {
        grid-column-start: 1;
        grid-column-end: 1;
        display: flex;
        justify-content: center;
        align-items: center;
        color: #fff;
        cursor: pointer;



        input {
            grid-column-start: 2;
            grid-column-end: 2;
            background: none;
            width: 100%;
            height: 60px;
            color: #fff;
            font-size: 1.6rem;

            &:focus {
                outline: none;
              }
            }

            .feature-icon {
                @include feature-icon(#fff);
            }
        }
    }
    .todo-list {
        padding-top: 20px;


        .item{
            display: grid;
            grid-template-columns: 70px auto 70px;
            grid-template-rows: 60px;
            width: 100%;
            height: 60px;
            margin-bottom: 2px;
            background: rgba($color: #000000, $alpha: .8);
            border-radius: 5px;
            overflow: hidden;
            opacity: 0;
            transition: all .5s linear;

            .item-checkbox {
          grid-column-start: 1;
          grid-column-end: 1;
          display: flex;
          justify-content: center;
          align-items: center;
          font-size: 1.6rem;
          color: #99C191;
          cursor: pointer;
        }

        .item-title {
          grid-column-start: 2;
          grid-column-end: 2;
          display: flex;
          justify-content: flex-start;
          align-items: center;
          font-size: 1.6rem;
        }
        .feature-icon {
          @include feature-icon(#333);
        }
      }

      .show {
        opacity: 1;
      }
    }
    complete-list {
      .item {
        position: relative;
        background: rgba($color: #fff, $alpha: .4);

        &::before {
          content: '';
          position: absolute;
          top: 30px;
          width: calc(100% - 120px);
          margin: 0 60px;
          border-bottom: 2px solid #555;
        }
      }
    }

    .show-completed {
      display: flex;
      justify-content: center;
      align-items: center;
      padding-top: 20px;

      .button {
        color: #fff;
        padding: 10px;
        font-size: 1.3rem;
        text-transform: uppercase;
        background: rgba($color: #000000, $alpha: .3);
        border-radius: 5px;
        overflow: hidden;
        cursor: pointer;
      }
    }

    .red-bg {
      background-color: #C23741;
      color: #fff !important;
    };
  }
</style>