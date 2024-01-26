# 2aman lafr9a -  la3ab o nta marata7

![football-insurance.webp](2aman%20lafr9a%20-%20la3ab%20o%20nta%20marata7%20ee18d6eea95c4dfe8ba216bfbc551b31/football-insurance.webp)

**Problem :**

In the realm of football, numerous players face injuries in every match, instilling a sense of fear as the sport represents their livelihood. Life unfolds with its inherent uncertainties, and players inevitably grapple with injuries and challenges. On the flip side, numerous insurance agencies strive to provide coverage for these athletes. However, reaching a consensus often proves elusive, as teams seek tailored solutions that may not align with offerings from other agencies.

**Solution:**

An application, powered by machine learning, revolutionizes the sports industry by providing team managers with intelligent recommendations for offers. The incorporation of blockchain technology ensures the security and transparency of contract storage while embracing a 100% digital experience, including cryptocurrency payments, Additionally, the application is built on a micro-services architecture, offering scalability, flexibility, and efficiency by breaking down functionalities into modular and independent services. This innovative approach not only streamlines the negotiation process but also enhances efficiency and security in the management of player contracts.

**Our application’s architecture:**

As stated before we chose to use a micro-services architecture using an API gateway written in Spring Boot as the medium for communication, in addition to allowing our micro-services to communicate we decided to utilize the GRPC framework due to its fast response times and broad language support.

![Untitled](2aman%20lafr9a%20-%20la3ab%20o%20nta%20marata7%20ee18d6eea95c4dfe8ba216bfbc551b31/Untitled.png)

As you can see above Client can only communicate with the API gateway, which in turn will check the credentials of the client with the authentication micro-service, and only then will the gateway allow it to access the other components of the application.

Let us explore our back-end schema:

1. **API Gateway**

This micro-service is a Java-based API Gateway application that uses Spring Boot and Maven. It serves as an intermediary for various services, including authentication, agency, offer, team, user, player, rating, and team manager services. These services are defined and accessed via gRPC clients.

The project uses GraphQL for defining the types and queries for the various entities in the system. These include Agency, Offer, Team, Player, Rating, and Team Manager. Each entity has its own GraphQL schema file, and the queries are defined in the query. graphics.

1. **Auth service:**
    
    ![Gateway.jpg](2aman%20lafr9a%20-%20la3ab%20o%20nta%20marata7%20ee18d6eea95c4dfe8ba216bfbc551b31/Gateway.jpg)
    

This microserver is responsible for JWT authentication, and role-based authorization, it is written with a low level language and a fast language **RUST** (Rust is a multi-paradigm, general-purpose programming language that emphasizes performance, type safety, and concurrency. It enforces memory safety, meaning that all references point to valid memory, without requiring the use of automated memory management techniques, such as garbage collector) 

