erDiagram
    product ||--o{ license : "has"
    license ||--o{ license_metric : "has metrics"
    license ||--o{ client_session : "has sessions"
    license ||--o{ audit_log : "logged in"
    
    product {
        text id PK
        text name
        text description
        text license_format
        text validator_type
        text public_key
        text api_prefix
        timestamptz created_at
        boolean is_active
    }
    
    license {
        text id PK
        text product_id PK,FK
        integer version PK
        text customer_key
        text license_type
        timestamptz valid_from
        timestamptz valid_until
        integer grace_period_days
        text license_format
        text content_base64
        text fingerprint
        text issuer_dn
        text status
        timestamptz registered_at
        text registered_by
        timestamptz created_at
        timestamptz updated_at
    }
    
    license_metric {
        bigint id PK
        text license_id FK
        text product_id FK
        integer license_version FK
        text metric_key
        text metric_value
        text data_type
        text description
        timestamptz created_at
    }
    
    client_session {
        bigint id PK
        text license_id FK
        text product_id FK
        integer license_version FK
        text client_id
        text client_name
        text client_version
        boolean is_active
        timestamptz registered_at
        timestamptz last_ping_at
        timestamptz expires_at
        inet ip_address
        text user_agent
        jsonb metadata
    }
    
    audit_log {
        bigint id PK
        text license_id FK
        text product_id
        integer license_version
        text operation
        text status
        text error_message
        text actor
        inet actor_ip
        jsonb request_data
        jsonb response_data
        timestamptz created_at
    }
