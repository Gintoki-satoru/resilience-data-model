[UML Diagram](ResilienceDataModelUML.drawio)
# Resilience Data Model
|SME type <br> idShort|Description|
|:----|:----|
|[SMC] <br> `Employee`|Models characteristics of the employee|
|[SMC] <br> `Incident`|Models characteristics of incidents, past or simulated|
|[SMC] <br> `Resource`|Models characteristics of assets, namely, transport systems, storage systems, and machines|
|[SMC] <br> `Shopfloor`|Models characteristics of the shopfloor, starting with the production plan, the working order and the operation|
|[SMC] <br> `Supply_Chain`|Models characteristics of the supply chain|
|[SMC] <br> `ResilienceKPI` |Output of the resilience assessment|

## SMC Employee
|SME type <br> idShort|Description|
|:----|:----|
|[property] <br> `employeeId`|UID of an employee|
|[file] <br> `competence`|The competence matrix of an employee|
|[file] <br> `certificates`|The certificates matrix of an employee|
|[file] <br> `shiftplan`|The shiftplan matrix of an employee|
|[range] <br> `status`|The status of an employee [free, working, sick, leave, break]|
|[file] <br> `responsibilities`|The responsibilities of an employee, e.g. machine, process|
## SMC Incident
|SME type <br> idShort|Description|
|:----|:----|
|[property] <br> `IncidentId`|UID of incident|
|[ref] <br> `resource`|Resources_id involved in the incident|
|[property] <br> `creationDate`|Start date of incident|
|[property] <br> `finishingDate`|Finish date of incident|
|[ref] <br> `fixer`|Employee_id of fixing employee|
|[property] <br> `severity`|Severity of incident|
|[property] <br> `failure_cost`|Failure cost of incident|
|[ref] <br> `operator`|Employee_id of operators during incidents|
|[range] <br> `status`|Status of incident [solved, unsolved]|
|[property] <br> `dueDate`|Due date when incident is finished|
|[SMC] <br> `Scenario`|Description of scenarios|
|[SMC] <br> `Variability`|Description of scenario variables|
|[SMC] <br> `DiagnosisResult`|Description of results of diagnoses|

### DiagnosisResult
| **SME type** <br> **idShort**     | **Description**                       |
|:----------------------------------|:--------------------------------------|
| **[property]** <br> `diagnosisId`| UID of diagnosis                      |
| **[property]** <br> `kpi`         | KPIs of diagnosis                     |
| **[file]** <br> `reports`         | Reports about the diagnosis           |

### Scenario
| **SME type** <br> **idShort**          | **Description**                             |
|:--------------------------------------|:--------------------------------------------|
| **[property]** <br> `scenarioId`| UID of scenarios                            |
| **[property]** <br> `penalty`| Penalty of Scenario                         |
| **[property]** <br> `penaltyDescription` | Description of penalty                     |
| **[property]** <br> `scenarioProbability` | Probability of scenario                    |
| **[property]** <br> `scenarioMasterPlan`| Master plan of scenario                    |
| **[SMC]** <br> `Variability`| Variability of scenario                   |

### Variability
| **SME type** <br> **idShort**          | **Description**                             |
|:--------------------------------------|:--------------------------------------------|
| **[property]** <br> `variable`        | Description of variable                     |
| **[property]** <br> `statistical_variability` | Statistical variability of variable |
| **[property]** <br> `distribution`    | Distribution of variable                    |

## Shopfloor
| **SME type** <br> **idShort**       | **Description**                           |
|:-----------------------------------|:------------------------------------------|
| **[SMC]** <br> `ProductionPlan` | Contents of production plans |
| **[ref]** <br> `ProductionSite` | Production Site of Shopfloor |

### Production_Plan
| **SME type** <br> **idShort**       | **Description**                           |
|:-----------------------------------|:------------------------------------------|
| **[SMC]** <br> `WorkingOrder`     | List of working orders                    |
| **[File]** <br> `ShopfloorSchedule`     | Production Schedule for Shopfloor                    |


#### WorkingOrder
| **SME type** <br> **idShort**           | **Description**                                 |
|:---------------------------------------|:------------------------------------------------|
| **[property]** <br> `workingOrderId`| UID of working order                           |
| **[ref]** <br> `incidence`             | Incidences_id of incidents happening during working order |
| **[property]** <br> `status`            | Status of working order                        |
| **[SMC]** <br> `Operation`              | List of operations needed for the working order |

#### Operation
| **SME type** <br> **idShort**           | **Description**                                 |
|:---------------------------------------|:------------------------------------------------|
| **[property]** <br> `operationId`      | UID of operation                               |
| **[property]** <br> `settingTime`      | Time to prepare for the working order          |
| **[property]** <br> `operationTime`    | Time needed for operation                      |
| **[property]** <br> `operationType`    | Type of operation                              |
| **[ref]** <br> `incidence`             | Incidences_id of incidents happening during operation |

