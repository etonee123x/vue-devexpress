<template>
  <div>
    <DxDataGrid
      v-if="dataSource"
      :show-borders="true"
      :allow-column-reordering="true"
      :data-source="dataSource"
    >
      <template #cellTemplate="{ data }">
        <a target="_blank"
           :href="'https://ec-crm.ru/orders/filter_template?orders_numbers='+data.value"
        >
          {{data.value}}
        </a>
      </template>
      <DxColumn
        data-field="order_number"
        caption="Номер заказа"
        cell-template="cellTemplate"
      />
      <DxColumn
        name="month"
        data-field="month"
        caption="Месяц"
      />
      <DxColumn
        data-field="created_day"
        caption="День"
        sort-order="desc"
      />
      <DxColumn
        data-field="created_time"
        caption="День"
        sort-order="desc"
      />
      <DxColumn
        data-field="name"
        caption="Менеджер"
      />
      <DxColumn
        data-field="shop_title"
        caption="Магазин"
      />
      <DxColumn
        data-field="order_status_title"
        caption="Статус"
      />
      <DxColumn
        data-field="otkaz_title"
        caption="Причина отказа"
      />
      <DxColumn
        data-field="email"
        caption="Емейл"
      />
      <DxColumn
        data-field="phone_key"
        caption="Телефон"
      />
      <DxColumn
        data-field="courier"
        caption="Курьер"
      />
      <DxColumn
        data-field="samovivoz"
        caption="Самовывоз"
      />
      <DxColumn
        data-field="order_sum"
        caption="Сумма заказа"
      >
        <dx-format
          type="currency"
          currency="RUB"
        />
      </DxColumn>
      <DxGroupPanel :visible="true"/>
      <DxSearchPanel :visible="true"/>
      <DxGrouping
        expand-mode="rowClick"
        :auto-expand-all="false"
      />
      <DxPaging :page-size="10"/>
      <DxPager
        :show-page-size-selector="true"
        :allowed-page-sizes="[10, 25, 50, 100]"
      ></DxPager>
      <DxSummary>
        <DxGroupItem
          column="order_number"
          summary-type="count"
          show-in-column="month"
          :customize-text="numberWithCommas"
          :show-in-group-footer="false"
          :align-by-column="true"
        />
        <DxGroupItem
          column="order_sum"
          summary-type="sum"
          :show-in-group-footer="false"
          :align-by-column="true"
          :customize-text="numberWithCommas"
        />
        <DxTotalItem
          column="order_number"
          summary-type="count"
        />
      </DxSummary>
      <DxSortByGroupSummaryInfo summary-item=""/>
    </DxDataGrid>
  </div>
</template>

<script>
import {
  DxDataGrid,
  DxColumn,
  DxGrouping,
  DxGroupPanel,
  DxSearchPanel,
  DxPaging,
  DxFormat,
  DxPager,
  DxSummary,
  DxGroupItem,
  DxSortByGroupSummaryInfo,
  DxTotalItem,

} from 'devextreme-vue/data-grid';
import { locale, loadMessages } from 'devextreme/localization';
import ruMessages from 'devextreme/localization/messages/ru.json';

const numberWithCommas = (x, text) => {
  const formatted = x.value.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ' ');
  return text ? `${text} ${formatted}` : formatted;
};

export default {
  name: 'ordersTable',
  components: {
    DxColumn,
    DxGroupPanel,
    DxGrouping,
    DxPaging,
    DxSearchPanel,
    DxDataGrid,
    DxFormat,
    DxPager,
    DxSummary,
    DxGroupItem,
    DxSortByGroupSummaryInfo,
    DxTotalItem,

  },
  created() {
    loadMessages(ruMessages);
    locale('ru');
  },
  props: [
    'dataSource',
  ],
  methods: {
    numberWithCommas(x) {
      const text = x.value.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ' ');
      // return {
      //   count: () => `Кол-во: ${text}`,
      //   sum: () => (text.length ? `Сумма: ${text}` : ''),
      //   avg: () => `Средн:: ${text}`,
      // };
      return `${text} cd`;
    },
  },
};
</script>

<style scoped>

</style>