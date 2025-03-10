h1. Feature: API Gateway Access Logging

h2. Description
Configure API Gateway access logs to capture REST API request/response metadata without sensitive payloads.

h3. Epic Link
Implement Comprehensive Logging Strategy for AWS Services

h2. Tasks
# Enable access logs for all API Gateway REST APIs
# Configure JSON log format with fields for:
## Request: requestTime, requestId, httpMethod, path, resourcePath
## Performance: status, responseLatency
## Integration: integrationRequestId, functionResponseStatus, integrationLatency
## Identity: principalId (for authorized users)
# Test and validate that request/response bodies are never logged
# Ensure X-Ray traceId is included in access logs for future trace correlation

h2. Acceptance Criteria
# Access logs are enabled for all API Gateway endpoints
# Logs capture all required metadata fields
# Request/response bodies are never included in logs
# Logs are properly formatted as JSON for easy querying
# X-Ray trace IDs are correctly included for correlation

h2. Technical Notes
From the provided article, the JSON log format should look like:

For traditional API Gateways with custom authorizer:
{code}
'{"requestTime":"$context.requestTime","requestId":"$context.requestId","httpMethod":"$context.httpMethod","path":"$context.path","resourcePath":"$context.resourcePath","status":$context.status,"responseLatency":$context.responseLatency,"xrayTraceId":"$context.xrayTraceId","integrationRequestId":"$context.integration.requestId","functionResponseStatus":"$context.integration.status","integrationLatency":"$context.integration.latency","integrationServiceStatus":"$context.integration.integrationStatus","authorizeStatus":"$context.authorize.status","authorizerStatus":"$context.authorizer.status","authorizerLatency":"$context.authorizer.latency","authorizerRequestId":"$context.authorizer.requestId","principalId":"$context.authorizer.principalId"}'
{code}

Or without custom authorizer:
{code}
'{"requestTime":"$context.requestTime","requestId":"$context.requestId","httpMethod":"$context.httpMethod","path":"$context.path","resourcePath":"$context.resourcePath","status":$context.status,"responseLatency":$context.responseLatency,"xrayTraceId":"$context.xrayTraceId","integrationRequestId":"$context.integration.requestId","functionResponseStatus":"$context.integration.status","integrationLatency":"$context.integration.latency","integrationServiceStatus":"$context.integration.integrationStatus"}'
{code}