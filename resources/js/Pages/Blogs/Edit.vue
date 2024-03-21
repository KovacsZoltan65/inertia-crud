<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head, useForm } from '@inertiajs/vue3';
import TextInput from '@/Components/TextInput.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import InputLabel from '@/Components/InputLabel.vue';
import InputError from '@/Components/InputError.vue';

const props = defineProps({
    blog: {
        type: Object,
        default: () => ({})
    }
});

const form = useForm({
    id: props.blog.id,
    title: props.blog.title,
    content: props.blog.content,
    slug: props.blog.slug
});

const submit = () => {
    form.put(route('blogs.update', props.blog.id));
};

</script>

<template>
    <Head title="Create Blog" />

    <AuthenticatedLayout>
        <template #header>
            <h2 class="text-xl font-semibold leading-tight text-gray-800">
                Blog Create
            </h2>
        </template>

        <div class="py-12">
            <div class="mx-auto max-w-7xl">
                <div class="overflow-hidden bg-white shadow-sm sm:rounded-lg">
                    <div class="p-6 bg-white border-b border-gray-200">

                        <form @submit.prevent="submit">
                            
                            <!-- TITLE -->
                            <div>
                                <InputLabel for="title" 
                                            value="Title" />

                                <TextInput id="title" name="title" 
                                           type="text" 
                                           class="mt-1 block w-full" 
                                           v-model="form.title" 
                                           required autofocus 
                                           autocomplete="username"/>

                                <InputError class="mt-2"
                                            :message="form.errors.title"/>
                            </div>

                            <!-- SLUG -->
                            <div>
                                <InputLabel for="slug" 
                                            value="Slug" />

                                <TextInput id="slug" name="slug" 
                                           type="text" 
                                           class="mt-1 block w-full" 
                                           v-model="form.slug" 
                                           required autofocus 
                                           autocomplete="username"/>

                                <InputError class="mt-2"
                                            :message="form.errors.title"/>
                            </div>

                            <!-- CONTENT -->
                            <div class="my-6">
                                <label for="content"
                                       class="block mb-2 text-sm font-medium text-gray-900">
                                    Content
                                </label>
                                <textarea type="text"
                                          v-model="form.content"
                                          name="content" id="content"
                                          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
                                ></textarea>

                                <div v-if="form.errors.content"
                                     class="text-sm text-red-600">
                                    {{ form.errors.content }}
                                </div>
                            </div>

                            <!-- BUTTON -->
                            <PrimaryButton type="submit"
                                           :class="{ 'opacity-25': form.processing }"
                                           :disabled="form.processing">
                                Submit
                            </PrimaryButton>

                        </form>

                    </div>
                </div>
            </div>
        </div>

    </AuthenticatedLayout>
</template>