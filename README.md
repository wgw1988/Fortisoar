{
  "type": "workflow_collections",
  "data": [
    {
      "@type": "WorkflowCollection",
      "name": "00 - Danny Playbook Test",
      "description": null,
      "visible": true,
      "image": null,
      "uuid": "63c971df-3a2d-4868-a827-537dcc408421",
      "id": 92,
      "deletedAt": null,
      "importedBy": [],
      "recordTags": [],
      "workflows": [
        {
          "@type": "Workflow",
          "triggerLimit": null,
          "name": "test11",
          "aliasName": null,
          "tag": null,
          "description": null,
          "isActive": true,
          "debug": true,
          "singleRecordExecution": false,
          "remoteExecutableFlag": false,
          "parameters": [],
          "synchronous": false,
          "lastModifyDate": 1712040371,
          "collection": "/api/3/workflow_collections/63c971df-3a2d-4868-a827-537dcc408421",
          "versions": [],
          "triggerStep": "/api/3/workflow_steps/9150285d-71b7-417c-908e-97495f5eb61a",
          "steps": [
            {
              "@type": "WorkflowStep",
              "name": "Start",
              "description": null,
              "arguments": {
                "__triggerLimit": true,
                "step_variables": {
                  "input": {
                    "params": []
                  }
                },
                "triggerOnSource": true,
                "triggerOnReplicate": false
              },
              "status": null,
              "top": "40",
              "left": "40",
              "stepType": "/api/3/workflow_step_types/b348f017-9a94-471f-87f8-ce88b6a7ad62",
              "group": null,
              "uuid": "9150285d-71b7-417c-908e-97495f5eb61a"
            },
            {
              "@type": "WorkflowStep",
              "name": "Telegram Test",
              "description": null,
              "arguments": {
                "config": "b5195722-9917-4e6e-ac0f-cddab46620ee",
                "params": {
                  "python_function": "import requests\n    \ntoken = '5047099630:AAFqDC0D90KWRoqZrRT9u69b3ZVAqNKIfqo'\nchat_id = ''\n\nresponse = requests.post(\n  url='https://api.telegram.org/bot{0}/{1}'.format(token, method),\n  data={'chat_id': 12345, 'text': 'hello friend'}\n).json()"
                },
                "version": "2.1.0",
                "connector": "code-snippet",
                "operation": "python_inline_code_editor",
                "operationTitle": "Execute Python Code",
                "step_variables": []
              },
              "status": null,
              "top": "208",
              "left": "188",
              "stepType": "/api/3/workflow_step_types/1fdd14cc-d6b4-4335-a3af-ab49c8ed2fd8",
              "group": null,
              "uuid": "1c22c42a-00d6-4cfe-ae9a-72a319945d50"
            }
          ],
          "routes": [
            {
              "@type": "WorkflowRoute",
              "name": "Start -> Telegram Test",
              "targetStep": "/api/3/workflow_steps/1c22c42a-00d6-4cfe-ae9a-72a319945d50",
              "sourceStep": "/api/3/workflow_steps/9150285d-71b7-417c-908e-97495f5eb61a",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "43f6795f-7f8b-4030-af4c-4198bb2e9506"
            }
          ],
          "groups": [],
          "priority": "/api/3/picklists/2b563c61-ae2c-41c0-a85a-c9709585e3f2",
          "uuid": "013288fa-fab2-4c0f-90db-3005cd15d3d9",
          "id": 853,
          "owners": [],
          "isPrivate": false,
          "deletedAt": null,
          "importedBy": [],
          "recordTags": []
        },
        {
          "@type": "Workflow",
          "triggerLimit": null,
          "name": "00 - BC Card Scenario 1 > Reputation Check",
          "aliasName": null,
          "tag": null,
          "description": null,
          "isActive": true,
          "debug": true,
          "singleRecordExecution": false,
          "remoteExecutableFlag": false,
          "parameters": [
            "ip_addr",
            "file_hash",
            "alert_iri",
            "alert_sourcedata"
          ],
          "synchronous": false,
          "lastModifyDate": 1712035937,
          "collection": "/api/3/workflow_collections/63c971df-3a2d-4868-a827-537dcc408421",
          "versions": [],
          "triggerStep": "/api/3/workflow_steps/4d2d1384-ff69-472a-8a29-224b8604b422",
          "steps": [
            {
              "@type": "WorkflowStep",
              "name": "Attacker TI Check",
              "description": null,
              "arguments": {
                "conditions": [
                  {
                    "option": "차단",
                    "step_iri": "/api/3/workflow_steps/19998fd2-d26d-447e-baf8-5ad184ff546d",
                    "condition": "{{ vars.steps.Find_Attacker_Indicator | length > 0 }}",
                    "step_name": "Copy 1 of NOP"
                  },
                  {
                    "option": "TI에 없음",
                    "default": true,
                    "step_iri": "/api/3/workflow_steps/6c7826ad-562b-4225-a285-d119ca782759",
                    "step_name": "Find cncHost"
                  }
                ],
                "step_variables": []
              },
              "status": null,
              "top": "160",
              "left": "20",
              "stepType": "/api/3/workflow_step_types/12254cf5-5db7-4b1a-8cb1-3af081924b28",
              "group": "/api/3/workflow_groups/b030b0c5-44ce-47f0-beb8-296ac42def78",
              "uuid": "43f27847-c46a-4d16-a056-5021fe97a7c8"
            },
            {
              "@type": "WorkflowStep",
              "name": "Attacker TI Comment",
              "description": null,
              "arguments": {
                "resource": {
                  "type": "/api/3/picklists/ff599189-3eeb-4c86-acb0-a7915e85ac3b",
                  "alerts": "{{vars.alert_iri}}",
                  "people": [],
                  "content": "<p>{{vars.steps.Find_Attacker_Indicator}}</p>",
                  "__replace": "",
                  "isImportant": false,
                  "peopleUpdated": false
                },
                "operation": "Overwrite",
                "collection": "/api/3/comments",
                "__recommend": [],
                "fieldOperation": {
                  "recordTags": "Overwrite"
                },
                "step_variables": []
              },
              "status": null,
              "top": "780",
              "left": "740",
              "stepType": "/api/3/workflow_step_types/2597053c-e718-44b4-8394-4d40fe26d357",
              "group": null,
              "uuid": "e9308e99-8201-47d1-8761-27cc70f57ca5"
            },
            {
              "@type": "WorkflowStep",
              "name": "Block IP",
              "description": null,
              "arguments": {
                "params": [],
                "version": "3.2.6",
                "connector": "cyops_utilities",
                "operation": "no_op",
                "operationTitle": "Utils: No Operation",
                "step_variables": []
              },
              "status": null,
              "top": "640",
              "left": "740",
              "stepType": "/api/3/workflow_step_types/0109f35d-090b-4a2b-bd8a-94cbc3508562",
              "group": null,
              "uuid": "19998fd2-d26d-447e-baf8-5ad184ff546d"
            },
            {
              "@type": "WorkflowStep",
              "name": "Check File Hash",
              "description": null,
              "arguments": {
                "query": {
                  "sort": [],
                  "limit": 30,
                  "logic": "AND",
                  "filters": [
                    {
                      "type": "primitive",
                      "field": "value",
                      "value": "{{vars.file_hash}}",
                      "operator": "eq",
                      "_operator": "eq"
                    }
                  ]
                },
                "module": "indicators?$limit=1",
                "step_variables": []
              },
              "status": null,
              "top": "60",
              "left": "20",
              "stepType": "/api/3/workflow_step_types/b593663d-7d13-40ce-a3a3-96dece928770",
              "group": "/api/3/workflow_groups/e7d3b349-d6de-4848-9ef9-1dce07d4a485",
              "uuid": "e17db7ea-1fc3-48bf-90f1-f29d5fe420ee"
            },
            {
              "@type": "WorkflowStep",
              "name": "cncHost Check",
              "description": null,
              "arguments": {
                "conditions": [
                  {
                    "option": "cncHost 존재",
                    "step_iri": "/api/3/workflow_steps/3d0dc47a-52cc-4c4c-845d-fbb4c49e179a",
                    "condition": "{{ vars.steps.Find_cncHost.data['code_output'] != \"\" }}",
                    "step_name": "cncHost is Cloud"
                  }
                ],
                "step_variables": []
              },
              "status": null,
              "top": "160",
              "left": "20",
              "stepType": "/api/3/workflow_step_types/12254cf5-5db7-4b1a-8cb1-3af081924b28",
              "group": "/api/3/workflow_groups/caa20612-3c9e-43f6-b9ef-771835a03af4",
              "uuid": "eaf271a7-3459-41cb-85e1-21eff0c9a2dc"
            },
            {
              "@type": "WorkflowStep",
              "name": "cncHost Cloud Check",
              "description": null,
              "arguments": {
                "conditions": [
                  {
                    "option": "cncHost가 CDN 또는 클라우드 일때",
                    "step_iri": "/api/3/workflow_steps/1209058d-cc6b-44e1-8897-0dc861e57998",
                    "condition": "{{ true }}",
                    "step_name": "Copy of Copy 2 of NOP"
                  },
                  {
                    "option": "cncHost가 CDN 또는 클라우드가 아닐때",
                    "default": true,
                    "step_iri": "/api/3/workflow_steps/20d1545b-56f5-4618-87e3-0ac78a17171a",
                    "step_name": "Copy of Copy of Copy 2 of NOP"
                  }
                ],
                "step_variables": []
              },
              "status": null,
              "top": "780",
              "left": "1200",
              "stepType": "/api/3/workflow_step_types/12254cf5-5db7-4b1a-8cb1-3af081924b28",
              "group": null,
              "uuid": "168821c8-8ef1-4784-b8a7-afd0e18e8025"
            },
            {
              "@type": "WorkflowStep",
              "name": "cncHost is Cloud",
              "description": null,
              "arguments": {
                "params": [],
                "version": "3.2.6",
                "connector": "cyops_utilities",
                "operation": "no_op",
                "operationTitle": "Utils: No Operation",
                "step_variables": []
              },
              "status": null,
              "top": "640",
              "left": "1200",
              "stepType": "/api/3/workflow_step_types/0109f35d-090b-4a2b-bd8a-94cbc3508562",
              "group": null,
              "uuid": "3d0dc47a-52cc-4c4c-845d-fbb4c49e179a"
            },
            {
              "@type": "WorkflowStep",
              "name": "Configure",
              "description": null,
              "arguments": {
                "ip_addr": "{{vars.input.params['ip_addr']}}",
                "alert_iri": "{{vars.input.params['alert_iri']}}",
                "file_hash": "{{vars.input.params['file_hash']}}",
                "alert_sourcedata": "{{vars.input.params['alert_sourcedata']}}"
              },
              "status": null,
              "top": "200",
              "left": "40",
              "stepType": "/api/3/workflow_step_types/04d0cf46-b6a8-42c4-8683-60a7eaa69e8f",
              "group": null,
              "uuid": "fbc50435-3c93-47a3-ac22-a080d8d42b4f"
            },
            {
              "@type": "WorkflowStep",
              "name": "Copy of Copy 2 of NOP",
              "description": null,
              "arguments": {
                "params": [],
                "version": "3.2.6",
                "connector": "cyops_utilities",
                "operation": "no_op",
                "operationTitle": "Utils: No Operation",
                "step_variables": []
              },
              "status": null,
              "top": "920",
              "left": "1380",
              "stepType": "/api/3/workflow_step_types/0109f35d-090b-4a2b-bd8a-94cbc3508562",
              "group": null,
              "uuid": "1209058d-cc6b-44e1-8897-0dc861e57998"
            },
            {
              "@type": "WorkflowStep",
              "name": "Copy of Copy of Copy 2 of NOP",
              "description": null,
              "arguments": {
                "params": [],
                "version": "3.2.6",
                "connector": "cyops_utilities",
                "operation": "no_op",
                "operationTitle": "Utils: No Operation",
                "step_variables": []
              },
              "status": null,
              "top": "920",
              "left": "1020",
              "stepType": "/api/3/workflow_step_types/0109f35d-090b-4a2b-bd8a-94cbc3508562",
              "group": null,
              "uuid": "20d1545b-56f5-4618-87e3-0ac78a17171a"
            },
            {
              "@type": "WorkflowStep",
              "name": "Country Comment",
              "description": null,
              "arguments": {
                "resource": {
                  "type": "/api/3/picklists/ff599189-3eeb-4c86-acb0-a7915e85ac3b",
                  "alerts": "{{vars.alert_iri}}",
                  "people": [],
                  "content": "<p>{{vars.steps.Whois_RDAP.data}}</p>",
                  "__replace": "",
                  "isImportant": false,
                  "peopleUpdated": false
                },
                "operation": "Overwrite",
                "collection": "/api/3/comments",
                "__recommend": [],
                "fieldOperation": {
                  "recordTags": "Overwrite"
                },
                "step_variables": []
              },
              "status": null,
              "top": "780",
              "left": "360",
              "stepType": "/api/3/workflow_step_types/2597053c-e718-44b4-8394-4d40fe26d357",
              "group": null,
              "uuid": "3c44fb7f-e57c-4e32-851f-438e5d3f1312"
            },
            {
              "@type": "WorkflowStep",
              "name": "Find Attacker Indicator",
              "description": null,
              "arguments": {
                "query": {
                  "sort": [],
                  "limit": 30,
                  "logic": "AND",
                  "filters": [
                    {
                      "type": "primitive",
                      "field": "value",
                      "value": "{{vars.ip_addr}}",
                      "operator": "eq",
                      "_operator": "eq"
                    },
                    {
                      "type": "object",
                      "field": "reputation",
                      "value": "/api/3/picklists/7074e547-7785-4979-be32-c6d0c863e4bd",
                      "_value": {
                        "@id": "/api/3/picklists/7074e547-7785-4979-be32-c6d0c863e4bd",
                        "display": "Malicious",
                        "itemValue": "Malicious"
                      },
                      "operator": "eq"
                    }
                  ]
                },
                "module": "indicators?$limit=1",
                "checkboxFields": true,
                "step_variables": []
              },
              "status": null,
              "top": "60",
              "left": "20",
              "stepType": "/api/3/workflow_step_types/b593663d-7d13-40ce-a3a3-96dece928770",
              "group": "/api/3/workflow_groups/b030b0c5-44ce-47f0-beb8-296ac42def78",
              "uuid": "7b629509-c319-482d-ba0c-6839f30f95ee"
            },
            {
              "@type": "WorkflowStep",
              "name": "Find cncHost",
              "description": null,
              "arguments": {
                "config": "b5195722-9917-4e6e-ac0f-cddab46620ee",
                "params": {
                  "python_function": "import re\nimport json\n\nsourcedata = {{vars.alert_sourcedata}}\n\nfor _event in sourcedata.get(\"associated_events\", {}):\n  rawMessage = _event.get(\"rawMessage\", \"\")\n  _re_search = re.search(r\"cs5Label=cncHost cs5=([-a-zA-Z0-9@:%._\\+~#=]{1,256}\\.[a-zA-Z0-9()]{1,6}\\b(?:[-a-zA-Z0-9()@:%_\\+.~#?&//=]*)) \", rawMessage)\nif _re_search:\n    print(_re_search.group())"
                },
                "version": "2.1.0",
                "connector": "code-snippet",
                "operation": "python_inline_code_editor",
                "operationTitle": "Execute Python Code",
                "step_variables": []
              },
              "status": null,
              "top": "60",
              "left": "20",
              "stepType": "/api/3/workflow_step_types/1fdd14cc-d6b4-4335-a3af-ab49c8ed2fd8",
              "group": "/api/3/workflow_groups/caa20612-3c9e-43f6-b9ef-771835a03af4",
              "uuid": "6c7826ad-562b-4225-a285-d119ca782759"
            },
            {
              "@type": "WorkflowStep",
              "name": "Find IP in Indicator",
              "description": null,
              "arguments": {
                "query": {
                  "sort": [],
                  "limit": 30,
                  "logic": "AND",
                  "filters": [
                    {
                      "type": "primitive",
                      "field": "value",
                      "value": "{{vars.ip_addr}}",
                      "operator": "eq",
                      "_operator": "eq"
                    }
                  ],
                  "__selectFields": [
                    "sourceData"
                  ]
                },
                "module": "indicators?$limit=1",
                "checkboxFields": true,
                "step_variables": []
              },
              "status": null,
              "top": "340",
              "left": "40",
              "stepType": "/api/3/workflow_step_types/b593663d-7d13-40ce-a3a3-96dece928770",
              "group": null,
              "uuid": "3f6ceb0c-ddde-4860-9401-16a6e11653b7"
            },
            {
              "@type": "WorkflowStep",
              "name": "Hash Block",
              "description": null,
              "arguments": {
                "params": [],
                "version": "3.2.6",
                "connector": "cyops_utilities",
                "operation": "no_op",
                "operationTitle": "Utils: No Operation",
                "step_variables": []
              },
              "status": null,
              "top": "640",
              "left": "1640",
              "stepType": "/api/3/workflow_step_types/0109f35d-090b-4a2b-bd8a-94cbc3508562",
              "group": null,
              "uuid": "1bbfd8ae-3323-4ecd-a066-05535d570230"
            },
            {
              "@type": "WorkflowStep",
              "name": "Hash Check",
              "description": null,
              "arguments": {
                "conditions": [
                  {
                    "option": "해쉬 악성",
                    "step_iri": "/api/3/workflow_steps/1bbfd8ae-3323-4ecd-a066-05535d570230",
                    "condition": "{{ vars.steps.Check_File_Hash | length > 0 and vars.steps.Check_File_Hash[0].reputation.itemValue == \"Malicious\" }}",
                    "step_name": "Hash Block"
                  },
                  {
                    "option": "TI 정보 없음",
                    "default": true,
                    "step_iri": "/api/3/workflow_steps/f50f8ef1-c9f1-4181-8c9a-5576eaef2a02",
                    "step_name": "NOP 11"
                  }
                ],
                "step_variables": []
              },
              "status": null,
              "top": "160",
              "left": "20",
              "stepType": "/api/3/workflow_step_types/12254cf5-5db7-4b1a-8cb1-3af081924b28",
              "group": "/api/3/workflow_groups/e7d3b349-d6de-4848-9ef9-1dce07d4a485",
              "uuid": "822c61ea-9a18-451a-8b0a-af95f75cc8f3"
            },
            {
              "@type": "WorkflowStep",
              "name": "is Private IP",
              "description": null,
              "arguments": {
                "params": {
                  "cidr": "10.0.0.0/8,172.16.0.0/12,192.168.0.0/16",
                  "ip_address": "{{vars.ip_addr}}"
                },
                "version": "3.2.6",
                "connector": "cyops_utilities",
                "operation": "ip_cidr_check",
                "operationTitle": "Utils: Is IP in CIDR",
                "step_variables": []
              },
              "status": null,
              "top": "60",
              "left": "20",
              "stepType": "/api/3/workflow_step_types/0109f35d-090b-4a2b-bd8a-94cbc3508562",
              "group": "/api/3/workflow_groups/f6138a81-8241-490b-9c44-51e440754e4f",
              "uuid": "e400d75a-e491-4242-b487-e2e2fd8265df"
            },
            {
              "@type": "WorkflowStep",
              "name": "is Private IP Check",
              "description": null,
              "arguments": {
                "conditions": [
                  {
                    "option": "내부 IP",
                    "step_iri": "/api/3/workflow_steps/7b629509-c319-482d-ba0c-6839f30f95ee",
                    "condition": "{{ vars.steps.is_Private_IP.data['ip_matched'] }}",
                    "step_name": "Find Attacker Indicator"
                  },
                  {
                    "option": "외부 IP",
                    "default": true,
                    "step_iri": "/api/3/workflow_steps/2f989ae2-53e4-450c-99ae-e5a2bb2866f0",
                    "step_name": "Whois RDAP"
                  }
                ],
                "step_variables": []
              },
              "status": null,
              "top": "140",
              "left": "20",
              "stepType": "/api/3/workflow_step_types/12254cf5-5db7-4b1a-8cb1-3af081924b28",
              "group": "/api/3/workflow_groups/f6138a81-8241-490b-9c44-51e440754e4f",
              "uuid": "b974a120-787c-4f3b-848f-be998cbf6b64"
            },
            {
              "@type": "WorkflowStep",
              "name": "NOP",
              "description": null,
              "arguments": {
                "params": [],
                "version": "3.2.6",
                "connector": "cyops_utilities",
                "operation": "no_op",
                "operationTitle": "Utils: No Operation",
                "step_variables": []
              },
              "status": null,
              "top": "680",
              "left": "360",
              "stepType": "/api/3/workflow_step_types/0109f35d-090b-4a2b-bd8a-94cbc3508562",
              "group": null,
              "uuid": "673079ff-c24b-4598-9764-794bda5eb1be"
            },
            {
              "@type": "WorkflowStep",
              "name": "NOP 11",
              "description": null,
              "arguments": {
                "params": [],
                "version": "3.2.6",
                "connector": "cyops_utilities",
                "operation": "no_op",
                "operationTitle": "Utils: No Operation",
                "step_variables": []
              },
              "status": null,
              "top": "320",
              "left": "1980",
              "stepType": "/api/3/workflow_step_types/0109f35d-090b-4a2b-bd8a-94cbc3508562",
              "group": null,
              "uuid": "f50f8ef1-c9f1-4181-8c9a-5576eaef2a02"
            },
            {
              "@type": "WorkflowStep",
              "name": "Process Isolation",
              "description": null,
              "arguments": {
                "params": [],
                "version": "3.2.6",
                "connector": "cyops_utilities",
                "operation": "no_op",
                "operationTitle": "Utils: No Operation",
                "step_variables": []
              },
              "status": null,
              "top": "780",
              "left": "1640",
              "stepType": "/api/3/workflow_step_types/0109f35d-090b-4a2b-bd8a-94cbc3508562",
              "group": null,
              "uuid": "04e60b0e-482d-4c5e-a699-3ca39b41d830"
            },
            {
              "@type": "WorkflowStep",
              "name": "Set SourceData",
              "description": null,
              "arguments": {
                "sourcedata": "{{vars.steps.Find_IP_in_Indicator[0].0.sourceData}}"
              },
              "status": null,
              "top": "460",
              "left": "40",
              "stepType": "/api/3/workflow_step_types/04d0cf46-b6a8-42c4-8683-60a7eaa69e8f",
              "group": null,
              "uuid": "dd4ac602-81fc-4c8b-8de4-29aec2b0b444"
            },
            {
              "@type": "WorkflowStep",
              "name": "Start",
              "description": null,
              "arguments": {
                "__triggerLimit": true,
                "step_variables": {
                  "input": {
                    "params": []
                  }
                },
                "triggerOnSource": true,
                "triggerOnReplicate": false
              },
              "status": null,
              "top": "60",
              "left": "40",
              "stepType": "/api/3/workflow_step_types/b348f017-9a94-471f-87f8-ce88b6a7ad62",
              "group": null,
              "uuid": "4d2d1384-ff69-472a-8a29-224b8604b422"
            },
            {
              "@type": "WorkflowStep",
              "name": "Whois Check",
              "description": null,
              "arguments": {
                "conditions": [
                  {
                    "option": "해외 IP",
                    "step_iri": "/api/3/workflow_steps/673079ff-c24b-4598-9764-794bda5eb1be",
                    "condition": "{{ vars.steps.Whois_RDAP.data['asn_country_code'] != \"KR\" }}",
                    "step_name": "NOP"
                  },
                  {
                    "option": "한국 IP",
                    "default": true,
                    "step_iri": "/api/3/workflow_steps/7b629509-c319-482d-ba0c-6839f30f95ee",
                    "step_name": "Find Attacker TI"
                  }
                ],
                "step_variables": []
              },
              "status": null,
              "top": "380",
              "left": "20",
              "stepType": "/api/3/workflow_step_types/12254cf5-5db7-4b1a-8cb1-3af081924b28",
              "group": "/api/3/workflow_groups/f6138a81-8241-490b-9c44-51e440754e4f",
              "uuid": "070d4571-3fdf-4987-bdcd-8f28c02226cf"
            },
            {
              "@type": "WorkflowStep",
              "name": "Whois RDAP",
              "description": null,
              "arguments": {
                "name": "Whois RDAP",
                "config": "eca9db2d-a2eb-4c4a-ae2c-2c50f9fe9d67",
                "params": {
                  "ip": "1.1.1.1"
                },
                "version": "1.0.2",
                "connector": "whois-rdap",
                "operation": "whois_ip",
                "ignore_errors": false,
                "operationTitle": "Whois IP",
                "pickFromTenant": false,
                "step_variables": []
              },
              "status": null,
              "top": "300",
              "left": "20",
              "stepType": "/api/3/workflow_step_types/0bfed618-0316-11e7-93ae-92361f002671",
              "group": "/api/3/workflow_groups/f6138a81-8241-490b-9c44-51e440754e4f",
              "uuid": "2f989ae2-53e4-450c-99ae-e5a2bb2866f0"
            }
          ],
          "routes": [
            {
              "@type": "WorkflowRoute",
              "name": "Attacker TI Check -> Copy 1 of NOP",
              "targetStep": "/api/3/workflow_steps/19998fd2-d26d-447e-baf8-5ad184ff546d",
              "sourceStep": "/api/3/workflow_steps/43f27847-c46a-4d16-a056-5021fe97a7c8",
              "label": "차단",
              "isExecuted": false,
              "group": null,
              "uuid": "a9095e09-69ac-4d27-ad08-513868eb53ab"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Attacker TI Check -> Find cncHost",
              "targetStep": "/api/3/workflow_steps/6c7826ad-562b-4225-a285-d119ca782759",
              "sourceStep": "/api/3/workflow_steps/43f27847-c46a-4d16-a056-5021fe97a7c8",
              "label": "TI에 없음",
              "isExecuted": false,
              "group": null,
              "uuid": "5f0166dc-e9ef-4a91-8349-d78ce39e6b6c"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Block IP -> Copy of Country Comment",
              "targetStep": "/api/3/workflow_steps/e9308e99-8201-47d1-8761-27cc70f57ca5",
              "sourceStep": "/api/3/workflow_steps/19998fd2-d26d-447e-baf8-5ad184ff546d",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "8b1eb603-cda4-441c-af36-e868d086081c"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Check File Hash -> Copy of cncHost Check",
              "targetStep": "/api/3/workflow_steps/822c61ea-9a18-451a-8b0a-af95f75cc8f3",
              "sourceStep": "/api/3/workflow_steps/e17db7ea-1fc3-48bf-90f1-f29d5fe420ee",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "4ffd40d2-860a-4be6-ac3a-3f622990a990"
            },
            {
              "@type": "WorkflowRoute",
              "name": "cncHost Check -> Check File Hash",
              "targetStep": "/api/3/workflow_steps/e17db7ea-1fc3-48bf-90f1-f29d5fe420ee",
              "sourceStep": "/api/3/workflow_steps/eaf271a7-3459-41cb-85e1-21eff0c9a2dc",
              "label": "",
              "isExecuted": false,
              "group": null,
              "uuid": "453f9b6f-ba57-44ea-a85e-02d1f2b48e42"
            },
            {
              "@type": "WorkflowRoute",
              "name": "cncHost Check -> Copy of NOP",
              "targetStep": "/api/3/workflow_steps/3d0dc47a-52cc-4c4c-845d-fbb4c49e179a",
              "sourceStep": "/api/3/workflow_steps/eaf271a7-3459-41cb-85e1-21eff0c9a2dc",
              "label": "cncHost 존재",
              "isExecuted": false,
              "group": null,
              "uuid": "fa26f0e3-e301-417f-bc12-1f821caaa9f3"
            },
            {
              "@type": "WorkflowRoute",
              "name": "cncHost Cloud Check -> Copy of Copy 2 of NOP",
              "targetStep": "/api/3/workflow_steps/1209058d-cc6b-44e1-8897-0dc861e57998",
              "sourceStep": "/api/3/workflow_steps/168821c8-8ef1-4784-b8a7-afd0e18e8025",
              "label": "cncHost가 CDN 또는 클라우드 일때",
              "isExecuted": false,
              "group": null,
              "uuid": "869c31ff-843a-40ef-a01f-daa06ba2637a"
            },
            {
              "@type": "WorkflowRoute",
              "name": "cncHost Cloud Check -> Copy of Copy of Copy 2 of NOP",
              "targetStep": "/api/3/workflow_steps/20d1545b-56f5-4618-87e3-0ac78a17171a",
              "sourceStep": "/api/3/workflow_steps/168821c8-8ef1-4784-b8a7-afd0e18e8025",
              "label": "cncHost가 CDN 또는 클라우드가 아닐때",
              "isExecuted": false,
              "group": null,
              "uuid": "0df1ca15-e885-4225-b56c-ae2a0ae7558a"
            },
            {
              "@type": "WorkflowRoute",
              "name": "cncHost is Cloud -> Check File Hash",
              "targetStep": "/api/3/workflow_steps/e17db7ea-1fc3-48bf-90f1-f29d5fe420ee",
              "sourceStep": "/api/3/workflow_steps/3d0dc47a-52cc-4c4c-845d-fbb4c49e179a",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "eb83f56f-d24f-49d3-b076-2e844386b875"
            },
            {
              "@type": "WorkflowRoute",
              "name": "cncHost is Cloud -> Copy 1 of cncHost Check",
              "targetStep": "/api/3/workflow_steps/168821c8-8ef1-4784-b8a7-afd0e18e8025",
              "sourceStep": "/api/3/workflow_steps/3d0dc47a-52cc-4c4c-845d-fbb4c49e179a",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "6c9d83d3-7258-4818-a59a-16f866157253"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Configure -> Find IP in Indicator",
              "targetStep": "/api/3/workflow_steps/3f6ceb0c-ddde-4860-9401-16a6e11653b7",
              "sourceStep": "/api/3/workflow_steps/fbc50435-3c93-47a3-ac22-a080d8d42b4f",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "dbaa2cb1-5c8f-49c0-9c49-88ff80c565ff"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Copy 2 of NOP -> Copy 1 of Copy 2 of NOP",
              "targetStep": "/api/3/workflow_steps/04e60b0e-482d-4c5e-a699-3ca39b41d830",
              "sourceStep": "/api/3/workflow_steps/1bbfd8ae-3323-4ecd-a066-05535d570230",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "93d63f1b-5961-4494-ac73-4979acd8ffbb"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Country Comment -> Find Attacker Indicator",
              "targetStep": "/api/3/workflow_steps/7b629509-c319-482d-ba0c-6839f30f95ee",
              "sourceStep": "/api/3/workflow_steps/3c44fb7f-e57c-4e32-851f-438e5d3f1312",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "d9fdc130-e5d0-4d87-9c02-ead99a127613"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Find Attacker TI -> Copy of Whois Check",
              "targetStep": "/api/3/workflow_steps/43f27847-c46a-4d16-a056-5021fe97a7c8",
              "sourceStep": "/api/3/workflow_steps/7b629509-c319-482d-ba0c-6839f30f95ee",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "1f5a326c-28a9-41c5-aef8-ef9e8b4cf11e"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Find cncHost -> Copy of Attacker TI Check",
              "targetStep": "/api/3/workflow_steps/eaf271a7-3459-41cb-85e1-21eff0c9a2dc",
              "sourceStep": "/api/3/workflow_steps/6c7826ad-562b-4225-a285-d119ca782759",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "5fb0b5af-5307-4b04-a796-b4bff885a547"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Find IP in Indicator -> Set SourceData",
              "targetStep": "/api/3/workflow_steps/dd4ac602-81fc-4c8b-8de4-29aec2b0b444",
              "sourceStep": "/api/3/workflow_steps/3f6ceb0c-ddde-4860-9401-16a6e11653b7",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "475b3f6b-2136-4572-8948-531d8919c2aa"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Hash Check -> Copy 2 of NOP",
              "targetStep": "/api/3/workflow_steps/1bbfd8ae-3323-4ecd-a066-05535d570230",
              "sourceStep": "/api/3/workflow_steps/822c61ea-9a18-451a-8b0a-af95f75cc8f3",
              "label": "해쉬 악성",
              "isExecuted": false,
              "group": null,
              "uuid": "9a22f0b5-1b9e-4f98-be29-0ab206d93ca9"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Hash Check -> Copy of Hash Block",
              "targetStep": "/api/3/workflow_steps/f50f8ef1-c9f1-4181-8c9a-5576eaef2a02",
              "sourceStep": "/api/3/workflow_steps/822c61ea-9a18-451a-8b0a-af95f75cc8f3",
              "label": "TI 정보 없음",
              "isExecuted": false,
              "group": null,
              "uuid": "49bb855b-e560-464a-a83b-dec5f8c25ef3"
            },
            {
              "@type": "WorkflowRoute",
              "name": "is Private IP Check -> Find Attacker Indicator",
              "targetStep": "/api/3/workflow_steps/7b629509-c319-482d-ba0c-6839f30f95ee",
              "sourceStep": "/api/3/workflow_steps/b974a120-787c-4f3b-848f-be998cbf6b64",
              "label": "내부 IP",
              "isExecuted": false,
              "group": null,
              "uuid": "784aa25d-c148-468d-99c4-28d1b2952a85"
            },
            {
              "@type": "WorkflowRoute",
              "name": "is Private IP Check -> Whois RDAP",
              "targetStep": "/api/3/workflow_steps/2f989ae2-53e4-450c-99ae-e5a2bb2866f0",
              "sourceStep": "/api/3/workflow_steps/b974a120-787c-4f3b-848f-be998cbf6b64",
              "label": "외부 IP",
              "isExecuted": false,
              "group": null,
              "uuid": "64de78af-20d0-4350-a217-5a6e3e1990a1"
            },
            {
              "@type": "WorkflowRoute",
              "name": "is Private IP -> is Private IP Check",
              "targetStep": "/api/3/workflow_steps/b974a120-787c-4f3b-848f-be998cbf6b64",
              "sourceStep": "/api/3/workflow_steps/e400d75a-e491-4242-b487-e2e2fd8265df",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "8dbc5cf5-9499-4186-9986-065e8391bb19"
            },
            {
              "@type": "WorkflowRoute",
              "name": "NOP -> Country Comment",
              "targetStep": "/api/3/workflow_steps/3c44fb7f-e57c-4e32-851f-438e5d3f1312",
              "sourceStep": "/api/3/workflow_steps/673079ff-c24b-4598-9764-794bda5eb1be",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "aca2dad1-cb92-4f33-b57a-daf8e051723b"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Set SourceData -> is Private IP",
              "targetStep": "/api/3/workflow_steps/e400d75a-e491-4242-b487-e2e2fd8265df",
              "sourceStep": "/api/3/workflow_steps/dd4ac602-81fc-4c8b-8de4-29aec2b0b444",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "1fff8645-8501-4750-962a-ad5e6d44d338"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Start -> Configure",
              "targetStep": "/api/3/workflow_steps/fbc50435-3c93-47a3-ac22-a080d8d42b4f",
              "sourceStep": "/api/3/workflow_steps/4d2d1384-ff69-472a-8a29-224b8604b422",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "9146010b-fce4-4ace-892f-ec61348f6235"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Whois Check -> Find Attacker TI",
              "targetStep": "/api/3/workflow_steps/7b629509-c319-482d-ba0c-6839f30f95ee",
              "sourceStep": "/api/3/workflow_steps/070d4571-3fdf-4987-bdcd-8f28c02226cf",
              "label": "한국 IP",
              "isExecuted": false,
              "group": null,
              "uuid": "1056d2f4-8cca-495e-91ad-ae02458e777f"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Whois Check -> NOP",
              "targetStep": "/api/3/workflow_steps/673079ff-c24b-4598-9764-794bda5eb1be",
              "sourceStep": "/api/3/workflow_steps/070d4571-3fdf-4987-bdcd-8f28c02226cf",
              "label": "해외 IP",
              "isExecuted": false,
              "group": null,
              "uuid": "1a719b3a-f2cb-4198-9ff3-200d757da02f"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Whois RDAP -> Whois Check",
              "targetStep": "/api/3/workflow_steps/070d4571-3fdf-4987-bdcd-8f28c02226cf",
              "sourceStep": "/api/3/workflow_steps/2f989ae2-53e4-450c-99ae-e5a2bb2866f0",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "4140c739-4b91-4c84-958a-1b962b5e3c07"
            }
          ],
          "groups": [
            {
              "@type": "WorkflowGroup",
              "name": "위협 국가 분기",
              "description": "",
              "type": "block",
              "isCollapsed": false,
              "hasTriggerStep": false,
              "hideInLogs": false,
              "metadata": [],
              "reusable": false,
              "top": "160",
              "left": "340",
              "height": "470",
              "width": "290",
              "uuid": "f6138a81-8241-490b-9c44-51e440754e4f",
              "recordTags": []
            },
            {
              "@type": "WorkflowGroup",
              "name": "C&C 존재",
              "description": "",
              "type": "block",
              "isCollapsed": false,
              "hasTriggerStep": false,
              "hideInLogs": false,
              "metadata": [],
              "reusable": false,
              "top": "160",
              "left": "1180",
              "height": "246",
              "width": "274",
              "uuid": "caa20612-3c9e-43f6-b9ef-771835a03af4",
              "recordTags": []
            },
            {
              "@type": "WorkflowGroup",
              "name": "Hash TI 결과",
              "description": "",
              "type": "block",
              "isCollapsed": false,
              "hasTriggerStep": false,
              "hideInLogs": false,
              "metadata": [],
              "reusable": false,
              "top": "160",
              "left": "1620",
              "height": "243",
              "width": "282",
              "uuid": "e7d3b349-d6de-4848-9ef9-1dce07d4a485",
              "recordTags": []
            },
            {
              "@type": "WorkflowGroup",
              "name": "공격자 TI 결과",
              "description": "",
              "type": "block",
              "isCollapsed": false,
              "hasTriggerStep": false,
              "hideInLogs": false,
              "metadata": [],
              "reusable": false,
              "top": "160",
              "left": "720",
              "height": "248",
              "width": "288",
              "uuid": "b030b0c5-44ce-47f0-beb8-296ac42def78",
              "recordTags": []
            }
          ],
          "priority": "/api/3/picklists/2b563c61-ae2c-41c0-a85a-c9709585e3f2",
          "uuid": "42f2e847-938f-4a65-841d-7ec05afdd508",
          "id": 854,
          "owners": [],
          "isPrivate": false,
          "deletedAt": null,
          "importedBy": [],
          "recordTags": []
        },
        {
          "@type": "Workflow",
          "triggerLimit": null,
          "name": "00 - BC Card Scenario 1 > Check Internal TI",
          "aliasName": null,
          "tag": null,
          "description": null,
          "isActive": true,
          "debug": true,
          "singleRecordExecution": false,
          "remoteExecutableFlag": false,
          "parameters": [
            "ip_addr"
          ],
          "synchronous": false,
          "lastModifyDate": 1712022908,
          "collection": "/api/3/workflow_collections/63c971df-3a2d-4868-a827-537dcc408421",
          "versions": [],
          "triggerStep": "/api/3/workflow_steps/fdcf4226-dca1-48c0-aecc-0a91ff2ed22e",
          "steps": [
            {
              "@type": "WorkflowStep",
              "name": "Configure",
              "description": null,
              "arguments": {
                "ip_addr": "{{vars.input.params['ip_addr']}}"
              },
              "status": null,
              "top": "165",
              "left": "125",
              "stepType": "/api/3/workflow_step_types/04d0cf46-b6a8-42c4-8683-60a7eaa69e8f",
              "group": null,
              "uuid": "4c8829bc-bfce-4a28-9d08-8dba24905e80"
            },
            {
              "@type": "WorkflowStep",
              "name": "Find Internal TI Value",
              "description": null,
              "arguments": {
                "query": {
                  "sort": [],
                  "limit": 30,
                  "logic": "AND",
                  "filters": [
                    {
                      "type": "primitive",
                      "field": "value",
                      "value": "{{vars.ip_addr}}",
                      "operator": "eq",
                      "_operator": "eq"
                    },
                    {
                      "type": "array",
                      "field": "typeOfFeed",
                      "value": [
                        "b788efc2-dadb-4448-9018-043b37266de4",
                        "7a874c06-b65b-4850-9dd0-ff1c1db6491f"
                      ],
                      "module": "typeOfFeed",
                      "display": "",
                      "operator": "in",
                      "template": "multiselectpicklist",
                      "enableJinja": true,
                      "OPERATOR_KEY": "$",
                      "useInOperator": true,
                      "previousOperator": "in",
                      "previousTemplate": "multiselectpicklist"
                    }
                  ]
                },
                "module": "threat_intel_feeds?$limit=1",
                "checkboxFields": true,
                "step_variables": []
              },
              "status": null,
              "top": "300",
              "left": "125",
              "stepType": "/api/3/workflow_step_types/b593663d-7d13-40ce-a3a3-96dece928770",
              "group": null,
              "uuid": "65002508-62b1-4839-9efe-5e3eaa1187d2"
            },
            {
              "@type": "WorkflowStep",
              "name": "Return",
              "description": null,
              "arguments": {
                "retval": "{{vars.steps.Find_Internal_TI_Value | length > 0}}"
              },
              "status": null,
              "top": "435",
              "left": "125",
              "stepType": "/api/3/workflow_step_types/04d0cf46-b6a8-42c4-8683-60a7eaa69e8f",
              "group": null,
              "uuid": "5f8ad7dc-5756-4225-9116-1cd0fa7bfc08"
            },
            {
              "@type": "WorkflowStep",
              "name": "Start",
              "description": null,
              "arguments": {
                "__triggerLimit": true,
                "step_variables": {
                  "input": {
                    "params": []
                  }
                },
                "triggerOnSource": true,
                "triggerOnReplicate": false
              },
              "status": null,
              "top": "30",
              "left": "125",
              "stepType": "/api/3/workflow_step_types/b348f017-9a94-471f-87f8-ce88b6a7ad62",
              "group": null,
              "uuid": "fdcf4226-dca1-48c0-aecc-0a91ff2ed22e"
            }
          ],
          "routes": [
            {
              "@type": "WorkflowRoute",
              "name": "Configure -> Find Whitelist Value",
              "targetStep": "/api/3/workflow_steps/65002508-62b1-4839-9efe-5e3eaa1187d2",
              "sourceStep": "/api/3/workflow_steps/4c8829bc-bfce-4a28-9d08-8dba24905e80",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "297f432b-7c10-4d3b-b581-fecb4066ebd0"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Find Whitelist Value -> Return",
              "targetStep": "/api/3/workflow_steps/5f8ad7dc-5756-4225-9116-1cd0fa7bfc08",
              "sourceStep": "/api/3/workflow_steps/65002508-62b1-4839-9efe-5e3eaa1187d2",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "eb3d12ed-4440-4d1f-80c0-73d2feaaa8b2"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Start -> Configure",
              "targetStep": "/api/3/workflow_steps/4c8829bc-bfce-4a28-9d08-8dba24905e80",
              "sourceStep": "/api/3/workflow_steps/fdcf4226-dca1-48c0-aecc-0a91ff2ed22e",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "acf8e636-15bf-4c0f-911a-9f70d14be796"
            }
          ],
          "groups": [],
          "priority": "/api/3/picklists/2b563c61-ae2c-41c0-a85a-c9709585e3f2",
          "uuid": "7abca430-74a5-4cfb-b557-5651c2ecc7cb",
          "id": 851,
          "owners": [],
          "isPrivate": false,
          "deletedAt": null,
          "importedBy": [],
          "recordTags": []
        },
        {
          "@type": "Workflow",
          "triggerLimit": null,
          "name": "00 - BC Card Scenario 1 > Pivot Query",
          "aliasName": null,
          "tag": null,
          "description": null,
          "isActive": true,
          "debug": true,
          "singleRecordExecution": false,
          "remoteExecutableFlag": false,
          "parameters": [
            "ip_addr",
            "incidentLastSeen",
            "alert_iri"
          ],
          "synchronous": false,
          "lastModifyDate": 1712040779,
          "collection": "/api/3/workflow_collections/63c971df-3a2d-4868-a827-537dcc408421",
          "versions": [],
          "triggerStep": "/api/3/workflow_steps/1e75bf5d-fc88-42c9-a357-7d658c84eaea",
          "steps": [
            {
              "@type": "WorkflowStep",
              "name": "Configure",
              "description": null,
              "arguments": {
                "ip_addr": "{{vars.input.params['ip_addr']}}",
                "alert_iri": "{{vars.input.params['alert_iri']}}",
                "incidentLastSeen": "{{vars.input.params.incidentLastSeen}}"
              },
              "status": null,
              "top": "165",
              "left": "125",
              "stepType": "/api/3/workflow_step_types/04d0cf46-b6a8-42c4-8683-60a7eaa69e8f",
              "group": null,
              "uuid": "ef9b4ee6-4fec-4906-96c3-f66b52d9bdc4"
            },
            {
              "@type": "WorkflowStep",
              "name": "Create FSM Events",
              "description": null,
              "arguments": {
                "for_each": {
                  "item": "{{vars.steps.FSM_Pivot_Query.data.events}}",
                  "__bulk": true,
                  "parallel": false,
                  "condition": "",
                  "batch_size": 100
                },
                "resource": {
                  "name": "{{vars.item.attributes.eventName}}",
                  "alerts": "{{vars.alert_iri}}",
                  "sourceId": "{{vars.item.id}}",
                  "__replace": "",
                  "sourceJSON": "{{vars.item | toJSON}}"
                },
                "_showJson": false,
                "operation": "Overwrite",
                "collection": "/api/3/events",
                "__recommend": [],
                "fieldOperation": {
                  "recordTags": "Overwrite"
                },
                "step_variables": []
              },
              "status": null,
              "top": "435",
              "left": "125",
              "stepType": "/api/3/workflow_step_types/2597053c-e718-44b4-8394-4d40fe26d357",
              "group": null,
              "uuid": "8dcaf41c-c22b-4ec8-88c0-0f9041174bf9"
            },
            {
              "@type": "WorkflowStep",
              "name": "FSM Pivot Query",
              "description": null,
              "arguments": {
                "name": "Fortinet FortiSIEM",
                "config": "d81f309e-6287-4d74-9526-30a0b1ce0c8c",
                "params": {
                  "to": "{{arrow.get(vars.incidentLastSeen + (60*5)).format(\"YYYY-MM-DDTHH:mm:ss.SSS\")}}Z",
                  "from": "{{arrow.get(vars.incidentLastSeen - (60*5)).format(\"YYYY-MM-DDTHH:mm:ss.SSS\")}}Z",
                  "start": 0,
                  "perPage": 50,
                  "attribute": [
                    "Destination IP"
                  ],
                  "select_clause": "phRecvTime,reptDevIpAddr,eventType,eventName,srcIpAddr,destIpAddr,user,rawEventMsg",
                  "time_selection": "Absolute Time",
                  "destination_ip_value": "{{vars.ip_addr}}"
                },
                "version": "5.2.0",
                "connector": "fortinet-fortisiem",
                "operation": "search_events",
                "operationTitle": "Search Events",
                "pickFromTenant": false,
                "step_variables": []
              },
              "status": null,
              "top": "300",
              "left": "125",
              "stepType": "/api/3/workflow_step_types/0bfed618-0316-11e7-93ae-92361f002671",
              "group": null,
              "uuid": "20ea6db2-cbbe-4f9e-81eb-2eed9e34f53c"
            },
            {
              "@type": "WorkflowStep",
              "name": "Start",
              "description": null,
              "arguments": {
                "__triggerLimit": true,
                "step_variables": {
                  "input": {
                    "params": []
                  }
                },
                "triggerOnSource": true,
                "triggerOnReplicate": false
              },
              "status": null,
              "top": "30",
              "left": "125",
              "stepType": "/api/3/workflow_step_types/b348f017-9a94-471f-87f8-ce88b6a7ad62",
              "group": null,
              "uuid": "1e75bf5d-fc88-42c9-a357-7d658c84eaea"
            }
          ],
          "routes": [
            {
              "@type": "WorkflowRoute",
              "name": "Configure -> asd",
              "targetStep": "/api/3/workflow_steps/20ea6db2-cbbe-4f9e-81eb-2eed9e34f53c",
              "sourceStep": "/api/3/workflow_steps/ef9b4ee6-4fec-4906-96c3-f66b52d9bdc4",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "2fea44e3-cf1c-4395-9860-8f3a2b2d6c3a"
            },
            {
              "@type": "WorkflowRoute",
              "name": "FSM Pivot Query -> Create FSM Events",
              "targetStep": "/api/3/workflow_steps/8dcaf41c-c22b-4ec8-88c0-0f9041174bf9",
              "sourceStep": "/api/3/workflow_steps/20ea6db2-cbbe-4f9e-81eb-2eed9e34f53c",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "afc20467-b057-4f15-ad9f-4ea4a1de90e0"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Start -> Configure",
              "targetStep": "/api/3/workflow_steps/ef9b4ee6-4fec-4906-96c3-f66b52d9bdc4",
              "sourceStep": "/api/3/workflow_steps/1e75bf5d-fc88-42c9-a357-7d658c84eaea",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "d0e4aa9c-8616-4911-8d34-62ca670bc24b"
            }
          ],
          "groups": [],
          "priority": "/api/3/picklists/2b563c61-ae2c-41c0-a85a-c9709585e3f2",
          "uuid": "a6265e33-3391-401e-a831-42d9ff470cc7",
          "id": 852,
          "owners": [],
          "isPrivate": false,
          "deletedAt": null,
          "importedBy": [],
          "recordTags": []
        },
        {
          "@type": "Workflow",
          "triggerLimit": null,
          "name": "00 - BC Card Scenario 1 > Alert",
          "aliasName": null,
          "tag": null,
          "description": null,
          "isActive": true,
          "debug": false,
          "singleRecordExecution": false,
          "remoteExecutableFlag": false,
          "parameters": [],
          "synchronous": false,
          "lastModifyDate": 1712042457,
          "collection": "/api/3/workflow_collections/63c971df-3a2d-4868-a827-537dcc408421",
          "versions": [],
          "triggerStep": "/api/3/workflow_steps/7e571a43-44ba-4697-8252-a8f5a3e03433",
          "steps": [
            {
              "@type": "WorkflowStep",
              "name": "Auto Close",
              "description": null,
              "arguments": [],
              "status": null,
              "top": "700",
              "left": "880",
              "stepType": "/api/3/workflow_step_types/04d0cf46-b6a8-42c4-8683-60a7eaa69e8f",
              "group": null,
              "uuid": "58139c3f-2a07-44f1-b92d-e832d3936f29"
            },
            {
              "@type": "WorkflowStep",
              "name": "Check Blacklist Destination IP",
              "description": null,
              "arguments": {
                "arguments": {
                  "ip_addr": "{{vars.dst_ip}}"
                },
                "apply_async": false,
                "step_variables": [],
                "pass_parent_env": false,
                "pass_input_record": false,
                "workflowReference": "/api/3/workflows/fd86c039-206d-4f5e-a42c-6535937310a2"
              },
              "status": null,
              "top": "40",
              "left": "20",
              "stepType": "/api/3/workflow_step_types/74932bdc-b8b6-4d24-88c4-1a4dfbc524f3",
              "group": "/api/3/workflow_groups/199092c5-4dd7-43fc-bdb7-afa677feac66",
              "uuid": "3cf2d95f-c7f4-4fec-8a0f-b5366e6621ed"
            },
            {
              "@type": "WorkflowStep",
              "name": "Check Blacklist IP",
              "description": null,
              "arguments": {
                "conditions": [
                  {
                    "option": "dst_ip가 blacklist에 있을때",
                    "step_iri": "/api/3/workflow_steps/58139c3f-2a07-44f1-b92d-e832d3936f29",
                    "condition": "{{ vars.steps.Check_Blacklist_Destination_IP.retval }}",
                    "step_name": "Auto Close"
                  },
                  {
                    "option": "dst_ip가 blacklist에 없을때",
                    "default": true,
                    "step_iri": "/api/3/workflow_steps/bb3e6c0e-f649-418d-977e-c8ef3fc62342",
                    "step_name": "Configure 2"
                  }
                ],
                "step_variables": []
              },
              "status": null,
              "top": "140",
              "left": "40",
              "stepType": "/api/3/workflow_step_types/12254cf5-5db7-4b1a-8cb1-3af081924b28",
              "group": "/api/3/workflow_groups/199092c5-4dd7-43fc-bdb7-afa677feac66",
              "uuid": "b1e04f3e-f5f3-4ea6-9d9d-c3777bcd776f"
            },
            {
              "@type": "WorkflowStep",
              "name": "Check External TI",
              "description": null,
              "arguments": [],
              "status": null,
              "top": "340",
              "left": "1280",
              "stepType": "/api/3/workflow_step_types/04d0cf46-b6a8-42c4-8683-60a7eaa69e8f",
              "group": null,
              "uuid": "c7e34a1b-0125-4e57-a5c8-035e16a8f402"
            },
            {
              "@type": "WorkflowStep",
              "name": "Check Hash 1",
              "description": null,
              "arguments": {
                "conditions": [
                  {
                    "option": "원본 파일 수집",
                    "step_iri": "/api/3/workflow_steps/eea45005-3bc8-4cbe-aa16-59aeb7a0464b",
                    "condition": "{{ vars.input.records[0].fileHash != '\"\"' }}",
                    "step_name": "Collect File EDR"
                  },
                  {
                    "option": "평결",
                    "default": true,
                    "step_iri": "/api/3/workflow_steps/9e815c4b-241a-44e7-8a75-b009224c91ff",
                    "step_name": "Configure 3"
                  }
                ],
                "step_variables": []
              },
              "status": null,
              "top": "300",
              "left": "1680",
              "stepType": "/api/3/workflow_step_types/12254cf5-5db7-4b1a-8cb1-3af081924b28",
              "group": null,
              "uuid": "cc578fa4-b129-4c74-bfa3-044ff1564242"
            },
            {
              "@type": "WorkflowStep",
              "name": "Check Internal TI",
              "description": null,
              "arguments": {
                "arguments": {
                  "ip_addr": "{{vars.dst_ip}}"
                },
                "apply_async": false,
                "step_variables": [],
                "pass_parent_env": false,
                "pass_input_record": false,
                "workflowReference": "/api/3/workflows/7abca430-74a5-4cfb-b557-5651c2ecc7cb"
              },
              "status": null,
              "top": "240",
              "left": "1280",
              "stepType": "/api/3/workflow_step_types/74932bdc-b8b6-4d24-88c4-1a4dfbc524f3",
              "group": null,
              "uuid": "867c9b23-9be1-4d19-92b5-67d3a6d46099"
            },
            {
              "@type": "WorkflowStep",
              "name": "Check Whitelist Destination IP",
              "description": null,
              "arguments": {
                "arguments": {
                  "ip_addr": "{{vars.dst_ip}}"
                },
                "apply_async": false,
                "step_variables": [],
                "pass_parent_env": false,
                "pass_input_record": false,
                "workflowReference": "/api/3/workflows/ecaf314f-ccaf-4ea2-b58f-d11b62ea6055"
              },
              "status": null,
              "top": "40",
              "left": "20",
              "stepType": "/api/3/workflow_step_types/74932bdc-b8b6-4d24-88c4-1a4dfbc524f3",
              "group": "/api/3/workflow_groups/fbd64d59-f463-4390-84eb-9a4b7c2f4065",
              "uuid": "a6559699-f76f-4b8a-839c-2d31b3649be1"
            },
            {
              "@type": "WorkflowStep",
              "name": "Check Whitelist IP",
              "description": null,
              "arguments": {
                "conditions": [
                  {
                    "option": "dst_ip가 whitelist에 있을때",
                    "step_iri": "/api/3/workflow_steps/4d445618-e28a-4dba-b913-353e39152918",
                    "condition": "{{ vars.steps.Check_Whitelist_Destination_IP.retval }}",
                    "step_name": "NOP"
                  },
                  {
                    "option": "dst_ip가 whitelist에 없을때",
                    "default": true,
                    "step_iri": "/api/3/workflow_steps/3cf2d95f-c7f4-4fec-8a0f-b5366e6621ed",
                    "step_name": "Check Blacklist Destination IP"
                  }
                ],
                "step_variables": []
              },
              "status": null,
              "top": "140",
              "left": "40",
              "stepType": "/api/3/workflow_step_types/12254cf5-5db7-4b1a-8cb1-3af081924b28",
              "group": "/api/3/workflow_groups/fbd64d59-f463-4390-84eb-9a4b7c2f4065",
              "uuid": "c2c6094c-a5dd-4427-9feb-e071cc41b4b0"
            },
            {
              "@type": "WorkflowStep",
              "name": "Collect File EDR",
              "description": null,
              "arguments": [],
              "status": null,
              "top": "460",
              "left": "1680",
              "stepType": "/api/3/workflow_step_types/04d0cf46-b6a8-42c4-8683-60a7eaa69e8f",
              "group": null,
              "uuid": "eea45005-3bc8-4cbe-aa16-59aeb7a0464b"
            },
            {
              "@type": "WorkflowStep",
              "name": "Collect Process EDR",
              "description": null,
              "arguments": [],
              "status": null,
              "top": "580",
              "left": "1680",
              "stepType": "/api/3/workflow_step_types/04d0cf46-b6a8-42c4-8683-60a7eaa69e8f",
              "group": null,
              "uuid": "e62f0016-debd-4027-ab31-7a840dc73125"
            },
            {
              "@type": "WorkflowStep",
              "name": "Configure",
              "description": null,
              "arguments": {
                "dst_ip": "{{vars.input.records[0].destinationIp}}",
                "src_ip": "{{vars.input.records[0].sourceIp}}",
                "file_hash": "{{vars.input.records[0].fileHash}}",
                "sourcedata": "{{vars.input.records[0].sourcedata | toDict}}"
              },
              "status": null,
              "top": "160",
              "left": "60",
              "stepType": "/api/3/workflow_step_types/04d0cf46-b6a8-42c4-8683-60a7eaa69e8f",
              "group": null,
              "uuid": "0e41dd84-2b3e-4195-a8fe-c1058007a450"
            },
            {
              "@type": "WorkflowStep",
              "name": "Configure 2",
              "description": null,
              "arguments": [],
              "status": null,
              "top": "160",
              "left": "1280",
              "stepType": "/api/3/workflow_step_types/04d0cf46-b6a8-42c4-8683-60a7eaa69e8f",
              "group": null,
              "uuid": "bb3e6c0e-f649-418d-977e-c8ef3fc62342"
            },
            {
              "@type": "WorkflowStep",
              "name": "Configure 3",
              "description": null,
              "arguments": [],
              "status": null,
              "top": "160",
              "left": "2100",
              "stepType": "/api/3/workflow_step_types/04d0cf46-b6a8-42c4-8683-60a7eaa69e8f",
              "group": null,
              "uuid": "9e815c4b-241a-44e7-8a75-b009224c91ff"
            },
            {
              "@type": "WorkflowStep",
              "name": "FortiSIEM Pivot Query",
              "description": null,
              "arguments": {
                "arguments": {
                  "ip_addr": "{{vars.dst_ip}}",
                  "alert_iri": "{{vars.input.records[0]['@id']}}",
                  "incidentLastSeen": "{{vars.sourcedata.incident_data.incidentLastSeen / 1000}}"
                },
                "apply_async": false,
                "step_variables": [],
                "pass_parent_env": false,
                "pass_input_record": false,
                "workflowReference": "/api/3/workflows/a6265e33-3391-401e-a831-42d9ff470cc7"
              },
              "status": null,
              "top": "560",
              "left": "1280",
              "stepType": "/api/3/workflow_step_types/74932bdc-b8b6-4d24-88c4-1a4dfbc524f3",
              "group": null,
              "uuid": "2770d7fd-d2fa-41d4-9dd5-5ea69ad48d3f"
            },
            {
              "@type": "WorkflowStep",
              "name": "Indicator Extracted",
              "description": null,
              "arguments": {
                "rule": {
                  "actions": [
                    {
                      "type": "resume_playbook",
                      "enabled": true,
                      "channel_uuid": "e2ce87c2-c55a-11ec-9d64-0242ac120002"
                    }
                  ],
                  "is_active": true,
                  "event_type": "update",
                  "entity_name": "Alerts",
                  "entity_type": "alerts",
                  "event_source": "crudhub",
                  "trigger_condition": {
                    "sort": [],
                    "limit": 30,
                    "logic": "AND",
                    "filters": [
                      {
                        "type": "primitive",
                        "field": "id",
                        "value": "{{vars.item.id}}",
                        "operator": "eq",
                        "_operator": "eq"
                      },
                      {
                        "type": "object",
                        "field": "status",
                        "value": "",
                        "_value": {
                          "@id": "",
                          "display": "",
                          "itemValue": ""
                        },
                        "operator": "changed"
                      },
                      {
                        "type": "object",
                        "field": "status",
                        "value": "/api/3/picklists/f1c079b1-6025-4c8c-be5f-8dc9b5b5b50b",
                        "_value": {
                          "@id": "/api/3/picklists/f1c079b1-6025-4c8c-be5f-8dc9b5b5b50b",
                          "display": "Automation",
                          "itemValue": "Automation"
                        },
                        "operator": "eq"
                      }
                    ]
                  }
                },
                "type": "ConditionBased",
                "delay": {
                  "days": 0,
                  "hours": 0,
                  "weeks": 0,
                  "minutes": 0,
                  "seconds": 0
                },
                "for_each": {
                  "item": "{{vars.input.records}}",
                  "condition": "{{vars.item.status.itemValue != \"Automation\"}}"
                },
                "step_variables": []
              },
              "status": null,
              "top": "280",
              "left": "60",
              "stepType": "/api/3/workflow_step_types/6832e556-b9c7-497a-babe-feda3bd27dbf",
              "group": null,
              "uuid": "87dd61f2-cf02-473c-93e6-0287a1e698ea"
            },
            {
              "@type": "WorkflowStep",
              "name": "Internal External Decision",
              "description": null,
              "arguments": [],
              "status": null,
              "top": "420",
              "left": "60",
              "stepType": "/api/3/workflow_step_types/04d0cf46-b6a8-42c4-8683-60a7eaa69e8f",
              "group": null,
              "uuid": "d15da70c-d6a7-4412-a9bd-2aabc574bdda"
            },
            {
              "@type": "WorkflowStep",
              "name": "NOP",
              "description": null,
              "arguments": {
                "params": [],
                "version": "3.2.6",
                "connector": "cyops_utilities",
                "operation": "no_op",
                "operationTitle": "Utils: No Operation",
                "step_variables": []
              },
              "status": null,
              "top": "700",
              "left": "460",
              "stepType": "/api/3/workflow_step_types/0109f35d-090b-4a2b-bd8a-94cbc3508562",
              "group": null,
              "uuid": "4d445618-e28a-4dba-b913-353e39152918"
            },
            {
              "@type": "WorkflowStep",
              "name": "Reputation Check",
              "description": null,
              "arguments": {
                "arguments": {
                  "ip_addr": "{{vars.dst_ip}}",
                  "alert_iri": "{{vars.input.records[0]['@id']}}",
                  "file_hash": "{{vars.file_hash}}",
                  "alert_sourcedata": "{{vars.sourcedata}}"
                },
                "apply_async": false,
                "step_variables": [],
                "pass_parent_env": false,
                "pass_input_record": false,
                "workflowReference": "/api/3/workflows/42f2e847-938f-4a65-841d-7ec05afdd508"
              },
              "status": null,
              "top": "300",
              "left": "2100",
              "stepType": "/api/3/workflow_step_types/74932bdc-b8b6-4d24-88c4-1a4dfbc524f3",
              "group": null,
              "uuid": "d629cc25-5ac5-4cd5-b191-ce48b3090847"
            },
            {
              "@type": "WorkflowStep",
              "name": "Start",
              "description": null,
              "arguments": {
                "resource": "alerts",
                "resources": [
                  "alerts"
                ],
                "__triggerLimit": true,
                "step_variables": {
                  "input": {
                    "params": [],
                    "records": [
                      "{{vars.input.records[0]}}"
                    ]
                  }
                },
                "triggerOnSource": true,
                "fieldbasedtrigger": {
                  "sort": [],
                  "limit": 30,
                  "logic": "AND",
                  "filters": [
                    {
                      "type": "primitive",
                      "field": "name",
                      "value": "%Trellix%",
                      "operator": "like",
                      "_operator": "like"
                    }
                  ]
                },
                "triggerOnReplicate": false
              },
              "status": null,
              "top": "40",
              "left": "60",
              "stepType": "/api/3/workflow_step_types/ea155646-3821-4542-9702-b246da430a8d",
              "group": null,
              "uuid": "7e571a43-44ba-4697-8252-a8f5a3e03433"
            },
            {
              "@type": "WorkflowStep",
              "name": "SWG FortiSIEM",
              "description": null,
              "arguments": {
                "name": "Fortinet FortiSIEM",
                "config": "d81f309e-6287-4d74-9526-30a0b1ce0c8c",
                "params": {
                  "cond": "reptDevName = \"Secui MF4\" AND srcIpAddr = \"{{vars.src_ip}}\" AND destIpAddr = \"{{vars.dst_ip}}\"",
                  "start": 0,
                  "value": 1,
                  "orderby": "phRecvTime DESC",
                  "perPage": 50,
                  "AttrList": "phRecvTime,reptDevIpAddr,eventType,eventName,srcIpAddr,destIpAddr,user,rawEventMsg",
                  "rel_time": "Minutes",
                  "time_selection": "Relative Time"
                },
                "version": "5.2.0",
                "connector": "fortinet-fortisiem",
                "operation": "run_report",
                "operationTitle": "Run Advanced Search Query",
                "pickFromTenant": false,
                "step_variables": []
              },
              "status": null,
              "top": "700",
              "left": "1280",
              "stepType": "/api/3/workflow_step_types/0bfed618-0316-11e7-93ae-92361f002671",
              "group": null,
              "uuid": "788c4971-e8d7-4bc1-8174-a89180d32a90"
            },
            {
              "@type": "WorkflowStep",
              "name": "User Sensor Ingest",
              "description": null,
              "arguments": [],
              "status": null,
              "top": "160",
              "left": "1680",
              "stepType": "/api/3/workflow_step_types/04d0cf46-b6a8-42c4-8683-60a7eaa69e8f",
              "group": null,
              "uuid": "32455bc0-14c5-4b0d-94e3-500dc13bbbe1"
            },
            {
              "@type": "WorkflowStep",
              "name": "Whois Lookup",
              "description": null,
              "arguments": {
                "name": "Whois RDAP",
                "config": "eca9db2d-a2eb-4c4a-ae2c-2c50f9fe9d67",
                "params": {
                  "ip": "1.1.1.1"
                },
                "version": "1.0.2",
                "connector": "whois-rdap",
                "operation": "whois_ip",
                "operationTitle": "Whois IP",
                "pickFromTenant": false,
                "step_variables": []
              },
              "status": null,
              "top": "460",
              "left": "1280",
              "stepType": "/api/3/workflow_step_types/0bfed618-0316-11e7-93ae-92361f002671",
              "group": null,
              "uuid": "03d56584-0ad2-4074-acc8-fca6c56bda30"
            }
          ],
          "routes": [
            {
              "@type": "WorkflowRoute",
              "name": "Check Blacklist DestinationIP -> Copy of Check Whitelist IP",
              "targetStep": "/api/3/workflow_steps/b1e04f3e-f5f3-4ea6-9d9d-c3777bcd776f",
              "sourceStep": "/api/3/workflow_steps/3cf2d95f-c7f4-4fec-8a0f-b5366e6621ed",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "9c40e412-8c61-40d8-bf54-4bea534c3e1b"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Check Blacklist IP -> Configure 2",
              "targetStep": "/api/3/workflow_steps/bb3e6c0e-f649-418d-977e-c8ef3fc62342",
              "sourceStep": "/api/3/workflow_steps/b1e04f3e-f5f3-4ea6-9d9d-c3777bcd776f",
              "label": "dst_ip가 blacklist에 없을때",
              "isExecuted": false,
              "group": null,
              "uuid": "dc7415ac-b23e-4a33-8c6c-fb990b111b2f"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Check External TI -> Whois Lookup",
              "targetStep": "/api/3/workflow_steps/03d56584-0ad2-4074-acc8-fca6c56bda30",
              "sourceStep": "/api/3/workflow_steps/c7e34a1b-0125-4e57-a5c8-035e16a8f402",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "c89d2ef9-f2f3-4c1d-8ce8-b582b4e3d645"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Check Hash 1 -> Collect File EDR",
              "targetStep": "/api/3/workflow_steps/eea45005-3bc8-4cbe-aa16-59aeb7a0464b",
              "sourceStep": "/api/3/workflow_steps/cc578fa4-b129-4c74-bfa3-044ff1564242",
              "label": "원본 파일 수집",
              "isExecuted": false,
              "group": null,
              "uuid": "48f6ddcf-6017-46ca-8705-0fa620d3eefc"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Check Hash 1 -> Configure 3",
              "targetStep": "/api/3/workflow_steps/9e815c4b-241a-44e7-8a75-b009224c91ff",
              "sourceStep": "/api/3/workflow_steps/cc578fa4-b129-4c74-bfa3-044ff1564242",
              "label": "평결",
              "isExecuted": false,
              "group": null,
              "uuid": "98412c36-293c-462e-89f1-7bdd253204e0"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Check Internal TI -> Copy of Configure 2",
              "targetStep": "/api/3/workflow_steps/c7e34a1b-0125-4e57-a5c8-035e16a8f402",
              "sourceStep": "/api/3/workflow_steps/867c9b23-9be1-4d19-92b5-67d3a6d46099",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "61efe7de-c0cc-414c-a7d2-4b86b0ba8f92"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Check Whitelist Destination IP -> Check Whitelist IP",
              "targetStep": "/api/3/workflow_steps/c2c6094c-a5dd-4427-9feb-e071cc41b4b0",
              "sourceStep": "/api/3/workflow_steps/a6559699-f76f-4b8a-839c-2d31b3649be1",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "ad62f1a3-8642-4927-ab6c-acd22d157463"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Check Whitelist IP -> Check Blacklist DestinationIP",
              "targetStep": "/api/3/workflow_steps/3cf2d95f-c7f4-4fec-8a0f-b5366e6621ed",
              "sourceStep": "/api/3/workflow_steps/c2c6094c-a5dd-4427-9feb-e071cc41b4b0",
              "label": "dst_ip가 whitelist에 없을때",
              "isExecuted": false,
              "group": null,
              "uuid": "03c7b9e2-b507-443f-9b42-6893961c25e7"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Check Whitelist IP -> NOP",
              "targetStep": "/api/3/workflow_steps/4d445618-e28a-4dba-b913-353e39152918",
              "sourceStep": "/api/3/workflow_steps/c2c6094c-a5dd-4427-9feb-e071cc41b4b0",
              "label": "dst_ip가 whitelist에 있을때",
              "isExecuted": false,
              "group": null,
              "uuid": "31f6af9d-d291-4310-a84f-ba192ff8601e"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Collect File EDR -> Copy 1 of Configure 2",
              "targetStep": "/api/3/workflow_steps/e62f0016-debd-4027-ab31-7a840dc73125",
              "sourceStep": "/api/3/workflow_steps/eea45005-3bc8-4cbe-aa16-59aeb7a0464b",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "4ebfa611-9b9b-4949-acd7-d3ce2937d113"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Collect Process EDR -> Configure 3",
              "targetStep": "/api/3/workflow_steps/9e815c4b-241a-44e7-8a75-b009224c91ff",
              "sourceStep": "/api/3/workflow_steps/e62f0016-debd-4027-ab31-7a840dc73125",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "e41e6582-d716-4096-9edb-7045370e3471"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Configure 2 -> Check Internal TI",
              "targetStep": "/api/3/workflow_steps/867c9b23-9be1-4d19-92b5-67d3a6d46099",
              "sourceStep": "/api/3/workflow_steps/bb3e6c0e-f649-418d-977e-c8ef3fc62342",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "669f7eb3-6e54-4f07-a5f9-57475a7303ed"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Configure 3 -> Reputation Check",
              "targetStep": "/api/3/workflow_steps/d629cc25-5ac5-4cd5-b191-ce48b3090847",
              "sourceStep": "/api/3/workflow_steps/9e815c4b-241a-44e7-8a75-b009224c91ff",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "68718911-8d21-4ec1-9671-301b089b9b5e"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Configure -> Waiting Extraction",
              "targetStep": "/api/3/workflow_steps/87dd61f2-cf02-473c-93e6-0287a1e698ea",
              "sourceStep": "/api/3/workflow_steps/0e41dd84-2b3e-4195-a8fe-c1058007a450",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "a2c65abf-31b9-4621-8ef3-1b79d50103b3"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Copy of Check Whitelist IP -> Auto Close",
              "targetStep": "/api/3/workflow_steps/58139c3f-2a07-44f1-b92d-e832d3936f29",
              "sourceStep": "/api/3/workflow_steps/b1e04f3e-f5f3-4ea6-9d9d-c3777bcd776f",
              "label": "dst_ip가 blacklist에 있을때",
              "isExecuted": false,
              "group": null,
              "uuid": "683c03e7-24ab-4800-8738-9c835a8e5cae"
            },
            {
              "@type": "WorkflowRoute",
              "name": "FortiSIEM Pivot Query -> SWG FortiSIEM",
              "targetStep": "/api/3/workflow_steps/788c4971-e8d7-4bc1-8174-a89180d32a90",
              "sourceStep": "/api/3/workflow_steps/2770d7fd-d2fa-41d4-9dd5-5ea69ad48d3f",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "9c8eab20-e371-43ea-8d52-b48ca1af53b7"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Indicator Extracted -> Internal External Decision",
              "targetStep": "/api/3/workflow_steps/d15da70c-d6a7-4412-a9bd-2aabc574bdda",
              "sourceStep": "/api/3/workflow_steps/87dd61f2-cf02-473c-93e6-0287a1e698ea",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "40e2675e-dfc5-417d-a21e-b6720e9363a9"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Internal External Decision -> Check Whitelist",
              "targetStep": "/api/3/workflow_steps/a6559699-f76f-4b8a-839c-2d31b3649be1",
              "sourceStep": "/api/3/workflow_steps/d15da70c-d6a7-4412-a9bd-2aabc574bdda",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "d41ece80-1dbc-4c52-867e-2bd1566ed0a8"
            },
            {
              "@type": "WorkflowRoute",
              "name": "NOP -> Auto Close",
              "targetStep": "/api/3/workflow_steps/58139c3f-2a07-44f1-b92d-e832d3936f29",
              "sourceStep": "/api/3/workflow_steps/4d445618-e28a-4dba-b913-353e39152918",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "530c6093-53a5-4734-a2fc-ef96325d6e3b"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Start -> Configure",
              "targetStep": "/api/3/workflow_steps/0e41dd84-2b3e-4195-a8fe-c1058007a450",
              "sourceStep": "/api/3/workflow_steps/7e571a43-44ba-4697-8252-a8f5a3e03433",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "9f266b39-263e-471c-acfe-655312267d46"
            },
            {
              "@type": "WorkflowRoute",
              "name": "SWG FortiSIEM -> Copy of Configure 2",
              "targetStep": "/api/3/workflow_steps/32455bc0-14c5-4b0d-94e3-500dc13bbbe1",
              "sourceStep": "/api/3/workflow_steps/788c4971-e8d7-4bc1-8174-a89180d32a90",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "90daee86-a555-409d-a4aa-190918ca4498"
            },
            {
              "@type": "WorkflowRoute",
              "name": "User Sensor Ingest -> Check Hash 1",
              "targetStep": "/api/3/workflow_steps/cc578fa4-b129-4c74-bfa3-044ff1564242",
              "sourceStep": "/api/3/workflow_steps/32455bc0-14c5-4b0d-94e3-500dc13bbbe1",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "65dcbb40-d759-408b-8999-440f7d3fa03a"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Whois Lookup -> FortiSIEM Pivot Query",
              "targetStep": "/api/3/workflow_steps/2770d7fd-d2fa-41d4-9dd5-5ea69ad48d3f",
              "sourceStep": "/api/3/workflow_steps/03d56584-0ad2-4074-acc8-fca6c56bda30",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "fa06b2f0-cbde-453a-b298-ddf340f4e3e9"
            }
          ],
          "groups": [
            {
              "@type": "WorkflowGroup",
              "name": "Blacklist 여부",
              "description": "",
              "type": "block",
              "isCollapsed": false,
              "hasTriggerStep": false,
              "hideInLogs": false,
              "metadata": [],
              "reusable": false,
              "top": "160",
              "left": "840",
              "height": "211",
              "width": "307",
              "uuid": "199092c5-4dd7-43fc-bdb7-afa677feac66",
              "recordTags": []
            },
            {
              "@type": "WorkflowGroup",
              "name": "Whitelist 여부",
              "description": "",
              "type": "block",
              "isCollapsed": false,
              "hasTriggerStep": false,
              "hideInLogs": false,
              "metadata": [],
              "reusable": false,
              "top": "160",
              "left": "420",
              "height": "216",
              "width": "303",
              "uuid": "fbd64d59-f463-4390-84eb-9a4b7c2f4065",
              "recordTags": []
            }
          ],
          "priority": "/api/3/picklists/2b563c61-ae2c-41c0-a85a-c9709585e3f2",
          "uuid": "d09a1833-8f0b-434f-ad8c-be39e428f433",
          "id": 848,
          "owners": [],
          "isPrivate": false,
          "deletedAt": null,
          "importedBy": [],
          "recordTags": []
        },
        {
          "@type": "Workflow",
          "triggerLimit": null,
          "name": "00 - BC Card Scenario 1 > Alert > Manual",
          "aliasName": null,
          "tag": null,
          "description": null,
          "isActive": true,
          "debug": true,
          "singleRecordExecution": false,
          "remoteExecutableFlag": false,
          "parameters": [],
          "synchronous": false,
          "lastModifyDate": 1712041581,
          "collection": "/api/3/workflow_collections/63c971df-3a2d-4868-a827-537dcc408421",
          "versions": [],
          "triggerStep": "/api/3/workflow_steps/162313c6-9976-40dd-a6de-a9089403721f",
          "steps": [
            {
              "@type": "WorkflowStep",
              "name": "BC Card Scenario 1",
              "description": null,
              "arguments": {
                "arguments": [],
                "apply_async": false,
                "step_variables": [],
                "pass_parent_env": true,
                "pass_input_record": false,
                "workflowReference": "/api/3/workflows/d09a1833-8f0b-434f-ad8c-be39e428f433"
              },
              "status": null,
              "top": "165",
              "left": "125",
              "stepType": "/api/3/workflow_step_types/74932bdc-b8b6-4d24-88c4-1a4dfbc524f3",
              "group": null,
              "uuid": "91614bd0-6beb-4511-af05-4d5936a539d3"
            },
            {
              "@type": "WorkflowStep",
              "name": "Start",
              "description": null,
              "arguments": {
                "route": "fbc7b2e9-417b-4c57-ba1c-00a3e5283686",
                "resources": [
                  "alerts"
                ],
                "__triggerLimit": true,
                "inputVariables": [],
                "step_variables": {
                  "input": {
                    "params": [],
                    "records": "{{vars.input.records}}"
                  }
                },
                "triggerOnSource": true,
                "displayConditions": {
                  "alerts": {
                    "sort": [],
                    "limit": 30,
                    "logic": "AND",
                    "filters": []
                  }
                },
                "executeButtonText": "Execute",
                "noRecordExecution": false,
                "showToasterMessage": {
                  "visible": false,
                  "messageVisible": true
                },
                "triggerOnReplicate": false,
                "singleRecordExecution": true
              },
              "status": null,
              "top": "30",
              "left": "125",
              "stepType": "/api/3/workflow_step_types/f414d039-bb0d-4e59-9c39-a8f1e880b18a",
              "group": null,
              "uuid": "162313c6-9976-40dd-a6de-a9089403721f"
            }
          ],
          "routes": [
            {
              "@type": "WorkflowRoute",
              "name": "Start -> BC Card Scenario 1",
              "targetStep": "/api/3/workflow_steps/91614bd0-6beb-4511-af05-4d5936a539d3",
              "sourceStep": "/api/3/workflow_steps/162313c6-9976-40dd-a6de-a9089403721f",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "63977d07-baaf-41fd-b9c5-8526e15eedaa"
            }
          ],
          "groups": [],
          "priority": "/api/3/picklists/2b563c61-ae2c-41c0-a85a-c9709585e3f2",
          "uuid": "e32d20d1-23fe-48f4-bbf1-55d669632a88",
          "id": 856,
          "owners": [],
          "isPrivate": false,
          "deletedAt": null,
          "importedBy": [],
          "recordTags": []
        },
        {
          "@type": "Workflow",
          "triggerLimit": null,
          "name": "00 - BC Card Scenario 1 > Check Whitelist",
          "aliasName": null,
          "tag": null,
          "description": null,
          "isActive": true,
          "debug": true,
          "singleRecordExecution": false,
          "remoteExecutableFlag": false,
          "parameters": [
            "ip_addr"
          ],
          "synchronous": false,
          "lastModifyDate": 1712022199,
          "collection": "/api/3/workflow_collections/63c971df-3a2d-4868-a827-537dcc408421",
          "versions": [],
          "triggerStep": "/api/3/workflow_steps/bbc33fd0-d013-424d-beae-eda2df6f2800",
          "steps": [
            {
              "@type": "WorkflowStep",
              "name": "Configure",
              "description": null,
              "arguments": {
                "ip_addr": "{{vars.input.params['ip_addr']}}"
              },
              "status": null,
              "top": "165",
              "left": "125",
              "stepType": "/api/3/workflow_step_types/04d0cf46-b6a8-42c4-8683-60a7eaa69e8f",
              "group": null,
              "uuid": "a72145a5-303c-4443-bec5-2059c68a9f79"
            },
            {
              "@type": "WorkflowStep",
              "name": "Find Whitelist Value",
              "description": null,
              "arguments": {
                "query": {
                  "sort": [],
                  "limit": 30,
                  "logic": "AND",
                  "filters": [
                    {
                      "type": "primitive",
                      "field": "whiteValue",
                      "value": "{{vars.ip_addr}}",
                      "operator": "eq",
                      "_operator": "eq"
                    }
                  ],
                  "__selectFields": [
                    "id"
                  ]
                },
                "module": "whitelistmgmts?$limit=1",
                "checkboxFields": true,
                "step_variables": []
              },
              "status": null,
              "top": "300",
              "left": "125",
              "stepType": "/api/3/workflow_step_types/b593663d-7d13-40ce-a3a3-96dece928770",
              "group": null,
              "uuid": "ccdad8b0-f697-4792-b38e-965893b50a03"
            },
            {
              "@type": "WorkflowStep",
              "name": "Return",
              "description": null,
              "arguments": {
                "retval": "{{vars.steps.Find_Whitelist_Value | length > 0}}"
              },
              "status": null,
              "top": "435",
              "left": "125",
              "stepType": "/api/3/workflow_step_types/04d0cf46-b6a8-42c4-8683-60a7eaa69e8f",
              "group": null,
              "uuid": "d04a8bdf-1857-45eb-ba55-a989a3942a33"
            },
            {
              "@type": "WorkflowStep",
              "name": "Start",
              "description": null,
              "arguments": {
                "__triggerLimit": true,
                "step_variables": {
                  "input": {
                    "params": []
                  }
                },
                "triggerOnSource": true,
                "triggerOnReplicate": false
              },
              "status": null,
              "top": "30",
              "left": "125",
              "stepType": "/api/3/workflow_step_types/b348f017-9a94-471f-87f8-ce88b6a7ad62",
              "group": null,
              "uuid": "bbc33fd0-d013-424d-beae-eda2df6f2800"
            }
          ],
          "routes": [
            {
              "@type": "WorkflowRoute",
              "name": "Configure -> Find Whitelist Value",
              "targetStep": "/api/3/workflow_steps/ccdad8b0-f697-4792-b38e-965893b50a03",
              "sourceStep": "/api/3/workflow_steps/a72145a5-303c-4443-bec5-2059c68a9f79",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "c88e9d72-ba19-4174-80b5-98e663b243a0"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Find Whitelist Value -> Return",
              "targetStep": "/api/3/workflow_steps/d04a8bdf-1857-45eb-ba55-a989a3942a33",
              "sourceStep": "/api/3/workflow_steps/ccdad8b0-f697-4792-b38e-965893b50a03",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "10ea7d3f-3d0b-4708-862a-9634cfdb48d4"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Start -> Configure",
              "targetStep": "/api/3/workflow_steps/a72145a5-303c-4443-bec5-2059c68a9f79",
              "sourceStep": "/api/3/workflow_steps/bbc33fd0-d013-424d-beae-eda2df6f2800",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "96c61578-4086-4953-8f95-68e3e2136e41"
            }
          ],
          "groups": [],
          "priority": "/api/3/picklists/2b563c61-ae2c-41c0-a85a-c9709585e3f2",
          "uuid": "ecaf314f-ccaf-4ea2-b58f-d11b62ea6055",
          "id": 849,
          "owners": [],
          "isPrivate": false,
          "deletedAt": null,
          "importedBy": [],
          "recordTags": []
        },
        {
          "@type": "Workflow",
          "triggerLimit": null,
          "name": "00 - BC Card Scenario 1 > Reputation Check > Manual",
          "aliasName": null,
          "tag": null,
          "description": null,
          "isActive": true,
          "debug": true,
          "singleRecordExecution": false,
          "remoteExecutableFlag": false,
          "parameters": [],
          "synchronous": false,
          "lastModifyDate": 1712035676,
          "collection": "/api/3/workflow_collections/63c971df-3a2d-4868-a827-537dcc408421",
          "versions": [],
          "triggerStep": "/api/3/workflow_steps/9d0305b1-1ff6-4e58-aba9-251ce638cf37",
          "steps": [
            {
              "@type": "WorkflowStep",
              "name": "Reputation Check",
              "description": null,
              "arguments": {
                "arguments": {
                  "ip_addr": "{{vars.input.records[0].destinationIp}}",
                  "alert_iri": "{{vars.input.records[0]['@id']}}",
                  "file_hash": "{{vars.input.records[0].fileHash}}",
                  "alert_sourcedata": "{{vars.input.records[0].sourcedata}}"
                },
                "apply_async": false,
                "step_variables": [],
                "pass_parent_env": false,
                "pass_input_record": false,
                "workflowReference": "/api/3/workflows/42f2e847-938f-4a65-841d-7ec05afdd508"
              },
              "status": null,
              "top": "200",
              "left": "40",
              "stepType": "/api/3/workflow_step_types/74932bdc-b8b6-4d24-88c4-1a4dfbc524f3",
              "group": null,
              "uuid": "73f7b62b-d95e-4793-afe6-3580d73d8dff"
            },
            {
              "@type": "WorkflowStep",
              "name": "Start",
              "description": null,
              "arguments": {
                "route": "5ab38b86-73d8-498b-8b57-0da841ee8903",
                "resources": [
                  "alerts"
                ],
                "__triggerLimit": true,
                "inputVariables": [],
                "step_variables": {
                  "input": {
                    "params": [],
                    "records": "{{vars.input.records}}"
                  }
                },
                "triggerOnSource": true,
                "displayConditions": {
                  "alerts": {
                    "sort": [],
                    "limit": 30,
                    "logic": "AND",
                    "filters": []
                  }
                },
                "executeButtonText": "Execute",
                "noRecordExecution": false,
                "showToasterMessage": {
                  "visible": false,
                  "messageVisible": true
                },
                "triggerOnReplicate": false,
                "singleRecordExecution": true
              },
              "status": null,
              "top": "60",
              "left": "40",
              "stepType": "/api/3/workflow_step_types/f414d039-bb0d-4e59-9c39-a8f1e880b18a",
              "group": null,
              "uuid": "9d0305b1-1ff6-4e58-aba9-251ce638cf37"
            }
          ],
          "routes": [
            {
              "@type": "WorkflowRoute",
              "name": "Start -> Reputation Check",
              "targetStep": "/api/3/workflow_steps/73f7b62b-d95e-4793-afe6-3580d73d8dff",
              "sourceStep": "/api/3/workflow_steps/9d0305b1-1ff6-4e58-aba9-251ce638cf37",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "01c882cd-13e8-45a7-bf03-05aa30ad9895"
            }
          ],
          "groups": [],
          "priority": "/api/3/picklists/2b563c61-ae2c-41c0-a85a-c9709585e3f2",
          "uuid": "f5d27b2f-3300-4720-9bc4-c702c17a7542",
          "id": 855,
          "owners": [],
          "isPrivate": false,
          "deletedAt": null,
          "importedBy": [],
          "recordTags": []
        },
        {
          "@type": "Workflow",
          "triggerLimit": null,
          "name": "00 - BC Card Scenario 1 > Check Blacklist",
          "aliasName": null,
          "tag": null,
          "description": null,
          "isActive": true,
          "debug": true,
          "singleRecordExecution": false,
          "remoteExecutableFlag": false,
          "parameters": [
            "ip_addr"
          ],
          "synchronous": false,
          "lastModifyDate": 1712022481,
          "collection": "/api/3/workflow_collections/63c971df-3a2d-4868-a827-537dcc408421",
          "versions": [],
          "triggerStep": "/api/3/workflow_steps/ab86eda8-cffa-43ea-a0fd-ed92a6a1fbab",
          "steps": [
            {
              "@type": "WorkflowStep",
              "name": "Configure",
              "description": null,
              "arguments": {
                "ip_addr": "{{vars.input.params['ip_addr']}}"
              },
              "status": null,
              "top": "165",
              "left": "125",
              "stepType": "/api/3/workflow_step_types/04d0cf46-b6a8-42c4-8683-60a7eaa69e8f",
              "group": null,
              "uuid": "998078da-0cce-467e-9ff9-814bc272db54"
            },
            {
              "@type": "WorkflowStep",
              "name": "Find Blacklist Value",
              "description": null,
              "arguments": {
                "query": {
                  "sort": [],
                  "limit": 30,
                  "logic": "AND",
                  "filters": [
                    {
                      "type": "primitive",
                      "field": "iP",
                      "value": "{{vars.ip_addr}}",
                      "operator": "eq",
                      "_operator": "eq"
                    }
                  ]
                },
                "module": "blocklistmgmts1s?$limit=1",
                "checkboxFields": true,
                "step_variables": []
              },
              "status": null,
              "top": "300",
              "left": "125",
              "stepType": "/api/3/workflow_step_types/b593663d-7d13-40ce-a3a3-96dece928770",
              "group": null,
              "uuid": "17f91a93-c252-4da6-9a14-c6386c2ec6a8"
            },
            {
              "@type": "WorkflowStep",
              "name": "Return",
              "description": null,
              "arguments": {
                "retval": "{{vars.steps.Find_Blacklist_Value | length > 0}}"
              },
              "status": null,
              "top": "435",
              "left": "125",
              "stepType": "/api/3/workflow_step_types/04d0cf46-b6a8-42c4-8683-60a7eaa69e8f",
              "group": null,
              "uuid": "3f2227b0-cc8f-4dfe-a90f-33db01a8d725"
            },
            {
              "@type": "WorkflowStep",
              "name": "Start",
              "description": null,
              "arguments": {
                "__triggerLimit": true,
                "step_variables": {
                  "input": {
                    "params": []
                  }
                },
                "triggerOnSource": true,
                "triggerOnReplicate": false
              },
              "status": null,
              "top": "30",
              "left": "125",
              "stepType": "/api/3/workflow_step_types/b348f017-9a94-471f-87f8-ce88b6a7ad62",
              "group": null,
              "uuid": "ab86eda8-cffa-43ea-a0fd-ed92a6a1fbab"
            }
          ],
          "routes": [
            {
              "@type": "WorkflowRoute",
              "name": "Configure -> Find Whitelist Value",
              "targetStep": "/api/3/workflow_steps/17f91a93-c252-4da6-9a14-c6386c2ec6a8",
              "sourceStep": "/api/3/workflow_steps/998078da-0cce-467e-9ff9-814bc272db54",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "79e70c84-02f1-49ae-90fa-066228dcd7d8"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Find Whitelist Value -> Return",
              "targetStep": "/api/3/workflow_steps/3f2227b0-cc8f-4dfe-a90f-33db01a8d725",
              "sourceStep": "/api/3/workflow_steps/17f91a93-c252-4da6-9a14-c6386c2ec6a8",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "c8f17f5e-bf03-4b66-ac33-40ce1f8cc3b8"
            },
            {
              "@type": "WorkflowRoute",
              "name": "Start -> Configure",
              "targetStep": "/api/3/workflow_steps/998078da-0cce-467e-9ff9-814bc272db54",
              "sourceStep": "/api/3/workflow_steps/ab86eda8-cffa-43ea-a0fd-ed92a6a1fbab",
              "label": null,
              "isExecuted": false,
              "group": null,
              "uuid": "5868c15a-1ee7-486d-91f4-567f88b541d6"
            }
          ],
          "groups": [],
          "priority": "/api/3/picklists/2b563c61-ae2c-41c0-a85a-c9709585e3f2",
          "uuid": "fd86c039-206d-4f5e-a42c-6535937310a2",
          "id": 850,
          "owners": [],
          "isPrivate": false,
          "deletedAt": null,
          "importedBy": [],
          "recordTags": []
        }
      ]
    }
  ],
  "exported_tags": []
}