# Config Central
_Centralized Configuration Store for a Distributed .Net Solution_

Configuration sucks. As a Dev, I don't really have to worry about that: I can just deploy a code change whenever I want.

But I'm also Ops these days. So sometimes I don't WANT to deploy a new version to change the configurable batch size for a process, or toggle a feature on or off.

My real motivation though? Move these settings out of web.config. I want to mostly develop against my local dev DB(s), with dev settings like faking out web service calls. But when I want to connect to the test environment, I want to change ONE setting in web.config and everything's using test env settings. I have no desire to have to hunt down which setting controls whether we're talking to a real or stub Active Directory.

_Enter Config Central._

## The DB instance defines your environment
We have different DB instances for each environment we have deployed. If you don't, please let me know why and how that works.

Our distributed applications have load-balanced components with identical [web/app].configs for a given environment. If you don't, centralized configuration isn't for you (for those settings, at least).

So it makes sense to associate those settings with the DB for that instance.

## Features
* **Typed .Net interface**. Not limited to strings coming out of the API.
* **No default values**. If you didn't define the value in the Configuration Store, expect a `MissingConfigurationException`.
* **ConfigurationVersion** as an opaque string property that is updated with every change.
* Set it and forget it **Caching**. No querying the store every time a value is looked up.
* **Pluggable** storage interface.
  * SQL Server Provider out of the gate.
  * In Memory provider for tests.
* **Dependency Injection-friendly**. A simple interface to inject into your services.

## Futures
* Access to the values over a **REST API** using ETags based on the ConfigurationVersion outlined above.
  * Need to think through the security model.
* **Web UI** for editing settings available as OWIN middleware.

