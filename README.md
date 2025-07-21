# WTB Blockchain API Specification

## General Information

- **Version**: 1.0.0

---

## `/api/blockchain/organisation`

### POST

**Summary**: Submit organisation request

**Request Body** (application/json):

```json
{
  "id": "ORG-001",
  "name": "GreenWind Turbines",
  "address": "123 Windmill Rd, Warrnambool, VIC",
  "requester_id": "USER-0123",
  "requester_name": "Alice Nguyen",
  "requester_email": "alice@greenwind.com",
  "request_timestamp": "2025-06-18T09:00:00Z"
}
```

**Responses**:

- `201 Created`: Organisation request submitted successfully
---

## `/api/blockchain/organisation/{organisation_id}`

### GET

**Summary**: Get organisation request details

**Path Parameter**:

- `organisation_id` (string): Organisation ID to retrieve

**Responses**:

```json
{
  "id": "ORG-001",
  "name": "GreenWind Turbines",
  "requester_id": "USER-0123",
  "requester_name": "Alice Nguyen",
  "requester_email": "alice@greenwind.com",
  "request_timestamp": "2025-06-18T09:00:00Z"
  "status": "requested",
  "approver_id": null,
  "approver_name": null,
  "approve_timestamp": null
}
```

---

## `/api/blockchain/organisation`

### PATCH
**Summary**: Submit organisation approval

**Request Body** (application/json):

```json
{
  "id": "ORG-001",
  "approver_id": "ADMIN-001",
  "approver_name": "Sophie Admin",
  "approve_timestamp": "2025-06-18T09:30:00Z"
}
```

**Responses**:

- `200 Success`: Organisation approval submitted successfully

---

## `/api/blockchain/job`

### POST

**Summary**: Submit a new job request for a wind farm

**Request Body** (application/json):

```json
{
  "job_id": "JOB-2025-0001",
  "organisation_id": "ORG-001",
  "total_turbines": 12,
  "request_option": "Recycle only",
  "request_type": "On-site shredding",
  "turbine_ids": ["TURB-0001", "TURB-0002", "TURB-0003"],
  "asset_location": "Site 7A – South Field",
  "expected_transport_time": "2025-07-05T10:00:00Z",
  "note": "Shredding will occur on-site. Limited access for large vehicles.",
  "contact_name": "Alice Nguyen",
  "contact_phone": "+61400111222",
  "contact_email": "alice@greenwind.com",
  "requester_id": "USER-0123",
  "requester_name": "Alice Nguyen",
  "request_timestamp": "2025-06-18T10:00:00Z"
}
```

**Responses**:

- `201 Created`: Job request submitted successfully

---

## `/api/blockchain/job`

### PATCH

**Summary**: Approve a submitted job

**Request Body** (application/json):

```json
{
  "job_id": "JOB-2025-0001",
  "approver_id": "ADMIN-001",
  "approver_name": "Sophie Admin",
  "approve_timestamp": "2025-06-18T10:30:00Z"
}
```

**Responses**:

- `200  Success`: Job approved

---

## `/api/blockchain/job/{job_id}`

### GET

**Summary**: Get job details

**Path Parameter**:

- `job_id` (string): Job ID to retrieve

**Responses**:

```json
{
  "job_id": "JOB-2025-0001",
  "organisation_id": "ORG-001",
  "total_turbines": 12,
  "request_option": "Recycle only",
  "request_type": "On-site shredding",
  "turbine_blades": ["TURB-0001", "TURB-0002", "TURB-0003"],
  "asset_location": "Site 7A – South Field",
  "expected_transport_time": "2025-07-05T10:00:00Z",
  "note": "Shredding will occur on-site. Limited access for large vehicles.",
  "contact_name": "Alice Nguyen",
  "contact_phone": "+61400111222",
  "contact_email": "alice@greenwind.com",
  "requester_id": "USER-0123",
  "requester_name": "Alice Nguyen",
  "request_timestamp": "2025-06-18T10:00:00Z"
  "approver_id": "ADMIN-001",
  "approver_name": "Sophie Admin",
  "approve_timestamp": "2025-06-18T10:30:00Z",
  "status": "approve",
  "reporter_id": null,
  "reporter_name": null,
  "report_timestamp": null
}
```

