<script>
import emailjs from '@emailjs/browser';

export default {
    name: 'ContactForm',
    data() {
        return {
            formData: {
                name: '',
                email: '',
                content: '',
            },
        };
    },
    mounted() {
        emailjs.init('rL0LsG1kN3CcwjKsX');
    },
    methods: {
        sendContactRequest() {
            emailjs.sendForm('service_03o9iwt', 'template_ioo4eub', this.$refs.contactForm)
                .then((response) => {
                    console.log('Email send succesfully!!:', response);
                    alert('Message send succesfully!!');
                    this.resetForm();
                })
                .catch((error) => {
                    console.error('Error while mail sending', error);
                    alert('Error while mail sending. Try Later.');
                });
        },
        resetForm() {
            this.formData.name = '';
            this.formData.email = '';
            this.formData.content = '';
        }
    }
};
</script>


<template>
    <form @submit.prevent="sendContactRequest" ref="contactForm">
        <div class="mb-3">
            <label for="to_name" class="form-label">Your Name</label>
            <input type="text" class="form-control" id="to_name" name="to_name" v-model="formData.name" required>
        </div>

        <div class="mb-3">
            <label for="from_name" class="form-label">Your Email Address</label>
            <input type="email" class="form-control" id="from_name" name="from_name" v-model="formData.email" required>
            <div class="form-text">Don't exchange data with anybody.</div>
        </div>

        <div class="form-floating mb-3">
            <textarea class="form-control" placeholder="Inserisci il tuo messaggio" id="message" name="message"
                v-model="formData.content" required></textarea>
            <label for="content">Message</label>
        </div>

        <button type="submit" class="btn my-btn">Send!!</button>
    </form>
</template>

<style lang="scss">
.my-btn {
    border: 1px solid #fd2bfd;
    background-color: #fd2bfd;
    color: black;

    &:hover {
        background-color: transparent;
        color: white;
    }
}
</style>
