# sourced-db

Use this repo as a template and import it into your JX cluster to deploy a PSQL based Sourced Event Store via Zalando PostgreSQL Operator, and then configures the database for use with sourced by creating the "Event" table with SchemaHero.

## Prerequisites

1. A Kubernetes cluster with ArgoCD configured to deploy this repo
2. Zalando PostgreSQL Operator installed on that cluster
3. SchemaHero installed on that cluster

## Usage

### Use the repo as a Template

1. Click "Use Template"
1. A constraint of PGO is that the database name starts with a "team" name. Name the repo as `${teamName}-sourced`. For example, if you are building a funnel for the marketing team, you might name it "marketing-sourced". You could have one for the whole org if it were a smaller project. Up to you - can always refactor later.
1. Renamed `charts/sourced-db` to `charts/${teamName}-sourced` to match the repo name
1. Find and Replace in the project `sourced-db` and replace with `${teamName}-sourced`.

### Day to Day usage

You may want to configure backups and restores via Zalando PostgreSQL Operator. See the docs for that project for info, and configure by changing the config in `charts/${teamName}-sourced/templates/postgresql-sourced.yaml`

Other than that, and scaling changes, you probably won't need to change this chart.
