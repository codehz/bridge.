<template>
    <v-dialog
        v-model="is_menu_open"
        :max-width="is_fullscreen ? 2000 : 500"
    >
        <v-card>
            <v-system-bar @dblclick.native="is_fullscreen = !is_fullscreen" height="30px" style="padding-right: 0;">
                <span class="px14-font">Extensions</span>
                <v-spacer></v-spacer>
                <v-toolbar-items>
                    <v-btn small icon @click.stop="is_fullscreen = !is_fullscreen">
                        <v-icon small>mdi-plus</v-icon>
                    </v-btn>
                    <v-divider vertical/>
                    <v-btn color="error" small icon @click.stop="is_menu_open = false">
                        <v-icon small>mdi-close</v-icon>
                    </v-btn>
                </v-toolbar-items>
            </v-system-bar>            

            <v-card-text :style="`max-height: ${window_height * 0.75}px; height: ${is_fullscreen ? window_height * 0.75 : 500}px; overflow-y: auto;`">
                <plugin-list v-if="filter != 'web'" :plugins="plugins" :filter="filter" :is_fullscreen="is_fullscreen"></plugin-list>
                <web-plugins v-else :is_fullscreen="is_fullscreen" :plugins="web_plugins" :installed_plugins="plugins"></web-plugins>
            </v-card-text>

            <v-card-actions>
                <v-bottom-navigation
                    v-model="filter"
                    :value="true"
                   
                >
                    <v-btn text value="active">
                        <span>Active</span>
                        <v-icon>mdi-bookmark</v-icon>
                    </v-btn>

                    <v-btn text value="available">
                        <span>Available</span>
                        <v-icon>mdi-apps</v-icon>
                    </v-btn>

                    <v-btn text value="web">
                        <span>Web</span>
                        <v-icon>mdi-cloud</v-icon>
                    </v-btn>
                </v-bottom-navigation>
            </v-card-actions>
        </v-card>
    </v-dialog>
</template>

<script>
import PluginList from "./PluginList";
import WebPlugins from "./WebPlugins";

export default {
    name: "plugin-install-main",
    components: {
        PluginList,
        WebPlugins
    },
    data() {
        return {
            is_fullscreen: false,
            filter: "active",
            web_plugins: undefined,
            window_height: window.innerHeight
        }
    },
    mounted() {
        fetch("https://solveddev.github.io/bridge-plugins/plugins.json")
            .then(data => data.json())
            .then(obj => this.web_plugins = obj)
            .catch(err => err ? console.warn(err) : null)
    },
    computed: {
        is_menu_open: {
            set(val) {
                this.$store.commit("setPluginMenuOpen", val)
            },
            get() {
                return this.$store.state.Plugins.is_menu_open;
            }
        },

        plugins() {
            return this.$store.state.Plugins.installed_plugins;
        }
    },

    created() {
        window.addEventListener("resize", this.on_resize);
    },
    destroyed() {
        window.removeEventListener("resize", this.on_resize);
    },
    methods: {
        on_resize() {
            this.window_height = window.innerHeight;
        }
    }
}
</script>

<style scoped>
    .window-title {
        margin-left: 8px;
        cursor: default;
    }
    .v-card__title {
        padding: 0;
    }
    .v-card__actions {
        padding: 0;
    }
</style>
