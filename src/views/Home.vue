<template>
  <a-layout>
    <a-layout-sider width="200" style="background: #fff">
      <a-menu
          v-model:selectedKeys="selectedKeys2"
          v-model:openKeys="openKeys"
          mode="inline"
          :style="{ height: '100%', borderRight: 0 }"
      >
        <a-sub-menu key="sub1">
          <template #title>
              <span>
                <user-outlined/>
                subnav 1
              </span>
          </template>
          <a-menu-item key="1">option1</a-menu-item>
          <a-menu-item key="2">option2</a-menu-item>
          <a-menu-item key="3">option3</a-menu-item>
          <a-menu-item key="4">option4</a-menu-item>
        </a-sub-menu>
        <a-sub-menu key="sub2">
          <template #title>
              <span>
                <laptop-outlined/>
                subnav 2
              </span>
          </template>
          <a-menu-item key="5">option5</a-menu-item>
          <a-menu-item key="6">option6</a-menu-item>
          <a-menu-item key="7">option7</a-menu-item>
          <a-menu-item key="8">option8</a-menu-item>
        </a-sub-menu>
        <a-sub-menu key="sub3">
          <template #title>
              <span>
                <notification-outlined/>
                subnav 3
              </span>
          </template>
          <a-menu-item key="9">option9</a-menu-item>
          <a-menu-item key="10">option10</a-menu-item>
          <a-menu-item key="11">option11</a-menu-item>
          <a-menu-item key="12">option12</a-menu-item>
        </a-sub-menu>
      </a-menu>
    </a-layout-sider>
    <a-layout-content
        :style="{ background: '#fff', padding: '24px', margin: 0, minHeight: '280px' }"
    >
      <a-list item-layout="vertical" size="large" :grid="{gutter: 20, column: 3}" :pagination="pagination"
              :data-source="listData">
        <template #renderItem="{ item }">
          <a-list-item key="item.name" class="list-item">
            <template #actions>
              <span v-for="{ type, text } in actions" :key="type">
                <component :is="type" style="margin-right: 8px"/>
                {{ text }}
              </span>
            </template>
            <a-list-item-meta :description="item.description">
              <template #title>
                <a :href="item.href">{{ item.name }}</a>
              </template>
              <template #avatar>
                <a-avatar :src="item.cover"/>
              </template>
            </a-list-item-meta>
          </a-list-item>
          <div class="btn_cls">
            <a-button type="primary" :size="size" v-on:click="updateEvent">??????</a-button>
            <a-button danger :size="size" v-on:click="delEvent(item.id)">??????</a-button>
          </div>
        </template>
      </a-list>
    </a-layout-content>
  </a-layout>
</template>

<script lang="ts">
import {defineComponent, onMounted, ref} from 'vue';
import {StarOutlined, LikeOutlined, MessageOutlined} from '@ant-design/icons-vue';
import axios from 'axios';

export default defineComponent({
  name: 'Home',
  components: {
    StarOutlined,
    LikeOutlined,
    MessageOutlined,
  },
  setup() {
    const listData = ref();
    const reqBodyStr = {"page": 1, "size": 5};
    const handleQueryList = () => {
      axios.post("/ebook/list", reqBodyStr).then(response => {
        listData.value = response.data.content.list;
      });
    };
    const pagination = {
      onChange: (page: number) => {
        console.log(page);
      },
      pageSize: 9,
    };
    const actions: Record<string, string>[] = [
      {type: 'StarOutlined', text: '156'},
      {type: 'LikeOutlined', text: '156'},
      {type: 'MessageOutlined', text: '2'},
    ];

    onMounted(() => {
      handleQueryList();
    })
    return {
      listData,
      pagination,
      actions,
      handleQueryList
    };
  },
  methods: {
    updateEvent: function () {
      console.log("clickde ......")
    },
    delEvent: function (id : any) {
      axios.delete("/ebook/delete/" + id)
      .then(resp => {
        this.handleQueryList();
        alert("success");
      });
    }
  }
});
</script>

<style scoped>
[data-v-fae5bece] >>> .list-item {
  float: left;
  margin: 10px 10px 10px 50px;
}

.btn_cls > .ant-btn {
  display: block;
  margin: 10px 20px;
}
</style>
