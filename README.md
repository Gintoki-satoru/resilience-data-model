*Insert UML here*
# Resilience Data Model
|SME type <br> idShort|Description|
|:----|:----|
|[SMC] <br> Employee|Models characteristics of the employee|
|[SMC] <br> Incidents|Models characteristics of incidents, past or simulated|
|[SMC] <br> Resources|Models characteristics of assets, namely, transport systems, storage systems, and machines|
|[SMC] <br> Shopfloor|Models characteristics of the shopfloor, starting with the production plan, the working order and the operation|
|[SMC] <br> Supply Chain|Models characteristics of the supply chain|

## SMC Employee
|SME type <br> idShort|Description|
|:----|:----|
|[property] <br> employee_id|UID of an employee|
|[file] <br> competences|The competence matrix of an employee|
|[file] <br> certificates|The certificates matrix of an employee|
|[file] <br> shiftplan|The shiftplan matrix of an employee|
|[range] <br> status|The status of an employee [free, working, sick, leave, break]|
|[file] <br> responsibilities|The responsibilities of an employee, e.g. machine, process|

## SMC Incidents
|SME type <br> idShort|Description|
|:----|:----|
|[property] <br> Incident_id|UID of incident|
|[ref] <br> resources|Resources_id involved in the incident|
|[property] <br> creation_date|Start date of incident|
|[property] <br> finishing_date|Finish date of incident|
|[ref] <br> fixer|Employee_id of fixing employee|
|[property] <br> severity|Severity of incident|
|[property] <br> failure_cost|Failure cost of incident|
|[ref] <br> operator|Employee_id of operators during incidents|
|[range] <br> status|Status of incident [solved, unsolved]|
|[property] <br> due_date|Due date when incident is finished|
|[SMC] <br> Scenario|Description of scenarios|
|[SMC] <br> Variability|Description of scenario variables|
|[SMC] <br> Diagnosis_Result|Description of results of diagnoses|

### DiagnosisResult
| **SME type** <br> **idShort**     | **Description**                       |
|:----------------------------------|:--------------------------------------|
| **[property]** <br> `diagnosis_id`| UID of diagnosis                      |
| **[property]** <br> `KPI`         | KPIs of diagnosis                     |
| **[file]** <br> `reports`         | Reports about the diagnosis           |

### Scenario
| **SME type** <br> **idShort**          | **Description**                             |
|:--------------------------------------|:--------------------------------------------|
| **[property]** <br> `scenario_id`      | UID of scenarios                            |
| **[property]** <br> `penalty`         | Penalty of Scenario                         |
| **[property]** <br> `penalty_description` | Description of penalty                     |
| **[property]** <br> `scenario_probability` | Probability of scenario                    |
| **[property]** <br> `scenario_master_plan` | Master plan of scenario                    |

### Variability
| **SME type** <br> **idShort**          | **Description**                             |
|:--------------------------------------|:--------------------------------------------|
| **[property]** <br> `variable`        | Description of variable                     |
| **[property]** <br> `statistical_variability` | Statistical variability of variable |
| **[property]** <br> `distribution`    | Distribution of variable                    |

## Shopfloor
| **SME type** <br> **idShort**       | **Description**                           |
|:-----------------------------------|:------------------------------------------|
| **[SMC]** <br> `ProductionPlan`     | Contents of production plans              |

### Production_Plan
| **SME type** <br> **idShort**       | **Description**                           |
|:-----------------------------------|:------------------------------------------|
| **[SMC]** <br> `Working_Order`     | List of working orders                    |

#### WorkingOrder
| **SME type** <br> **idShort**           | **Description**                                 |
|:---------------------------------------|:------------------------------------------------|
| **[property]** <br> `working_order_id`  | UID of working order                           |
| **[ref]** <br> `incidences`             | Incidences_id of incidents happening during working order |
| **[property]** <br> `status`            | Status of working order                        |
| **[SMC]** <br> `Operation`              | List of operations needed for the working order |

