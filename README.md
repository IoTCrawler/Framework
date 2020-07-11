<img src="images/IoTCrawler_Logo.png" width="200" height="34" />

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)

- [IoTCrawler Framework](#iotcrawler-framework)
- [Documentation](#documentation)
- [Contributing](#contributing)
- [About Us](#about-us)
- [License](#license)

# IoTCrawler Framework

IoTCrawler is a research project funded under the European Union's Horizon 2020 research and innovation program. The aim of the project is to develop a search engine for the Internet of Things (IoT). IoTCrawler focuses on integration and interoperability across different platforms, dynamic and reconfigurable solutions for discovery and integration of data and services from legacy and new systems. It facilitates adaptive, and privacy-aware secure algorithms and mechanisms for crawling, indexing, and ranking in distributed IoT systems. The project spans among multiple industries, universities and cities.IoTCrawler framework is consist of multiple components:

- [MetaData Repository](https://github.com/IoTCrawler/ScorpioBroker) is a context broker which integrate and distribute context information among the other components of the IoTCrawler using query-response and publish-subscribe pattern.
- [Orchestrator](https://github.com/IoTCrawler/Orchestrator) allows client IoT applications to subscribe to data streams without having a public endpoint as well as tracks subscription requests.
- [Indexing](https://github.com/IoTCrawler/Indexing) is utilized to crawl and index IoT entities with queries based on sensor type and location.
- [Ranking](https://github.com/IoTCrawler/Ranking) aims to aid users and applications to not only find a set of resources relevant to their needs, but also to select the best or most appropriate one(s) from the set.
- [Semantic Enrichment](https://github.com/IoTCrawler/SemanticEnrichment) is responsible for annotating data streams with Quality of Information (QoI).
- [Authorization Enabler]() is comprized of [PAP-PDP](https://github.com/IoTCrawler/PAP-PDP), [PEP-Proxy](https://github.com/IoTCrawler/PEP-Proxy), [Keyrock](https://github.com/IoTCrawler/Keyrock), [Security Facade](https://github.com/IoTCrawler/Security-Facade), [Capability Manager](https://github.com/IoTCrawler/Capability-Manager) and [Blockchain Handler]() which all put in place to establish security in the IoTCrawler framework.

# Documentation

Please find further information about the architecture, getting started and tutorials on our online documentation.

- [latest](https://iotcrawler.readthedocs.io/en/latest/index.html)

# Contributing

IoTCrawler is an Open Souce, community driven reseacrch project. We welcome your [contribution](https://iotcrawler.readthedocs.io/en/latest/contributing/contributing.html) in the project.

# About Us

The IoTCrawler project consists of 10 [partners](https://iotcrawler.eu/index.php/partners/) from across EU and is a combination of research institutions, leading technological industries and a municipality.

# License

The information here is made available under the Apache License, Version 2.0 (Apache-2.0), located in the [LICENSE](LICENSE) file. The source code files of different components of IoTCrawler are provided under EUPL-1.2, Apache-2.0 and MIT licenses. You will find more information in respective component repository.