## Resource
| **SME type** <br> **idShort**       | **Description**                                 |
|:-----------------------------------|:------------------------------------------------|
| **[SMC]** <br> `Asset`| General Description of Assets|
| **[ref]** <br> `incident`| Incidence_id of incident of a resource|
| **[ref]** <br> `Shopfloor`| Shopfloor where resource is located

### Asset
| **SME type** <br> **idShort**           | **Description**                                 |
|:---------------------------------------|:------------------------------------------------|
| **[property]** <br> `assetId`| UID of the asset|
| **[property]** <br> `mttr`| Mean time to repair|
| **[property]** <br> `mtbf`| Mean time before failure|
| **[property]** <br> `failureRate`| Failure rate of the asset|
| **[property]** <br> `repairRate`| Repair rate of asset|
| **[SMC]** <br> `TransportSystem`| Description of transport systems|
| **[SMC]** <br> `MaterialStorageSystem`| Description of the storage systems|
| **[SMC]** <br> `Machine`| Description of the machines|

#### TransportSystem
| **SME type** <br> **idShort**           | **Description**                                 |
|:---------------------------------------|:------------------------------------------------|
| **[property]** <br> `transportSystemId` | UID of transport system|
| **[property]** <br> `transportTime`| Time of transport|
| **[property]** <br> `routing`| Route of transport|

#### MaterialStorageSystem
| **SME type** <br> **idShort**          | **Description**                             |
|:--------------------------------------|:--------------------------------------------|
| **[property]** <br> `storageId`| UID of storage system|
| **[property]** <br> `availableSlots`| Number of available slots|

#### Machine
| **SME type** <br> **idShort**          | **Description**                             |
|:--------------------------------------|:--------------------------------------------|
| **[SMC]** <br> `criticalComponent` | Group of critical components                |
| **[property]** <br> `machineId`| UID of machine                              |
| **[property]** <br> `execution_state`| Current execution state of machine|
| **[property]** <br> `toolLifetime`| Lifetime of current tool|

##### criticalComponent
| **SME type** <br> **idShort**          | **Description**                             |
|:--------------------------------------|:--------------------------------------------|
| **[SMC]** <br> `componentDiagnosis` | Reference to Diagnosis of component                |                 |
| **[SMC]** <br> `componentId` | ID of critical omponent                |                 |

## SupplyChain
| **SME type** <br> **idShort**           | **Description**                              |
|:---------------------------------------|:---------------------------------------------|
| **[SMC]** <br> `Logistics`| Description of logistics|
| **[SMC]** <br> `MarketAnalysis`| Main metrics of the market|
| **[SMC]** <br> `ProductionSite`| Main metrics of the production site|
| **[ref]** <br> `incident`| Incidence_id of incidents in the supply chain |
| **[ref]** <br> `SupplyPlan`| Reference to supply plan

### Logistics
| **SME type** <br> **idShort**            | **Description**                             |
|:----------------------------------------|:--------------------------------------------|
| **[property]** <br> `transportationId`  | UID of transportation                       |
| **[property]** <br> `transportationCapacity` | Capacity of transportation                |
| **[property]** <br> `transportationCost` | Cost of transportation                    |

### MarketAnalysis
| **SME type** <br> **idShort**               | **Description**                               |
|:-------------------------------------------|:----------------------------------------------|
| **[property]** <br> `demandQuantity`       | Quantity of demand                            |
| **[property]** <br> `productPrice`         | Price of product                              |
| **[property]** <br> `supplyMarketCapacity`| Capacity of the supply market                 |
| **[property]** <br> `supplyMarketPrice`   | Price at the supply market                    |

### ProductionSite
| **SME type** <br> **idShort**              | **Description**                               |
|:------------------------------------------|:----------------------------------------------|
| **[property]** <br> `siteId`              | UID of production site                        |
| **[property]** <br> `productivity`         | Price of product                              |
| **[property]** <br> `operationalCost`     | Capacity of the supply market                 |
| **[property]** <br> `energyCost`          | Price at the supply market                    |
| **[property]** <br> `inventoryCapacity`   | Capacity of Inventory                         |
| **[property]** <br> `inventoryCost`       | Cost of inventory                             |

## ResilienceKPI
| **SME type** <br> **idShort**     | **Description**                       |
|:----------------------------------|:--------------------------------------|
| **[SMC]** <br> `value`| values of resilience kpi|
| **[SMC]** <br> `description`|descriptions of resilience KPI |
