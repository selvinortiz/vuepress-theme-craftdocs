<template>
    <div class="code-toggle">
        <ul class="code-language-switcher" v-if="!usePageToggle">
            <li v-for="language in languages">
                <a :class="{ active: language === selectedLanguage }" @click="setLanguage(language)">{{ $site.themeConfig.codeLanguages[language] }}</a>
            </li>
        </ul>
        <div v-for="language in languages">
            <slot :name="language" v-if="language == (usePageToggle ? $store.state.codeLanguage : selectedLanguage)"/>
        </div>
    </div>
</template>

<script>
    export default {
        props: ['languages'],

        data() {
            return {
                selectedLanguage: this.languages[0]
            }
        },

        computed: {
            usePageToggle() {
                return this.$page.frontmatter.split && this.$page.frontmatter.code
            }
        },

        methods: {
            setLanguage(language) {
                this.selectedLanguage = language
            }
        }
    }
</script>
