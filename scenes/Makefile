.PHONY : all

#n.b. the '-y' sets autoexec scripts to 'on' so that driver expressions will work
UNAME_S := $(shell uname -s)
ifeq ($(UNAME_S),Darwin)
	BLENDER = /Applications/Blender.app/Contents/MacOS/blender -y
else ifeq ($(UNAME_S),Linux)
	BLENDER = ../../../blender-4.2.1-linux-x64/blender -y
else
	BLENDER = blender
endif

EXPORT_MESHES=export-meshes.py
EXPORT_WALKMESHES=export-walkmeshes.py
EXPORT_SCENE=export-scene.py

DIST=../dist

all:\
	$(DIST)/phone-bank.pnct \
	$(DIST)/phone-bank.w \
	$(DIST)/phone-bank.scene \

/Applications/Blender.app/Contents/MacOS/blender --background --python export-meshes.py -- myscene.blend:Collection ../dist/myscene.pnct
/Applications/Blender.app/Contents/MacOS/blender --background --python export-scene.py -- myscene.blend:Collection ../dist/myscene.scene
/Applications/Blender.app/Contents/MacOS/blender --background --python export-walkmeshes.py -- myscene.blend:Walkmeshes ../dist/myscene.w

$(DIST)/phone-bank.scene : phone-bank.blend $(EXPORT_SCENE)
	$(BLENDER) --background --python $(EXPORT_SCENE) -- '$<':Platforms '$@'

$(DIST)/phone-bank.w : phone-bank.blend $(EXPORT_WALKMESHES)
	$(BLENDER) --background --python $(EXPORT_WALKMESHES) -- '$<':WalkMeshes '$@'
