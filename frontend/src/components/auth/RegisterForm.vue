<script setup>
import { SignupSchema } from "../../validation/auth";
import { Form, Field, ErrorMessage } from "vee-validate";
import { Button } from "@/components/ui/button/index.js";
import {
  Card,
  CardHeader,
  CardTitle,
  CardFooter,
  CardContent,
} from "@/components/ui/card/index";
import { router } from "@/router/index";
</script>

<template>
  <Card class="w-1/3 m-auto">
    <CardHeader class="text-center">
      <CardTitle>Welcome !</CardTitle>
    </CardHeader>
    <CardContent>
      <Form action="" @submit="submitLogin" :validation-schema="SignupSchema">
        <div class="w-full my-8">
          <label for="email" class="block">User name</label>
          <Field
            id="username"
            name="username"
            type="text"
            class="w-full rounded-sm p-2 outline-none border focus-visible:border-[#03C988]"
          />
          <ErrorMessage name="username" class="text-red-500" />
        </div>
        <div class="w-full my-8">
          <label for="email" class="block">Email</label>
          <Field
            id="email"
            name="email"
            type="email"
            class="w-full rounded-sm p-2 outline-none border focus-visible:border-[#03C988]"
          />
          <ErrorMessage name="email" class="text-red-500" />
        </div>
        <div class="w-full my-8">
          <label for="password" class="block">Password</label>
          <Field
            id="password"
            name="password"
            type="password"
            class="w-full rounded-sm p-2 outline-none border focus-visible:border-[#03C988]"
          />
          <ErrorMessage name="password" class="text-red-500" />
        </div>
        <Button class="w-full font-semibold" :disabled="isSending">
          Register
        </Button>
      </Form>
    </CardContent>
    <CardFooter class="w-fit m-auto flex flex-col items-center">
      <p v-if="error" class="text-red-500 font-semibold">
        Something went wrong try again later !
      </p>
      <p v-if="success" class="text-green-500 font-semibold">
        User created successfully !
      </p>
      <RouterLink class="underline" to="/login"
        >Already have an account ?</RouterLink
      >
    </CardFooter>
  </Card>
</template>

<script>
import { createUser } from "@/api/auth";

export default {
  data() {
    return {
      isSending: false,
      error: false,
      success: false,
    };
  },
  methods: {
    async submitLogin(values) {
      try {
        this.isSending = true;
        this.error = false;
        const response = await createUser(values);

        if (response.status === 201) {
          this.success = true;
          setTimeout(() => {
            router.push({ name: "login" });
          }, 2000);
        } else {
          this.error = true;
          this.isSending = false;
        }
      } catch (error) {
        this.error = true;
        this.isSending = false;
      }
    },
  },
};
</script>
