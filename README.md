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
  "turbine_blades": [ 
    { 
      "type": "Vestas V112", 
      "height_m": 55, 
      "length_m": 55, 
      "weight_kg": 9000, 
      "manufacturer": "Vestas" 
    } 
  ],
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
  "turbine_blades": [ 
    { 
      "type": "Vestas V112", 
      "height_m": 55, 
      "length_m": 55, 
      "weight_kg": 9000, 
      "manufacturer": "Vestas" 
    } 
  ],
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

### Blade

| Field | Type | Description |
|-------|------|-------------|
| `id` | string | Unique job identifier |
| `job_id` | string | Associated organisation ID |
| `type` | string | Blade model/type |
| `blade_height_m` | number | Blade height in meters |
| `blade_length_m` | number | Blade length in meters |
| `blade_weight_kg` | number | Blade weight in kilograms |
| `blade_manufacturer` | string | Blade manufacturer |

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


