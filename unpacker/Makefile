# Copyright 2014 The Chromium OS Authors. All rights reserved.
# Use of this source code is governed by a BSD-style license that can be
# found in the LICENSE file.

release: pnacl_for_release vulcanized-polymer
	PNACL_TARGET=Release PACKAGE_DIR=release $(MAKE) -f Makefile.package

debug: pnacl_for_debug vulcanized-polymer
	PNACL_TARGET=Debug PACKAGE_DIR=debug $(MAKE) -f Makefile.package

vulcanized-polymer: third-party/polymer.html
	mkdir vulcanized-polymer
	`npm bin`/vulcanize --inline-scripts third-party/polymer.html | \
		`npm bin`/crisper --html vulcanized-polymer/polymer.html \
		--js vulcanized-polymer/polymer.js

.PHONY: pnacl_for_release
pnacl_for_release:
	CONFIG=Release $(MAKE) -f Makefile.pnacl

.PHONY: pnacl_for_debug
pnacl_for_debug:
	CONFIG=Debug $(MAKE) -f Makefile.pnacl

.PHONY: clean
clean:
	$(MAKE) -f Makefile.pnacl clean
	PNACL_TARGET=Release PACKAGE_DIR=release $(MAKE) -f Makefile.package clean
	PNACL_TARGET=Debug PACKAGE_DIR=debug $(MAKE) -f Makefile.package clean
	rm -rf vulcanized-polymer
	rm -rf pnacl
