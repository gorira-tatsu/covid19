<template>
  <v-col cols="12" md="6" class="DataCard">
    <client-only>
      <data-view
        :title="$t('検査陽性者の状況')"
        :title-id="'details-of-confirmed-cases'"
        :date="date"
      >
        <template v-slot:additionalDescription>
          <span>{{ $t('（注）') }}</span>
          <ul>
            <li>
              {{ $t('チャーター機帰国者、クルーズ船乗客等は含まれていない') }}
            </li>
            <!--<li>
              {{
                $t(
                  '「重症」は、人工呼吸器管理（ECMOを含む）が必要な患者数を計上。'
                )
              }}
              <app-link
                to="https://www.bousai.metro.tokyo.lg.jp/_res/projects/default_project/_page_/001/011/435/7kai/202008207.pdf"
              >
                {{ $t('重症基準の考え方はこちら') }}
              </app-link>
            </li>
            <li>
              {{
                $t(
                  '退院者数の把握には一定の期間を要しており、確認次第数値を更新している'
                )
              }}
            </li>-->
          </ul>
        </template>
        <confirmed-cases-details-table
          :aria-label="$t('検査陽性者の状況')"
          v-bind="confirmedCases"
        />
        <!--<div>
          <app-link
            :class="$style.button"
            to="https://www.fukushihoken.metro.tokyo.lg.jp/iryo/kansen/shibou.html"
          >
            {{ $t('死亡日別による死亡者数の推移はこちら') }}
          </app-link>
        </div>-->
        <template v-slot:footer>
          <open-data-link
            :url="'http://open-data.pref.hyogo.lg.jp/?page_id=141'"
          />
        </template>
      </data-view>
    </client-only>
  </v-col>
</template>

<script>
// import dayjs from 'dayjs'

// import AppLink from '@/components/AppLink.vue'
import ConfirmedCasesDetailsTable from '@/components/ConfirmedCasesDetailsTable.vue'
import DataView from '@/components/DataView.vue'
import OpenDataLink from '@/components/OpenDataLink'
// import Data from '@/data/data.json'
import mainSummary from '@/data/main_summary.json'
import formatConfirmedCases from '@/utils/formatConfirmedCases'

export default {
  components: {
    DataView,
    ConfirmedCasesDetailsTable,
    // AppLink,
    OpenDataLink,
  },
  data() {
    // const mainSummary = Data.main_summary
    // 検査陽性者の状況
    const confirmedCases = formatConfirmedCases(mainSummary)

    // const date = dayjs(mainSummary.children[0].date).format('YYYY/MM/DD HH:mm')
    const date = mainSummary.last_update

    return {
      confirmedCases,
      date,
    }
  },
}
</script>

<style lang="scss" module>
.button {
  margin: 20px 0 0;
  color: $blue-1 !important;
  &:hover {
    color: $white !important;
  }

  @include button-text('sm');
}
</style>
