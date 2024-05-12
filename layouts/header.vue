<script setup lang="ts">
import { CircleUser } from "lucide-vue-next";

import { Button } from "@/components/ui/button";
import {
  DropdownMenu,
  DropdownMenuContent,
  DropdownMenuItem,
  DropdownMenuTrigger,
} from "@/components/ui/dropdown-menu";
</script>
<template>
  <div class="w-full py-6 px-8 flex justify-end absolute">
    <div class="flex flex-col">
      <DropdownMenu>
        <DropdownMenuTrigger as-child>
          <Button variant="secondary" size="icon" class="rounded-full">
            <CircleUser class="h-5 w-5" />
          </Button>
        </DropdownMenuTrigger>
        <DropdownMenuContent align="end">
          <div>
            <DropdownMenuItem>Logout</DropdownMenuItem>
          </div>
          <div>
            <DropdownMenuItem
              ><NuxtLink to="/auth/signin"> Sign in </NuxtLink>
            </DropdownMenuItem>
            <DropdownMenuItem
              ><NuxtLink to="/auth/signup">
                Sign up
              </NuxtLink></DropdownMenuItem
            >
          </div>
        </DropdownMenuContent>
      </DropdownMenu>
    </div>
  </div>
  <slot />
</template>
