---
title: Weekly Sales by State
---

<Details title='Weekly Sales by State'>

  This page shows weekly sales data by State. Use the dropdowns to filter by category and year.
</Details>

```sql states
  select
      state
  from needful_things.orders
  group by state
```

<Dropdown data={states} name=state value=state multiple=true selectAllByDefault=true>
</Dropdown>

```sql orders_by_state
  select 
      date_trunc('week', order_datetime) as week,
      sum(sales) as sales_usd,
      state
  from needful_things.orders
  where state IN ${inputs.state.value}
  group by all
  order by week desc
```

<BarChart
    data={orders_by_state}
    title="Sales by State, {inputs.state.label}"
    x=week
    y=sales_usd
    series=state
/>
