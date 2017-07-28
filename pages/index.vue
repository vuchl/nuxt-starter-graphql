<template>
  <section class="container" style="display: flex; flex-wrap: wrap; flex-direction: row">
    <pre>
      <h3>allArtistsQuery</h3>
      <code>
        {{artists}}
      </code>
    </pre>
    <pre>
      <h3>allReleasesQuery</h3>
      <code>
        {{releases}}
      </code>
    </pre>
    <pre style="display: flex; flex-direction: column;">
      <div style="width: 100%; height: 50%; overflow: scroll">
        <h3>latestRelease (by createdAt)</h3>
        <code>
          {{latestCreatedRelease}}
        </code>
      </div>
      <div style="width: 100%; height: 50%; overflow: scroll">
        <h3>latestRelease (by updatedAt)</h3>
        <code>
          {{latestUpdatedRelease}}
        </code>
      </div>
    </pre>
  </section>
</template>

<script>
import allArtistsQuery from '~/queries/allArtists.gql'
import allReleasesQuery from '~/queries/allReleases.gql'
import latestReleaseByCreatedAtQuery from '~/queries/latestCreatedRelease.gql'
import latestReleaseByUpdatedAtQuery from '~/queries/latestUpdatedRelease.gql'

export default {
  apollo: {
    artists: {
      query: allArtistsQuery,
      prefetch: true
    },
    releases: {
      query: allReleasesQuery,
      prefetch: false
    },
    latestCreatedReleaseArray: {
      query: latestReleaseByCreatedAtQuery,
      prefetch: true
    },
    latestUpdatedReleaseArray: {
      query: latestReleaseByUpdatedAtQuery,
      prefetch: false
    }
  },
  computed: {
    latestUpdatedRelease () {
      return this.latestUpdatedReleaseArray[0] || {}
    },
    latestCreatedRelease () {
      return this.latestCreatedReleaseArray[0] || {}
    }
  }
}
</script>

<style>
pre {
  width: 33%;
  height: 400px;
  overflow: scroll;
}
.container
{
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
.title
{
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}
.subtitle
{
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}
.links
{
  padding-top: 15px;
}
</style>
