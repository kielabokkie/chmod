<template>
  <div class="chmod">
    <div>
      <h1>chmod</h1>
    </div>
    <input placeholder="rwxr-xr-x" size="10" maxlength="10" v-model="permissions" class="large" v-on:input="parse">
    <div class="result">{{ result }}</div>
  </div>
</template>

<script>
export default {
  name: 'chmod',
  data () {
    return {
      permissions: '',
      permissionsParts: '',
      result: '000'
    }
  },
  methods: {
    parse: function () {
      // Strip the first character if it contains the special permissions flag
      this.permissionsParts = this.permissions.replace(/^[_\-dlst]/, '')

      // Stop parsing if the string is not 9 characters
      if (this.permissionsParts.length !== 9) {
        return
      }

      var sectionOne = this.parseSection(1)
      var sectionTwo = this.parseSection(2)
      var sectionThree = this.parseSection(3)
      this.result = sectionOne.toString() + sectionTwo.toString() + sectionThree.toString()
    },
    parseSection: function (section) {
      var start = 0
      switch (section) {
        case 2:
          start = 3
          break
        case 3:
          start = 6
          break
      }
      var sectionString = this.permissionsParts.substring(start, start + 3)
      var first = this.getPermission(sectionString.substring(0, 1))
      var second = this.getPermission(sectionString.substring(1, 2))
      var third = this.getPermission(sectionString.substring(2, 3))
      return first + second + third
    },
    getPermission: function (character) {
      switch (character) {
        case 'r':
          return 4
        case 'w':
          return 2
        case 'x':
          return 1
        default:
          return 0
      }
    }
  }
}
</script>

<style scoped>
h1 {
  font-size: 60px;
  margin-bottom: 20px;
}
input {
  padding: 5px 10px 5px 5px;
  margin-bottom: 10px;
  display: block;
  border: none;
  text-align: center;
}
input:focus {
  outline:none;
}
.result {
  font-size: 100px;
  font-weight: bold;
}
.large {
  font-size: 50px;
  font-weight: bold;
}
</style>
