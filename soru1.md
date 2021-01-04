

```SQL
  with tabular_form as (
select name, car.id as car_id ,car.model as car_model ,fact.year as manufacture_year,purchase
from ilhan_sozer.semi_structured_hw
cross join unnest(car) as car
cross join unnest(manufacture) as fact
on car.id = fact.id
)
select name, car_id,
car_model,
manufacture_year,
array(select as struct p.* replace((TIMESTAMP_ADD(p.date, INTERVAL 3 HOUR)) as date) from unnest(purchase) as p) as purchase
from tabular_form;

```
