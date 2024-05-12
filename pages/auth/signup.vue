<script setup lang="ts">
import { Button } from "@/components/ui/button";
import {
  Card,
  CardContent,
  CardDescription,
  CardHeader,
  CardTitle,
} from "@/components/ui/card";
import { Input } from "@/components/ui/input";
import { Label } from "@/components/ui/label";

import { Eye, EyeOff } from "lucide-vue-next";

const showPass = ref(false);
const errors = ref<string[]>([]);
const form = reactive({
  firstName: "",
  lastName: "",
  email: "",
  password: "",
});

function signUp() {
  errors.value = [];
  if (form.firstName === "") errors.value.push("Please, input your firstname");
  if (form.lastName === "") errors.value.push("Please, input your lastname");
  if (!form.email.includes("@"))
    errors.value.push("Please, input your email correctly");
  if (form.password.trim() === "")
    errors.value.push("Please, input your password");
  if (errors.value.length) {
  }
}
</script>

<template>
  <div class="h-screen flex justify-center items-center">
    <div>
      <Card class="mx-auto max-w-sm">
        <CardHeader>
          <CardTitle class="text-xl"> Sign Up </CardTitle>
          <CardDescription>
            Enter your information to create an account
          </CardDescription>
        </CardHeader>
        <CardContent>
          <div class="grid gap-4">
            <div class="grid grid-cols-2 gap-4">
              <div class="grid gap-2">
                <Label for="first-name">First name</Label>
                <Input
                  id="first-name"
                  placeholder="Max"
                  v-model="form.firstName"
                  required
                />
              </div>
              <div class="grid gap-2">
                <Label for="last-name">Last name</Label>
                <Input
                  id="last-name"
                  placeholder="Robinson"
                  v-model="form.lastName"
                  required
                />
              </div>
            </div>
            <div class="grid gap-2">
              <Label for="email">Email</Label>
              <Input
                id="email"
                type="email"
                placeholder="m@example.com"
                v-model="form.email"
                required
              />
            </div>
            <div class="grid gap-2 relative">
              <Label for="password">Password</Label>
              <Input
                id="password"
                ref="inputPasswordCN"
                :type="showPass ? 'text' : 'password'"
                v-model="form.password"
                required
              />
              <Eye
                class="w-6 h-6 absolute right-3 top-[41.5px] -translate-y-1/2 hover:cursor-pointer"
                @click="showPass = !showPass"
                v-if="!showPass"
              />
              <EyeOff
                class="w-6 h-6 absolute right-3 top-[41.5px] -translate-y-1/2 hover:cursor-pointer"
                @click="showPass = !showPass"
                v-else
              />
            </div>
            <div>
              <div
                class="bg-red-500 rounded-lg text-white p-6"
                v-if="errors.length"
              >
                <p v-for="error in errors" :key="error">{{ error }}</p>
              </div>
            </div>
            <Button type="submit" class="w-full" @Click="signUp">
              Create an account
            </Button>
          </div>
          <div class="mt-4 text-center text-sm">
            Already have an account?
            <a href="#" class="underline"> Sign in </a>
          </div>
        </CardContent>
      </Card>
    </div>
  </div>
</template>
