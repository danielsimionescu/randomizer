<template>
  <v-flex xs12 md6 lg3>
    <v-card style="margin:5px">
      <h2 class="subheading">{{group.type}}</h2>
      <v-list>
        <template v-for="(item) in sortedList">
          <v-list-tile :key="item.title" avatar class="picked">
            <a :href="item.url" target="_blank">
              <v-list-tile-avatar :tile="true">
                <img :src="item.logo">
              </v-list-tile-avatar>
            </a>
            <v-list-tile-content>
              <v-list-tile-title>
                {{item.name}} <span class='text--secondary' v-if="item.language">({{item.language}})</span>
              </v-list-tile-title>
              <v-list-tile-sub-title>
                {{item.creator}}
              </v-list-tile-sub-title>
            </v-list-tile-content>
          </v-list-tile>
        </template>
      </v-list>
    </v-card>
  </v-flex>
</template>

<script>
export default {
  name: 'List',
  props: ['group'],
  computed: {
    sortedList() {
      const copy = [...this.group.items];

      return copy.sort((a, b) => {
        var nameA = a.name.toUpperCase(); // ignore upper and lowercase
        var nameB = b.name.toUpperCase(); // ignore upper and lowercase
        if (nameA < nameB) {
          return -1;
        }
        if (nameA > nameB) {
          return 1;
        }

        // names must be equal
        return 0;
      });
    }
  }
};
</script>

<style scoped>
  .subheading {
    padding: 10px 0 0 10px;
  }
</style>
