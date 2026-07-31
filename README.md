# Agari

Publisher: Agari <br>
Connector Version: 1.0.1 <br>
Product Vendor: Agari <br>
Product Name: Agari <br>
Minimum Product Version: 4.9.39220

This app integrates with Agari to implement the investigative and generic actions that protect against phishing and Business Email Compromise (BEC) attacks

### Configuration variables

This table lists the configuration variables required to operate Agari. These variables are specified when configuring a Agari asset in Splunk SOAR.

VARIABLE | REQUIRED | TYPE | DESCRIPTION
-------- | -------- | ---- | -----------
**client_id** | required | string | Client ID |
**client_secret** | required | password | Client Secret |
**sort** | required | string | Sort the result data set based on the 'created_at' field |
**start_date** | optional | string | The initial start date for ingestion. The start date should be within the last two weeks |
**add_fields** | optional | string | Fields to add to the default message payload (allows comma-delimited string) |
**filter** | optional | string | Filtering the policy events based on the search filters (allows multiple filters using and/or conjunctions) |
**policy_name** | optional | string | Find by the policy name while fetching the policy events |
**policy_action** | optional | string | Find by the policy action while fetching the policy events |
**policy_enabled** | optional | string | Find by the policies enabled while fetching the policy events |
**exclude_alert_types** | optional | string | Exclude the alert type while fetching the policy events |
**cef_mapping** | optional | string | JSON dictionary represented as a serialized JSON string. Each key in the dictionary is a potential key name in the message artifact that is to be renamed to the value |
**max_results** | optional | numeric | Maximum number of results to ingest. The default value is 100 |
**max_workers_for_polling** | optional | numeric | Maximum number of workers to use while fetching the results from the Agari Server. The default value is 1 |

### Supported Actions

