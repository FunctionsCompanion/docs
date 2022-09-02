---
layout: default
title: sfdx Commands
nav_order: 8
---

# Helpful sfdx Commands

- Logging in

    - sfdx update
    - sf --version
    - sfdx auth:web:login --setdefaultdevhubusername

- COMMIT BEFORE THE FOLLOWING

    - ./buildit.sh
    - sf env list --all
    - Just building after a change
        - sf deploy functions -o "MY_ORG"

- Setting up log drain (Replace MY below with env prefix)

    - sf env logdrain list -e MY_ENV
    - sf env logdrain add -e "MY_ENV" --drain-url <logdrain url>
    - sf deploy functions -o "MY_ORG"
    - sf env create compute -o "MY_ORG" -a "MY_ENV"

- Removing the log drain

    - sf env logdrain list -e MY_ENV
    - sf env logdrain remove -e MY_ENV --drain-url <logdrain url>
    - logdrain choices
        - syslog://logger.lastmileops.ai:20514 - lmo docker instance

- Deleting the env and org

    - sf env delete -e MY_ENV
    - sfdx force:org:delete -u MY_ORG

- Running
    - Set the API Key
        - sfdx force:org:open -u MY_ORG
        - When the page opens go to https://<sfurl>/lightning/n/FCConnect
        - Enter the apiKey
    - Run the tests
        - runAllSync.sh
        - runAllAsync.sh

- Other Commands
    - sfdx force:org:list
