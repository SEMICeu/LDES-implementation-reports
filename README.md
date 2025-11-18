# LDES-implementation-reports
This repository contains all the implementation reports SEMIC and the community have made to support the usage of the LDES specification.
The intention of these reports is to support specific use cases for LDES allowing the community to learn from this, allowing for easy LDES adoption and to solve edge cases for LDES.
The following Implementation reports exist:

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
</table> 
If you want to share your Report feel free to open a <a href="https://github.com/SEMICeu/LDES-implementation-reports/pulls">pull request</a>, an <a href="https://github.com/SEMICeu/LDES-implementation-reports/issues">issue</a> or contact us at digit-semic-team@ec.europa.eu .
