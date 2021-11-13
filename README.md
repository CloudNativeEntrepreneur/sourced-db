# sourced-db

Use this repo as a template and import it into your JX cluster to deploy a PSQL based Sourced Event Store via Zalando PostgreSQL Operator, and then configures the database for use with sourced by creating the "Event" table with SchemaHero.

## Prerequisites

1. A Kubernetes cluster with Jenkins X for pipelines to work
2. Zalando PostgreSQL Operator installed on that cluster
3. SchemaHero installed on that cluster

A K-in-D cluster configured with these tools, except JX, can be found [here](https://github.com/CloudNativeEntrepreneur/local-dev-cluster) for running locally. I usually put `Makefile`s with each project in a [meta repo](https://github.com/mateodelnorte/meta) so I can deploy all local copies at once.

## Usage

### Use the repo as a Template

1. Click "Use Template"
1. A constraint of PGO is that the database name starts with a "team" name. Name the repo as `${teamName}-sourced`. For example, if you are building a funnel for the marketing team, you might name it "marketing-sourced". You could have one for the whole org if it were a smaller project. Up to you - can always refactor later.
1. Renamed `charts/sourced-db` to `charts/${teamName}-sourced` to match the repo name
1. Find and Replace in the project `sourced-db` and replace with `${teamName}-sourced`.

### Import into JX

1. Import the new repo into your JX cluster – within the cloned project's directory 

```
jx project import . --no-draft
```

This will set up the following Pipelines:

#### Pull Request Pipelines

Lint's the Helm chart

#### Release Pipeline

Releases the chart to your chart repository (configured via JX) as a versioned artifact, and promote to configured environments. In JX the promotion happens via a Pull Request to your gitops repo with the new version number of the chart.

### Day to Day usage

You may want to configure backups and restores via Zalando PostgreSQL Operator. See the docs for that project for info, and configure by changing the config in `charts/${teamName}-sourced/templates/postgresql-sourced.yaml`

Other than that, and scaling changes, you probably won't need to change this chart.
