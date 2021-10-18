<template>
  <base-card>
  <base-button @click="setSelectedTab('stored-resources')" :mode="storeRestButtonMode">Stored Resources</base-button>
  <base-button @click="setSelectedTab('add-resource')" :mode="addResButtonNode">Add Resource</base-button>
  </base-card>
  <keep-alive>
  <component :is="selectedTab"></component>
  </keep-alive>
</template>

<script>
import StoredResources from './StoredResorces.vue';
import AddResource from './AddResource.vue'
export default {
    components:{
        StoredResources,
        AddResource
        },

    data(){
        return {
            selectedTab: 'stored-resources',
            storedResources:[
                {
                    id: 'official-guide',
                    title: 'Offical Guide',
                    description: 'This is official vue js Documentation.',
                    link:'https://vuejs.org'
                },
                {
                    id: 'gooogle',
                    title: 'gooogle Guide',
                    description: 'This is google',
                    link:'https://google.com'
                },
            ]
        }
    },
    provide(){
        return {
            resorces: this.storedResources,
            addresource: this.addResources
        }
    },
    computed:{
        storeRestButtonMode(){
            return this.selectedTab ==='stored-resources' ? null:'flat'
        },
        addResButtonNode(){
            return this.selectedTab ==='add-resource' ? null:'flat';
        }
    },
    methods:{
        setSelectedTab(tab){
            this.selectedTab = tab;
        },
        addResources(title,description,url){
            const newResource = {
                id: new Date().toISOString(),
                title: title,
                description:description,
                link:url,
            }
            this.storedResources.unshift(newResource);
            this.selectedTab = 'stored-resources';
        }
    }
}
</script>

<style>

</style>