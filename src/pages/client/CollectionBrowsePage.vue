<template>
  <div class="browse-page grid-container full">
    <div>
      <header-section />
    </div>
    <div class="search grid-x flexible">
      <div class="cell grid-sidebar" v-if="isFilterVisible">
        <search-grid-filter isCollectionsPage="true"
                            :provider="provider"
                            @onSearchFilterChanged="onSearchFormSubmit"/>
      </div>
      <div class="cell search-grid-ctr">
        <search-grid-form @onSearchFormSubmit="onSearchFormSubmit"
                          searchBoxPlaceholder="Search this collection" />
        <search-grid v-if="query.provider"
                     :query="query"
                     :searchTerm="providerName"
                     @onLoadMoreImages="onLoadMoreImages"></search-grid>
      </div>
    </div>
    <footer-section></footer-section>
  </div>
</template>

<script>
import FooterSection from '@/components/FooterSection';
import HeaderSection from '@/components/HeaderSection';
import SearchGrid from '@/components/SearchGrid';
import SearchGridForm from '@/components/SearchGridForm';
import SearchGridFilter from '@/components/SearchGridFilter';
import CollectionBrowseMixin from '@/pages/mixins/CollectionBrowseMixin';

const CollectionBrowsePage = {
  components: {
    HeaderSection,
    SearchGridForm,
    SearchGridFilter,
    SearchGrid,
    FooterSection,
  },
  mixins: [CollectionBrowseMixin],
};

export default CollectionBrowsePage;
</script>

<style lang="scss" scoped>
  .search-grid {
    margin: 30px 30px 60px 30px;
  }

  .search-grid-ctr {
    background: #e9ebee;
    min-height: 600px;
    margin: 0;
    transition: margin .7s ease-in-out;
    flex: 1 1 0px;

    /* 48em = 768px */
    @media (max-width: 49em) {
      width: 100%;
      flex: none;
    }
  }

  .search-grid-ctr__filter-visible {
    margin-top: 30px;
  }

  .grid-sidebar {
    width: 350px;

    /* 48em = 768px */
    @media (max-width: 49em) {
      width: 100%;
    }
  }
</style>
