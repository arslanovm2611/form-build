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
</script>

<template>
  <div class="flex h-screen items-center justify-center">
    <Card class="mx-auto max-w-sm w-96">
      <CardHeader>
        <CardTitle class="text-2xl"> Login </CardTitle>
        <CardDescription>
          Enter your email below to login to your account
        </CardDescription>
      </CardHeader>
      <CardContent>
        <div class="grid gap-4">
          <div class="grid gap-2">
            <Label for="email">Email</Label>
            <Input
              id="email"
              type="email"
              placeholder="m@example.com"
              required
            />
          </div>
          <div class="grid gap-2">
            <div class="flex items-center">
              <Label for="password">Password</Label>
              <NuxtLink
                to="/auth/reset-password"
                class="ml-auto inline-block text-sm underline"
              >
                Forgot your password?
              </NuxtLink>
            </div>
            <div class="relative">
              <Input
                id="password"
                ref="inputPasswordCN"
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
          <Button type="submit" class="w-full"> Login </Button>
        </div>
      </CardContent>
    </Card>
  </div>
</template>
