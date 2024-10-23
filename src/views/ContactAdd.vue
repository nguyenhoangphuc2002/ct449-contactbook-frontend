<template>
    <div class="page">
        <h4>Thêm Liên hệ Mới</h4>
        <ContactForm :contact="contactLocal" @submit:contact="submitContact" @delete:contact="deleteContact" />
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
            contactLocal: {
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
        async submitContact(data) {
            try {
                await ContactService.create(data);
                alert('Liên hệ đã được thêm thành công.');
                this.$router.push({ name: "contactbook" });
            } catch (error) {
                console.log(error);
                this.message = "Có lỗi xảy ra khi thêm liên hệ.";
            }
        },
        deleteContact() {
            // Không cần chức năng xóa ở đây, có thể bỏ qua hoặc chỉ để thông báo
            alert("Không thể xóa liên hệ chưa được lưu.");
        },
    },
};
</script>

<style scoped>
.page {
    max-width: 750px;
    margin: auto;
}
</style>
