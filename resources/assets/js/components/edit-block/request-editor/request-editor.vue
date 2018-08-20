<template>
    <div class="request-editor">
        <div class="columns is-multiline is-desktop" v-if="request">
            <div class="column is-full-desktop is-7-widescreen">
                <div class="card current-route is-fullwidth">
                    <header class="card-header">
                        <p class="card-header-title">Headers</p>
                    </header>
                    <vm-headers :headers="request.headers"
                                @updated="request.headers = $arguments[0]"
                    ></vm-headers>
                </div>
                <div class="card current-route is-fullwidth">
                    <header class="card-header">
                        <p class="card-header-title">Data</p>
                    </header>
                    <vm-json-editor :json="request.body"
                                    style="height: 300px"
                                    @changed="request.body = $arguments[0], changed = true"
                    ></vm-json-editor>
                </div>
            </div>
            <div class="column is-full-desktop is-5-widescreen">
                <vm-route-info></vm-route-info>
            </div>
        </div>
    </div>
</template>

<script>
    import vmJsonEditor from '../../json-editor/json-editor.vue'
    import vmRouteInfo from './route-info.vue'
    import vmHeaders from './headers/headers.vue'

    import vmNavigationTabs from '../../ligth-components/navigation-tabs.vue'

    import requestEditorData from './request-editor-data.js'


    export default {
        data: () => requestEditorData,
        components: {
            vmJsonEditor,
            vmHeaders,
            vmRouteInfo,
            vmNavigationTabs,
        },
        vuex: {
            getters: {
                mode: state => state.request.mode,
            },
            actions: {
                setMode: ({dispatch}, mode) => dispatch('SET_EDITOR_MODE', mode)
            }
        },
    }
</script>

<style scoped>
    .request-editor {
        padding-bottom: 10px;
    }
</style>