DOREMUS Music Embeddings
========================

Vectors of music entities.

This folder is intended to hosts graph embedding for different concepts belonging to music knowledge, from instruments to works to playlist.

The embeddings have been computed on top of the [DOREMUS knowledge base](http://data.doremus.org), which contains data about over 148.000 works, 26.000 artists, 5.000 concerts, apart of a interesting set of [controlled vocabularies](http://data.doremus.org/vocabularies).


## Format

For each different concept, we provide 3 different files:
- `*.emb.u` **URI file**, that contains the URIs of involved resources;
- `*.emb.l` **Label file**, with the label in English (if present) or in any available language;
- `*.emb.v` **Vector file**, which contains the embeddings as space-separated floats in the interval (-1, +1).

For more complex concepts like artists and expressions, we provide also:
- `*.emb.h` **Header file**, that contains the ordered list of involved sub-features with the relative number of related dimensions (i.e. in the `artist.emb.h`, the first 2 dimensions refer to the period).

Each line of those file represents a single entity, as the parallel line in the other files.
Considering musical keys as example, line 3 in the [URI file](https://github.com/DOREMUS-ANR/recommender/blob/master/embeddings/key.emb.u#L3) identifies an entity whose label is at line 3 in [label file](https://github.com/DOREMUS-ANR/recommender/blob/master/embeddings/key.emb.l#L3) and whose embeddings are at line 3 in [vector file](https://github.com/DOREMUS-ANR/recommender/blob/master/embeddings/key.emb.v#L3)

## Contents

|name   | n. entities |dimensions| description|source |
|-------|----------------|------------|--------|--------|
|key    | 30             |100| Musical keys (e.g. _C major_) | [Key vocabulary](http://data.doremus.org/vocabulary/key/) |
|genre | 530 |80| Musical genres (e.g. _symphony_)| 6 vocabularies: [IAML](http://data.doremus.org/vocabulary/iaml/genre/), [Redomi](http://data.doremus.org/vocabulary/redomi/genre/), [Itema3](http://data.doremus.org/vocabulary/itema3/genre/), [Musical Doc of Itema3](http://data.doremus.org/vocabulary/itema3/genre/musdoc/), [Diabolo](http://data.doremus.org/vocabulary/diabolo/genre/), [Rameau](http://data.bnf.fr/ark:/12148/) |
|mop|3.278|80|Medium of performance (instruments, voices, ensambles)|5 vocabularies:       [MIMO](http://www.mimo-db.eu/InstrumentsKeywords), [IAML](http://data.doremus.org/vocabulary/iaml/mop/), [Redomi](http://data.doremus.org/vocabulary/redomi/mop/), [Itema3](http://data.doremus.org/vocabulary/itema3/mop/),  [Diabolo](http://data.doremus.org/vocabulary/diabolo/mop/)|
|artist|24.423|14|Composers, performers, conductors, groups|SPARQL query to [endpoint](http://data.doremus.org/sparql)|
|expression|148.177|13|Musical works (i.e. _Moonlight Sonata_, _Bolero_, _Traviata_)|SPARQL query to [endpoint](http://data.doremus.org/sparql)|

## Embedding strategy

Details will be published soon :)

As an anticipation:
- We use _node2vec_ [\[1\]](#node2vec), in the implementation of [entity2vec](https://github.com/MultimediaSemantics/entity2vec/blob/master/entity2vec/node2vec.py);
- We apply an L2 normalisation.


<span id="node2vec">[1]<span> _node2vec: Scalable Feature Learning for Networks_. A. Grover, J. Leskovec. ACM SIGKDD International Conference on Knowledge Discovery and Data Mining (KDD), 2016.
