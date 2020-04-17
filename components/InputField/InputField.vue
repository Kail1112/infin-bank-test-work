<template>
  <label :class="dark | modificationClass(inline, input, type)">
    <span class="input-signature"
          v-if="displaySignature"
          v-text="signature"/>
    <input type="text"
           v-model="input"
           :placeholder="placeholder">
  </label>
</template>

<script>
  export default {
    name: "InputField",
    data () {
      return {
        input: ''
      }
    },
    watch: {
      input (val) {
        if (this.type === 'card') this.input = val.replace(/(\D|\s)/g, '').split(/(\d{4})/g).filter(item => item !== '').slice(0, 4).join('  ')
        if (this.type === 'date') this.input = val.replace(/(\D|\s)/g, '').split(/(\d{2})/g).filter(item => item !== '').slice(0, 2).join('/')
      }
    },
    props: {
      type: [String, null], /// Тип заполнения
      placeholder: [String, Number, null], /// Placeholder
      showSignature: [Boolean, null], /// Показывать ли подпись сбоку
      signature: [String, null], /// Подпись сбоку
      dark: [Boolean, null], /// Применить ли темную тему
      inline: [Boolean, null], /// Показывать ли данные в линию
    },
    filters: {
      /// modificationClass - применение различных стилей
      modificationClass (dark, inline, input, type) {
        const classList = dark ? ( inline ? 'input-label dark inline' : 'input-label dark' ) : ( inline ? 'input-label inline' : 'input-label' )
        const checkType = type ?? false
        let error = ''
        if (checkType !== false) {
          if (type === 'card') {
            const checkLen = input.length === 0 ? false : input.length < 22
            if (checkLen) error = 'error'
          }
          if (type === 'date') {
            const checkLen = input.length === 0 ? false : input.length < 5
            if (checkLen) error = 'error'
          }
        }
        return `${classList} ${error}`
      },
      /*---------------------------------*/
    },
    computed: {
      /// displaySignature - показать ли подпись
      displaySignature () {
        const checkPropsShowSignature = this?.showSignature ?? false
        const checkPropsSignature = this?.signature ?? false
        return checkPropsShowSignature !== false && checkPropsSignature !== false
      },
      /*---------------------------------*/
    }
  }
</script>
