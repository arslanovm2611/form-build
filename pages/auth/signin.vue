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
  email: "",
  password: "",
});

function signIp() {
  errors.value = [];
  if (!form.email.includes("@"))
    errors.value.push("Please, input your email correctly");
  if (form.password.trim() === "")
    errors.value.push("Please, input your password");
  if (errors.value.length === 0) {
    console.log(form);
  } else {
  }
}
</script>

<template>
  <div class="flex h-screen items-center justify-center">
    <Card class="mx-auto max-w-sm w-96">
      <CardHeader>
        <CardTitle class="text-2xl"> Sign in </CardTitle>
        <CardDescription>
          Enter your email below to sign in to your account
        </CardDescription>
      </CardHeader>
      <CardContent>
        <div class="grid gap-4">
          <div class="grid gap-2">
            <Label for="email">Email</Label>
            <Input
              id="email"
              type="email"
              v-model="form.email"
              placeholder="m@example.com"
              required
            />
          </div>
          <div class="grid gap-2">
            <div class="relative">
              <Input
                id="password"
                ref="inputPasswordCN"
                v-model="form.password"
                :type="showPass ? 'text' : 'password'"
                required
              />
              <Eye
                class="w-6 h-6 absolute right-3 top-[20.5px] -translate-y-1/2 hover:cursor-pointer"
                @click="showPass = !showPass"
                v-if="!showPass"
              />
              <EyeOff
                class="w-6 h-6 absolute right-3 top-[20.5px] -translate-y-1/2 hover:cursor-pointer"
                @click="showPass = !showPass"
                v-else
              />
            </div>
          </div>
          <div
            class="bg-red-500 rounded-lg text-white p-6"
            v-if="errors.length"
          >
            <p v-for="error in errors" :key="error">{{ error }}</p>
          </div>
          <Button type="submit" class="w-full" @click="signIp"> Login </Button>
        </div>
      </CardContent>
    </Card>
  </div>
</template>
