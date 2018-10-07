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
          <Text>
            Advanced Options
          </Text>

          <Box
            horizontal
            padded
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
                <Text>Minimum Value:    </Text>
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
    maxValue: 12
  }),
  methods: {
    generate () {
      const options = {
        upperCaseAlpha: this.upperCase,
        lowerCaseAlpha: this.lowerCase,
        number: this.numbers,
        specialCharacter: this.specialCharacters,
        minimumLength: this.minValue,
        maximumLength: this.maxValue
      }
      this.password = pg.generatePassword(options)
    },
    exit() {
      this.$exit();
    }
  }
}
</script>
