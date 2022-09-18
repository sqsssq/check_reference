<!--
 * @Author: Qing Shi
 * @LastEditTime: 2022-09-18 23:41:37
-->
<!-- bib input -->
<template>
    <div style="height: 100%;">
        <el-row :gutter="30" style="height: 100%;">
            <el-col :span="12">
                <h1>BibTex</h1>
                <el-input v-model="inputData" placeholder="Please input" style="height: auto;"
                    :autosize="{ maxRows: 15, minRows: 15 }" type="textarea" />
                <el-button type="primary" style="margin-top: 20px;" @click="checkRepeat(inputData)">Check</el-button>
            </el-col>
            <el-col :span="12">
                <h1>Repeat Reference</h1>
                <!-- <div v-for="(d, i) in repeatReference" :key="i">
                    {{'[' + (i + 1) + '] ' + d }}
                </div> -->
                <el-table :data="repeatReference" stripe border  :show-header=true style="width: 100%; height: 325px;">
                    <el-table-column prop="num" label="S/N" width="50" align='center' />
                    <!-- <el-table-column prop="name" label="Name" width="180" /> -->
                    <el-table-column prop="title" label="Title" align='center' />
                </el-table>
            </el-col>
        </el-row>
    </div>
</template>

<script>
import { ref } from 'vue';
export default {
    data () {
        return {
            importHeight: this.clientHeight,
            inputData: ref(''),
            minR: ref(0),
            repeatReference: []
        };
    },

    components: {},

    computed: {},

    //   mounted: {},

    methods: {
        rowStyle() {
      return {  wordBreak: 'keep-all' };
    },
        checkRepeat: function (data) {
            // console.log(typeof data);
            // data.indexOf('title');
            // console.log(data.split('\n'));
            let str = data;
            let patt = new RegExp("title", "g");
            let result;
            let index_title = new Array();
            let mapTitle = new Object();
            let titleCnt = new Object();

            while ((result = patt.exec(str)) != null) {
                // document.write(result);
                // document.write("<br />");
                // document.write(patt.lastIndex);
                // console.log(result);    
                if ((data[result.index - 1] >= 'a' && data[result.index - 1] <= 'z') || (data[result.index - 1] >= 'A' && data[result.index - 1] <= 'Z'))
                    continue;
                index_title.push(result.index);
            }
            // console.log(index_title);
            for (let i = 0; i < index_title.length; i++) {
                let startOfTitle = 0;
                let allTitle = '';
                let allTitleLow = '';
                for (let j = index_title[i]; data[j] != '}'; ++j) {
                    // console.log(data[j]);
                    if (data[j] == '{') {
                        startOfTitle = 1;
                    }
                    if (startOfTitle && data[j] != '{') {
                        if ((data[j] >= 'a' && data[j] <= 'z') || (data[j] >= 'A' && data[j] <= 'Z'))
                            allTitleLow += data[j];
                        allTitle += data[j];
                    }
                }
                allTitleLow = allTitleLow.toLowerCase();
                let startTitle = 0;
                let endTitle = allTitle.length - 1;
                for (let k = 0; k < allTitle.length; ++k) {
                    if (allTitle[k] != ' ') break;
                    startTitle++;
                }
                for (let k = allTitle.length - 1; k >= 0; --k) {
                    if (allTitle[k] != ' ') break;
                    endTitle--;
                }
                allTitle = allTitle.slice(startTitle, endTitle + 1);
                // console.log(allTitle, startTitle, endTitle, allTitle.slice(startTitle, endTitle + 1));
                mapTitle[allTitleLow] = allTitle;
                if (typeof (titleCnt[allTitleLow]) == 'undefined') {
                    titleCnt[allTitleLow] = 0;
                }
                titleCnt[allTitleLow]++;
            }
            let repeatTitle = new Array();
            let cnt = 1;
            for (let i in titleCnt) {
                if (titleCnt[i] > 1) {
                    repeatTitle.push({
                        num: '[' + cnt + ']',
                        title: mapTitle[i]
                    });
                    cnt++;
                }
            }
            // console.log(titleCnt, repeatTitle);
            this.repeatReference = repeatTitle;
        },

    },

    watch: {
    }
}

</script>
<style scoped>
h1 {
    font-size: 30px;
}
</style>