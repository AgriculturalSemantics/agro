OBO=http://purl.obolibrary.org/obo
ONT=agro
BASE=$(OBO)/$(ONT)
SRC=$(ONT)-edit.owl
RELEASEDIR=../..
ROBOT= robot
OWLTOOLS= owltools
DOSDPTOOLS = dosdp-tools


all: all_imports all_patterns $(ONT).owl 
# $(ONT).obo # removed obo target for now
test: touch $(ONT).owl
prepare_release: all
	cp $(ONT).owl $(RELEASEDIR) &&\
	mkdir -p $(RELEASEDIR)/imports &&\
	cp imports/*{owl,obo} $(RELEASEDIR)/imports &&\
	git add $(RELEASEDIR)/imports/*{obo,owl} &&\
	(test -f subsets/*owl && cp subsets/*{owl,obo} $(RELEASEDIR)/subsets && git add $(RELEASEDIR)/subsets/* || echo "no subsets") &&\
	echo "Release files are now in $(RELEASEDIR) - now you should commit, push and make a release on github"

touch:
	touch $(SRC)

$(ONT).owl: $(SRC)
	$(ROBOT) merge -i $< reason -r ELK -s true annotate -V $(BASE)/releases/`date +%Y-%m-%d`/$(ONT).owl -o $@
#$(ONT).obo: $(ONT).owl
#	$(ROBOT) convert -i $< -o $(ONT).obo


IMPORTS = envo bfo chebi obi iao pato uo po peco ncbitaxon foodon ro to
IMPORTS_OWL = $(patsubst %, imports/%_import.owl,$(IMPORTS)) 

#$(patsubst %, imports/%_import.obo,$(IMPORTS))

# Make this target to regenerate ALL
all_imports: $(IMPORTS_OWL)

# Use ROBOT, driven entirely by terms lists NOT from source ontology
imports/%_import.owl: mirror/%.owl imports/%_terms.txt
	$(ROBOT) extract -i $< -T imports/$*_terms.txt --method BOT -O  $(BASE)/$@ -o $@
.PRECIOUS: imports/%_import.owl

#imports/%_import.obo: imports/%_import.owl
#	$(OWLTOOLS) $(USECAT) $< -o -f obo $@

#patterns
PATTERNS = eq
PATTERNS_OWL = $(patsubst %, patterns/%.owl,$(PATTERNS))

# Make this target to regenerate ALL patterns
all_patterns: $(PATTERNS_OWL)

patterns/%.owl: patterns/%.tsv
	$(DOSDPTOOLS) --outfile=$@ --obo-prefixes=true --template=patterns/$*.yaml --ontology=imports/pato_import.owl generate --infile=$<
	robot annotate -O "http://purl.obolibrary.org/obo/agro/patterns/$*.owl" -i $@ -o $@
.PRECIOUS: patterns/%.owl

# clone remote ontology locally, perfoming some excision of relations and annotations
mirror/%.owl: $(SRC)
	$(OWLTOOLS) $(OBO)/$*.owl --remove-annotation-assertions -l -s -d --remove-dangling-annotations  -o $@
.PRECIOUS: mirror/%.owl

release: $(ONT).owl 
# $(ONT).obo # add this to the release targets if OBO is desired
	cp $^ $(RELEASEDIR) && cp imports/* $(RELEASEDIR)/imports
