
# Project: Lunar Events

- Author:   Edgar Rios
- Date:     2025-01-19
- Version:  1.0



Visit the homepage: https://mermaid.js.org/syntax/entityRelationshipDiagram.html

Create Diagram using this code

erDiagram
    FACT_LUNAR_EVENTS ||--o{ DIM_TIME : occurs_at
    FACT_LUNAR_EVENTS ||--o{ DIM_LOCATION : happens_in
    FACT_LUNAR_EVENTS ||--o{ DIM_EVENT_TYPE : is_of_type

    FACT_LUNAR_EVENTS {
        string event_id PK
        string time_key FK
        string location_key FK
        string event_type_key FK
        float duration
        float magnitude
        string details
    }

    DIM_TIME {
        string time_key PK
        date full_date
        int year
        int month
        int day
        string moon_phase
    }

    DIM_LOCATION {
        string location_key PK
        string region
        float latitude
        float longitude
        string timezone
    }

    DIM_EVENT_TYPE {
        string event_type_key PK
        string type_name
        string category
        string description
    }
