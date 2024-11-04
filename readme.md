# Personal CRM GPT with Airtable API

This README will guide you through setting up a custom GPT instance with a schema for managing a Personal CRM. This setup includes managing **Teammates**, **Events**, **Goals**, **Achievements**, and **Milestones** using the Airtable API. The schema is defined in OpenAPI 3.1.0 format.

## Prerequisites

1. **Airtable Account**: You'll need an Airtable account and a base set up with tables for **Teammates**, **Events**, **Goals**, **Achievements**, and **Milestones**.
2. **API Key**: Obtain your Airtable API key or personal access token with `data.records:read` and `data.records:write` permissions.
3. **Airtable Base ID**: Find your Airtable base ID from your Airtable API documentation dashboard.
4. **GPT Instance**: Access to set up a custom GPT instance where you can upload an OpenAPI specification.

## Getting Started

### Step 1: Airtable Setup

Set up your Airtable base with tables that match the following structure. Each table should contain the fields defined below:

#### Teammates Table

- `Name` (Single Line Text)
- `Notes` (Multi-line Text)
- `Job Title` (Single Line Text)
- `Events` (Linked Record to Events table)
- `Goals` (Linked Record to Goals table)
- `Achievements` (Linked Record to Achievements table)
- `created` (Auto-generated Created Time)

#### Events Table

- `Name` (Single Line Text)
- `Notes` (Multi-line Text)
- `Created` (Auto-generated Created Time)
- `Teammate` (Linked Record to Teammates table)
- `Happened On` (Date)

#### Goals Table

- `Name` (Single Line Text)
- `Notes` (Multi-line Text)
- `Created` (Auto-generated Created Time)
- `Complete by` (Date)
- `Completed` (Checkbox)
- `Teammate` (Linked Record to Teammates table)

#### Achievements Table

- `Name` (Single Line Text)
- `Notes` (Multi-line Text)
- `Teammate` (Linked Record to Teammates table)
- `Completed on` (Date)
- `Created` (Auto-generated Created Time)
- `Milestones` (Linked Record to Milestones table)

#### Milestones Table

- `Name` (Single Line Text)
- `Notes` (Multi-line Text)
- `Achievements` (Linked Record to Achievements table)
- `Link` (URL)

### Step 2: Set up OpenAPI Specification

Use the provided OpenAPI 3.1.0 schema for the Personal CRM API. The schema should include all endpoints for managing the records (list, create, retrieve, and update) across the five tables: **Teammates**, **Events**, **Goals**, **Achievements**, and **Milestones**.

### Step 3: Configure the Custom GPT with OpenAPI Schema

1. **Upload the OpenAPI Specification**: In your GPT instance, navigate to the API schema settings and upload the OpenAPI YAML file. This should provide all necessary endpoints and schemas for the tables.
2. **Set API Base URL**: Ensure the API base URL is set to `https://api.airtable.com/v0/<Your_Base_ID>` where `<Your_Base_ID>` is replaced by your Airtable base ID.
3. **Authenticate Requests**: In the GPT API configuration, add an `Authorization` header with the value `Bearer <Your_API_Key>`, replacing `<Your_API_Key>` with your Airtable API key or token.

### Step 4: Testing Endpoints

Use the **Test** feature in the GPT interface to ensure that each endpoint works as expected:

- List all records for each table (`GET` endpoints for `/Teammates`, `/Events`, `/Goals`, `/Achievements`, `/Milestones`)
- Retrieve a single record by ID (`GET` endpoint with `{recordId}`)
- Create new records (`POST` endpoints)
- Update records (`PATCH` endpoints with `{recordId}`)

### Step 5: Customize Prompt for GPT Instance

Once the schema is operational, customize the GPT instance’s prompt to interact with your Personal CRM. Example prompts might include:

- "Show me all teammates and their linked goals."
- "Create a new event for teammate John Doe with the title 'Quarterly Review.'"
- "List all milestones linked to the achievement 'Launch Alpha Product.'"

### Additional Configuration (Optional)

- **Error Handling**: Customize error messages within your GPT instance to give meaningful feedback if a request fails.
- **Field Mapping**: In case the Airtable field names differ, ensure that your field names in Airtable match the schema in the OpenAPI file.
- **Pagination**: For larger datasets, use the Airtable `offset` parameter to paginate through responses.

## Schema Summary

Here is a quick summary of the available tables and endpoints in your GPT custom setup:

- **Teammates**: `/Teammates`, `/Teammates/{teammateId}`
- **Events**: `/Events`, `/Events/{eventId}`
- **Goals**: `/Goals`, `/Goals/{goalId}`
- **Achievements**: `/Achievements`, `/Achievements/{achievementId}`
- **Milestones**: `/Milestones`, `/Milestones/{milestoneId}`

Each table endpoint supports:

- **GET**: Retrieve a list or a specific record
- **POST**: Create a new record
- **PATCH**: Update an existing record

---

Your custom GPT instance should now be configured to manage your Personal CRM with Airtable!
