#
# Licensed to the Apache Software Foundation (ASF) under one
# or more contributor license agreements. See the NOTICE file
# distributed with this work for additional information
# regarding copyright ownership. The ASF licenses this file
# to you under the Apache License, Version 2.0 (the
# "License"); you may not use this file except in compliance
# with the License. You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing,
# software distributed under the License is distributed on an
# "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
# KIND, either express or implied. See the License for the
# specific language governing permissions and limitations
# under the License.
#

stubs: ../v0.16/ThriftTest.thrift
	$(THRIFT) --gen php ../v0.16/ThriftTest.thrift
	$(THRIFT) --gen php:inlined ../v0.16/ThriftTest.thrift
	$(MKDIR_P) gen-php-classmap
	$(THRIFT) -out gen-php-classmap --gen php:classmap ../v0.16/ThriftTest.thrift

php_ext_dir:
	mkdir -p php_ext_dir
	ln -s ../../../lib/php/src/ext/thrift_protocol/modules/thrift_protocol.so php_ext_dir/
	ln -s "$$(php-config --extension-dir)/json.so" php_ext_dir/
	ln -s "$$(php-config --extension-dir)/sockets.so" php_ext_dir/

precross: stubs php_ext_dir

check: stubs php_ext_dir

clean-local:
	$(RM) -r gen-*/
	$(RM) -r php_ext_dir

distdir:
	$(MAKE) $(AM_MAKEFLAGS) distdir-am

dist-hook:
	$(RM) -r $(distdir)/gen-*/
	$(RM) -r $(distdir)/php_ext_dir/

client: stubs php_ext_dir
	php TestClient.php
