<script setup lang="ts">
import type { FormError, FormSubmitEvent } from '@nuxt/ui/dist/runtime/types'
import type { FormLogin } from '../types/index'
import { reactive, ref } from 'vue';

const loading = ref(false)
const state = reactive<FormLogin>({
	username: '',
	password: ''
})

const validate = (state: FormLogin): FormError[] => {
	const errors: any = []
	if(!state.username || state.username === '') errors.push({ path: 'username', message: 'Required' })
	if(!state.password || state.password === '') errors.push({ path: 'password', message: 'Required' })
	return errors
}

const onSubmit = (event: FormSubmitEvent<FormLogin>) => {
	try {
		loading.value = true
		
		console.log(event.data)
	} catch (error) {
		console.log(error)
	} finally {
		setTimeout(() => {
			loading.value = false
		}, 5000);
	}
}
</script>
<template>
	<UContainer>
		<div class="grid place-items-center h-screen">
			<div class="w-1/4 flex flex-col">
					<UForm :validate="validate" :state="state" @submit="onSubmit">
						<UFormGroup label="Username" name="username" class="mb-4">
							<UInput v-model="state.username" :loading="loading" :disabled="loading"/>
						</UFormGroup>
						<UFormGroup label="Password" name="password" class="mb-4">
							<UInput v-model="state.password" type="password" :loading="loading" :disabled="loading"/>
						</UFormGroup>
						<UButton type="submit" :disabled="loading">
							Submit
						</UButton>
					</UForm>
			</div>
		</div>
	</UContainer>
</template>