#### Operation
| **SME type** <br> **idShort**           | **Description**                                 |
|:---------------------------------------|:------------------------------------------------|
| **[property]** <br> `operation_id`      | UID of operation                               |
| **[property]** <br> `setting_time`      | Time to prepare for the working order          |
| **[property]** <br> `operation_time`    | Time needed for operation                      |
| **[property]** <br> `operation_type`    | Type of operation                              |
| **[ref]** <br> `incidences`             | Incidences_id of incidents happening during operation |

## Resource
| **SME type** <br> **idShort**       | **Description**                                 |
|:-----------------------------------|:------------------------------------------------|
| **[SMC]** <br> `Assets`            | General Description of Assets                  |
| **[ref]** <br> `incident`          | Incidence_id of incident of a resource         |

### Asset
| **SME type** <br> **idShort**           | **Description**                                 |
|:---------------------------------------|:------------------------------------------------|
| **[property]** <br> `asset_id`          | UID of the asset                               |
| **[property]** <br> `mttr`              | Mean time to repair                            |
| **[property]** <br> `mtbf`              | Mean time before failure                       |
| **[property]** <br> `failure_rate`      | Failure rate of the asset                      |
| **[property]** <br> `repair_rate`       | Repair rate of asset                           |
| **[SMC]** <br> `Transport_System`       | Description of transport systems               |
| **[SMC]** <br> `Material_Storage_System`| Description of the storage systems             |
| **[SMC]** <br> `Machine`               | Description of the machines                    |

#### TransportSystem
| **SME type** <br> **idShort**           | **Description**                                 |
|:---------------------------------------|:------------------------------------------------|
| **[property]** <br> `transport_system_id` | UID of transport system                        |
| **[property]** <br> `transport_time`     | Time of transport                              |
| **[property]** <br> `routing`            | Route of transport                             |

#### MaterialStorageSystem
| **SME type** <br> **idShort**          | **Description**                             |
|:--------------------------------------|:--------------------------------------------|
| **[property]** <br> `storage_id`       | UID of storage system                       |
| **[property]** <br> `available_slots`  | Number of available slots                   |

#### Machine
| **SME type** <br> **idShort**          | **Description**                             |
|:--------------------------------------|:--------------------------------------------|
| **[property]** <br> `machine_id`       | UID of machine                              |
| **[property]** <br> `critical_components` | List of critical components                |
| **[property]** <br> `execution_state`  | Current execution state of machine          |
| **[property]** <br> `tool_lifetime`    | Lifetime of current tool                    |
| **[ref]** <br> `machine_diagnosis`     | Diagnosis_id of machine                     |

## SupplyChain
| **SME type** <br> **idShort**           | **Description**                              |
|:---------------------------------------|:---------------------------------------------|
| **[SMC]** <br> `Logistics`             | Description of logistics                     |
| **[SMC]** <br> `Market_analysis`       | Main metrics of the market                   |
| **[SMC]** <br> `Production_site`       | Main metrics of the production site          |
| **[ref]** <br> `incident`              | Incidence_id of incidents in the supply chain |

### Logistics
| **SME type** <br> **idShort**            | **Description**                             |
|:----------------------------------------|:--------------------------------------------|
| **[property]** <br> `transportation_id`  | UID of transportation                       |
| **[property]** <br> `transportation_capacity` | Capacity of transportation                |
| **[property]** <br> `transportation_cost` | Cost of transportation                    |

### MarketAnalysis
| **SME type** <br> **idShort**               | **Description**                               |
|:-------------------------------------------|:----------------------------------------------|
| **[property]** <br> `demand_quantity`       | Quantity of demand                            |
| **[property]** <br> `product_price`         | Price of product                              |
| **[property]** <br> `supply_market_capacity`| Capacity of the supply market                 |
| **[property]** <br> `supply_market_price`   | Price at the supply market                    |

### ProductionSite
| **SME type** <br> **idShort**              | **Description**                               |
|:------------------------------------------|:----------------------------------------------|
| **[property]** <br> `site_id`              | UID of production site                        |
| **[property]** <br> `productivity`         | Price of product                              |
| **[property]** <br> `operational_cost`     | Capacity of the supply market                 |
| **[property]** <br> `energy_cost`          | Price at the supply market                    |
| **[property]** <br> `inventory_capacity`   | Capacity of Inventory                         |
| **[property]** <br> `inventory_cost`       | Cost of inventory                             |

