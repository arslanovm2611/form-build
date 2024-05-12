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
</script>

<template>
  <div class="flex h-screen items-center justify-center">
    <Card class="mx-auto max-w-sm w-96">
      <CardHeader>
        <CardTitle class="text-2xl"> Reset Password </CardTitle>
        <CardDescription>
          Enter your email below to reset password
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
          <Button type="submit" class="w-full"> Reset </Button>
        </div>
      </CardContent>
    </Card>
  </div>
</template>
