<template>
    <li>
        <div>
            <strong><router-link :to="`/brigade/${project.brigade_slug}`">{{ project.brigade }}</router-link>:</strong> <router-link :to="`/project/${project.brigade_slug}/${project.slug}`">{{project.name}}</router-link>

        </div>
        <div class="project-description" v-if="project.description">
            {{ project.description }} 
        </div>
        <div class='other-topics'>
            <span v-for="(t,index) in  other_topics(project.topics)" v-bind:key="index">
                <strong v-if="index == 0">Other topics:</strong>
                <span v-if="index > 0">,</span>
                <router-link :to="`/topics/${normalize(t)}`">
                    {{ t }}
                </router-link>
            </span>
        </div>
        <div class="links" v-if="project.link_url">
            <strong>Project:</strong> <a v-bind:href="project.link_url">{{ project.link_url }}</a>
        </div>
        <div class="links" v-if="project.code_url">
             <i class="fa fa-github"></i> <strong>Code:</strong> <a v-bind:href="project.code_url">{{ project.code_url }}</a>
        </div>
        <div class="metrics">
            <span class="passed-metric" v-if="project.topics" :title="project.topics">
                <i class="fa fa-check"></i> topics
            </span>
            <span class="passed-metric" v-if="project.description" :title="project.description">
                <i class="fa fa-check"></i> description
            </span>
        </div>
        <router-link :to="`/project/${project.brigade_slug}/${project.slug}`" class="badge badge-primary">Improve your project's visibility and impact</router-link>
    </li>
</template>

<script>
import slugify from '../utils.js'

export default {
    props: ['project'] ,
    methods: {
        other_topics(topics){
            return _.filter(topics, t => t != this.topic);
        },
        normalize(topic) {
            return slugify(topic)
        }
    }
}
</script>

<style scoped>
    .project-description {
        margin-top: 0.5em;
        font-style: italic;
    }
    
    .metrics {
        margin: 10px 0 0 0;
    }
</style>