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
      </Box>
    </Box>
  </Window>
</template>

<script>
export default {
  data: () => ({
    title: 'Passwordify',
    password: ''
  }),
  methods: {
    exit() {
      this.$exit();
    }
  }
}
</script>
