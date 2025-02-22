<!--
Copyright 2020 DigitalOcean

This code is licensed under the MIT License.
You may obtain a copy of the License at
https://github.com/digitalocean/nginxconfig.io/blob/master/LICENSE or https://mit-license.org/

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and / or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions :

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
-->

<template>
    <div>
        <div class="field is-horizontal">
            <div class="field-label">
                <label class="label">{{ i18n.templates.globalSections.performance.gzipCompression }}</label>
            </div>
            <div class="field-body">
                <div class="field">
                    <div :class="`control${gzipCompressionChanged ? ' is-changed' : ''}`">
                        <div class="checkbox">
                            <PrettyCheck v-model="gzipCompression" class="p-default p-curve p-fill p-icon">
                                <i slot="extra" class="icon fas fa-check"></i>
                                {{ i18n.templates.globalSections.performance.enableGzipCompression }}
                            </PrettyCheck>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div class="field is-horizontal">
            <div class="field-label">
                <label class="label">{{ i18n.templates.globalSections.performance.brotliCompression }}</label>
            </div>
            <div class="field-body">
                <div class="field">
                    <div :class="`control${brotliCompressionChanged ? ' is-changed' : ''}`">
                        <div class="checkbox">
                            <PrettyCheck v-model="brotliCompression" class="p-default p-curve p-fill p-icon">
                                <i slot="extra" class="icon fas fa-check"></i>
                                {{ i18n.templates.globalSections.performance.enableBrotliCompression }}
                            </PrettyCheck>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div class="field is-horizontal">
            <div class="field-label">
                <label class="label">{{ i18n.templates.globalSections.performance.expirationForAssets }}</label>
            </div>
            <div class="field-body">
                <div class="field">
                    <div :class="`control${assetsExpirationChanged ? ' is-changed' : ''}`">
                        <input v-model="assetsExpiration"
                               class="input"
                               type="text"
                               :placeholder="$props.data.assetsExpiration.default"
                        />
                    </div>
                </div>
            </div>
        </div>

        <div class="field is-horizontal">
            <div class="field-label">
                <label class="label">{{ i18n.templates.globalSections.performance.expirationForMedia }}</label>
            </div>
            <div class="field-body">
                <div class="field">
                    <div :class="`control${mediaExpirationChanged ? ' is-changed' : ''}`">
                        <input v-model="mediaExpiration"
                               class="input"
                               type="text"
                               :placeholder="$props.data.mediaExpiration.default"
                        />
                    </div>
                </div>
            </div>
        </div>

        <div class="field is-horizontal">
            <div class="field-label">
                <label class="label">{{ i18n.templates.globalSections.performance.expirationForSvgs }}</label>
            </div>
            <div class="field-body">
                <div class="field">
                    <div :class="`control${svgExpirationChanged ? ' is-changed' : ''}`">
                        <input v-model="svgExpiration"
                               class="input"
                               type="text"
                               :placeholder="$props.data.svgExpiration.default"
                        />
                    </div>
                </div>
            </div>
        </div>

        <div class="field is-horizontal">
            <div class="field-label">
                <label class="label">{{ i18n.templates.globalSections.performance.expirationForFonts }}</label>
            </div>
            <div class="field-body">
                <div class="field">
                    <div :class="`control${fontsExpirationChanged ? ' is-changed' : ''}`">
                        <input v-model="fontsExpiration"
                               class="input"
                               type="text"
                               :placeholder="$props.data.fontsExpiration.default"
                        />
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import PrettyCheck from 'pretty-checkbox-vue/check';
    import i18n from '../../i18n';
    import delegatedFromDefaults from '../../util/delegated_from_defaults';
    import computedFromDefaults from '../../util/computed_from_defaults';

    const defaults = {
        gzipCompression: {
            default: true,
            enabled: true,
        },
        brotliCompression: {
            default: false,
            enabled: true,
        },
        assetsExpiration: {
            default: '7d',
            enabled: true,
        },
        mediaExpiration: {
            default: '7d',
            enabled: true,
        },
        svgExpiration: {
            default: '7d',
            enabled: true,
        },
        fontsExpiration: {
            default: '7d',
            enabled: true,
        },
    };

    export default {
        name: 'GlobalPerformance',                                      // Component name
        display: i18n.templates.globalSections.performance.performance, // Display name for tab
        key: 'performance',                                             // Key for data in parent
        delegated: delegatedFromDefaults(defaults),                     // Data the parent will present here
        components: {
            PrettyCheck,
        },
        props: {
            data: Object,                                               // Data delegated back to us from parent
        },
        data () {
            return {
                i18n,
            };
        },
        computed: computedFromDefaults(defaults, 'performance'),        // Getters & setters for the delegated data
    };
</script>
