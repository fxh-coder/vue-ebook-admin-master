<template>
  <div class="detail">
    <el-form ref="postForm" :model="postForm" class="form-container">
      <sticky :z-index="10" :class-name="'sub-navbar'">
        <el-button v-if="!isEdit" @click.prevent.stop="showGuide">显示帮助</el-button>
        <el-button v-loading="loading" style="margin-left: 10px;" type="success" @click="submitForm">
          {{ isEdit ? '编辑电子书' : '新增电子书' }}
        </el-button>
      </sticky>
      <div class="detail-container">
        <el-row>
          <Warning />
          <el-col :span="24">
            <ebook-upload
              :file-list="fileList"
              :disabled="isEdit"
              @onSuccess="onUploadSuccess"
              @onRemove="onUploadRemove"
            />
          </el-col>
          <el-col :span="24">
            <el-form-item prop="title">
              <MdInput
                v-model="postForm.title"
                :maxlength="100"
                name="name"
                required
              >
                书名
              </MdInput>
            </el-form-item>
            <el-row>
              <el-col :span="12">
                <el-form-item label="作者：" :label-width="labelWidth">
                  <el-input
                    v-model="postForm.author"
                    placeholder="作者"
                    style="width: 100%"
                  />
                </el-form-item>
              </el-col>
              <el-col :span="12">
                <el-form-item label="出版社：" :label-width="labelWidth">
                  <el-input
                    v-model="postForm.publisher"
                    placeholder="出版社"
                    style="width: 100%"
                  />
                </el-form-item>
              </el-col>
            </el-row>
            <el-row>
              <el-col :span="12">
                <el-form-item label="语言：" :label-width="labelWidth">
                  <el-input
                    v-model="postForm.language"
                    placeholder="语言"
                    style="width: 100%"
                  />
                </el-form-item>
              </el-col>
              <el-col :span="12">
                <el-form-item label="根文件：" :label-width="labelWidth">
                  <el-input
                    v-model="postForm.rootFile"
                    placeholder="根文件"
                    style="width: 100%"
                    disabled
                  />
                </el-form-item>
              </el-col>
            </el-row>
            <el-row>
              <el-col :span="12">
                <el-form-item label="文件路径：" :label-width="labelWidth">
                  <el-input
                    v-model="postForm.filePath"
                    placeholder="文件路径"
                    style="width: 100%"
                    disabled
                  />
                </el-form-item>
              </el-col>
              <el-col :span="12">
                <el-form-item label="解压路径：" :label-width="labelWidth">
                  <el-input
                    v-model="postForm.unzipPath"
                    placeholder="解压路径"
                    style="width: 100%"
                    disabled
                  />
                </el-form-item>
              </el-col>
            </el-row>
            <el-row>
              <el-col :span="12">
                <el-form-item label="封面路径：" :label-width="labelWidth">
                  <el-input
                    v-model="postForm.coverPath"
                    placeholder="封面路径"
                    style="width: 100%"
                    disabled
                  />
                </el-form-item>
              </el-col>
              <el-col :span="12">
                <el-form-item label="文件名称" :label-width="labelWidth">
                  <el-input
                    v-model="postForm.fileName"
                    placeholder="文件名称"
                    style="width: 100%"
                    disabled
                  />
                </el-form-item>
              </el-col>
            </el-row>
            <el-row>
              <el-col :span="24">
                <el-form-item label="封面：" :label-width="labelWidth">
                  <a v-if="postForm.cover" :href="postForm.cover" target="_blank">
                    <img :src="postForm.cover" class="preview-img">
                  </a>
                  <span v-else>无</span>
                </el-form-item>
              </el-col>
            </el-row>
            <el-row>
              <el-col :span="24">
                <el-form-item label="目录：" :label-width="labelWidth">
                  <div v-if="postForm.contents && postForm.contents.length > 0" class="contents-wrapper">
                    <el-tree />
                  </div>
                  <span v-else>无</span>
                </el-form-item>
              </el-col>
            </el-row>
          </el-col>
        </el-row>
      </div>
    </el-form>
  </div>
</template>

<script>
import Sticky from '../../../components/Sticky/index'
import Warning from './Warning'
import EbookUpload from '../../../components/EbookUpload'
import MdInput from '../../../components/MDinput/index'

export default {
  components: {
    Sticky,
    Warning,
    EbookUpload,
    MdInput
  },
  props: {
    isEdit: Boolean
  },
  data() {
    return {
      loading: false,
      postForm: {},
      fileList: [],
      labelWidth: '120px'
    }
  },
  methods: {
    onUploadSuccess() {},
    onUploadRemove() {},
    submitForm() {
      this.loading = true
    },
    showGuide() {}
  }
}
</script>

<style lang="scss" scoped>
  @import "~@/styles/mixin.scss";

  .detail {
    position: relative;
    .detail-container {
      padding: 40px 45px 20px 50px;
      .preview-img {
        width: 200px;
        height: 270px;
      }
      .contents-wrapper {
        padding: 5px 0;
      }
    }
  }
</style>
