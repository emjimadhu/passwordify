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
                v-model="upperCase"
              >
                Uppercase Letters
              </Checkbox>

              <Checkbox
                v-model="lowerCase"
              >
                Lowercase Letters
              </Checkbox>

              <Checkbox
                v-model="numbers"
              >
                Numbers
              </Checkbox>

              <Checkbox
                v-model="specialCharacters"
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
                />
              </Box>
              <Box
                horizontal
              >
                <Text>Maximum Value:    </Text>
                <Spinbox
                  v-model="maxValue"
                />
              </Box>
              <Box
                horizontal
              >
                <Text>Exact Value:             </Text>
                <Spinbox
                  v-model="exactValue"
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
    upperCase: false,
    lowerCase: false,
    numbers: false,
    specialCharacters: false,
    minValue: 8,
    maxValue: 12,
    exactValue: 8,
    showAdvancedOptions: false,
    advancedOptions: {},
    hasOneMinimumValue: false
  }),
  methods: {
    generate () {
      let options = {
        upperCaseAlpha: this.upperCase,
        lowerCaseAlpha: this.lowerCase,
        number: this.numbers,
        specialCharacter: this.specialCharacters,
        minimumLength: this.minValue,
        maximumLength: this.maxValue,
        exactLength: this.exactValue
      }

      if (this.hasOneMinimumValue) {
        options['upperCaseAlpha'] = this.upperCase
        options['lowerCaseAlpha'] = this.lowerCase
        options['number'] = this.numbers
        options['specialCharacter'] = this.specialCharacters
      } else {
        options['lowerCaseAlpha'] = true
        options['number'] = true
      }

      this.password = pg.generatePassword(options)
    },
    exit() {
      this.$exit();
    }
  },
  watch: {
    showAdvancedOptions (v) {
      if (this.upperCase || this.Lowercase || this.numbers || this.specialCharacters) {
        this.hasOneMinimumValue = true
      } else {
        this.hasOneMinimumValue = true
      }
    }
  }
}
</script>
