These notes are for the EDITORS of agro

For more details on ontology management, please see the OBO tutorial:

 * https://github.com/jamesaoverton/obo-tutorial

## Editors Version

Do you have an ID range in the idranges file (agro-idranges.owl),
in this directory). If not, get one from the head curator. 

The editors version is [agro-edit.obo](agro-edit.obo)

** DO NOT EDIT agro.obo OR agro.owl **

agro.obo is the release version

The editors version can be edited using OBO-Edit. Protege can be used
ONLY IF the version is 5beta-snapshot18 or higher. DO NOT EDIT WITH
PREVIOUS VERSIONS.

## ID Ranges

TODO - these are not set up

These are stored in the file

 * [agro-idranges.owl](agro-idranges.owl)

** ONLY USE IDs WITHIN YOUR RANGE!! **

## Setting ID ranges in OBO-Edit

In the Metadata menu, select the ID manager option. You can set the ID range of any 
profile you create here by clicking on the settings icon (cog wheels) next to the profile 
name. In the window that appears, you can set the ID range by editing the default rule: 
"ID:$sequence(<number of digits>,<minimum of range>,<maximum of range>)$"
Thus, "AGRO:$sequence(8,2000000,2999999)$" will set a range of 8 digit IDs from 200000 
to 2999999.  
 
## Git Quick Guide

TODO add instructions here

## Release Manager notes

You should only attempt to make a release AFTER the edit version is
committed and pushed, and the travis build passes.

to release:

    cd src/ontology
    make

If this looks good type:

    make release

This generates derived files such as agro.owl and agro.obo and places
them in the top level (../..). The versionIRI will be added.

Commit and push these files.

    git commit -a

And type a brief description of the release in the editor window

IMMEDIATELY AFTERWARDS (do *not* make further modifications) go here:

 * https://github.com/AgriculturalSemantics/agro/releases
 * https://github.com/AgriculturalSemantics/agro/releases/new

The value of the "Tag version" field MUST be

    vYYYY-MM-DD

The initial lowercase "v" is REQUIRED. The YYYY-MM-DD *must* match
what is in the versionIRI of the derived agro.owl (data-version in
agro.obo).

Release title should be YYYY-MM-DD, optionally followed by a title (e.g. "january release")

Then click "publish release"

__IMPORTANT__: NO MORE THAN ONE RELEASE PER DAY.

The PURLs are already configured to pull from github. This means that
BOTH ontology purls and versioned ontology purls will resolve to the
correct ontologies. Try it!

 * http://purl.obolibrary.org/obo/agro.owl <-- current ontology PURL
 * http://purl.obolibrary.org/obo/agro/releases/YYYY-MM-DD.owl <-- change to the release you just made

For questions on this contact Chris Mungall or email obo-admin AT obofoundry.org

# Travis Continuous Integration System

Check the build status here: [![Build Status](https://travis-ci.org/AgriculturalSemantics/agro.svg?branch=master)](https://travis-ci.org/agro-ontology/agro)

This replaces Jenkins for this ontology

## General Guidelines

See:
http://wiki.geneontology.org/index.php/Curator_Guide:_General_Conventions
