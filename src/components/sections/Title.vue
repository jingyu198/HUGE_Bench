<script setup>
const logo = ''

const title = 'HUGE-Bench: A Benchmark for High-Level UAV Vision-Language-Action Tasks'

const authorRows = [
  [
    { name: 'Jingyu Guo', marks: '1,*' },
    { name: 'Ziye Chen', marks: '1,*' },
    { name: 'Ziwen Li', marks: '2' },
    { name: 'Zhengqing Gao', marks: '2' },
    { name: 'Jiaxin Huang', marks: '2' },
  ],
  [
    { name: 'Hanlue Zhang', marks: '2' },
    { name: 'Fengming Huang', marks: '3,4' },
    { name: 'Yu Yao', marks: '4' },
    { name: 'Tongliang Liu', marks: '2,4,†' },
    { name: 'Mingming Gong', marks: '1,2,†' },
  ],
]

const institutes = [
  { marks: '1', name: 'The University of Melbourne' },
  { marks: '2', name: 'MBZUAI' },
  { marks: '3', name: 'Navlyn' },
  { marks: '4', name: 'The University of Sydney' },
]

const resourceButtons = [
  { label: 'Paper', icon: 'paper' },
  {
    label: 'Code',
    icon: 'github',
    link: 'https://github.com/jingyu198/HUGE-Bench?tab=readme-ov-file',
  },
  { label: 'Dataset', icon: 'dataset' },
]

const authorNotes = '* Equal contribution; † Corresponding author.'
</script>

<template>
  <section class="title-section">
    <el-row v-if="logo" justify="center">
      <el-image :src="logo" class="logo" fit="cover" />
    </el-row>

    <el-row justify="center">
      <el-col :span="20">
        <h1 class="paper-title">{{ title }}</h1>
      </el-col>
    </el-row>

    <el-row justify="center">
      <el-col :span="20">
        <div class="authors">
          <div v-for="(row, index) in authorRows" :key="index" class="author-row">
            <span v-for="author in row" :key="author.name" class="author-pill">
              {{ author.name }}<sup class="name-sup">{{ author.marks }}</sup>
            </span>
          </div>
        </div>
      </el-col>
    </el-row>

    <el-row justify="center">
      <el-col :span="20">
        <div class="institutes">
          <span v-for="institute in institutes" :key="institute.marks" class="institute-inline">
            <sup class="address-sup">{{ institute.marks }}</sup>{{ institute.name }}
          </span>
        </div>
      </el-col>
    </el-row>

    <el-row justify="center">
      <div class="author-notes">{{ authorNotes }}</div>
    </el-row>

    <el-row justify="center">
      <el-col :span="20">
        <div class="resource-buttons">
          <component
            v-for="button in resourceButtons"
            :key="button.label"
            :is="button.link ? 'a' : 'button'"
            class="resource-button"
            :href="button.link"
            :target="button.link ? '_blank' : undefined"
            :rel="button.link ? 'noreferrer' : undefined"
            :type="button.link ? undefined : 'button'"
          >
            <span class="resource-icon" aria-hidden="true">
              <svg v-if="button.icon === 'paper'" viewBox="0 0 24 24">
                <path d="M14 2H7a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V7zm0 1.5L17.5 7H14zM9 12h6v1.5H9zm0 3h6v1.5H9zm0-6h2.5V10.5H9z" />
              </svg>
              <svg v-else-if="button.icon === 'github'" viewBox="0 0 24 24">
                <path d="M12 .5a12 12 0 0 0-3.79 23.39c.6.11.82-.26.82-.58v-2.06c-3.33.72-4.03-1.41-4.03-1.41-.55-1.38-1.33-1.75-1.33-1.75-1.09-.74.08-.73.08-.73 1.2.09 1.84 1.22 1.84 1.22 1.08 1.82 2.82 1.29 3.5.98.11-.77.42-1.29.76-1.59-2.66-.3-5.47-1.31-5.47-5.86 0-1.3.47-2.36 1.23-3.19-.12-.3-.53-1.52.12-3.16 0 0 1.01-.32 3.3 1.22a11.6 11.6 0 0 1 6 0c2.29-1.54 3.3-1.22 3.3-1.22.65 1.64.24 2.86.12 3.16.77.83 1.23 1.89 1.23 3.19 0 4.56-2.82 5.55-5.5 5.84.43.37.82 1.08.82 2.18v3.23c0 .32.22.69.83.58A12 12 0 0 0 12 .5" />
              </svg>
              <svg v-else viewBox="0 0 24 24">
                <path d="M12 3c-4.97 0-9 1.57-9 3.5S7.03 10 12 10s9-1.57 9-3.5S16.97 3 12 3m-9 5v4.5C3 14.43 7.03 16 12 16s9-1.57 9-3.5V8c-1.93 1.42-5.4 2.25-9 2.25S4.93 9.42 3 8m0 6v3.5C3 19.43 7.03 21 12 21s9-1.57 9-3.5V14c-1.93 1.42-5.4 2.25-9 2.25S4.93 15.42 3 14" />
              </svg>
            </span>
            <span>{{ button.label }}</span>
          </component>
        </div>
      </el-col>
    </el-row>
  </section>
</template>

<style scoped>
.title-section {
  padding-top: 28px;
}

.paper-title {
  font-family: "MyFont", Verdana, sans-serif;
  letter-spacing: 1px;
  font-size: 42px;
  line-height: 1.25;
  margin: 20px 0 28px;
  text-align: center;
}

.authors {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
}

.author-row {
  display: flex;
  justify-content: center;
  gap: 12px 18px;
  flex-wrap: nowrap;
}

.author-pill {
  font-size: 20px;
  line-height: 1.6;
  white-space: nowrap;
}

.name-sup {
  color: #606266;
  margin-left: 2px;
}

.resource-buttons {
  margin-top: 18px;
  display: flex;
  justify-content: center;
  gap: 16px;
  flex-wrap: wrap;
}

.resource-button {
  border: none;
  display: inline-flex;
  align-items: center;
  gap: 10px;
  padding: 14px 28px;
  border-radius: 999px;
  background: #373737;
  color: #ffffff;
  font-size: 18px;
  font-weight: 500;
  line-height: 1;
  cursor: pointer;
}

.resource-icon {
  display: inline-flex;
  align-items: center;
  justify-content: center;
}

.resource-icon svg {
  width: 22px;
  height: 22px;
  fill: currentColor;
}

.institutes {
  margin-top: 18px;
  display: flex;
  justify-content: center;
  gap: 0 14px;
  flex-wrap: nowrap;
}

.institute-inline {
  font-size: 18px;
  line-height: 1.8;
  text-align: center;
  white-space: nowrap;
}

.address-sup {
  color: #606266;
  margin-right: 2px;
}

.author-notes {
  font-family: Arial, sans-serif;
  font-size: 14px;
  margin: 18px 0 12px;
  text-align: center;
}

.logo {
  width: 150px;
  height: 150px;
  border-radius: 50%;
  box-shadow: #ced3dc 0px 0px 3px 2px;
  margin-top: 20px;
}

@media (max-width: 900px) {
  .paper-title {
    font-size: 34px;
  }

  .author-row {
    flex-wrap: wrap;
  }

  .author-pill,
  .institute-inline {
    font-size: 16px;
  }

  .institutes {
    flex-wrap: wrap;
  }
}
</style>
