<script setup lang="ts">
import * as z from 'zod';

const toast = useToast();

const props = defineProps({
  shouldShowMagicLink: {
      type: Boolean,
      default: false
    }
});

const magicLinkFields = [{
  name: 'magiclink',
  label: 'Magic link?',
  size:"lg",
  type: 'select' as const,
  searchable: false,
  items: [
    { label: 'Magic Link', value: 'magiclink' },
    { label: 'Basic Login', value: 'basiclogin' },
  ],
  ui: {
    root: 'absolute top-4 end-4 w-24',
    /** hide the label (or use 'sr-only' for screen-readers) */
    labelWrapper: 'hidden'
  }
},
{
  name: 'email',
  type: 'text' as const,
  label: 'Email',
  placeholder: 'Enter your email',
  required: true
}, {
  name: 'remember',
  label: 'Remember me',
  type: 'checkbox' as const
}];
const basicLoginFields = [{
  name: 'magiclink',
  label: 'Magic link?',
  size:"lg",
  type: 'select' as const,
  searchable: false,
  items: [
    { label: 'Magic Link', value: 'magiclink' },
    { label: 'Basic Login', value: 'basiclogin' },
  ],
  ui: {
    root: 'absolute top-4 end-4 w-24',
    /** hide the label (or use 'sr-only' for screen-readers) */
    labelWrapper: 'hidden'
  }
},{
  name: 'email',
  type: 'text' as const,
  label: 'Email',
  placeholder: 'Enter your email',
  required: true
}, {
  name: 'password',
  label: 'Password',
  type: 'password' as const,
  placeholder: 'Enter your password'
},  {
  name: 'remember',
  label: 'Remember me',
  type: 'checkbox' as const
}];

const providers = [{
  label: 'Google',
  icon: 'i-simple-icons-google',
  onClick: () => {
    toast.add({ title: 'Google', description: 'Login with Google' })
  }
}, {
  label: 'GitHub',
  icon: 'i-simple-icons-github',
  onClick: () => {
    toast.add({ title: 'GitHub', description: 'Login with GitHub' })
  }
}];

const schema = z.object({
  email: z.string().email('Invalid email'),
  password: z.string().min(8, 'Must be at least 8 characters')
});

type Schema = z.output<typeof schema>;

function onSubmit(payload: FormSubmitEvent<Schema>) {
  console.log('Submitted', payload)
}
const fields = computed(() => {
console.log(props.shouldShowMagicLink)
 if(props.shouldShowMagicLink) {
  return magicLinkFields;
 } 
 return basicLoginFields;
});
</script>

<template>
  <div class="flex flex-col items-center justify-center gap-4 p-4">
    <UPageCard class="w-full max-w-md">
      <UAuthForm
        class="relative"
        :schema="schema"
        title="Login"
        description="Enter your credentials to access your account."
        icon="i-lucide-user"
        :fields="fields"
        @submit="onSubmit"
      />
    </UPageCard>
  </div>
</template>

