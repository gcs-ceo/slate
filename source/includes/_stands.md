# Stands

These are individual, semi-autonomous, equipment stands that will come in multiple variations

Each stand can hold different amounts and types of equipment

<aside class="notice">A new stand should be created as soon as a new stand is ordered. This is when a stands should be assigned it's type, locks, and partners.</aside>

## Stands Table

>Example Stand Object:

```json
{
    "id": 0001
}
```

Field | Type | Null | Description
--------- | ------- | ----------- | -----------
**(PK) Id** | int | NotNullable | Unique Id of the stand
StandStatusId | int | Nullable | Id for the status of the stand
StandTypeId | int | Nullable | Id for the type of stand
PartnerId | int | Nullable | The partner id the stand belongs to
DateOpened | datetime2 | Nullable | The date the stand opened for business
**DateCreated** | datetime2 | NotNullable | Default (getutcdate()) Date the stand was created
**DateModified** | datetime2 | NotNullable | Default (getutcdate()) Date the stand was last modified

Required in **bold**

## List All Stands 

Retreives all stands and can be paginated

## List All Stands by Partner

Retrieves all the stands owned by a specific partner and can be paginated

## Create New Stand

Creates a new stand with the provided properties

## Delete a Stand

Updates stand's status to 0 (Archived)

## Update a Stand

Updates a stand with the provided properties

