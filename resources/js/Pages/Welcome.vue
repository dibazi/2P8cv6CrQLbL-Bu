<template>

   <div class="relative flex items-top justify-center min-h-screen bg-gray-100 dark:bg-gray-900 sm:items-center sm:pt-0">
        <div class="hidden fixed top-0 right-0 px-6 py-4 sm:block">
                <inertia-link :href="route('login')" class="text-sm text-gray-700 underline">
                    Entree
                </inertia-link>

            <template>
                <inertia-link :href="route('login')" class="text-sm text-gray-700 underline">
                    Log in
                </inertia-link>

                <inertia-link :href="route('register')" class="ml-4 text-sm text-gray-700 underline">
                    S'enregistrer
                </inertia-link>
            </template>
        </div>

<div class="container">

            
    <jet-authentication-card>
        <template #logo>
            Kaji
        </template>

        <jet-validation-errors class="mb-4" />

        <form @submit.prevent="submit">
            <div>
                <jet-label for="name" value="Nom" />
                <jet-input id="name" type="text" class="mt-1 block w-full" required v-model="form.name"  autofocus autocomplete="name" />
            </div>

            <div class="mt-4">
                <jet-label for="email" value="Adresse mail" />
                <jet-input id="email" type="email" class="mt-1 block w-full" required v-model="form.email"  />
            </div>
            <div class="mt-4">
                <jet-label for="email" value="Genre" />
                <select name="genre" v-model="form.gender" required class="block mt-1 w-full border-gray-300 focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50 rounded-md shadow-sm">
                    <option value="femme">Femme/fille</option>
                    <option value="home">Home/garcon</option>
                </select>
            </div>

            <div class="mt-4">
                <jet-label for="password" value="Mot de pass" />
                <jet-input id="password" type="password" required class="mt-1 block w-full" v-model="form.password"  autocomplete="new-password" />
            </div>

            <div class="mt-4">
                <jet-label for="password_confirmation" value="Confirme Mot de pass" />
                <jet-input id="password_confirmation" type="password" required class="mt-1 block w-full" v-model="form.password_confirmation" autocomplete="new-password" />
            </div>

            <div class="mt-4" v-if="$page.props.jetstream.hasTermsAndPrivacyPolicyFeature">
                <jet-label for="terms">
                    <div class="flex items-center">
                        <jet-checkbox name="terms" id="terms" v-model:checked="form.terms" />

                        <div class="ml-2">
                            I agree to the <a target="_blank" :href="route('terms.show')" class="underline text-sm text-gray-600 hover:text-gray-900">Terms of Service</a> and <a target="_blank" :href="route('policy.show')" class="underline text-sm text-gray-600 hover:text-gray-900">Privacy Policy</a>
                        </div>
                    </div>
                </jet-label>
            </div>

            <div class="flex items-center justify-end mt-4">
                <inertia-link :href="route('login')" class="underline text-sm text-gray-600 hover:text-gray-900">
                    Deja enregistrer?
                </inertia-link>

                <jet-button class="ml-4" :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
                    S'enregistrer
                </jet-button>
            </div>
        </form>
    </jet-authentication-card>

</div>
</div>

</template>

<script>
    import JetAuthenticationCard from '@/Jetstream/AuthenticationCard'
    import JetAuthenticationCardLogo from '@/Jetstream/AuthenticationCardLogo'
    import JetButton from '@/Jetstream/Button'
    import JetInput from '@/Jetstream/Input'
    import JetCheckbox from "@/Jetstream/Checkbox";
    import JetLabel from '@/Jetstream/Label'
    import JetValidationErrors from '@/Jetstream/ValidationErrors'

    export default {
        components: {
            JetAuthenticationCard,
            JetAuthenticationCardLogo,
            JetButton,
            JetInput,
            JetCheckbox,
            JetLabel,
            JetValidationErrors
        },

        data() {
            return {
                form: this.$inertia.form({
                    name: '',
                    email: '',
                    gender: '',
                    password: '',
                    password_confirmation: '',
                    terms: false,
                })
            }
        },

        methods: {
            submit() {
                this.form.post(this.route('register'), {
                    onFinish: () => this.form.reset('password', 'password_confirmation'),
                })
            }
        }
    }
</script>