## `/api/blockchain/progress`

### POST

**Summary**: Submit progress update by the recycler

**Request Body** (application/json):

```json
{
  "job_id": "JOB-2025-0001",
  "completed_blades": 2,
  "total_blades": 10,
  "percentage": 20,
  "updater_id": "RECYCLER-201",
  "updater_name": "Bob Smith",
  "timestamp": "2025-06-19T15:00:00Z"
}
```

**Responses**:

- `201 Created`: Progress update logged

---

## `/api/blockchain/job`

### PATCH

**Summary**: Mark the project as completed by the recycler

**Request Body** (application/json):

```json
{
  "job_id": "JOB-2025-0001",
  "reporter_id": "RECYCLER-201",
  "reporter_name": "Bob Smith",
  "report_timestamp": "2025-06-20T17:00:00Z"
}
```

**Responses**:

- `200 Success`: Project marked as completed

---

## `/api/blockchain/job-finalise-aggrement`

### POST

**Summary**: Final confirmation from both parties (requesting)

**Request Body** (application/json):

```json
{
  "job_id": "JOB-2025-0001",
  "requester_id": "RECYCLER-201",
  "requester_name": "Bob Smith",
  "request_timestamp": "2025-06-20T17:00:00Z",
}
```
**Responses**:

- `201 Created`: Project finalised by both parties (approving)

---
### PATCH

**Summary**: Final confirmation from both parties

**Request Body** (application/json):

```json
{
  "job_id": "JOB-2025-0001",
  "approver_id": "USER-0123",
  "approver_name": "Alice Nguyen",
  "appove_timestamp": "2025-06-21T08:00:00Z"
}
```

**Responses**:
- `201 Created`: Project finalised by both parties

---

## `/api/blockchain/job-finalise-agreement/{job_id}`

### GET

**Summary**: Get an agreement

**Path Parameter**:

- `job_id` (string): Job ID to retrieve

**Responses**:

```json
{
  "job_id": "JOB-2025-0001",
  "requester_id": "RECYCLER-201",
  "requester_name": "Bob Smith",
  "request_timestamp": "2025-06-20T17:00:00Z",
  "approver_id": "USER-0123",
  "approver_name": "Alice Nguyen",
  "appove_timestamp": "2025-06-21T08:00:00Z"
}
```
---
## New API Endpoints for Turbine Management (Extension)

### `/api/blockchain/turbine`

#### POST

**Summary**: Register a new wind turbine asset.

**Request Body** (application/json):
```json
{
  "turbine_id": "TURB-0001",
  "turbine_serial_number": "VESTAS-112-2020-0009",
  "wind_farm_name": "South Ridge Wind Farm",
  "organisation_id": "ORG-001",
  "turbine_model": "Vestas V112",
  "manufacturer": "Vestas",
  "number_of_blades": 3,
  "blade_length_m": 55,
  "estimated_blade_weight_kg_each": 9000,
  "installation_date": "2020-03-15",
  "expected_end_of_life_date": "2040-03-15",
  "planned_decommission_date": "2039-12-31",
  "wind_farm_address": "123 Windmill Rd, Warrnambool, VIC",
  "state": "VIC",
  "postcode": "3280",
  "site_zone": "North Section",
  "turbine_location_description": "Near Ridge Road",
  "latitude": -38.383,
  "longitude": 142.487,
  "site_accessibility": "Limited",
  "operational_status": "Operational",
  "last_updated": "2025-07-21T10:00:00Z"
}
```

**Response**:
- `201 Created`: Turbine registered successfully

---

### `/api/blockchain/turbine/{turbine_id}`

#### GET
**Summary**: Retrieve turbine asset details

**Path Parameter**:
- `turbine_id` (string): Turbine ID

