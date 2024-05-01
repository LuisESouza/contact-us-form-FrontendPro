<script setup>
    import MessageForm from "./MessageForm.vue";
    import { ref } from "vue";
    import axios from 'axios';


    const ACCESS_KEY = "543c4711-7969-4d93-9ce3-d582a76282b4";
    const apiUrl = `https://api.web3forms.com/submit`;

    const name = ref("");
    const email = ref("");
    const subject = ref("");
    const message = ref("");

    const submit = async () => {
        if (name.value.trim() == "" || subject.value.trim() == "" || message.value.trim() == "") {
            alert("Enter the data correctly");
            return;
        }

        try{
            const response = await axios.post(apiUrl, {
                access_key: ACCESS_KEY,
                name: name,
                email: email,
                subject: subject,
                message: message,
            });

            if (response.data.success) {
                alert("Email sent successfully!");
                console.log(response);
            }
        }catch(error){
            console.log("Error sending email: ", error);
            alert("An error occurred while sending the email.");
        }
    };
</script>

<template>
    <form @submit.prevent="submit">
        <MessageForm />
        <input v-model="name" type="text" id="name" placeholder="Name">
        <input v-model="email" type="email" id="email" placeholder="Email">
        <input v-model="subject" type="text" id="subject" placeholder="Subject">
        <textarea v-model="message" id="message" cols="30" rows="4" placeholder="Message"></textarea>
        <button>Send</button>
    </form>
</template>

<style scoped>
    form {
        background-color: #FFFFFF;
        display: flex;
        flex-direction: column;
        gap: 25px;
        width: 30%;
        margin: auto;
        margin-top: 10vh;
        padding: 25px;
        border-radius: 6px;
        align-items: center;
        box-shadow: 5px 5px 5px rgba(0, 0, 0, 0.1);
    }
    input{
        padding: 8px;
        outline: none;
        border: 1px solid gray;
        border-radius: 5px;
        width: 80%;
    }
    input:focus{
        border: 1px solid #7985FF;
        color: #7985FF;
    }
    textarea{
        resize: none;
        padding: 10px;
        outline: none;
        border: 1px solid gray;
        border-radius: 5px;
        width: 80%;
    }
    textarea:focus{
        border: 1px solid #7985FF;
        color: #7985FF;
    }
    button{
        padding: 8px;
        height: 43px;
        width: 85%;
        background: linear-gradient(to right, #65ADFF, #778AFF);
        border: none;
        border-radius: 6px;
        cursor: pointer;
        color: white;
        margin-bottom: 50px;
    }
    button:hover{
        transform: scale(1.02);
        transition: .4s;
        border: 2px solid #7985FF;
        box-shadow: 0 0 15px rgba(101, 173, 255, 0.5);
    }
    button:focus{
        outline: none;
        transform: scale(1.02);
        transition: .4s;
        border: 2px solid #7985FF;
        box-shadow: 0 0 15px rgba(101, 173, 255, 0.5);
    }

</style>