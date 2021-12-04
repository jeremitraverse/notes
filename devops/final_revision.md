# FIRST WAY
- Dev send changes to ops
  - Infrastructure problems, because often created manually
    - Takes time because ops engineer are busy and understaff
      - Automatisation and on demand services
    - Prone to low quality
      - Human error
      - All the good dev practice that we have for the codebase won't
        be applied to the infrastructure
  
  - Automating the infrastructure creation
    - Provisionning (cloud)
    - Configuration (Ansible, Puppet, Chef)
    - Deployment
    - Maintenance
**DONE STATE** When the dev as finished the code and passed all the tests

## DEV FLOW
1. Code is tested on a production like environment
2. Ask for an integration
3. Build is triggered
  - Trigger the CI
    - Compile
    - Test
  - Cons:
    - Can take a lot of time
    - Can loose time when we have a build failure at the last step of the build
    - Too decrease time, we run locally before making a push:
      - Run integrations test
      - Run systems test
      - Run unit test
        - We want to increase the amount of unit test because they are easy and cheap
4. Output is a binary file that has to be stocked in a artifact repo
5. In case of a build failure
  - Mobilize all the team to work on the bug
    - Pull the Andon cord
    - Stop other dev to push code to the main branch

**DONE STATE** state when the code is well integrated with the codebase

## CONTINUOUS INTEGRATION
- Working on different and short lived branches
  - Code in developpement is isolated
  - Makes integration more difficult
    - Having conflicts
  - More the lifetime of a branch is long, the higher the chance to have integration
    problems
- Having a single main branch

- Having the code pass through a stablization branch before deployment
  - Two types of deployment
    - Based on servers
      - Deploy on server, check if everything is alright, then pass to the next one
      - Blue Green
        - Having a server (blue) that has the new version, and another server (green)
          that has the old version and gradually moving users from green to blue
    - Based on applications
      - Toggle switch
        - Code is on production, but hidden behind a switch

## ARCHITECTURE
- Two types
  - Monolithic
    - PROS:
      - Easier at the beggining of the project
      - More performant when the user base is small
        - No overhead of the microservices connection
    - CONS:
      - Gets hard the more the project gets big

  - Microservices
    - PROS:
      - Easy to maintain
      - Scalable
      - More performant when the userbase is high
    - CONS:
      - Needs a complexe infrastructure
      - Technologies

- There's not only one strategy that works everytime
- Depends on  
  - User base/ load
  - Team size
  - Age of the software
- The more often we see migration from monolithic to microservices
  - Strangler pattern
    - Start from a functionality and hide it behind an API
    - Remove the code from the main codebase 
    - The most difficult part of this pattern is to find the first functionality
      to transform

# SECOND WAY
- Increase feedbacks from ops to dev
  - Using telemetry
    - Put in place the infrastructure to :
      1. Collect data
        - OS (memory consumption, network)
        - Application (exception, try/catch)
        - Business (userbase, successful/unsucessful authentification)
        - Deployment pipeline (failed tests, build time)
      2. Store data
      3. Visualize data (Grafana)
      4. By looking at the data, we can send alerts
    - The more logs that we have, the slower the program gets hence the need to log only
      useful metrics
      - Metrics to detect potential failure point
- Statistical methods to analyze telemetry
  - Outliers detection
    - Detect service that use more memory
  - Gaussian distribution
  - Need telemetry that gives us indication on the status of the deployment
    - Fix forward
    - Rollback
- Pager-rotation to solve the issue 
  - Dev that are on the rotation needs to focus on the issue
  - Dev that are the closest to the problem has the best toolkit to solve the issue
  - Allow dev to see how hard is it to fix ops issues
- Context research
  - Study how the user interact with the product the way that it's intend too
- Make sure that the new functionality provides value to the product
  - A/B testing
    1. We supposed ______
    2. Improves _______
    3. We'll go forward if ________
    - We need metrics to understand how the clients goes through the client funnel

**DONE STATE** when the functionality gives value to the product

- Peer reviews
  - Opposite to code approbation from an external source
  - Peer programing
  - Pull request
    - Github flow
      1. Dev create a small lived branch from the main branch
      2. Ask for a merge. The ask for merge action creates a discussion with the 
      maintainers and bots
      3. Integrate the code to the main branch
    - Need to increase the quality of the pull requests

# THIRD WAY
- Main goal is to bring upfront the continuous learning culture and the just culture
  - Create a Postmortem report
    - Git
    - Wiki
    - Morgue (Etsy)
  - Having a resilient environment
    - Chaos Monkey
    - Value Chain


**IMPORTANT POINT**
- Folwer's pyramid
- A/B Testing