[test connectivity](#action-test-connectivity) - Validate the asset configuration for test connectivity using supplied configuration <br>
[list policy events](#action-list-policy-events) - List all the policy events <br>
[get policy event](#action-get-policy-event) - Fetches a single policy event from Agari for the given policy event ID <br>
[list messages](#action-list-messages) - List all the messages <br>
[get message](#action-get-message) - Fetches a single message from Agari for the given message ID <br>
[remediate message](#action-remediate-message) - Deletes or moves a message from the inbox for the provided message ID <br>
[on poll](#action-on-poll) - Action handler for the on poll ingest functionality

## action: 'test connectivity'

Validate the asset configuration for test connectivity using supplied configuration

Type: **test** <br>
Read only: **True**

#### Action Parameters

No parameters are required for this action

#### Action Output

No Output

## action: 'list policy events'

List all the policy events

Type: **investigate** <br>
Read only: **True**

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**max_results** | optional | Max number of policy events to return. The default value is 100 | numeric | |
**offset** | optional | This parameter allows the user to set the starting point or offset for the response. The default value is 0 | numeric | |
**sort** | optional | A comma-delimited string that specifies the field ordering (with direction) to be applied to the response | string | |
**rem_fields** | optional | A comma-delimited list of fields to remove from the default payload | string | |
**add_fields** | optional | A comma-delimited list of optional fields to add to the default payload | string | |
**filter** | optional | Search filters that can be applied to the response | string | |
**fields** | optional | A comma-delimited list of fields to include in the payload | string | |
**start_date** | optional | The earliest date time (UTC) a search should target (ISO 8601 format) | string | |
**end_date** | optional | The latest date time (UTC) a search should target (ISO 8601 format) | string | |
**policy_name** | optional | Find by policy name | string | `agari policy name` |
**policy_action** | optional | Find by policy action. Valid values are deliver, move, inbox, delete, none, and all | string | |
**policy_enabled** | optional | Find by enabled policies | string | |
**exclude_alert_types** | optional | Exclude Policy types. Valid values are MessageAlert, SystemAlert, and None | string | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.add_fields | string | | alert_definition_name |
action_result.parameter.end_date | string | | 2021-04-21T12:23:27Z |
action_result.parameter.exclude_alert_types | string | | SystemAlert |
action_result.parameter.fields | string | | id, updated_at, created_at |
action_result.parameter.filter | string | | created_at.after(2020-04-20T07:21:33Z) |
action_result.parameter.max_results | numeric | | 100 |
action_result.parameter.offset | numeric | | 5 |
action_result.parameter.policy_action | string | | delete |
action_result.parameter.policy_enabled | string | | True |
action_result.parameter.policy_name | string | `agari policy name` | Untrusted Messages |
action_result.parameter.rem_fields | string | | notified_original_recipients, summary |
action_result.parameter.sort | string | | created_at ASC, id ASC |
action_result.parameter.start_date | string | | 2021-04-21T09:58:30Z |
action_result.data.\*.alert_definition_name | string | `agari policy name` | SystemAlert |
action_result.data.\*.created_at | string | | 2021-04-28T12:04:14Z |
action_result.data.\*.id | numeric | `agari policy event id` | 646349268 |
action_result.data.\*.notified_original_recipients | boolean | | False |
action_result.data.\*.policy_action | string | | none |
action_result.data.\*.policy_enabled | boolean | | True |
action_result.data.\*.summary | boolean | | False |
action_result.data.\*.updated_at | string | | 2021-04-28T12:04:14Z |
action_result.summary.total_policy_events | numeric | | 32 |
action_result.message | string | | Total policy events: 32 |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'get policy event'

Fetches a single policy event from Agari for the given policy event ID

Type: **investigate** <br>
Read only: **True**

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** | required | Policy Event ID | numeric | `agari policy event id` |
**rem_fields** | optional | A comma-delimited list of fields to remove from the default payload | string | |
**add_fields** | optional | A comma-delimited list of optional fields to add to the default payload | string | |
**fields** | optional | A comma-delimited list of fields to include in the payload | string | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.add_fields | string | | collector_message_id, created_at |
action_result.parameter.fields | string | | policy_name,created_at |
action_result.parameter.id | numeric | `agari policy event id` | 644270112 |
action_result.parameter.rem_fields | string | | policy_name,created_at |
action_result.data.\*.alert_event.collector_message_id | string | `agari internal message id` | b78fc523a-a623-11eb-8180-0242ac130004 |
action_result.data.\*.alert_event.conditions.message_trust_score_max | numeric | | 1.1 |
action_result.data.\*.alert_event.conditions.message_trust_score_min | numeric | | 0 |
action_result.data.\*.alert_event.created_at | string | | 2021-04-26T00:09:51Z |
action_result.data.\*.alert_event.id | numeric | `agari policy event id` | 644270122 |
action_result.data.\*.alert_event.links.messages | string | `url` | https://api.agari.com/v1/ep/messages/0ef8f426-a2ff-11eb-8180-0242ac130004 |
action_result.data.\*.alert_event.message_details.date | string | | 2021-04-26T00:09:51Z |
action_result.data.\*.alert_event.message_details.from | string | | ABC <test@btacase.com> |
action_result.data.\*.alert_event.message_details.subject | string | | Unusual sign-on detected |
action_result.data.\*.alert_event.message_details.to | string | `email` | abc@testing.com |
action_result.data.\*.alert_event.message_details.trust_score | numeric | | 0.5 |
action_result.data.\*.alert_event.policy_name | string | `agari policy name` | Brand Display Name Impostors |
action_result.data.\*.code | numeric | | 200 |
action_result.data.\*.status | string | | ok |
action_result.data.\*.version | numeric | | 1 |
action_result.summary | string | | |
action_result.message | string | | Policy Event fetched successfully |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'list messages'

List all the messages

Type: **investigate** <br>
Read only: **True**

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**max_results** | optional | Max number of messages to return. The default value is 100 | numeric | |
**offset** | optional | The offset, or starting point, for the paged response. The default value is 0 | numeric | |
**sort** | optional | A comma-delimited string that specifies the field ordering (with direction) to be applied to the response | string | |
**rem_fields** | optional | A comma-delimited list of fields to remove from the default payload | string | |
**add_fields** | optional | A comma-delimited list of optional fields to add to the default payload | string | |
**fields** | optional | A comma-delimited list of fields to include in the payload | string | |
**search** | optional | Search using the advanced search syntax | string | |
**start_date** | optional | The earliest date time (UTC) a search should target (ISO 8601 format) | string | |
**end_date** | optional | The latest date time (UTC) a search should target (ISO 8601 format) | string | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.add_fields | string | | from_domain |
action_result.parameter.end_date | string | | 2021-04-26T00:09:51Z |
action_result.parameter.fields | string | | from_domain |
action_result.parameter.max_results | numeric | | 100 |
action_result.parameter.offset | numeric | | 5 |
action_result.parameter.rem_fields | string | | from_domain |
action_result.parameter.search | string | | policy_ids is not null and domain_tags is null |
action_result.parameter.sort | string | | date ASC, id ASC |
action_result.parameter.start_date | string | | 2021-04-20T07:21:33Z |
action_result.data.\*.attachment_extensions | string | | com |
action_result.data.\*.attachment_filenames | string | | details_spreadsheet.com |
action_result.data.\*.attachment_sha256 | string | `sha256` | 275a021bbfb6489e54d471899f7db9d1663fc695ec2fe2a2c4538aabf651fd0f |
action_result.data.\*.attack_types | string | | address_group (Individual display name impostor) |
action_result.data.\*.authenticity | string | | 1.0 |
action_result.data.\*.date | string | | 2021-04-28T22:22:34+00:00 |
action_result.data.\*.domain_reputation | string | | 8.5 |
action_result.data.\*.domain_tags | string | | webmail |
action_result.data.\*.enforcement_action | string | | delete |
action_result.data.\*.enforcement_result | string | | error |
action_result.data.\*.from | string | | <test@test.com> |
action_result.data.\*.from_domain | string | `domain` | test.com |
action_result.data.\*.has_attachment | string | | false |
action_result.data.\*.id | string | `agari internal message id` | 3ace7cd8-a870-11eb-8180-0242ac130004 |
action_result.data.\*.ip | string | `ip` | 67.231.152.167 |
action_result.data.\*.mail_from_domain | string | | test.com |
action_result.data.\*.message_details_link | string | `url` | https://api.agari.com/v1/ep/messages/3ace7cd8-a870-11eb-8180-0242ac130004 |
action_result.data.\*.message_id | string | `agari global message id` | <fba004ad8c112300f0df43d713ad6ec5@test.com> |
action_result.data.\*.message_trust_score | string | | 1.0 |
action_result.data.\*.policy_ids | numeric | | 9014 |
action_result.data.\*.ptr_name | string | | abc-001ae501.pphosted.com |
action_result.data.\*.reply_to | string | `email` | abc@test.com |
action_result.data.\*.sbrs | string | | 2.7 |
action_result.data.\*.sender_type | string | | w (Well-Known) |
action_result.data.\*.subject | string | | Valid SMTP 52.41.68.250 |
action_result.data.\*.timestamp_ms | string | | 1619648554000 |
action_result.data.\*.to | string | `email` | abc@test.com |
action_result.summary.total_messsages | numeric | | 100 |
action_result.message | string | | Total messsages: 100 |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'get message'

Fetches a single message from Agari for the given message ID

Type: **investigate** <br>
Read only: **True**

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** | required | Message ID | string | `agari internal message id` |
**rem_fields** | optional | A comma-delimited list of fields to remove from the default payload | string | |
**add_fields** | optional | A comma-delimited list of optional fields to add to the default payload | string | |
**fields** | optional | A comma-delimited list of fields to include in the payload | string | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.add_fields | string | | from_domain |
action_result.parameter.fields | string | | from_domain |
action_result.parameter.id | string | `agari internal message id` | 0ef8f426-a2ff-11eb-8180-0242ac130004 |
action_result.parameter.rem_fields | string | | from_domain |
action_result.data.\*.code | numeric | | 200 |
action_result.data.\*.message.attack_class.display_name_impostor | string | | alerts@test.com is not expected to be sent on behalf of abc |
action_result.data.\*.message.attack_class.lookalike_domain | string | | is an impostor of alerts.test.com |
action_result.data.\*.message.authentication_results | string | | Non-aligned SPF Pass; Non-aligned DKIM Pass; DMARC Pass |
action_result.data.\*.message.authenticity_score | numeric | | 1 |
action_result.data.\*.message.date | string | | 2021-04-22T00:09:51+00:00 |
action_result.data.\*.message.dkim_d_tag | string | | abc.com |
action_result.data.\*.message.domain_reputation | numeric | | 2.7 |
action_result.data.\*.message.enforcement_action | string | | This message could not be deleted. |
action_result.data.\*.message.from | string | | ABC Alerts <alerts@test.com> |
action_result.data.\*.message.from_domain | string | `domain` | abc.com |
action_result.data.\*.message.id | string | `agari internal message id` | 0ef8f456-a2ff-11eb-8180-0242ac130004 |
action_result.data.\*.message.mail_from | string | | abc.com |
action_result.data.\*.message.matched_policies | string | `agari policy name` | Untrusted Messages |
action_result.data.\*.message.message_id | string | `agari global message id` | <161905019164.262797.551062412555126933@ip-172-31-1-60.us-west-2.compute.internal> |
action_result.data.\*.message.message_trust_score | numeric | | 0.5 |
action_result.data.\*.message.reply_to | string | | |
action_result.data.\*.message.risk_reason | string | | from suspicious domain |
action_result.data.\*.message.sbrs | numeric | | -9.3 |
action_result.data.\*.message.sending_ip_address.ip | string | `ip` | 37.235.48.209 |
action_result.data.\*.message.sending_ip_address.ptr_name | string | | abc.com |
action_result.data.\*.message.subject | string | | Your account will be blocked |
action_result.data.\*.message.timestamp_ms | numeric | | 1619050191000 |
action_result.data.\*.message.to | string | `email` | abc@testing.com |
action_result.data.\*.status | string | | ok |
action_result.data.\*.version | numeric | | 1 |
action_result.summary | string | | |
action_result.message | string | | Message fetched successfully |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'remediate message'

Deletes or moves a message from the inbox for the provided message ID

Type: **generic** <br>
Read only: **False**

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** | required | Message ID | string | `agari internal message id` |
**remediation_operation** | required | This parameter allows the user to move or delete the suspected message from the inbox | string | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.id | string | `agari internal message id` | 0ef8f426-a2ff-11eb-8180-0242ac130004 |
action_result.parameter.remediation_operation | string | | move delete |
action_result.data.\*.code | numeric | | 200 |
action_result.data.\*.enforcement.enforce | string | | move |
action_result.data.\*.enforcement.success | boolean | | True |
action_result.data.\*.status | string | | ok |
action_result.data.\*.version | numeric | | 1 |
action_result.summary | string | | |
action_result.message | string | | Message remediated successfully |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'on poll'

Action handler for the on poll ingest functionality

Type: **ingest** <br>
Read only: **True**

This action ingests policy events and associated messages from Agari.

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**container_count** | optional | Maximum number of containers to ingest | numeric | |
**start_time** | optional | Parameter ignored in this app | numeric | |
**end_time** | optional | Parameter ignored in this app | numeric | |
**artifact_count** | optional | Parameter ignored in this app | numeric | |

#### Action Output

No Output

______________________________________________________________________

Auto-generated Splunk SOAR Connector documentation.

Copyright 2026 Splunk Inc.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing,
software distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and limitations under the License.