[https://en.wikipedia.org/wiki/Rust_(programming_language)](https://en.wikipedia.org/wiki/Rust_(programming_language))

It uses a MySql database ( Relational database ) as  a primary database to store its data, and redis to cache the user data so the access to db will be fast, and it provides a GRPC interface to deal with it, it’s dumps and all that it knows is AUTH only, the methods it provides are 

```protobuf
rpc SignUp(SignUpRequest) returns (SignUpResponse);
rpc SignIn(SignInRequest) returns (SignInResponse);
rpc validateToken(TokenValidationRequest) returns (TokenValidationResponse);
```

what makes this microservice essential and special, it’s stateless, reusable, and central, but it’s too crucial because it’s a point of failure, and it’s used by the API gateway to validate authorizations and make sure that all routes are protected, and it hides the details of auth from any other microservers so devs can focus only on the business logic of their microservices.

1. **Agencies and Offer Management:**

These 2 services were written in GOLANG and used a PostgreSQL database, the Agencies micro-service is responsible for managing agencies. It provides functionalities such as creating, updating, retrieving, and deleting agencies.

The Offers micro-service is responsible for managing offers. It provides functionalities such as creating, updating, retrieving, and deleting offers.

[https://en.wikipedia.org/wiki/Go_(programming_language)](https://en.wikipedia.org/wiki/Go_(programming_language))

It uses a PostgreSQL database ( Relational database ) as  a primary database to store its data, and it provides a GRPC interface to deal with it, it’s dumps and all that it knows is Agency/ offers only, the methods it provides are 

```protobuf
	# Agency
	rpc GetAgencies(GetAgenciesRequest) returns (GetAgenciesResponse);
  rpc GetAgency(GetAgencyRequest) returns (GetAgencyResponse);
  rpc CreateAgency(CreateAgencyRequest) returns (CreateAgencyResponse);
  rpc UpdateAgency(UpdateAgencyRequest) returns (UpdateAgencyResponse);
  rpc DeleteAgency(DeleteAgencyRequest) returns (DeleteAgencyResponse);

	# Offers
	rpc GetOffers(GetOffersRequest) returns (GetOffersResponse);
  rpc GetOffer(GetOfferRequest) returns (GetOfferResponse);
  rpc CreateOffer(CreateOfferRequest) returns (CreateOfferResponse);
  rpc UpdateOffer(UpdateOfferRequest) returns (UpdateOfferResponse);
  rpc DeleteOffer(DeleteOfferRequest) returns (DeleteOfferResponse);
```

1. **Teams and player management:**

These 2 services were written in RUBY and used a mysql database, the Teams micro-service is responsible for managing Teams. It provides functionalities such as creating, updating, retrieving, and deleting Teams.

The player micro-service is responsible for managing player. It provides functionalities such as creating, updating, retrieving, and deleting player.

[https://en.wikipedia.org/wiki/Ruby_(programming_language)](https://en.wikipedia.org/wiki/Ruby_(programming_language))

It uses a Mysql database ( Relational database ) as  a primary database to store its data, and it provides a GRPC interface to deal with it, it’s dumps and all that it knows is teams/ players only, the methods it provides are 

```protobuf
# Team manager
		rpc GetTeamManager (GetTeamManagerRequest) returns (GetTeamManagerResponse) {}
    rpc GetTeamManagers (GetTeamManagersRequest) returns (GetTeamManagersResponse) {}
    rpc CreateTeamManager (CreateTeamManagerRequest) returns (CreateTeamManagerResponse) {}
    rpc UpdateTeamManager (UpdateTeamManagerRequest) returns (UpdateTeamManagerResponse) {}
    rpc DeleteTeamManager (DeleteTeamManagerRequest) returns (DeleteTeamManagerResponse) {}
# Players
		rpc GetPlayer(GetPlayerRequest) returns (GetPlayerResponse) {}
    rpc CreatePlayer(CreatePlayerRequest) returns (CreatePlayerResponse) {}
    rpc UpdatePlayer(UpdatePlayerRequest) returns (UpdatePlayerResponse) {}
    rpc DeletePlayer(DeletePlayerRequest) returns (DeletePlayerResponse) {}
    rpc GetPlayers(GetPlayersRequest) returns (GetPlayersResponse) {}
# Teams
    rpc CreateTeam(CreateTeamRequest) returns (CreateTeamResponse) {}
    rpc GetTeam(GetTeamRequest) returns (GetTeamResponse) {}
    rpc UpdateTeam(UpdateTeamRequest) returns (UpdateTeamResponse) {}
    rpc DeleteTeam(DeleteTeamRequest) returns (DeleteTeamResponse) {}
    rpc GetTeams(GetTeamsRequest) returns (GetTeamsResponse) {}
```

# Recommendation System

In the dynamic world of sports, where team managers are tasked with building and enhancing their teams, our Recommendation System comes to the forefront as a powerful tool designed to assist team managers in making informed decisions. Whether you are a seasoned team manager or just starting out, our platform aims to streamline the player selection process by incorporating intelligent recommendations for insurance offers tailored to the preferences and historical choices of each team's unique player.

## Project Overview

### Objective

The primary objective of our Recommendation System is to empower team managers with a data-driven approach when assigning insurance offers to their players. By leveraging machine learning techniques and collaborative filtering algorithms, the system analyzes player data, preferences, and historical choices to provide top-k recommendations for insurance offers that align with the individual player's profile.

### How It Works

1. **Player Information Input:**
    - Team managers input detailed information about each player, including personal details, performance metrics, and other relevant attributes.
2. **Preferences Analysis:**
    - The system analyzes the preferences of each player, considering factors such as age, overall performance, and club affiliations.
3. **Collaborative Filtering:**
    - Leveraging collaborative filtering, the system identifies similar players based on historical data and preferences.
4. **Top-k Recommendations:**
    - The system generates top-k recommendations for insurance offers by comparing the player's preferences with those of similar players.

### Use Case Scenario

Imagine a team manager adding a new player to their roster. When it comes time to assign insurance offers, the team manager may not have extensive knowledge of the insurance market. This is where our Recommendation System steps in, providing personalized recommendations based on the player's characteristics and the choices of players with similar profiles.

## Key Features

- **Dynamic Recommendations:** The system adapts to changes in player data and preferences, ensuring recommendations stay relevant over time.
- **User-Friendly Interface:** Team managers can easily navigate the platform, input player data, and access insurance recommendations seamlessly.
- **Scalability:** The system is designed to handle growing datasets and an increasing number of users, making it suitable for teams of all sizes.

# Technologies & Tools

## Backend Development

### 1. Python Programming Language and Jupyter Notebook

- **Use Cases:**
    - Backend logic implementation.
    - Machine learning and data analysis.

### 2. Flask Framework

- **Use Case:**
    - API development for communication between frontend and backend.

### 3. Git/GitHub

- **Use Cases:**
    - Version control for collaborative development.
    - Source code management.

### 4. Apache Kafka

![Untitled](https://github.com/2aman-lafr9a/RecommendationSystem/assets/90706276/21df5958-b8a5-4a19-9ca3-8f561e0262e6)

- **Use Case:**
    - Kafka facilitates real-time event streaming, essential for dynamic updates in the recommendation system.

### 5. Apache Zookeeper

![Untitled(1)](https://github.com/2aman-lafr9a/RecommendationSystem/assets/90706276/dc3cae98-bea5-4477-8b5d-04c92750a66b)

- **Use Case:**
    - Zookeeper ensures distributed coordination and synchronization.

## MLOps

### 1. Docker

![Untitled(2)](https://github.com/2aman-lafr9a/RecommendationSystem/assets/90706276/c544d466-2f20-4b2d-95c9-46d5e6535c5d)

- **Use Case:**
    - Containerization for consistent deployment across environments.

### 2. Apache Airflow

![Untitled(3)](https://github.com/2aman-lafr9a/RecommendationSystem/assets/90706276/df79daf4-f709-4105-9207-4eed52fbad9e)

- **Use Cases:**
    - Orchestrating and scheduling workflows.
    - Automation of data processing and model training pipelines.

### 3. Data Version Control (DVC)

![file-type-dvc-icon-512x293-js3het8o](https://github.com/2aman-lafr9a/RecommendationSystem/assets/90706276/6163b22e-1155-4e82-a2fd-d4ad3d517486)

- **Use Case:**
    - Efficient versioning of datasets for reproducibility and traceability.

### 4. CI/CD using GitHub Actions (CML - Continuous Machine Learning)

![Untitled(4)](https://github.com/2aman-lafr9a/RecommendationSystem/assets/90706276/3a9b7b6a-43de-4b09-99bc-28bbdd3d70b4)

- **Use Cases:**
    - Continuous integration for automated testing.
    - Continuous deployment for seamless updates.

## Databases

### 1. Cassandra Database

![Untitled(5)](https://github.com/2aman-lafr9a/RecommendationSystem/assets/90706276/ca17e3e7-8238-412a-8158-8b2d04570e5b)

- **Use Cases:**
    - Scalable storage and retrieval of player data.
    - Efficient handling of large datasets.

### 2. PostgreSQL Database

- **Use Cases:**
    - Management of rating data and insurances data.
    - Relational database capabilities.

# Getting Started

...

# Recommendation System Overview

A **Recommendation System** is a software application designed to provide personalized suggestions or advice to users. Its primary goal is to enhance user experience by predicting and recommending items of interest, such as products, services, or content, based on user preferences and historical interactions.

## Collaborative Filtering

**Collaborative Filtering** is a popular technique in Recommendation Systems that leverages the collective preferences and behavior of users. It assumes that users who agreed in the past tend to agree in the future. There are two main types:

1. **User-User Collaborative Filtering:** Recommends items to a user based on the preferences of other users with similar tastes.
2. **Item-Item Collaborative Filtering:** Recommends items that are similar to those the user has liked or interacted with.

![Untitled-2024-01-18-1833](https://github.com/2aman-lafr9a/RecommendationSystem/assets/90706276/6664becc-0c94-48a4-9ed8-fb900d8ec125)

## User-Item Collaborative Filtering

**User-Item Collaborative Filtering** is a type of Collaborative Filtering where recommendations are made by identifying users who are similar to the target user and suggesting items that those similar users have liked or interacted with.

![RecSys1](https://github.com/2aman-lafr9a/RecommendationSystem/assets/90706276/fe058e49-e070-4969-af4b-b911b6864540)

# Architecture

## 1. **Pre-processing**

![RecSys3](https://github.com/2aman-lafr9a/RecommendationSystem/assets/90706276/8d4b0338-1c5d-42ff-be43-4ac436000e44)

## 2. Model Training

![RecSys4](https://github.com/2aman-lafr9a/RecommendationSystem/assets/90706276/5b480d9c-8cef-4fd9-af90-bce07555fb48)

## 3. User-Based Collaborative Filtering

![RecSys5](https://github.com/2aman-lafr9a/RecommendationSystem/assets/90706276/6891d9c3-e383-4e92-848b-fe5e887da321)

![RecSys6](https://github.com/2aman-lafr9a/RecommendationSystem/assets/90706276/4c2443d2-382f-47c5-a2db-beaf0ac0f236)

    
    The a**rchitecture of the blockchain:**
    
    ![1_3VnQFDfautjlj690oaf5hg.webp](2aman%20lafr9a%20-%20la3ab%20o%20nta%20marata7%20ee18d6eea95c4dfe8ba216bfbc551b31/1_3VnQFDfautjlj690oaf5hg.webp)
    
    This architecture illustrates the interaction between various components involved in a decentralized application (DApp) built on the Ethereum blockchain, specifically a DApp that utilizes smart contracts. The components are as follows:
    
    1. **Internet**: The global network that enables data communication between devices.
    2. **Web Server**: A server that hosts the web application, serving static files like HTML, CSS, and JavaScript to users' browsers.
    3. **Browser**: A software application used to access and display web content, such as a DApp's user interface.
    4. **Block**: A fundamental unit of data storage in blockchain technology, containing a collection of transactions.
    5. **Front-end**: The user interface of a DApp, built using technologies like JavaScript, HTML, and CSS.
    6. **Smart Contracts**: Self-executing digital agreements deployed on the Ethereum blockchain, governing the logic and functionality of a DApp.
    7. **Ethereum Virtual Machine (EVM)**: A virtual machine that executes smart contracts on the Ethereum blockchain, ensuring consistent and predictable behavior across all nodes.
    8. **Ethereum Blockchain**: The decentralized, distributed ledger that stores and maintains the state of smart contracts and transactions on the Ethereum network.
    
    The architecture can be described as follows:
    
    1. The Internet enables communication between the web server and the user's browser.
    2. The web server hosts the front-end components (HTML, CSS, JavaScript) of the DApp, serving them to the user's browser upon request.
    3. The user's browser receives and displays the front-end components, allowing the user to interact with the DApp.
    4. When the user interacts with the DApp, the browser sends transactions to the Ethereum blockchain.
    5. The transactions are grouped into blocks and added to the Ethereum blockchain by the network's nodes.
    6. The smart contracts, deployed on the Ethereum blockchain, execute the logic and functionality of the DApp.
    7. The Ethereum Virtual Machine ensures consistent execution of smart contracts across all nodes in the Ethereum network.
    8. The Ethereum blockchain maintains the state of smart contracts and transactions, providing a tamper-proof, decentralized record of all interactions.

**Deployment :**

The deployment has been successfully executed in Azure using a comprehensive stack that includes Docker, Docker Compose, Kubernetes (k8s), Jenkins, Azure Container Registry, Azure Storage, Azure DNS, and Azure Load Balancer. Let's break down the role of each technology in this deployment:

1. **Docker:** Docker is used for containerization, allowing the application and its dependencies to be packaged into a single container. Containers ensure consistency across different environments and simplify deployment.
2. **Docker Compose:** Docker Compose is used to define and manage multi-container Docker applications. It allows you to specify the services, networks, and volumes required for the application in a **`docker-compose.yml`** file.
3. **Kubernetes (k8s):** Kubernetes is a container orchestration platform that automates the deployment, scaling, and management of containerized applications. It provides features such as load balancing, auto-scaling, and self-healing.
4. **Jenkins:** Jenkins is a popular open-source automation server used for building, testing, and deploying code. In this context, Jenkins likely automates the CI/CD (Continuous Integration/Continuous Deployment) pipeline, triggering builds and deployments based on changes to the codebase.
5. **Azure Container Registry:** Azure Container Registry is a private container registry in Azure where Docker container images are stored. It provides a secure and scalable way to manage and deploy container images.
6. **Azure Storage:** Azure Storage is used for storing various types of data, such as artifacts, logs, and configuration files. It can be utilized for persistent storage needs within the deployment.
7. **Azure DNS Registry:** Azure DNS is a domain name system (DNS) service provided by Azure. Azure DNS Registry is likely a typo, and it might refer to Azure DNS for managing domain names and mapping them to the deployed services.
8. **Azure Load Balancer:** Azure Load Balancer distributes incoming network traffic across multiple servers to ensure no single server is overwhelmed. It enhances the availability and reliability of applications by balancing the load across multiple instances of the deployed application.
9. **Azure Monitor:**
- **Overview:** Azure Monitor is a comprehensive solution for collecting, analyzing, and acting on telemetry data from Azure resources.
- **Metrics:** Azure Monitor provides metrics for Azure resources, enabling users to visualize and analyze the performance of their applications and infrastructure.
- **Logs:** Azure Monitor collects and analyzes log data from resources, offering powerful querying and analysis capabilities with Azure Monitor Logs (formerly known as Log Analytics).

In summary, this deployment stack combines containerization, orchestration, automation, and cloud services to create a robust and scalable infrastructure on Azure. Docker and Docker Compose help with packaging and managing containers, Kubernetes orchestrates these containers, Jenkins automates the deployment pipeline, and Azure services provide a cloud-native environment for hosting and managing the application.

# Client Side:

## Technologies used

- **React**
    
    ![Untitled](2aman%20lafr9a%20-%20la3ab%20o%20nta%20marata7%20ee18d6eea95c4dfe8ba216bfbc551b31/Untitled%203.png)
    
     
    
    # **React Overview**
    
    ## **What is React?**
    
    React is an open-source JavaScript library developed by Facebook for building user interfaces or UI components. It is known for its simplicity, flexibility, and efficiency. If you're new to React or need a refresher, this section will provide you with a brief overview of React and its key concepts.
    
    ## **Key Concepts**
    
    ### **1. Components**
    
    In React, the UI is broken down into components, which are modular, reusable building blocks. Components encapsulate both the UI and the logic associated with it, making it easier to manage and maintain code.
    
    ### **2. JSX (JavaScript XML)**
    
    React uses JSX, a syntax extension that allows you to write HTML-like code within JavaScript. JSX makes it more straightforward to define the structure of components and helps create a more readable and concise codebase.
    
    ### **3. Virtual DOM**
    
    React uses a Virtual DOM to optimize the updating of the actual DOM. Instead of updating the entire DOM tree, React updates a virtual representation of it and then calculates the most efficient way to update the real DOM.
    
    ### **4. State and Props**
    
    State represents the data that a component manages, while props (short for properties) are data passed from a parent component to a child component. Both play a crucial role in making components dynamic and interactive.
    

[https://react.dev/](https://react.dev/)

To have successful software, you need to have a great foundation. It needs to be scalable, easy to upgrade and easy to maintain.

The days when every React project had to be pieced together via elaborate Webpack configuration are behind us, and now we can take advantage of frameworks such as [Next.js](https://nextjs.org/)  the idea is : combine the latest web technologies under **one package**. Which is just perfect!

You get :

- new features, bug fixes and security updates with a simple - update of ONE package
- easy maintenance
- built and maintained by a huge community and technology leaders ….
    
    
    ### Next.js
    

# **Benefits of Using Frontend Frameworks**

## **1. Efficiency in Development:**

- Frameworks provide a structured and organized way of building applications, reducing the time and effort required for development.
- They often come with a set of conventions and best practices, making it easier for developers to collaborate and maintain code.

## **2. Reusability of Components:**

- Components in frameworks are designed to be reusable, promoting a modular approach to development.
- Developers can create encapsulated components that can be reused across different parts of the application or even in other projects.

## **3. Declarative Syntax:**

- Many frameworks, including React, use a declarative syntax, which makes it easier to understand and reason about the code.
- Developers describe what they want to achieve, and the framework takes care of the underlying logic.

## **4. Virtual DOM (React):**

- React's virtual DOM allows for efficient updates to the actual DOM, reducing unnecessary re-rendering and improving performance.
- Changes are batched and optimized, resulting in a smoother user experience.

## **5. Community and Ecosystem:**

- Frameworks often have large and active communities, providing access to a wealth of resources, libraries, and third-party tools.
- This community support can be invaluable for problem-solving, learning, and staying updated with best practices.

## **6. Performance Optimization:**

- Frameworks are often optimized for performance, implementing features like code splitting, lazy loading, and server-side rendering (as in Next.js).
- These optimizations contribute to faster page loads, improved SEO, and an overall better user experience.

## **7. Maintainability:**

- The structured nature of frameworks promotes maintainability, making it easier for developers to understand, update, and debug code.
- Frameworks often enforce coding standards and provide tools for testing and debugging.

# **Benefits of Using Next.js (Built on React)**

## **1. Server-Side Rendering (SSR):**

- Next.js allows for server-side rendering, improving initial page load times and enhancing search engine optimization (SEO).
- Pages can be pre-rendered on the server, delivering a fully rendered page to the client.

## **2. Automatic Code Splitting:**

- Code splitting is automatic in Next.js, leading to smaller initial bundle sizes and faster page loads.
- Only the code necessary for the current view is loaded, and additional code is loaded on-demand.

## **3. Simplified Routing:**

- Next.js provides a file-based routing system, simplifying the organization of pages in the project.
- Dynamic routes and catch-all routes are easily implemented.

## **4. API Routes:**

- Next.js allows the creation of API routes within the same project, simplifying the integration of backend functionality directly within the frontend.

## **5. Static Site Generation (SSG):**

- Next.js supports static site generation, enabling the generation of static HTML at build time.
- This is particularly useful for content that doesn't change frequently, improving performance and reducing the load on servers.

## **6. Community and Documentation:**

- Next.js benefits from the strong React community and has its own active community.
- The framework provides comprehensive documentation, making it easier for developers to get started and find solutions to common challenges.

## **7. Easy Deployment:**

- Deploying Next.js applications is straightforward, and the framework supports a variety of deployment options, including serverless deployments and static site hosting.

Using frameworks like React and Next.js offers a multitude of advantages, ranging from improved developer efficiency to enhanced application performance and maintainability. These benefits contribute to a better overall development experience and the delivery of high-quality, scalable applications.

Next.JS is the best choice in most cases. It works best for server-side rendered applications, but can also be used for client-side and statically exported websites. It works equally well with content-driven websites regardless of the amount of content.

Pros

- Created by Vercel
- Provides outstanding server-side capabilities
- SEO/SMO friendly
- Works just as well for applications that don't require SSR
- Has static export
- Can combine server-side rendering with static export
- Good choice when you need to handle secrets (aka API keys that must not be exposed on the client)
- With server comes huge responsibility: security
- Uses framework-specific abstractions such as `getServerSideProps`, so when doing a refactor to another framework, it requires extra effort

Rendering on the web is a difficult topic. It wasn’t that long ago that rendering was the responsibility of backend engineers. Today, it’s the job of a fullstack developer.

Luckily, there are many great resources available. Big kudos to Jason Miller and Addy Osmani for putting together an article on Google 

Developers: [https://developers.google.com/web/updates/2019/02/rendering-on-the-web](https://developers.google.com/web/updates/2019/02/rendering-on-the-web)

![Untitled](2aman%20lafr9a%20-%20la3ab%20o%20nta%20marata7%20ee18d6eea95c4dfe8ba216bfbc551b31/Untitled%204.png)

## **NEXT UI**

**Next UI** is a comprehensive UI library tailored for use with Next.js, a popular React framework. Developed with a focus on enhancing the user interface and user experience, Next UI provides a collection of pre-designed, responsive, and customizable components that seamlessly integrate with Next.js projects. Whether you're building a web application, e-commerce site, or a dynamic dashboard, Next UI simplifies the development process by offering a set of well-crafted components and styles that adhere to modern design principles.

- **Component Library:**
    - Next UI comes equipped with a rich set of components, including navigation bars, modals, buttons, forms, and more. These components are designed to be versatile, enabling developers to easily customize them to match the specific requirements of their projects.
- **Responsive Design:**
    - All components within Next UI are built with responsiveness in mind, ensuring a seamless user experience across various devices and screen sizes. The responsive nature of Next UI components facilitates the development of applications that are accessible and user-friendly on desktops, tablets, and mobile devices.
- **Easy Integration with Next.js:**
    - Next UI is crafted to seamlessly integrate with Next.js projects, providing a harmonious development experience. The library aligns with Next.js conventions, making it effortless for developers to incorporate these UI components into their applications.
- **Customization and Theming:**
    - Next UI emphasizes customization, allowing developers to tailor the appearance of components to match the unique branding and styling preferences of their projects. The library supports theming, enabling the creation of cohesive and visually appealing user interfaces.
- **Modern Design Aesthetics:**
    - Next UI follows modern design principles, offering components with clean aesthetics and thoughtful user interactions. The library is continuously updated to stay in sync with the latest design trends, ensuring that your applications maintain a contemporary look and feel.

[https://nextui.org/](https://nextui.org/)

Hierarchy of the Project : 

![Untitled](2aman%20lafr9a%20-%20la3ab%20o%20nta%20marata7%20ee18d6eea95c4dfe8ba216bfbc551b31/Untitled%205.png)

Ta2minUi stands as a comprehensive Next.js project, orchestrating the frontend logic of a sophisticated application. The organized hierarchy within the main 'Ta2minUi' folder is designed to provide clarity and efficiency in development:

- **app Directory:**
    - Within 'app,' each subfolder represents a key application route, including:
        - 'auth': User authentication logic.
        - 'offers': Functionality related to managing and displaying offers.
        - 'players': Components and features for handling player-related information.
        - 'team': Logic associated with managing teams.
        - 'agency': Specific functionalities related to agencies.
        - 'teamManager': Features associated with team managers.
        - 'page.tsx': The main page component.
        - 'provider.tsx': Logic for application state management.
        - 'layout.tsx': Components dedicated to structuring the UI.
- **components Directory:**
    - 'components' serves as a repository for reusable UI elements, fostering a modular approach to development:
        - 'charts': Components related to data visualization using charts.
        - 'darkmoodSwitcher': Elements facilitating toggling between dark and light modes.
        - 'home': Components specifically tailored for the home page.
        - 'hooks': A collection of custom React hooks for application-wide use.
        - 'icons': Components responsible for rendering various icons.
        - 'layout': Components for structuring the UI layout.
        - 'navbar': Components associated with navigation bars.
        - 'offers': Components specifically designed for displaying and managing offers.
        - 'players': Components focused on displaying and managing player information.
        - 'sidebar': Components responsible for rendering the sidebar navigation.
        - 'table': Components related to displaying tabular data.
        - 'teams': Components dedicated to managing teams.
- **graphql Directory:**
    - The 'graphql' folder manages GraphQL-related files and queries,
- **styles Directory:**
    - The 'styles' folder serves as a centralized repository for stylesheets and related assets, contributing to a cohesive and visually appealing user interface.
    - 

This meticulously structured hierarchy not only ensures a clear organization of the project but also enhances the ease of development, maintenance, and collaboration. Ta2minUi is a testament to the power of Next.js when coupled with a well-structured architecture, fostering a seamless development experience and setting the stage for the creation of powerful and scalable web applications.

**Dark Mode and Light Mode:**

- The 'darkmoodSwitcher' component provides users with the functionality to seamlessly toggle between dark mode and light mode.
- Dark mode offers a visually comfortable and energy-efficient option for users in low-light environments.
- Light mode provides a standard, well-lit interface for users who prefer a traditional viewing experience.
- The integration of these modes reflects Ta2minUi's commitment to providing a personalized and user-friendly interface, enhancing the overall user experience.

**DARK MODE** 

![Untitled](2aman%20lafr9a%20-%20la3ab%20o%20nta%20marata7%20ee18d6eea95c4dfe8ba216bfbc551b31/Untitled%206.png)

**LIGHT MODE**

![Untitled](2aman%20lafr9a%20-%20la3ab%20o%20nta%20marata7%20ee18d6eea95c4dfe8ba216bfbc551b31/Untitled%207.png)

The switcher :

![Untitled](2aman%20lafr9a%20-%20la3ab%20o%20nta%20marata7%20ee18d6eea95c4dfe8ba216bfbc551b31/Untitled%208.png)

![Untitled](2aman%20lafr9a%20-%20la3ab%20o%20nta%20marata7%20ee18d6eea95c4dfe8ba216bfbc551b31/Untitled%209.png)

# **Contributors:**

Sohaib MANAH: [sohaibMan](https://github.com/sohaibMan)

[sohaibMan - Overview](https://github.com/sohaibMan)

[https://www.linkedin.com/in/sohaibmanah/](https://www.linkedin.com/in/sohaibmanah/)

Anas Zenagui : [ZenaguiAnas](https://github.com/ZenaguiAnas)

[ZenaguiAnas - Overview](https://github.com/ZenaguiAnas)

Bakr Asskali:  [AsskaliBakr](https://github.com/ZenaguiAnas)

[BakrAsskali - Overview](https://github.com/BakrAsskali)

[https://www.linkedin.com/in/bakr-asskali-1b2975225/](https://www.linkedin.com/in/bakr-asskali-1b2975225/)

Ismail OUKHA : [itsmeismaill](https://github.com/itsmeismaill)

[itsmeismaill - Overview](https://github.com/itsmeismaill)

[](https://www.linkedin.com/in/ismail-oukha-90a070227/)

**HADDAD MOHAMMED : [HADDADmed](https://github.com/HADDADmed)**

[HADDADmed - Overview](https://github.com/HADDADmed)

[https://www.linkedin.com/in/mohammed-haddad-828507216/](https://www.linkedin.com/in/mohammed-haddad-828507216/)

# **Github Project Repo Link:**

[2aman-lafr9a](https://github.com/2aman-lafr9a)

# O**riented by :**

Dr. *Lotfi* EL *ACHAAK*

[https://www.linkedin.com/in/lotfi-elaachak-a9202324/](https://www.linkedin.com/in/lotfi-elaachak-a9202324/)

[SCRUM](https://www.notion.so/SCRUM-5dad4303e81c4568a750c931f4cc3ff4?pvs=21)
