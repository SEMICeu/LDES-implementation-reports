# era-dcat-ap-feed
LDES feed for ERA's DCAT-AP metadata

This is a proof-of-concept [RDF-Connect](https://rdf-connect.github.io/) pipeline to produce a [DCAT-AP-Feed](https://semiceu.github.io/LDES-DCAT-AP-feeds/index.html) from the EU Railway Agency's DCAT-AP metadata, available as a queryable named graph at <http://data.europa.eu/949/graph/uat/dcat>.

The [pipeline](pipeline/rdfc-pipeline.ttl) is executed periodically (every 18 hours) as a GitLab CI/CD [pipeline](.gitlab-ci.yml) to:
1. fetch the DCAT-AP data from ERA's servers
2. detect any changes in the described assets
3. write detected changes to the LDES feed

The LDES feed is kept as a collection of static documents which are served using GitLab Pages. The entrypoint to the LDES is: <https://era-europa-eu.gitlab.io/public/interoperable-data-programme/era-ontology/era-dcat-ap-feed/index.trig>

The source implementation is available in GitLab at: <https://gitlab.com/era-europa-eu/public/interoperable-data-programme/era-ontology/era-dcat-ap-feed>

## How it works

The pipeline uses [RDF-Connect](https://rdf-connect.github.io/) processors to:
1. **Fetch** DCAT-AP metadata via SPARQL query from ERA's Virtuoso endpoint
2. **Detect changes** by comparing with previous state stored in LevelDB
3. **Generate ActivityStreams** events (Create, Update, Delete) for changed resources
4. **Bucketize** events using time-based fragmentation (monthly buckets)
5. **Write** to disk as static LDES fragments served via GitLab Pages

## Setup

### Prerequisites
- Node.js 22 or higher
- npm

### Local development

```bash
cd pipeline
npm install
npx @rdfc/js-runner rdfc-pipeline.ttl
```


## Architecture

```
[ERA Virtuoso SPARQL Endpoint]
         ↓
   [HttpFetch Processor]
         ↓
  [DumpsToFeed Processor] → [LevelDB State]
         ↓
    [Sdsify Processor]
         ↓
   [Bucketize Processor] → [Feed State JSON]
         ↓
 [LdesDiskWriter Processor]
         ↓
     [docs/ directory] → [GitLab Pages]
```

## Additional Resources

- [GitLab CI/CD Documentation](https://docs.gitlab.com/ee/ci/)
- [GitLab Pages Documentation](https://docs.gitlab.com/ee/user/project/pages/)
- [Pipeline Schedules Documentation](https://docs.gitlab.com/ee/ci/pipelines/schedules.html)
- [RDF-Connect Documentation](https://rdf-connect.github.io/)
- [DCAT-AP Feed Specification](https://semiceu.github.io/LDES-DCAT-AP-feeds/)

## Support

For issues specific to:

- **RDF-Connect pipeline**: Check [RDF-Connect GitHub](https://github.com/rdf-connect)
- **ERA KG metadata**: Contact ERA technical support