**Response**:
```json
{
  "turbine_id": "TURB-0001",
  "turbine_serial_number": "VESTAS-112-2020-0009",
  "wind_farm_name": "South Ridge Wind Farm",
  "organisation_id": "ORG-001",
  "turbine_model": "Vestas V112",
  "manufacturer": "Vestas",
  "number_of_blades": 3,
  "blade_length_m": 55,
  "estimated_blade_weight_kg_each": 9000,
  "installation_date": "2020-03-15",
  "expected_end_of_life_date": "2040-03-15",
  "planned_decommission_date": "2039-12-31",
  "wind_farm_address": "123 Windmill Rd, Warrnambool, VIC",
  "state": "VIC",
  "postcode": "3280",
  "site_zone": "North Section",
  "turbine_location_description": "Near Ridge Road",
  "latitude": -38.383,
  "longitude": 142.487,
  "site_accessibility": "Limited",
  "operational_status": "Operational",
  "last_updated": "2025-07-21T10:00:00Z"
}
```
---

### `/api/blockchain/turbine/{turbine_id}`

#### PATCH

**Summary**: Update turbine information

**Request Body** (application/json): Partial update fields allowed

```json
{
  "turbine_id": "TURB-0001",
  "turbine_serial_number": "VESTAS-112-2020-0009",
  "manufacturer": "Vestas",
  "number_of_blades": 3,
}
```

**Response**:
- `200 Success`: Turbine information updated

---

### `/api/blockchain/turbine/by-organisation/{organisation_id}`

#### GET

**Summary**: Get all turbines associated with an organisation

**Path Parameter**:
- `organisation_id` (string)

**Response**: List of turbine objects

```json
[{
  "turbine_id": "TURB-0001",
  "turbine_serial_number": "VESTAS-112-2020-0009",
  "wind_farm_name": "South Ridge Wind Farm",
  "organisation_id": "ORG-001",
  "turbine_model": "Vestas V112",
  "manufacturer": "Vestas",
  "number_of_blades": 3,
  "blade_length_m": 55,
  "estimated_blade_weight_kg_each": 9000,
  "installation_date": "2020-03-15",
  "expected_end_of_life_date": "2040-03-15",
  "planned_decommission_date": "2039-12-31",
  "wind_farm_address": "123 Windmill Rd, Warrnambool, VIC",
  "state": "VIC",
  "postcode": "3280",
  "site_zone": "North Section",
  "turbine_location_description": "Near Ridge Road",
  "latitude": -38.383,
  "longitude": 142.487,
  "site_accessibility": "Limited",
  "operational_status": "Operational",
  "last_updated": "2025-07-21T10:00:00Z"
},
{
  "turbine_id": "TURB-0002",
  "turbine_serial_number": "VESTAS-112-2020-0009",
  "wind_farm_name": "South Ridge Wind Farm",
  "organisation_id": "ORG-001",
  "turbine_model": "Vestas V112",
  "manufacturer": "Vestas",
  "number_of_blades": 3,
  "blade_length_m": 55,
  "estimated_blade_weight_kg_each": 9000,
  "installation_date": "2020-03-15",
  "expected_end_of_life_date": "2040-03-15",
  "planned_decommission_date": "2039-12-31",
  "wind_farm_address": "123 Windmill Rd, Warrnambool, VIC",
  "state": "VIC",
  "postcode": "3280",
  "site_zone": "North Section",
  "turbine_location_description": "Near Ridge Road",
  "latitude": -38.383,
  "longitude": 142.487,
  "site_accessibility": "Limited",
  "operational_status": "Operational",
  "last_updated": "2025-07-21T10:00:00Z"
}]
```
---
## Schema Definitions

### Organisation

