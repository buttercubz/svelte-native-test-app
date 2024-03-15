<script lang="ts">
  import Button from "@/lib/components/ui/button/button.svelte";
  import Input from "@/lib/components/ui/input/input.svelte";
  import Label from "@/lib/components/ui/label/label.svelte";
  import { Page } from "konsta/svelte";
  import { cn } from "@/lib/utils";
</script>

<Page>
  <div
    class="container relative flex-col items-center justify-center md:grid lg:max-w-none lg:grid-cols-2 lg:px-0"
  >
    <div class="lg:p-8">
      <div
        class="mx-auto flex w-full flex-col justify-center space-y-6 sm:w-[350px]"
      >
        <div class="flex flex-col space-y-2 text-center">
          <h1 class="text-2xl font-semibold tracking-tight">
            Create an account
          </h1>
          <p class="text-sm text-muted-foreground">
            Enter your email below to create your account
          </p>
        </div>

        <div class={cn("grid gap-6")}>
          <form>
            <div class="grid gap-2">
              <div class="grid gap-1">
                <Label class="sr-only" for="email">Email</Label>
                <Input
                  id="email"
                  placeholder="name@example.com"
                  type="email"
                  autocapitalize="none"
                  autocomplete="email"
                  autocorrect="off"
                />
              </div>
              <Button>
                <!-- {#if isLoading} -->
                <!-- <Icons.spinner class="mr-2 h-4 w-4 animate-spin" /> -->
                <!-- {/if} -->
                Sign In with Email
              </Button>
            </div>
          </form>
          <div class="relative">
            <div class="absolute inset-0 flex items-center">
              <span class="w-full border-t" />
            </div>
            <div class="relative flex justify-center text-xs uppercase">
              <span class="bg-background px-2 text-muted-foreground">
                Or continue with
              </span>
            </div>
          </div>
          <Button variant="outline" type="button">
            <!-- {#if isLoading} -->
            <!-- <Icons.spinner class="mr-2 h-4 w-4 animate-spin" /> -->
            <!-- {:else} -->
            <!-- <Icons.gitHub class="mr-2 h-4 w-4" /> -->
            <!-- {/if} -->
            {" "}
            GitHub
          </Button>
        </div>

        <p class="px-8 text-center text-sm text-muted-foreground">
          By clicking continue, you agree to our{" "}
          <a
            href="/terms"
            class="underline underline-offset-4 hover:text-primary"
          >
            Terms of Service
          </a>{" "}
          and{" "}
          <a
            href="/privacy"
            class="underline underline-offset-4 hover:text-primary"
          >
            Privacy Policy
          </a>
          .
        </p>
      </div>
    </div>
  </div>
</Page>
