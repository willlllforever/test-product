<template>
  <el-form ref="form" :model="form" :inline="inline" :rules="rules" label-width="80px" label-position="left">
    <el-form-item v-for="item in formOption" :label="item.label" :key="item.label" :prop="item.model">
        <el-input 
            v-if="item.type === 'input'" 
            v-model="form[item.model]" 
            :placeholder="'请输入' + item.label">
        </el-input>
        <!-- <el-select 
            v-if="item.type === 'select'" 
            v-model="form[item.model]" 
            :required="item.option ? true : false" 
            :placeholder="'请选择' + item.label">
            <el-option v-for="option in item.option" :label="option" :value="option" :key="option"></el-option>
        </el-select> -->
        <el-input 
            v-if="item.type === 'textarea'" 
            v-model="form[item.model]" 
            :required="item.required ? true : false">
        </el-input>
        <el-radio-group 
            v-if="item.type === 'select'" 
            v-model="form[item.model]" 
            :placeholder="'请选择' + item.label">
            <el-radio v-for="option in item.option" :label="option" :key="option"></el-radio>
        </el-radio-group>
    </el-form-item>
    <el-form-item>
        <el-button type="primary" @click="submitForm('form')">保存</el-button>
    </el-form-item>
  </el-form>
</template>

<script>
export default {
    props: {
        form: Object,
        inline: Boolean,
        formOption: Array,
        rules: Object
    },
    data() {
        return {
            
        }
    },
    methods: {
        submitForm(formName) {
            this.$refs[formName].validate((valid) => {
            if (valid) {
                alert('submit!');
            } else {
                console.log('error submit!!');
                return false;
            }
            });
        },
    }
}
</script>

<style>

</style>