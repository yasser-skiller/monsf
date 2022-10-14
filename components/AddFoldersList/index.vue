<template>
  <div>

    <div id="list1" class="dropdown-check-list  cursor_pointer bgfillGreen border_Green_2 px-3 py-2 mt-5 font-16" tabindex="100">
      <span class="anchor ">
        <img :src="require(`~/assets/icon/file0.svg`)" class="icon ml-2" alt="icon"/>
        <span class="text_green"> اضف السؤال لمجلد</span>
      </span>
      <ul class="items FoldersListCheckbox mt-2"  v-for="list in Folders" :key="list.index">
        <div class="d-flex justify-content-between">
          <li class="d-flex" v-on:click="AddQuestion(Quiz_data[Quiz_serial],list)">
            <input type="checkbox" :class="list.name" :id="list.name"/>
            <label :for="list.name" class="mx-2">{{list.name}}</label>
          </li>

          <div>
            <span
              class="cursor_pointer text-danger font-weight-bold"
              v-on:click="RemaoveFolder(list)"
            >x
            </span>
            <span
              class="cursor_pointer font-weight-bold"
              v-on:click="EditFolderListCheckboxItem = list; EditeListName = list.title"
              v-b-modal.modal-EditList
            >
            <img :src="require(`~/assets/icon/edit.png`)" class="icon mr-2" alt="icon"/>
            </span>
          </div>
        </div>

      </ul>
    </div>

    <b-modal id="modal-EditList" title="تعديل اسم المجلد" hide-footer>
      <b-form-input v-model="EditeListName" class="my-4" placeholder="اكتب اسم المجلد"></b-form-input>
      <b-button size="sm" class="btn btn_Green my-2 py-2 px-r px-l rounded_0" type="button"  v-on:click="EditFolderListCheckbox(EditFolderListCheckboxItem)"> تعديل</b-button>
    </b-modal>

    <img
      :src="require(`~/assets/icon/plus.png`)"
      class="icon mr-3 cursor_pointer"
      alt="icon"
      v-b-modal.modal-addList
    />

    <b-modal id="modal-addList" title="إضافة مجلد جديد" hide-footer>
      <b-form-input v-model="ListName" class="my-4" placeholder="اكتب اسم المجلد"></b-form-input>
      <b-button size="sm" class="btn btn_Green my-2 py-2 px-r px-l rounded_0" type="button"  v-on:click="AddFolders"> إنشاء</b-button>
    </b-modal>
  </div>
</template>

<script>
import config from "@/config";

