# KNOWNTARGETS will not be passed along to CoqMakefile
KNOWNTARGETS := Makefile.coq
# KNOWNFILES will not get implicit targets from the final rule, and so
# depending on them won't invoke the submake
# Warning: These files get declared as PHONY, so any targets depending
# on them always get rebuilt
KNOWNFILES   := Makefile _CoqProject

.DEFAULT_GOAL := invoke-coqmakefile

Makefile.coq: Makefile _CoqProject
	$(COQBIN)coq_makefile -f _CoqProject -o Makefile.coq

invoke-coqmakefile: Makefile.coq
	$(MAKE) --no-print-directory -f Makefile.coq $(filter-out $(KNOWNTARGETS),$(MAKECMDGOALS))

.PHONY: invoke-coqmakefile $(KNOWNFILES)

####################################################################
##                      Your targets here                         ##
####################################################################

# This should be the last rule, to handle any targets not declared above
%: invoke-coqmakefile
	@true

clean:
# remove all coq generated files from all subdirectories
	find . -name "*.vo" -type f -delete
	find . -name "*.glob" -type f -delete
	find . -name "*.v.d" -type f -delete
	find . -name "*.vo.d" -type f -delete
	find . -name "*.vo.aux" -type f -delete
	find . -name "*.vok" -type f -delete
	find . -name "*.vos" -type f -delete
	find . -name "*.aux" -type f -delete