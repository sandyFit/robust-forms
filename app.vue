<script setup>
const formData = ref({
  username: 'sandyfit',
  password: '',
})

const handleSubmit = async data => {
  await wait(3000);
  console.log(data);
}

</script>

<template>
  <div>
    <!-- Override FormKit's smart defaults for ultimate customization with section classes and slots
        inner-class -->
    <FormKit 
      type="text"
      label="Username"
      name="username"
      help="Pick a new username"
      validation="required|matches:/^@[a-zA-Z]+$/|length:5"
      value="@FormKit"
      prefix-icon="avatarMan"
      inner-class="mycustom-inner"
    >
    <template #label="context">
      {{ context.label }}
      ?
      <span>{{ context.help }}</span> 
    </template>

    <template #help></template>
  </FormKit>
    <FormKit type="select"/>
    <FormKit type="textarea"/>

    <div>
      <!-- :actions='false' to customize the default button -->
      <FormKit 
        type="form" 
        :value="formData"
        :actions="false"
        @submit="handleSubmit"
        >
        <template #default="{state}">
          <h1 >Login</h1>
          <FormKit 
            type="text" 
            label="Username" 
            name="username"
            validation="required|url|length:8"/>
          <FormKit type="password" label="Password" name="password" />                 
          <button :disable="state.loading">
            {{ state.loading ? 'Loading...' : 'Login' }}
          </button>
        </template>
      </FormKit>
    </div>
  </div>
</template>
