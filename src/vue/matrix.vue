<template>
    <table :class="question.cssClasses.root">
        <thead>
            <tr>
                <td v-show="question.hasRows"></td>
                <th v-for="column in question.columns"><survey-string :locString="column.locText"/></th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="(row, rowIndex) in question.visibleRows" :class="question.cssClasses.row">
                <td v-show="question.hasRows"><survey-string :locString="row.locText"/></td>
                <td v-for="(column, columnIndex) in question.columns">
                    <label :class="question.cssClasses.label">
                        <input type="radio" :class="question.cssClasses.itemValue" :name="row.fullName" v-model="row.value" :value="column.value" :disabled="question.isReadOnly" :id="(columnIndex === 0) && (rowIndex === 0) ? question.inputId : ''" v-bind:aria-label="question.locTitle.renderedHtml"/>
                        <span class="circle"></span>
                        <span class="check"></span>
                        <span :style="{ 'display': 'none' }">{{question.locTitle.renderedHtml}}</span>
                    </label>
                </td>
            </tr>
        </tbody>
    </table>
</template>

<script lang="ts">
    import Vue from 'vue'
    import {Component, Prop} from 'vue-property-decorator'
    import {default as Question} from './question'
    import {QuestionMatrixModel} from '../question_matrix'

    @Component
    export default class Matrix extends Question<QuestionMatrixModel> {
    }
    Vue.component("survey-matrix", Matrix)
</script>
