<template>
  <div
    class="mx-auto flex w-full flex-col justify-center space-y-6 sm:w-[350px] z-40 relative"
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
      <div class="flex flex-col space-y-4">
        <UButton block color="white" v-for="provider of providers">
          <template #leading>
            <icon :name="provider.icon" class="mr-2 h-4 w-4"></icon>
            {{ provider.name }}
          </template>
          {{ provider.name }}
        </UButton>
      </div>
    </div>
    <p class="px-8 text-center text-sm text-muted-foreground">
      By clicking continue, you agree to our
      <a class="underline underline-offset-4 hover:text-primary" href="/terms"
        >Terms of Service</a
      >
      and
      <a class="underline underline-offset-4 hover:text-primary" href="/privacy"
        >Privacy Policy</a
      >.
    </p>
  </div>
</template>
<script>
export default {
  data() {
    return {
      loading: false,
      providers: {},
      loginMethod: "",
      form: {
        email: "ryantaber17@gmail.com",
        password: "admin",
      },
      providers: [
        {
          name: "Google",
          icon: "ri:google-fill",
          auth: () => {
            const supabase = useSupabaseClient();
            supabase.auth.signInWithOAuth({
              provider: "google",
            });
          },
        },
        {
          name: "GitHub",
          icon: "ri:github-fill",
          auth: () => {
            const supabase = useSupabaseClient();
            supabase.auth.signInWithOAuth({
              provider: "github",
            });
          },
        },
        // Add more providers here
        // {
        //   name: "Twitter",
        //   icon: "ri:twitter-fill",
        //   auth: () => {
        //     const supabase = useSupabaseClient();
        //     supabase.auth.signInWithOAuth({
        //       provider: "twitter",
        //     });
        //   },
        // },
      ],
    };
  },
  methods: {
    async basicLogin() {
      const supabase = useSupabaseClient();
      try {
        this.loading = true;
        const { error } = await supabase.auth.signInWithPassword({
          email: this.form.email,
          password: this.form.password,
        });
        if (error) throw error;
        this.$router.push("/");
      } catch (error) {
        alert(error.error_description || error.message);
      } finally {
        this.loading = false;
      }
    },
  },
  computed: {
    loginValid() {
      if (this.form.username && this.form.password) {
        return true;
      } else {
        return false;
      }
    },
  },
};
</script>
