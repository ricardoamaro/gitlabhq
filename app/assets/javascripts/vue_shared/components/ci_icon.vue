<script>
  import { statusIconEntityMap } from '../ci_status_icons';

  /**
   * Renders CI icon based on API response shared between all places where it is used.
   *
   * Receives status object containing:
   * status: {
   *   details_path: "/gitlab-org/gitlab-ce/pipelines/8150156" // url
   *   group:"running" // used for CSS class
   *   icon: "icon_status_running" // used to render the icon
   *   label:"running" // used for potential tooltip
   *   text:"running" // text rendered
   * }
   *
   * Used in:
   * - Pipelines table Badge
   * - Pipelines table mini graph
   * - Pipeline graph
   * - Pipeline show view badge
   * - Jobs table
   * - Jobs show view header
   * - Jobs show view sidebar
   */
  export default {
    props: {
      status: {
        type: Object,
        required: true,
      },
    },

    computed: {
      statusIconSvg() {
        return statusIconEntityMap[this.status.icon];
      },

      cssClass() {
        const status = this.status.group;
        return `ci-status-icon ci-status-icon-${status} js-ci-status-icon-${status}`;
      },
    },
  };
</script>
<template>
  <span
    :class="cssClass"
    v-html="statusIconSvg">
  </span>
</template>
