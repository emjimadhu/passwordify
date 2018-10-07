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
    password: ''
  }),
  methods: {
    generate () {
      this.password = pg.generatePassword()
    },
    exit() {
      this.$exit();
    }
  }
}
</script>
