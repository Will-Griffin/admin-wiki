# When to use RAID
when there is something that may evolve into a blocker

# RAID Types

## RAID - Risk
A project risk is an uncertain event that may occur during a project but hasn't happened. Use this type when:
- Delivery Risk - something that may impact the delivery milestone deadline.
- Operational Risk - risks that may impact customer operations, such as risks to security posture if not following the delivery team's recommendation.

## RAID - Action
Open an **Action** item when you depend on an activity that you don't have direct control. Examples:
- need Joe to create an Azure subscription (tag Joe so he can take action)
- need Mark to configure network proxy to allow traffic flow to xxx
- need Maria to grant AAD role XXX to complete task YYY

## RAID - Issue
An **Issue** is an event or condition that has already happened and has negative consequences to the project. Create an **Issue** when you encounter something that prevents moving forward with a task. An **Issue** differs from an **Action** in that an **Issue** is something the creator is responsible for and is actively working to resolve the issue. For example:
- I cannot complete a task because I need to troubleshoot why packets are getting lost.


## RAID - Decision
Use a **Decision** when there is a dependency on a judgment. Examples:

- Decide on whether to use an Azure Storage Account vs. a database for storing a specific type of data.
- Decide on using CMK vs. PMK.
- Something needs to be decided by the team.
