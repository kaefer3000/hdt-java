# HDT-Fuseki

This module sets up a Fuseki SPARQL Endpoint backed up by one or many HDT files.
It does nothing more but supply the HDT libraries to Fuseki.
So as alternative, download Fuseki, edit `fuseki-server` such that it loads the HDT libraries, and start Fuseki with the configuration file (`--config=fuseki_example.ttl`).

## Compiling

`mvn package`

## Using

1. Index your HDT file, if you have not already done so:
```sh
java -cp 'lib/*' org.rdfhdt.hdt.fuseki.HDTGenerateIndex <hdtfilename>
```
2. Put the name of your HDT file in the fuseki configuration (`fuseki_example.ttl`) where it says:
```Turtle
<#graph1> rdfs:label "RDF Graph1 from HDT file" ;
        rdf:type hdt:HDTGraph ;
        hdt:fileName "file1.hdt" ; # <---- Here, obviously

```
3. Start up Fuseki:
```sh
java -cp 'lib/*' org.apache.jena.fuseki.cmd.FusekiCmd --config=fuseki_example.ttl
```
4. Open your Web Browser and go to:
http://localhost:3030
5. Enjoy

On Windows, you may have to adjust the classpath.

## Old stuff:
### Configuring

hdtEndpoint is a fork of Fuseki's fuseki-server. Therefore you can use any of Fuseki's configuration options, such as --port or --gzip

### Loading more than one HDT file

Passing more than one HDT in the command line is not supported. In this case you need to create a Jena assembly specification that defines how to create the dataset. A dataset is defined as a default graph, and zero to many named graphs. A fully-commented example is available at fuseki_example.ttl. As mentioned before, this is a general Fuseki config file, so you can use any of the options of Jena assemblies, for example you can load a few HDT files together with some TDB datasets in the same server.

