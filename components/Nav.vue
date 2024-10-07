<template>
    <div class="h-20 overflow-hidden flex justify-between items-center border-[var(--nui-primary-color)] px-4 2xl:px-20">
        <div class="w-56">
            YOUR LOGO
        </div>
        <ul class="flex gap-6">
            <li>
                <ULink
                    to="/"
                    active-class="text-primary"
                    inactive-class="text-gray-500 dark:text-gray-400 hover:text-gray-700 dark:hover:text-gray-200"
                >
                    Home
                </ULink>
            </li>
            <li>
                <ULink
                    to="/learning"
                    active-class="text-primary"
                    inactive-class="text-gray-500 dark:text-gray-400 hover:text-gray-700 dark:hover:text-gray-200"
                >
                    Learning
                </ULink>
            </li>
            <!-- <li>
                <ULink
                    to="/Contact"
                    active-class="text-primary"
                    inactive-class="text-gray-500 dark:text-gray-400 hover:text-gray-700 dark:hover:text-gray-200"
                >
                    Contact
                </ULink>
            </li> -->
        </ul>
        <div class="w-56 flex justify-end items-center gap-4">
            <ColorScheme><USelect v-model="$colorMode.preference" :options="['system', 'light', 'dark']" /></ColorScheme>
            Login
        </div>
    </div>
</template>