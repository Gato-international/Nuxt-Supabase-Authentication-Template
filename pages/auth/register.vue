<template>
  <div
    class="mx-auto flex w-full flex-col justify-center space-y-6 sm:w-[350px] z-40"
  >
    <div class="flex flex-col space-y-2 text-center">
      <h1 class="text-2xl font-semibold tracking-tight">Create an account</h1>
      <p class="text-sm text-muted-foreground">
        Enter your email below to create your account
      </p>
    </div>
    <div class="grid gap-6">
      <form>
        <div class="grid gap-2">
          <div class="grid gap-1">
            <label
              class="text-sm font-medium leading-none peer-disabled:cursor-not-allowed peer-disabled:opacity-70 sr-only"
              for="email"
              >Email</label
            >
            <UInput
              v-model="value"
              placeholder="name@example.com"
              type="email"
              autocapitalize="none"
              autocomplete="email"
              autocorrect="off"
            />
          </div>
          <UButton block>Sign In with Email</UButton>
        </div>
      </form>
      <div class="relative">
        <UDivider label="Or continue with" />
        <!-- Auth Providers -->
      </div>
    </div>
  </div>
</template>
