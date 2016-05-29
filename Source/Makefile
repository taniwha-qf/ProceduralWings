KSPDIR		:= ${HOME}/ksp/KSP_linux
MANAGED		:= ${KSPDIR}/KSP_Data/Managed
GAMEDATA	:= ${KSPDIR}/GameData
pWingsGAMEDATA  := ${GAMEDATA}/ProceduralDynamics
PLUGINDIR	:= ${pWingsGAMEDATA}/Plugins

TARGETS		:= pWings.dll

pWings_FILES := \
	FlapToggler.cs \
	StaticWingGlobals.cs \
	WingManipulator.cs \
	WingTankConfiguration.cs \
	WingTankResource.cs \
	$e

RESGEN2		:= resgen2
GMCS		:= mcs
GMCSFLAGS	:= -optimize -warnaserror
GIT			:= git
TAR			:= tar
ZIP			:= zip

all: ${TARGETS}
#all: version ${TARGETS}

.PHONY: version
version:
	@./git-version.sh

info:
	@echo "pWings Build Information"
	@echo "    resgen2:    ${RESGEN2}"
	@echo "    gmcs:       ${GMCS}"
	@echo "    gmcs flags: ${GMCSFLAGS}"
	@echo "    git:        ${GIT}"
	@echo "    tar:        ${TAR}"
	@echo "    zip:        ${ZIP}"
	@echo "    KSP Data:   ${KSPDIR}"

pWings.dll: ${pWings_FILES}
	${GMCS} ${GMCSFLAGS} -t:library -lib:${MANAGED} \
		-r:Assembly-CSharp,Assembly-CSharp-firstpass \
		-r:UnityEngine,UnityEngine.UI \
		-r:KSPUtil \
		-out:$@ $^

clean:
	rm -f ${TARGETS}

install: all
	mkdir -p ${PLUGINDIR}
	cp ${TARGETS} ${PLUGINDIR}

.PHONY: all clean install