export default {
  props : ["Quiz_data","Quiz_serial"],
  data (){
    return {
      ListName: '',
      EditeListName:'',
      FoldersList:[{title: 'default', content: []}],
      Folders:[],
      EditFolderListCheckboxItem: '',
    }
  },
  mounted() {
    setTimeout(() => {
      this.GetWatcher();
      this.Drop();
      this.fetchFolders();
    }, 1000);
  },
  methods: {
    GetWatcher(){
      console.log("Quiz_data ....",this.Quiz_data[this.Quiz_serial].id)
      var myHeaders = new Headers();
      myHeaders.append("Authorization", `Bearer${config.token}`);
      myHeaders.append("Content-Type", "application/json");
      // myHeaders.append("Cookie", "__wpdm_client=f5ddc77fd332e35ab25f445937d36c7c; _learn_press_session_079eddece82f2d2937cd2c203a8195b0=77e4246fa580e1b1de925170f59b9887%7C%7C1665855786%7C%7Ca35f3656287cbaac2c9668ecdd670d92");

      var raw = JSON.stringify({
        "question_id": 17480
      });

      var requestOptions = {
        method: 'GET',
        headers: myHeaders,
        body: raw,
        redirect: 'follow'
      };
      fetch(config.apiUrl+"wp-json/learnpress/v1/folders/question", requestOptions)
        .then(response => response.text())
        .then(result => {
          console.log("ddd.....",JSON.parse(result))
        })
        .catch(error => console.log('error', error));
    },
    Drop(){
      var checkList = document.getElementById('list1');
      checkList.getElementsByClassName('anchor')[0].onclick = function(evt) {
        checkList.classList.toggle('visible');
      }
    },
    RemaoveFolder(list){
      var myHeaders = new Headers();
      myHeaders.append("Authorization", `Bearer${config.token}`);

      var requestOptions = {
        method: 'DELETE',
        headers: myHeaders,
        redirect: 'follow'
      };

      fetch(config.apiUrl+`wp-json/learnpress/v1/folders/${parseInt(list.id)}`, requestOptions)
        .then(response => response.text())
        .then(result =>{
          console.log("RemaoveFolder",JSON.parse(result))
          this.fetchFolders()
        })
        .catch(error => console.log('error', error));
    },
    EditFolderListCheckbox(item){
      console.log("EditFolderListCheckbox",item,this.EditeListName)
      var myHeaders = new Headers();
      myHeaders.append("Authorization", `Bearer${config.token}`);
      myHeaders.append("Content-Type", "application/json");
      myHeaders.append("Cookie", "__wpdm_client=f5ddc77fd332e35ab25f445937d36c7c; _learn_press_session_079eddece82f2d2937cd2c203a8195b0=77e4246fa580e1b1de925170f59b9887%7C%7C1665855786%7C%7Ca35f3656287cbaac2c9668ecdd670d92");

      var raw = JSON.stringify({
        "name": this.EditeListName
      });

      var requestOptions = {
        method: 'PUT',
        headers: myHeaders,
        body: raw,
        redirect: 'follow'
      };

      fetch(`${config.apiUrl}wp-json/learnpress/v1/folders/${item.id}`, requestOptions)
        .then(response => response.text())
        .then(result => {
          this.fetchFolders();
        })
        .catch(error => console.log('error', error));
    },
    fetchFolders(){
      var myHeaders = new Headers();
      myHeaders.append("Authorization", `Bearer${config.token}`);
      myHeaders.append("Cookie", "__wpdm_client=9a6d88491b5c975242839b1e203e9118");


      var requestOptions = {
        method: 'GET',
        headers: myHeaders,
        redirect: 'follow'
      };

      fetch(config.apiUrl+"wp-json/learnpress/v1/folders/", requestOptions)
        .then(response => response.text())
        .then(result =>{
          this.Folders = JSON.parse(result)
        })
        .catch(error => console.log('error f', error));
    },
    AddFolders(){
      if(this.ListName !== ''){
        var myHeaders = new Headers();
        myHeaders.append("Authorization", `Bearer${config.token}`);
        myHeaders.append("Content-Type", "application/json");
        myHeaders.append("Cookie", "__wpdm_client=9a6d88491b5c975242839b1e203e9118");

        var raw = JSON.stringify({
          "name": this.ListName
        });

        var requestOptions = {
          method: 'POST',
          headers: myHeaders,
          body: raw,
          redirect: 'follow'
        };

        fetch(config.apiUrl+"wp-json/learnpress/v1/folders/", requestOptions)
          .then(response => response.text())
          .then(result => {
            this.fetchFolders()
          })
          .catch(error => console.log('error', error));
      }
    },
    AddQuestion(question,folder){
      var myHeaders = new Headers();
      myHeaders.append("Authorization", `Bearer${config.token}`);
      myHeaders.append("Content-Type", "application/json");
      myHeaders.append("Cookie", "__wpdm_client=9a6d88491b5c975242839b1e203e9118");

      var raw = JSON.stringify({
        "folder_id": parseInt(folder.id),
        "question_id": question.id
      });

      var requestOptions = {
        method: 'POST',
        headers: myHeaders,
        body: raw,
        redirect: 'follow'
      };

      fetch(config.apiUrl+"wp-json/learnpress/v1/folders/question", requestOptions)
        .then(response => response.text())
        .then(result => {
          console.log("AddQuestion",JSON.parse(result))
        })
        .catch(error => console.log('error', error));
    },
  }
}

</script>



<style scoped>
.dropdown-check-list {
  display: inline-block;
}

.dropdown-check-list .anchor {
  position: relative;
  cursor: pointer;
  display: inline-block;
}

.dropdown-check-list .anchor:after {
  position: absolute;
  content: "";
  border-left: 2px solid #039A7B;
  border-top: 2px solid #039A7B;
  padding: 5px;
  right: 270px;
  top: 20%;
  transform: rotate(-135deg);
}

.dropdown-check-list .anchor:active:after {
  right: 270px;
  top: 21%;
}

.dropdown-check-list ul.items {
  padding: 2px;
  display: none;
  margin: 0;
  border-top: none;
}

.dropdown-check-list ul.items li {
  list-style: none;

}

.dropdown-check-list.visible .anchor {
  color: #0094ff;
}

.dropdown-check-list.visible .items {
  display: block;
}


</style>
