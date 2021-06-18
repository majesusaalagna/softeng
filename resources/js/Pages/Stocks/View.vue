<template>
    <div>
        <Layout>
            <div class="flex justify-center w-full">
                <div class="bg-white flex flex-col w-1/3 mt-20 p-6">
                    <div class="flex flex-row justify-between">
                        <h2 class="text-lg">Stock Form</h2>

                        <inertia-link :href="route('stock.destroy', form.id)" method="delete">
                        Delete
                        </inertia-link>
                    </div>
                    <form
                        id="stock-form"
                        name="stock-form"
                        v-on:submit.prevent="submit"
                    >
                        <div class="flex flex-col pt-6">
                            <label for="id">ID</label>
                            <input
                                type="text"
                                id="id"
                                name="id"
                                v-model="form.id"
                                autocomplete="off"
                                readonly
                            />
                            <div class="text-red-700 text-sm">
                                {{ errors.id }}
                            </div>
                        </div>

                        <div class="flex flex-col pt-6">
                            <label for="stock_category_id">Stock Category ID</label>
                            <select id="stock_category_id" v-model="form.stock_category_id">
                                <option v-for="item in stock_category_id" :key="item.id" v-bind:value="item.id">{{item.id}}</option>
                            </select>
                           
                            <div class="text-red-700 text-sm">
                                {{ errors.stock_category_id }}
                            </div>
                        </div>

                        <div class="flex flex-col pt-6">
                            <label for="description">Description</label>
                            <input
                                type="text"
                                id="description"
                                name="description"
                                v-model="form.description"
                                autocomplete="off"
                            />
                            <div class="text-red-700 text-sm">
                                {{ errors.description }}
                            </div>
                        </div>

                        <div class="flex flex-col pt-6">
                            <label for="uom">UOM</label>
                            <input
                                type="text"
                                id="uom"
                                name="uom"
                                v-model="form.uom"
                                autocomplete="off"
                            />
                            <div class="text-red-700 text-sm">
                                {{ errors.uom }}
                            </div>
                        </div>

                        <div class="flex flex-col pt-6">
                            <label for="barcode">Barcode</label>
                            <input
                                type="text"
                                id="barcode"
                                name="barcode"
                                v-model="form.barcode"
                                autocomplete="off"
                            />
                            <div class="text-red-700 text-sm">
                                {{ errors.barcode }}
                            </div>
                        </div>

                       <div class="flex flex-col pt-6">
                            <label for="barcode">Discontinued Yes</label>
                            <input type="checkbox" id="yes" true-value="Y" false-value="N" v-model="form.discontinued"/>
                            <div class="text-red-700 text-sm">
                                {{ errors.discontinued }}
                            </div>
                        </div>
                        <div class="flex flex-col pt-6">
                            <label for="barcode">Discontinued No</label>
                            <input type="checkbox" id="no" true-value="N" false-value="Y" v-model="form.discontinued"/>
                            <div class="text-red-700 text-sm">
                                {{ errors.discontinued }}
                            </div>
                        </div>

                        <div class="flex flex-col pt-6">
                            <button
                                type="submit"
                                class="bg-indigo-800 text-white p-2"
                            >
                                Update
                            </button>
                        </div>
                    </form>
                </div>
            </div>
        </Layout>
    </div>
</template>

<script>
import { ref, reactive } from "vue";
import Layout from "@/Layouts/Authenticated";
import { Inertia } from "@inertiajs/inertia";
export default {
    components: {
        Layout,
    },
    props: {
        errors: Object,
        model: Object,
        stock_category_id: Array
    },
    setup(props, context) {
        const form = reactive({
            id: props.model.id,
            stock_category_id: props.model.stock_category_id,
            description: props.model.description,
            uom: props.model.uom,
            barcode: props.model.barcode,
            discontinued: props.model.discontinued,
            photo_path: props.model.photo_path,
        });
        const submit = () => {
            Inertia.put(route("stock.update", form), form, {
                onSuccess: () => {
                    // Handle success event
                    form.id = null;
                    form.stock_category_id = null;
                    form.description = null;
                    form.uom = null;
                    form.barcode = null;
                    form.discontinued = null;
                    form.photo_path = null;
                    //   this.reset();
                },
            });
        };
        return {
            form,
            submit,
        };
    },
};
</script>