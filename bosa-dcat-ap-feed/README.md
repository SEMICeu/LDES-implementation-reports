# bosa-dcat-ap-feed
DCAT-AP Feed for the Belgian federal open data catalog

This implementation report documents two complementary aspects of the [DCAT-AP-Feeds specification](https://semiceu.github.io/LDES-DCAT-AP-feeds/index.html):

1. **Publishing**: how the Federal Public Service for Policy and Support (BOSA) Belgium publishes the Belgian federal DCAT-AP catalog as a [DCAT-AP-Feed](https://semiceu.github.io/LDES-DCAT-AP-feeds/index.html) using an [RDF-Connect](https://rdf-connect.github.io/) pipeline.
2. **Consuming**: how the EU Publications Office (OP) can automatically ingest DCAT-AP-feeds into their [Piveau](https://doc.piveau.eu/general/introduction/) catalog management platform using a new Piveau Consus plugin.

## Publishing: the belgium-dcat-ap-feed pipeline

The [pipeline](https://github.com/rdf-connect/belgium-dcat-ap-feed/blob/master/pipeline/github-pipeline.ttl) reads the Belgian DCAT-AP catalog from a compressed RDF/XML dump (`all/datagovbe_edp.xml.gz`), detects changes against a persisted LevelDB state, generates ActivityStreams events, and writes the resulting LDES feed as a set of static files.

The feed is published in two contexts:
- **BOSA premises**: live deployment at <https://mqa.data.gov.be/ldes> (coordination ongoing to align with the latest pipeline version).
- **GitHub Pages**: automatically published via a GitHub Action at <https://rdf-connect.github.io/belgium-dcat-ap-feed/index.trig>.

The source implementation is available at: <https://github.com/rdf-connect/belgium-dcat-ap-feed>

## How the publishing pipeline works

The pipeline uses [RDF-Connect](https://rdf-connect.github.io/) processors to:
1. **Read** the compressed RDF/XML catalog dump (`rdfc:GlobRead` + `rdfc:GunzipFile`)
2. **Detect changes** by comparing with previous state stored in LevelDB (`rdfc:DumpsToFeed`)
3. **Annotate** stream members with SDS metadata (`rdfc:Sdsify`)
4. **Bucketize** events using time-based fragmentation (`rdfc:Bucketize`)
5. **Write** to disk as static LDES fragments (`rdfc:LdesDiskWriter`)

## Publishing setup

### Prerequisites
- Node.js 22 or higher
- npm

### Local development

```bash
cd pipeline
npm install
npx rdfc github-pipeline.ttl
```

## Publishing architecture

```
[Belgian DCAT-AP RDF/XML dump: all/datagovbe_edp.xml.gz]
         ↓
      [GlobRead]
         ↓
      [GunzipFile]
         ↓
 [DumpsToFeed Processor] → [LevelDB State]
         ↓
     [Sdsify Processor]
         ↓
 [Bucketize Processor] → [Feed State JSON]
         ↓
  [LdesDiskWriter Processor]
         ↓
 [docs/ directory] → [GitHub Pages / BOSA deployment]
```

## Consuming: the piveau-consus-importing-ldes plugin

A new [Piveau Consus](https://doc.piveau.eu/consus/) segment plugin was developed to allow the OP to automatically ingest DCAT-AP-feeds into Piveau. The plugin starts an LDES client, streams each RDF entity from the feed, converts the quads to N-Quads, and forwards them to the next segment in the Consus pipeline chain.

The plugin has been validated in a controlled testing environment and is being coordinated for testing at the OP premises.

The source implementation is available at: <https://github.com/rdf-connect/piveau-consus-importing-ldes>

## Consuming architecture

```
Consus Control Plane
        ↓
    [Descriptor with LDES config]
        ↓
   HTTP PUT to /pipe
        ↓
   HTTPConsumer (listens)
        ↓
   Piveau Processor
        ├─ Connect to LDES endpoint
        ├─ Stream RDF entities
        └─ Convert to N-Quads
        ↓
   Send to next Consus segment
        ↓
   [Next segment processes metadata]
```

## Additional Resources

- [Source repository: belgium-dcat-ap-feed](https://github.com/rdf-connect/belgium-dcat-ap-feed)
- [Source repository: piveau-consus-importing-ldes](https://github.com/rdf-connect/piveau-consus-importing-ldes)
- [RDF-Connect Documentation](https://rdf-connect.github.io/)
- [Piveau Documentation](https://doc.piveau.eu/general/introduction/)
- [DCAT-AP Feed Specification](https://semiceu.github.io/LDES-DCAT-AP-feeds/)
- [Full implementation report](https://semiceu.github.io/LDES-implementation-reports/bosa-dcat-ap-feed/)
