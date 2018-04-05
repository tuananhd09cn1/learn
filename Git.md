
Instance
Branch
Description, Instructions, Notes
Instance
Branch
Description, Instructions, Notes
Stable	stable	
Accepts merges from Working and Hotfixes.
This branch will build to QA server.
Affter QA confirm all task and issue resolved, We will release a version.
Working	master	
Accepts merges from Features/Issues and Hotfixes
This branch will build to DEV Server.
Features/Issues	topic-*	Always branch off HEAD of Working
Hotfix	hotfix-*	Always branch off Stable
Tags	v* (Tags)	Release version
Production	production	Current Release
Main Branches
The main repository will always hold two evergreen branches:
master
stable
The main branch should be considered origin/master and will be the main branch where the source code of HEAD always reflects a state with the latest delivered development changes for the next release. As a developer, you will you be branching and merging from master.
Consider origin/stable to always represent the latest code deployed to production. During day to day development, the stable branch will not be interacted with.
When the source code in the master branch is stable and has been deployed, all of the changes will be merged into stable and tagged with a release number. 
Supporting Branches
Supporting branches are used to aid parallel development between team members, ease tracking of features, and to assist in quickly fixing live production problems. Unlike the main branches, these branches always have a limited life time, since they will be removed eventually.
The different types of branches we may use are:
Feature branches
Bug branches
Hotfix branches
