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
        <div class="grid gap-4">
          <div class="space-y-2">
            <div>
              <label
                class="text-xs font-medium leading-8 peer-disabled:cursor-not-allowed peer-disabled:opacity-70"
                for="email"
                >Password</label
              >
              <UInput
                v-model="form.email"
                color="white"
                placeholder="Password"
                type="email"
                autocapitalize="none"
                autocomplete="email"
                autocorrect="off"
              />
            </div>
            <div>
              <label
                class="text-xs font-medium leading-8 peer-disabled:cursor-not-allowed peer-disabled:opacity-70"
                for="email"
                >Confirm Password</label
              >
              <UInput
                v-model="form.password"
                color="white"
                placeholder="Confirm Password"
                type="password"
                autocapitalize="none"
                autocomplete="email"
                autocorrect="off"
              />
            </div>
          </div>
          <UButton
            :disabled="loginValid"
            color="emerald"
            @click="signInWithEmailPassword()"
            block
            >Sign In with Email</UButton
          >
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
<script setup>
definePageMeta({
  auth: false,
});
</script>
<script>
export default {
  data() {
    return {
      loading: false,
      providers: {},
      loginMethod: "",
      form: {
        email: "ryntab@github.com",
        password: "password",
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
    async signInWithEmailPassword() {
      console.log("login");
      this.loading = true;
      const supabase = useSupabaseClient();

      const { data: response, error } = await supabase.auth.signInWithPassword({
        email: this.form.email,
        password: this.form.password,
      });

      if (error) {
        console.log(error);
        this.loading = false;
        return;
      }

      if (response) {
        const { user, session } = response;
        if (user && session) {
          this.$router.push("/");
        }
      }

      // try {
      //   this.loading = true;
      //   await this.$store.dispatch("user/loginUser", this.login);
      //   this.loading = false;
      // } catch (err) {
      //   this.loading = false;
      // }
    },
    async signInWithOTP() {
      const { data, error } = await useSupabaseClient().auth.signInWithOtp({
        email: "example@email.com",
        options: {
          emailRedirectTo: "http://localhost:3000/user/dashboard",
        },
      });

      if (error) {
        console.log(error);
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
