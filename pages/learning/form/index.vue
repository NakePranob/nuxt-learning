<script setup>
const formData = reactive({
    name: '',
    email: '',
    gender: 'male',
    message: '',
    interests: [],
    agree: false, // สำหรับ Checkbox
    preferredContact: '' // สำหรับ Radio
});

const interestsList = ['เล่นเกม', 'เตะบอล', 'อ่านหนังสือ', 'ฟังเพลง'];

const genderOptions = [
    { value: 'male', label: 'ชาย' },
    { value: 'female', label: 'หญิง' },
    { value: 'other', label: 'อื่น ๆ' }
];

const contactOptions = [
    { value: 'email', label: 'อีเมล' },
    { value: 'phone', label: 'โทรศัพท์' }
];

const submitForm = () => {
    console.log('ข้อมูลฟอร์ม:', formData);
    // ที่นี่คุณสามารถทำการส่งข้อมูลไปยัง API หรือทำการประมวลผลเพิ่มเติม
};
</script>

<template>
    <UContainer>
        <div class="flex flex-col gap-4">
            <h1>ฟอร์มตัวอย่างใน Nuxt UI</h1>
            <form @submit.prevent="submitForm" class="flex flex-col gap-4">
                <UInput
                    v-model="formData.name"
                    label="ชื่อ"
                    placeholder="กรุณากรอกชื่อ"
                    required
                />
                
                <UInput
                    v-model="formData.email"
                    label="อีเมล"
                    placeholder="กรุณากรอกอีเมล"
                    type="email"
                    required
                />

                <USelect 
                    v-model="formData.gender"
                    label="เพศ"
                    :options="genderOptions"
                    required
                />
                
                <UTextarea
                    v-model="formData.message"
                    label="ข้อความ"
                    placeholder="กรุณากรอกข้อความ"
                    required
                />

                <h2>กิจกรรมที่สนใจ</h2>
                <div v-for="interest in interestsList" :key="interest">
                    <UCheckbox
                        v-model="formData.interests"
                        :label="interest"
                        :value="interest"
                    />
                </div>

                <UDivider label="Finish" />
                
                <!-- Checkbox -->
                <UCheckbox
                    v-model="formData.agree"
                    label="ฉันยอมรับข้อกำหนดและเงื่อนไข"
                    required
                />

                <!-- Radio Buttons -->
                <h2>วิธีการติดต่อที่ต้องการ</h2>
                <div v-for="option in contactOptions" :key="option.value">
                    <URadio 
                        v-model="formData.preferredContact"
                        :label="option.label"
                        :value="option.value"
                    />
                </div>

                <UButton type="submit" class="text-center">ส่งข้อมูล</UButton>
            </form>
        </div>
    </UContainer>
</template>
