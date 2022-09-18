<!-- <script setup>
import TheWelcome from "../components/TheWelcome.vue";
</script>

<template>
  <main>
    <TheWelcome />
  </main>
</template> -->
<!-- Home View -->
<template>
  <div class="common-layout" style="width: 100%;">
    <el-container style="height: 100vh">
      <el-header style="">
        <BibNav />
      </el-header>
      <el-container>
        <!-- <el-aside width="200px">Aside</el-aside> -->
        <el-container>
          <el-main style=" height: calc(100% - 120px);">
            <el-row :gutter="20" style="height: 100%;">
              <el-col :span="24">
                <BibInput />
              </el-col>
              <!-- <el-col :span="12">
              </el-col> -->
            </el-row>
          </el-main>
          <el-footer
            style="height: 30px; background-color: #ffffff; color: black; line-height: 30px; text-align:center">
            Copyright ©2022 Qing Shi. ALL Rights Reserved

          </el-footer>
        </el-container>
      </el-container>
    </el-container>
  </div>
</template>

<script>
import BibInput from "../components/bibInput.vue";
import BibNav from "../components/bibNav.vue";
export default {
  name: 'home_view',
  data () {
    return {
    };
  },

  components: { BibInput, BibNav },

  computed: {},

  // mounted: {},

  methods: {}
}

</script>
<style scoped>
.el-row {
  margin-bottom: 20px;
}

.el-row:last-child {
  margin-bottom: 0;
}

.el-col {
  border-radius: 4px;
}

.grid-content {
  border-radius: 4px;
  min-height: 36px;
}
</style>