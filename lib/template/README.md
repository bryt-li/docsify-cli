# Headline

> An awesome project.


```
@startuml

interface IT
interface ops
interface users

component [Clients - APP/Web] as APP
component [Configuration Maintenance - Web] as WEB

ops --> APP
users --> APP
IT --> WEB #blue

package "Server-side" {

	component [API Gateway] as API_GATEWAY #lightgreen

	package "Configuration Center" {
		component [Configuration - Service] as CONF #eee
		database "Configuration DB" as CONF_DB #999
		component [Zookeeper] as ZK #eee

		CONF --> CONF_DB
		CONF --> ZK
	}

	API_GATEWAY ..> CONF #blue

	rectangle "Deployments" {
		cloud "Production Deployment" as PROD  #aliceblue {
		
			rectangle "Production Service Deployment" as PROD_SERVICE {
				component [API - Service] as API << Multiple >>
				component [Queue-based Task Dispatcher] as Q << Single >> #eee
				component [Backend - Service] as BE << Multiple >>
				API --> Q
				Q --> BE
			}

			rectangle "Production Persistance Deployment" {
				package "Production Env" as PROD_DATA {
					component [DB Read Cache] as CACHE #ddd
					database "Core DB" as DB #ddd
					database "Queue DB" as QDB #ddd
				}
				package "Production Sandbox Environment" as SANDBOX_DATA #ddd {
				}
			}

			API --> CACHE
			BE --> DB
			API --> DB
			Q -> QDB

			PROD_SERVICE --> ZK

		}

		cloud "Staging Deployment" as STAGING #aliceblue {
			rectangle "Staging Service Deployment" as STAGING_SERVICE {
			}

			rectangle "Staging Persistance Deployment" as STAGING_DATA #ddd {
			}
			STAGING_SERVICE --> STAGING_DATA
		}

		cloud "Develop Deployment" as DEV  #aliceblue {
			rectangle "Develop Service Deployment" as DEV_SERVICE {
			}

			rectangle "Develop Persistance Deployment" as DEV_DATA #ddd {
			}
			DEV_SERVICE --> DEV_DATA
		}

	}

	API_GATEWAY --> API
	API_GATEWAY ---> STAGING_SERVICE
	API_GATEWAY ---> DEV_SERVICE

}

APP --> API_GATEWAY
WEB --> API_GATEWAY #blue

@enduml
```
