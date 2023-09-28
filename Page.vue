<template>
    <div>
        <AccordionWrapper>
            <template #groups>
                <AccordionGroup is-first :unique-id="<UNIQUE ID FOR THIS GROUP [STRING]>">
                    <template #header>
                        Header 1
                    </template>
                    <template #content>
                        Content 1
                    </template>
                </AccordionGroup>

                <AccordionGroup is-last :unique-id="<UNIQUE ID FOR THIS GROUP [STRING]>">
                    <template #header>
                        Header 2
                    </template>
                    <template #content>
                        Content 2
                    </template>
                </AccordionGroup>
            </template>
        </AccordionWrapper>
    </div>
</template>

<script>
import AccordionWrapper   from "@/Components/AccordionWrapper";
import AccordionGroup     from "@/Components/AccordionGroup";

export default {
    name: 'Page',
    components: {
        AccordionGroup,
        AccordionWrapper,
    }
}
</script>
