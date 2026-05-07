<div style="text-align: center;">
<img src="https://semiceu.github.io/style-guide/_/img/semic-logo.png" alt="SEMIC Logo" width="200" style="vertical-align: middle;">
</div>

# The Linked Data Event Streams (LDES) implementation reports

This repository contains implementation reports that SEMIC and the community have made to support the use of the [LDES specification](https://w3id.org/ldes/specification).

The intention of these reports is to document specific LDES use cases, help the community learn from them, support easy LDES adoption, and address LDES edge cases.
The following implementation reports exist:

<table>  
    <tr>      
      <th>Implementation Report</th>      
      <th>Description</th>       
    </tr>
    <tr>  
      <td>  
         <a href="https://semiceu.github.io/LDES-DCAT-AP-feeds/index.html">LDES DCAT-AP feeds</a>
      </td>      
      <td> 
        Publishing a full data dump over and over again will delegate change detection -- a fault prone process -- to data consumers. With DCAT-AP Feeds we propose that DCAT-AP catalog maintainers publish an event source API that can help to replicate the catalog towards a harvester, and always keep it in-sync in the way that is intended by the publisher. Therefore, this spec describes how to publish your DCAT-AP entity changes using the Activity Streams vocabulary and LDES. It also provides a specification for harvesters to provide transparency into their harvesting progress.
      </td> 
    </tr>
	<tr>
	  <td>
        <a href="https://semiceu.github.io/LDES-implementation-reports/cultural-heritage-feeds/">Cultural Heritage Event Streams with LDES</a>
	  </td>
	  <td>
	   This implementation report specifies how cultural-heritage datasets (e.g., artworks, museum objects, vocabularies) can be exposed as incremental event streams using LDES and ActivityStreams. It covers the stream design, versioning, retention policies, activity types (Create/Update/Delete), publisher/consumer real-world instances, and conformance requirements.
	  </td>
	</tr>
	<tr>
	  <td>
        <a href="https://semiceu.github.io/LDES-implementation-reports/era-dcat-ap-feed/">ERA DCAT-AP Feed</a>
	  </td>
	  <td>
	   This implementation report is a proof-of-concept RDF-Connect pipeline that generates a DCAT-AP Feed from the European Union Railway Agency's DCAT-AP metadata. It covers change detection, ActivityStreams event generation, time-based bucketization, and static feed publication via GitLab Pages.
	  </td>
	</tr>
</table>

If you want to share your report or implementation, feel free to open a <a href="https://github.com/SEMICeu/LDES-implementation-reports/pulls">pull request</a>, file an <a href="https://github.com/SEMICeu/LDES-implementation-reports/issues">issue</a>, or contact us at digit-semic-team@ec.europa.eu.
