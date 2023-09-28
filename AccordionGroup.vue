<template>
    <div class="accordion-group">
        <div :class="{
                        'accordion-header-active': isOpened,
                        'accordion-header-regular': ! isOpened,
                        'rounded-t-lg': isFirst,
                        'rounded-b-lg': isLast && ! isOpened
                     }"
             class="accordion-header" @click="opened = ! isOpened"
        >
            <h3 :class="isFirst ? 'rounded-t-full' : ''" class="w-full relative">
                <slot name="header"></slot>
                <span class="absolute inset-y-0 right-1.5">
                    <svg class="h-4 w-4 mt-1" focusable="false" role="img" viewBox="0 0 448 512" xmlns="http://www.w3.org/2000/svg">
                        <path :class="{ 'hidden': isOpened }" d="M443.5 162.6l-7.1-7.1c-4.7-4.7-12.3-4.7-17 0L224 351 28.5 155.5c-4.7-4.7-12.3-4.7-17 0l-7.1 7.1c-4.7 4.7-4.7 12.3 0 17l211 211.1c4.7 4.7 12.3 4.7 17 0l211-211.1c4.8-4.7 4.8-12.3.1-17z" fill="currentColor"></path>
                        <path :class="{ 'hidden': ! isOpened }" d="M4.465 366.475l7.07 7.071c4.686 4.686 12.284 4.686 16.971 0L224 178.053l195.494 195.493c4.686 4.686 12.284 4.686 16.971 0l7.07-7.071c4.686-4.686 4.686-12.284 0-16.97l-211.05-211.051c-4.686-4.686-12.284-4.686-16.971 0L4.465 349.505c-4.687 4.686-4.687 12.284 0 16.97z" fill="currentColor"></path>
                    </svg>
                </span>
            </h3>
        </div>
        <div :class="{
                        'rounded-b-lg': isLast,
                        'h-auto py-1 px-2 border': isOpened,
                        'h-0 p-0 border-none': ! isOpened
                     }"
              class="accordion-content">
            <slot name="content"></slot>
        </div>
    </div>
</template>
<script>
export default {
    name: 'AccordionGroup',
    props: {
        uniqueId: String,
        isFirst: Boolean,
        isLast: Boolean
    },
    data() {
        return {
            isOpened: false
        }
    },
    mounted() {
        this.isOpened = this.opened
    },
    computed: {
        uniqueName() {
            return 'accordion-' + this.uniqueId;
        },
        opened: {
            get() {
                if ( !( this.uniqueName in localStorage ) ) {
                    localStorage[ this.uniqueName ] = false;
                }
                return localStorage[ this.uniqueName ] === 'true' || localStorage[ this.uniqueName ] === true;
            },
            set( val ) {
                val = val === 'true' || val === true;
                this.isOpened = val;
                localStorage[ this.uniqueName ] = val;
            }
        }
    }
}
</script>
