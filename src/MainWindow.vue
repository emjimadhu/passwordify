<template>
  <Window
    :title="title"
    width="500"
    height="400"
    margined
    @close="exit"
  >
    <Box
      padded
    >
      <Text>This is a simple app to Generate Password.</Text>

      <!-- Simple Vertical Spacing -->
      <Box padded><Text /></Box>
      <Box padded><Text /></Box>

      <Box
        padded
      >
        <Text>
          The Following is your Generated password
        </Text>
        <TextInput
          readonly
          :value="password"
        />

        <!-- Simple Vertical Spacing -->
        <Box padded><Text /></Box>

        <Button
          @click="generate"
        >
          GENERATE
        </Button>

        <!-- Simple Vertical Spacing -->
        <Box padded><Text /></Box>

        <Box
          padded
        >
          <Checkbox
            v-model="showAdvancedOptions"
          >
            Advanced Options?
          </Checkbox>

          <Box
            horizontal
            padded
            v-if="showAdvancedOptions"
          >
            <Box>
              <Checkbox
                v-model="options.upperCaseAlpha"
              >
                Uppercase Letters
              </Checkbox>

              <Checkbox
                v-model="options.lowerCaseAlpha"
              >
                Lowercase Letters
              </Checkbox>

              <Checkbox
                v-model="options.number"
              >
                Numbers
              </Checkbox>

              <Checkbox
                v-model="options.specialCharacter"
              >
                Special Charaters
              </Checkbox>
            </Box>

            <Box>
              <Box
                horizontal
              >
                <Text>Minimum Value:     </Text>
                <Spinbox
                  v-model="minValue"
                  :min="8"
                />
              </Box>
              <Box
                horizontal
              >
                <Text>Maximum Value:    </Text>
                <Spinbox
                  v-model="maxValue"
                  :min="8"
                />
              </Box>
              <Box
                horizontal
              >
                <Text>Exact Value:             </Text>
                <Spinbox
                  v-model="exactValue"
                  :min="8"
                />
              </Box>
            </Box>
          </Box>
        </Box>
      </Box>
    </Box>
  </Window>
</template>

<script>
// Requiring the Library
const PasswordGenerator = require('strict-password-generator').default

// Creating an Instance
const pg = new PasswordGenerator()

export default {
  data: () => ({
    title: 'Passwordify',
    password: '',
    options: {
      upperCaseAlpha: false,
      lowerCaseAlpha: false,
      number: false,
      specialCharacter: false
    },
    minValue: 8,
    maxValue: 12,
    exactValue: 8,
    showAdvancedOptions: false
  }),
  methods: {
    generate () {
      let options = JSON.parse(JSON.stringify(this.options))
      let requiredMinimum = 0
      for (let option in options) {
        if (options[option]) {
          requiredMinimum++
        }
      }

      if (requiredMinimum === 0) {
        options['lowerCaseAlpha'] = true
        options['number'] = true
      }

      options['minimumLength'] = this.minValue
      options['maximumLength'] = this.maxValue
      options['exactLength'] = this.exactValue

      this.password = pg.generatePassword(options)
    },
    exit() {
      this.$exit()
    }
  }
}
</script>
