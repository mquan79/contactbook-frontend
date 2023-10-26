<template>
    <div class="page">
        <h4>Thêm Liên hệ</h4>
        <ContactForm
            :contact="data"
            @submit:contact="addContact"
        />
        <p>{{ message }}</p>
    </div>
</template>

<script>
import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";

export default {
    components: {
        ContactForm,
    },
    data() {
        return {
            data: {
                name: "",
                email: "",
                address: "",
                phone: "",
                favorite: false,
            },
            message: "",
        };
    },
    methods: {
        async addContact(data) {
            try {
                await ContactService.create(data);
                this.message = "Liên hệ đã được thêm mới.";
            } catch (error) {
                console.error(error);
                this.message = "Đã xảy ra lỗi khi thêm liên hệ.";
            }
        },
    },
};
</script>
