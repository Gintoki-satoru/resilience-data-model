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