| Field | Type | Description |
|-------|------|-------------|
| `id` | string | Unique identifier for the organisation |
| `name` | string | Name of the organisation |
| `address` | string | Name of the organisation |
| `requester_id` | string | ID of the requesting user |
| `requester_name` | string | Name of the requesting user |
| `requester_email` | string (email) | Email of the requesting user |
| `request_timestamp` | string (date-time) | ISO 8601 timestamp |
| `status` | string |`requested`, `approved`  |
| `approver_id` | string | ID of the approving user |
| `approver_name` | string | Name of the approving user |
| `approve_timestamp` | string (date-time) | ISO 8601 timestamp |

---

### Job

| Field | Type | Description |
|-------|------|-------------|
| `id` | string | Unique job identifier |
| `organisation_id` | string | Associated organisation ID |
| `company_name` | string | Name of the company requesting |
| `address` | string | Physical address of the job site |
| `total_turbines` | integer | Number of turbines |
| `request_option` | string | Recycling request option |
| `request_type` | string | Recycling type |
| `asset_location` | string | Location of the blade asset |
| `expected_transport_time` | string (date-time) | Planned time of transport |
| `note` | string | Additional notes |
| `contact_name` | string | Contact person's name |
| `contact_phone` | string | Contact phone number |
| `contact_email` | string | Contact email address |
| `requester_id` | string | Requesting user's ID |
| `requester_name` | string | Requesting user's name |
| `request_timestamp` | string (date-time) | ISO 8601 timestamp |
| `approver_id` | string | ID of the approving user |
| `approver_name` | string | Name of the approving user |
| `approve_date` | string (date-time) | ISO 8601 timestamp |
| `reporter_id` | string | ID of the finalising user |
| `reporter_name` | string | Name of the finalising user |
| `report_timestamp` | string (date-time) | ISO 8601 timestamp |
| `status` | string | `requested`, `approved`, `finalised`  |

---

### Turbine

| Field | Type | Description |
|-------|------|-------------|
| `turbine_id`                  | string   | Internal asset ID |
| `job_id` | string | Associated Job ID |
| `turbine_serial_number`       | string   | Manufacturer's serial number |
| `wind_farm_name`              | string   | Name of the wind farm |
| `organisation_id`             | string   | Linked organisation ID |
| `turbine_model`               | string   | Model name |
| `manufacturer`                | string   | Manufacturer name |
| `number_of_blades`            | integer  | Typically 2 or 3 |
| `blade_length_m`              | number   | Length in meters |
| `estimated_blade_weight_kg_each` | number | Per blade weight |
| `installation_date`           | string (date) | Installed date |
| `expected_end_of_life_date`   | string (date) | Designated EOL |
| `planned_decommission_date`   | string (date) | Planned decommission |
| `wind_farm_address`           | string   | Site address |
| `state`                       | string   | Australian state |
| `postcode`                    | string   | Postal code |
| `site_zone`                   | string   | Internal zone mapping |
| `turbine_location_description`| string   | e.g., access notes |
| `latitude`                    | number   | Optional GPS |
| `longitude`                   | number   | Optional GPS |
| `site_accessibility`          | string   | Good / Limited / Poor |
| `operational_status`          | string   | Operational / Decommissioned / Planned |
| `last_updated`                | string (date-time) | ISO 8601 timestamp |
---

### JobProgress

| Field | Type | Description |
|-------|------|-------------|
| `id` | string | Unique job identifier |
| `job_id` | string | Job identifier |
| `completed_blades` | integer | Number of blades completed |
| `total_blades` | integer | Total number of blades |
| `percentage` | integer | Completion percentage |
| `updater_id` | string | Recycler's user ID |
| `updater_name` | string | Recycler's name |
| `timestamp` | string (date-time) | ISO 8601 timestamp |

---

### JobFinaliseAgreement

| Field | Type | Description |
|-------|------|-------------|
| `job_id` | string | Job identifier |
| `requester_id` | string | Recycler's user ID |
| `requester_name` | string | Recycler's name |
| `request_timestamp`| string (date-time) | ISO 8601 timestamp |
| `approver_id` | string | Windfarm user's ID |
| `approver_name` | string | Windfarm user's name |
| `approve_timestamp` | string (date-time) | ISO 8601 timestamp |


