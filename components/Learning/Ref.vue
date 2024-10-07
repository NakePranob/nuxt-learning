<script setup lang="ts">
    defineProps({
        msg: String,
    })

    // ใช้ ref สำหรับค่าที่เป็น primitive type (ตัวแปรเดียว)
    const count = ref<number>(0)
    const fullname = ref<string>('')
    const file = ref<File | null>(null)
    const imageUrl = ref<string | null>(null) // เก็บ URL ของภาพที่จะแสดง

    // ใช้ reactive สำหรับ object ที่มีหลายค่าและไม่ต้องใส่ value ให้แต่ละ field โดยตรง
    const count2 = reactive<{ count: number }>({ count: 0 })
    const formName = reactive({ firstname: '', lastname: '' })

    watch(
        // ()=> [formName.firstname, formName.lastname], -- หรือจะใช้แบบนี้ก็ได้ใช้ในกรณีดักจับแค่บางตัวแปร
        formName,
        (newFullName, OldFullName) => {
            // fullname.value = `${newFullName[0]} ${newFullName[1]}`
            fullname.value = `${newFullName.firstname} ${newFullName.lastname}`
        }
    )

    // watchEffect(()=>{ -- ใช้แบบนี้ได้เหมือนกัน จะดังจับตัวแปรใน fucntion
    //     fullname.value = `${formName.firstname} ${formName.lastname}`
    // })

    const items = reactive<string[]>([
        'https://picsum.photos/1920/1080?random=1',
        'https://picsum.photos/1920/1080?random=2',
        'https://picsum.photos/1920/1080?random=3',
        'https://picsum.photos/1920/1080?random=4',
        'https://picsum.photos/1920/1080?random=5',
        'https://picsum.photos/1920/1080?random=6'
    ])

    // ฟังก์ชันสำหรับเพิ่มค่าของ count
    function increment() {
        count.value++
    }

    // ฟังก์ชันสำหรับเพิ่มค่าของ count2 (object)
    function increment2() {
        count2.count++
    }

    // ฟังก์ชันสำหรับแสดงภาพจาก input type file
    function showImage(event: Event) {
        const input = event.target as HTMLInputElement;
        console.log('input', input);
        if (input && input.files && input.files[0]) {
            file.value = input.files[0];
            console.log(file.value);
            imageUrl.value = URL.createObjectURL(file.value); // สร้าง URL สำหรับไฟล์ภาพ
        } else {
            console.error("ไม่มีไฟล์ที่เลือกหรือข้อมูล input ไม่ถูกต้อง");
        }
    }
</script>

<template>
    <UContainer>
        <div class="flex flex-col gap-4 pb-6">
            <h1>{{ msg }}</h1>
            <div>
                fullname: {{ fullname }}
            </div>
            <div>
                <label for="firstname">ชื่อ</label>
                <UInput v-model="formName.firstname" type="text" />
            </div>
            <div>
                <label for="lastname">นามสกุล</label>
                <UInput v-model="formName.lastname" type="text" />
            </div>
            <div>
                Counter: {{ count }}
            </div>
            <UInput v-model.number="count" type="number" />
            <UButton @click="increment">Add Counter</UButton>

            <div>
                Counter2: {{ count2.count }}
            </div>
            <UInput v-model="count2.count"/>
            <UButton @click="increment2">Add Counter2</UButton>

            <!-- Input สำหรับการอัปโหลดไฟล์ -->
            <UInput type="file" size="sm" accept="image/*" icon="i-heroicons-folder" @input="showImage" />

            <!-- แสดงภาพที่อัปโหลด -->
            <UCard v-if="imageUrl" class="flex justify-center">
                <img :src="imageUrl" alt="Uploaded Image" class="w-64 h-64 object-contain" />
            </UCard>
            <UCard v-else class="flex justify-center">
                ยังไม่มีรูปภาพ
            </UCard>
            <UCarousel v-slot="{ item }" :items="items" :ui="{ item: 'basis-full' }" class="rounded-lg overflow-hidden h-96" arrows>
                <img :src="item" class="w-full object-center object-cover" draggable="false">
            </UCarousel>
            <ul class="px-12">
                <li v-for="(item, index) in items" :key="item">
                    {{ index + 1 }}. {{ item }}
                </li>
            </ul>
        </div>
    </UContainer>
</template>
