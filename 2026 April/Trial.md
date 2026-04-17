## Part 1 : Data Migration and Processing

### GSP860 : Migrating On-premises MySQL Using a Continuous Database Migration Service Job
```
gcloud services enable datamigration.googleapis.com --quiet
gcloud services enable servicenetworking.googleapis.com --quiet
```
```
curl -O https://raw.githubusercontent.com/PerkVerse/google-cloud-arcade/refs/heads/main/2026/April%202026/Sprint2/lab1.sh
sudo chmod +x lab1.sh
./lab1.sh
```

### GSP647 : Configuring IAM Permissions with gcloud
```
export ZONE=$(gcloud compute project-info describe \
--format="value(commonInstanceMetadata.items[google-compute-default-zone])")
gcloud compute ssh centos-clean --zone=$ZONE --quiet
```
```
curl -O https://raw.githubusercontent.com/PerkVerse/google-cloud-arcade/refs/heads/main/2026/April%202026/Sprint2/lab2.sh
sudo chmod +x lab2.sh
./lab2.sh
```
```
echo -n "Enter PROJECTID2: "
read PROJECTID2
if [[ -z "$PROJECTID2" ]]; then
echo "ERROR: PROJECTID2 cannot be empty"
exit 1
fi
gcloud config set project $PROJECTID2
gcloud iam service-accounts create instance-admin-sa 
--display-name "Instance Admin SA" || true
export SA=instance-admin-sa@$PROJECTID2.iam.gserviceaccount.com
```

### GSP212 : VPC Flow Logs - Analyzing Network Traffic
```
curl -O https://raw.githubusercontent.com/PerkVerse/google-cloud-arcade/refs/heads/main/2026/April%202026/Sprint2/lab3.sh
sudo chmod +x lab3.sh
./lab3.sh
```

### GSP185 : App Dev: Storing Image and Video Files in Cloud Storage - Python
```
curl -O https://raw.githubusercontent.com/PerkVerse/google-cloud-arcade/refs/heads/main/2026/April%202026/Sprint2/lab4.sh
sudo chmod +x lab4.sh
./lab4.sh
```

## 2. Access, Monitoring, and Analytics

### GSP050 : Working with Cloud Dataprep on Google Cloud
```
Manual LAB
```

### GSP932 : Creating dynamic SQL derived tables with LookML and Liquid

### create view user_facts :
```
view: user_facts {
  derived_table: {
    sql: SELECT
           order_items.user_id AS user_id
          ,COUNT(distinct order_items.order_id) AS lifetime_order_count
          ,SUM(order_items.sale_price) AS lifetime_revenue
          ,MIN(order_items.created_at) AS first_order_date
          ,MAX(order_items.created_at) AS latest_order_date
          FROM cloud-training-demos.looker_ecomm.order_items
          WHERE {% condition select_date %} order_items.created_at {% endcondition %}
          GROUP BY user_id;;
  }
  
  filter: select_date {
    type: date
    suggest_explore: order_items
    suggest_dimension: order_items.created_date
  }

  measure: count {
    hidden: yes
    type: count
    drill_fields: [detail*]
  }

  dimension: user_id {
    primary_key: yes
    type: number
    sql: ${TABLE}.user_id ;;
  }

  dimension: lifetime_order_count {
    type: number
    sql: ${TABLE}.lifetime_order_count ;;
  }

  dimension: lifetime_revenue {
    type: number
    sql: ${TABLE}.lifetime_revenue ;;
  }

  measure: average_lifetime_revenue {
    type: average
    sql: ${TABLE}.lifetime_revenue ;;
  }


  measure: average_lifetime_order_count {
    type: average
    sql: ${TABLE}.lifetime_order_count ;;
  }

  dimension_group: first_order_date {
    type: time
    sql: ${TABLE}.first_order_date ;;
  }

  dimension_group: latest_order_date {
    type: time
    sql: ${TABLE}.latest_order_date ;;
  }

  set: detail {
    fields: [user_id, lifetime_order_count, lifetime_revenue, first_order_date_time, latest_order_date_time]
  }
}
```
### Update training_ecommerce File
```
connection: "bigquery_public_data_looker"

# include all the views
include: "/views/*.view"
include: "/z_tests/*.lkml"
include: "/**/*.dashboard"

datagroup: training_ecommerce_default_datagroup {
  # sql_trigger: SELECT MAX(id) FROM etl_log;;
  max_cache_age: "1 hour"
}

persist_with: training_ecommerce_default_datagroup

label: "E-Commerce Training"

explore: order_items {

  join: user_facts {
    type: left_outer
    sql_on: ${order_items.user_id} = ${user_facts.user_id};;
    relationship: many_to_one
  }

  join: users {
    type: left_outer
    sql_on: ${order_items.user_id} = ${users.id} ;;
    relationship: many_to_one
  }

  join: inventory_items {
    type: left_outer
    sql_on: ${order_items.inventory_item_id} = ${inventory_items.id} ;;
    relationship: many_to_one
  }

  join: products {
    type: left_outer
    sql_on: ${inventory_items.product_id} = ${products.id} ;;
    relationship: many_to_one
  }

  join: distribution_centers {
    type: left_outer
    sql_on: ${products.distribution_center_id} = ${distribution_centers.id} ;;
    relationship: many_to_one
  }
}

explore: events {
  join: event_session_facts {
    type: left_outer
    sql_on: ${events.session_id} = ${event_session_facts.session_id} ;;
    relationship: many_to_one
  }
  join: event_session_funnel {
    type: left_outer
    sql_on: ${events.session_id} = ${event_session_funnel.session_id} ;;
    relationship: many_to_one
  }
  join: users {
    type: left_outer
    sql_on: ${events.user_id} = ${users.id} ;;
    relationship: many_to_one
  }
}

```

### GSP409 : Explore and Create Reports with Looker Studio
```
Manual LAB
```

### GSP758 : Measuring Speech-to-Text Accuracy
```
Manual LAB
```
