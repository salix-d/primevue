<template>
    <DocSectionText v-bind="$attrs"> </DocSectionText>
    <div class="card flex justify-center">
        <Form v-slot="$form" :resolver="resolver" :initialValues="initialValues" @submit="onFormSubmit" class="flex flex-col gap-4 w-full md:w-56">
            <div class="flex flex-col gap-1">
                <Select name="city.name" :options="cities" optionLabel="name" placeholder="Select a City" fluid />
                <Message v-if="$form.city?.name?.invalid" severity="error" size="small" variant="simple">{{ $form.city.name.error?.message }}</Message>
            </div>
            <Button type="submit" severity="secondary" label="Submit" />
        </Form>
    </div>
    <DocSectionCode :code="code" :dependencies="{ zod: '3.23.8' }" />
</template>

<script>
import { zodResolver } from '@primevue/forms/resolvers/zod';
import { z } from 'zod';

export default {
    data() {
        return {
            initialValues: {
                city: { name: '' }
            },
            resolver: zodResolver(
                z.object({
                    city: z.union([
                        z.object({
                            name: z.string().min(1, 'City is required.')
                        }),
                        z.any().refine((val) => false, { message: 'City is required.' })
                    ])
                })
            ),
            cities: [
                { name: 'New York', code: 'NY' },
                { name: 'Rome', code: 'RM' },
                { name: 'London', code: 'LDN' },
                { name: 'Istanbul', code: 'IST' },
                { name: 'Paris', code: 'PRS' }
            ],
            code: {
                basic: `
<Form v-slot="$form" :resolver="resolver" :initialValues="initialValues" @submit="onFormSubmit" class="flex flex-col gap-4 w-full md:w-56">
    <div class="flex flex-col gap-1">
        <Select name="city.name" :options="cities" optionLabel="name" placeholder="Select a City" fluid />
        <Message v-if="$form.city?.name?.invalid" severity="error" size="small" variant="simple">{{ $form.city.name.error?.message }}</Message>
    </div>
    <Button type="submit" severity="secondary" label="Submit" />
</Form>
`,
                options: `
<template>
    <div class="card flex justify-center">
        <Form v-slot="$form" :resolver="resolver" :initialValues="initialValues" @submit="onFormSubmit" class="flex flex-col gap-4 w-full md:w-56">
            <div class="flex flex-col gap-1">
                <Select name="city.name" :options="cities" optionLabel="name" placeholder="Select a City" fluid />
                <Message v-if="$form.city?.name?.invalid" severity="error" size="small" variant="simple">{{ $form.city.name.error?.message }}</Message>
            </div>
            <Button type="submit" severity="secondary" label="Submit" />
        </Form>
    </div>
</template>

<script>
import { zodResolver } from '@primevue/forms/resolvers/zod';
import { z } from 'zod';

export default {
    data() {
        return {
            initialValues: {
                city: { name: '' }
            },
            resolver: zodResolver(
                z.object({
                    city: z.union([
                        z.object({
                            name: z.string().min(1, 'City is required.')
                        }),
                        z.any().refine((val) => false, { message: 'City is required.' })
                    ])
                })
            ),
            cities: [
                { name: 'New York', code: 'NY' },
                { name: 'Rome', code: 'RM' },
                { name: 'London', code: 'LDN' },
                { name: 'Istanbul', code: 'IST' },
                { name: 'Paris', code: 'PRS' }
            ],
        }
    },
    methods: {
        onFormSubmit({ valid }) {
            if (valid) {
                this.$toast.add({ severity: 'success', summary: 'Form is submitted.', life: 3000 });
            }
        }
    }
}
<\/script>
`,
                composition: `
<template>
    <div class="card flex justify-center">
        <Form v-slot="$form" :resolver="resolver" :initialValues="initialValues" @submit="onFormSubmit" class="flex flex-col gap-4 w-full md:w-56">
            <div class="flex flex-col gap-1">
                <Select name="city.name" :options="cities" optionLabel="name" placeholder="Select a City" fluid />
                <Message v-if="$form.city?.name?.invalid" severity="error" size="small" variant="simple">{{ $form.city.name.error?.message }}</Message>
            </div>
            <Button type="submit" severity="secondary" label="Submit" />
        </Form>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import { zodResolver } from '@primevue/forms/resolvers/zod';
import { useToast } from "primevue/usetoast";
import { z } from 'zod';

const toast = useToast();
const initialValues = ref({
    city: { name: '' }
});
const resolver = ref(zodResolver(
    z.object({
        city: z.union([
            z.object({
                name: z.string().min(1, 'City is required.')
            }),
            z.any().refine((val) => false, { message: 'City is required.' })
        ])
    })
));
const cities = ref([
    { name: 'New York', code: 'NY' },
    { name: 'Rome', code: 'RM' },
    { name: 'London', code: 'LDN' },
    { name: 'Istanbul', code: 'IST' },
    { name: 'Paris', code: 'PRS' }
]);

const onFormSubmit = ({ valid }) => {
    if (valid) {
        toast.add({ severity: 'success', summary: 'Form is submitted.', life: 3000 });
    }
};
<\/script>
        `
            }
        };
    },
    methods: {
        onFormSubmit({ valid }) {
            if (valid) {
                this.$toast.add({ severity: 'success', summary: 'Form is submitted.', life: 3000 });
            }
        }
    }
};
</script>
