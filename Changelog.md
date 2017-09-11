## 3.4.10

### Fixes
* Restore backward compatibility to session handler. Thanks @koleo!
* Fix increment using floating point values.
* Use correct C client bits for various Ubuntu builds.
* Update to 4.0.7 version of C client.
* Fix seg fault when configuration has "shm" option.
* Update composer to reflect PHP7 support

## 3.4.9

### Features
* Support PHP 7

## 3.4.8

### Features
* Added Aersospike::operateOrdered API which takes the same parameters as Aerospike::operate but returns an indexed array of results, rather than a key-value associative array. _CLIENT-652_
* Added support for Geospatial index using GeoJSON. _CLIENT-542_ **Requires server >= 3.7.0**

### Fixes
* Use session.gc\_maxlifetime for the session timeout (was session.cache\_expire). _CLIENT-705_

## 3.4.7

### Features
* Upgraded to C client [4.0.2](http://www.aerospike.com/download/client/c/notes.html#4.0.2).
* Added [list operations](https://github.com/citrusleaf/aerospike-client-php/blob/master/doc/apiref_kv.md) as standalone methods. _CLIENT-561_  **Requires server >= 3.7.0**
* Added list operators for operate(). _CLIENT-646_  **Requires server >= 3.7.0**
* [isConnected()](https://github.com/aerospike/aerospike-client-php5/tree/master/doc/aerospike_isconnected.md) now testing the client’s connections to the nodes. _CLIENT-624_
* Allow the Aerospike class to be extendable. _CLIENT-648_
* Added a [compression_threshold](https://github.com/aerospike/aerospike-client-php5/blob/master/doc/aerospike_construct.md#parameters) client config parameter. _CLIENT-627_
* Added OPT\_SCAN\_INCLUDELDT option for [scan()](https://github.com/aerospike/aerospike-client-php5/tree/master/doc/aerospike_scan.md). _CLIENT-610_

## 3.4.6

### Features
* Secondary-index record UDFs using [queryApply()](https://github.com/aerospike/aerospike-client-php5/tree/master/doc/aerospike_queryapply.md). _CLIENT-299_
* Enable shared-memory cluster tending through the [constructor](https://github.com/aerospike/aerospike-client-php5/tree/master/doc/aerospike_construct.md) config. _CLIENT-595_
* Added the config params max\_threads, thread\_pool\_size. _CLIENT-296_
* Removed the deprecated method createIndex(). Use [addIndex()](https://github.com/aerospike/aerospike-client-php5/tree/master/doc/aerospike_addindex.md). _CLIENT-585_
* Cleaned up the client [documentation](https://github.com/aerospike/aerospike-client-php5/tree/master/doc/README.md). Thanks @sergeyklay for your help.
* Issues #72, #73, #74. Thanks @sergeyklay again!

### Fixes
* Fixed shared-memory cluster tending by generating a unique shm key per-hostname. _CLIENT-9_
* Fixed issue #62. _CLIENT-596_


## 3.4.5

### Fixes
* Fixed a memory leak in batch read operations. _CLIENT-568_


## 3.4.4

### Features
* Added explicit control over the [batch protocol](http://www.aerospike.com/docs/guide/batch.html#server-configuration) through a `php.ini` config variable `aerospike.use_batch_direct`, or constructor config parameter `Aerospike::USE_BATCH_DIRECT`. The default value is 0 (i.e. _batch-index_) for servers with **version >=  3.6.0**. _CLIENT-567_
* Added support for Ubuntu 15. Thanks @lwille.


## 3.4.3

### Features
* Upgraded to C client [3.1.24](http://www.aerospike.com/download/client/c/notes.html#3.1.24).
* A new **backward incompatible** format for the data returned by [existsMany()](https://github.com/aerospike/aerospike-client-php5/blob/master/doc/aerospike_existsmany.md), as mentioned in the [release notes for 3.4.0](https://github.com/aerospike/aerospike-client-php5/releases/tag/3.4.0). The underlying C client interfaces with a new API for batch reads called [batch index](https://www.aerospike.com/docs/guide/batch.html), which is implemented in server versions **>= 3.6.0**. Since batch reads can now target multiple namespaces, the old format is no longer appropriate. Instead, an indexed array is returned in an order corresponding to the array of keys passed as the argument to existsMany(). _CLIENT-28_
* Allow TTL to be set with the write methods [increment()](https://github.com/aerospike/aerospike-client-php5/blob/master/doc/aerospike_increment.md), [append()](https://github.com/aerospike/aerospike-client-php5/blob/master/doc/aerospike_append.md), [prepend()](https://github.com/aerospike/aerospike-client-php5/blob/master/doc/aerospike_prepend.md), [operate()](https://github.com/aerospike/aerospike-client-php5/blob/master/doc/aerospike_operate.md), [removeBin()](https://github.com/aerospike/aerospike-client-php5/blob/master/doc/aerospike_removebin.md) using  [OPT\_TTL](https://github.com/aerospike/aerospike-client-php5/blob/master/doc/aerospike.md). _CLIENT-510_
* Updated the methods of class [LList](https://github.com/aerospike/aerospike-client-php5/blob/master/doc/aerospike_llist.md). Added filters to find, findFirst, findLast, findRange.
* Expanded the examples for LList with [integer](https://github.com/aerospike/aerospike-client-php5/blob/master/examples/ldt/integer_elements.php), [string](https://github.com/aerospike/aerospike-client-php5/blob/master/examples/ldt/string_elements.php), and [map](https://github.com/aerospike/aerospike-client-php5/blob/master/examples/ldt/map_elements.php) elements.
* Removed deprecated LDT classes (LMap, LSet, LStack) and methods.
* Fixed the documentation for the Enterprise Edition [security methods](https://github.com/aerospike/aerospike-client-php5/blob/master/doc/apiref_security.md).
* Fixed the installer to place the Lua system files in `/usr/local/aerospike/lua` by default. Path override can be done by setting the environment variables `LUA_SYSPATH`, `LUA_USRPATH` before invoking [`build.sh`](https://github.com/aerospike/aerospike-client-php5/blob/master/src/aerospike/build.sh).
* Travis-CI cleanup.

### Fixes
* Fixed bug where malformed keys triggered a segfault in getMany(). _CLIENT-140_ / _AER-4342_
* Fixed the client to cast PHP floats to and from as_double. _CLIENT-225_
* Fixed issue #53 - correct configuration inheritance. _CLIENT-88_
* Fixed issue #54 - return the correct error status for empty put(). _CLIENT-69_
* Fixed issue #57 - incorrectly identifying RHEL. Thanks, @npenteado :+1:


## 3.4.2

### Features
* Upgraded to C client [3.1.22](http://www.aerospike.com/download/client/c/notes.html#3.1.22). _AER-3909_
* A new **backward incompatible** format for the data returned by [getMany()](https://github.com/aerospike/aerospike-client-php5/blob/master/doc/aerospike_getmany.md), as mentioned in the [release notes for 3.4.0](https://github.com/aerospike/aerospike-client-php5/releases/tag/3.4.0). The underlying C client interfaces with a new API for batch reads called [batch index](https://www.aerospike.com/docs/guide/batch.html), which is implemented in server versions **>= 3.6.0**. Since batch reads can now target multiple namespaces, the old format is no longer appropriate. Instead, an indexed array is returned in an order corresponding to the array of keys passed as the argument to getMany().  _AER-4064_
* Tests and API documentation updated. Thanks to @rmondragon for his help.


## 3.4.1

### Features
* Added [Security Methods](https://github.com/aerospike/aerospike-client-php5/blob/master/doc/apiref_security.md) for Aerospike [Enterprise Edition](http://www.aerospike.com/docs/amc/user_guide/enterprise/). _AER-3475_
* Added support for Debian 8.
* Clarified configuration steps for the activating the extension with web servers, such as Nginx and Apache. Thanks Mickael Hassine.

### Fixes
* Fixed case where [scan aggregations](https://github.com/aerospike/aerospike-client-php5/blob/master/doc/aerospike_aggregate.md) caused the scan jobs to hang. _AER-3813_


## 3.4.0

## Welcome to the 3.4 release branch

This is the first release along the 3.4 branch. The astute observation of @arussellsaw in issue #48 has initiated a bit of realignment with other language clients (for example, [aerospike/aerospike-client-python](https://github.com/aerospike/aerospike-client-python)) with regards to multiple results, such as produced by [aggregate()](https://github.com/aerospike/aerospike-client-php5/blob/master/doc/aerospike_aggregate.md). In subsequent releases following **3.4.0**, the batch-read methods getMany() and existsMany() will change as well.

* In aggregate(), the result will no longer be wrapped in a pseudo-record format. Gone are the array keys _metadata_ and _key_, as they are meaningless. An aggregation returns transformed and reduced results which no longer are the same as the source data, the records matched by the secondary index query. Further, we are pulling the results up out of the _bin_ array key. If your Lua produces a single result map you will get back an array with that maps' fields as array keys. If your reducer returns multiple results, you will get an array of arrays, each of them key-value pairs. The example at [examples/query_examples/aggregate.php](https://github.com/aerospike/aerospike-client-php5/blob/master/examples/query_examples/aggregate.php) shows both types of aggregation. After installing the new version of the client run `cd examples/query_examples/ && php aggregate.php -a -c`.
* An upcoming change to getMany() and existsMany() (in a release > 3.4.0) will modify the returned result to an indexed array of records. In both cases, it will be equivalent to running get() or exists() in a loop and aggregating the returned records one-by-one into a PHP array. The batch-read methods will return a plural of the single equivalent methods. For example, getMany() on keys 1,2,3 in namespace _test_ and set _demo_ will return an array of what you expect from calling get() on each of those keys in a loop.

I hope you will see the benefit in these changes, and that if you use UDFs and batch-read methods the integration work on your end is minimal.

### Features
* Support for `null` as valid argument to a UDF. _AER-4003_
* Prefer to always download the appropriate C client ahead of building the extension. _AER-4001_

### Fixes
* Fixed issue #48 - a new **backward incompatible** format for data returned by aggregate(). _AER-3948_ Thanks @arussellsaw.


## 3.3.16

### Features
* Added an optional ttl argument to Aerospike::OPERATOR_TOUCH in [operate()](https://github.com/aerospike/aerospike-client-php5/blob/master/doc/aerospike_operate.md). _AER-3566_
* Copy registered modules to user path in [register()](https://github.com/aerospike/aerospike-client-php5/blob/master/doc/aerospike_register.md). _AER-3627_
* [LList](https://github.com/aerospike/aerospike-client-php5/blob/master/doc/aerospike_llist.md) changes:  added isValid(), findRange(), setPageSize(). Modified scan() in a *compatibility breaking* way.

### Fixes
* Fixed issue #46 - reusing keys from scan/query. _AER-3748_
* Fixed issue #44 - accept numeric strings for increment(). _AER-3812_
* Fixed bug preventing a default value of 'user' for serializer. _AER-3527_
* Partially fixed issue #43 - bigger static allocation for as\_val. _AER-3708_
* Expanded checks for libcrypto. Thanks @jumping


## 3.3.15

### Features
* Upgraded to C client [3.1.16](http://www.aerospike.com/download/client/c/notes.html#3.1.16).
* Added support for [indexing complex types](https://github.com/aerospike/aerospike-client-php5/blob/master/doc/aerospike_addindex.md) (lists, map) and for [querying](https://github.com/aerospike/aerospike-client-php5/blob/master/doc/aerospike_query.md) against those secondary indexes using the [contains](https://github.com/aerospike/aerospike-client-php5/blob/master/doc/aerospike_predicatecontains.md) and [range](https://github.com/aerospike/aerospike-client-php5/blob/master/doc/aerospike_predicaterange.md) predicates. Those will become fully available with a near-future release of Aerospike server.  _AER-3425_,  _AER-3434_

### Fixes
* Fixed to allow OPT\_SERIALIZER to be set to SERIALIZER\_USER in an apply() call. _AER-3528_


## 3.3.14

### Features
* Fixed issue #41 - Implemented authentication in support of the Enterprise edition of Aerospike. _AER-3551_
* Slight clean-up of the doc and examples.

### Fixes
* Making sure the bin-name length limit is 14, not 13 :wink: _AER-3571_


## 3.3.13

### Features
* Implemented [configuration globals](https://github.com/aerospike/aerospike-client-php5/blob/master/doc/aerospike_construct.md#parameters) through the constructor.
* Added support for namespaces with a null set in index creation, scan() and query().
* [Aerospike\Bytes](https://github.com/aerospike/aerospike-client-php5/blob/master/src/Bytes.php) wrapper added, and doc updated regarding the [handling of binary-strings](https://github.com/aerospike/aerospike-client-php5/blob/master/doc/README.md#handling-unsupported-types) that may contain the null-byte (**\0**).
* Large Ordered List:
 - Deprecated: get_capacity(),set_capacity() methods of the LDT parent class.
 - Added the methods: find_first, find_last, find_range, exists, config, setPageSize. **Requires server >= 3.5.8**

### Fixes
* Fixed issue #33 fixed for non-ZTS PHP (still in progress for the other case).


## 3.3.12

* Upgraded to C client [3.1.11](http://www.aerospike.com/download/client/c/notes.html#3.1.11).
* Fixed issue #35.


## 3.3.11

* Upgraded to C client 3.1.8
* Fixed issue #30. The [increment()](https://github.com/aerospike/aerospike-client-php5/blob/master/doc/aerospike_increment.md) method is **modified** to reflect the behavior of the C client (aka _upsert_)
* Support for generation policies in [remove()](https://github.com/aerospike/aerospike-client-php5/blob/master/doc/aerospike_remove.md). **Requires server version >= 3.5.3**


## 3.3.10

* Upgraded to C client 3.1.2
* Removed dependency on Lua as a prerequisite
* Added [Aerospike::getKeyDigest()](https://github.com/aerospike/aerospike-client-php5/blob/master/doc/aerospike_getkeydigest.md)
* Fixed issue #16
* Fixed issue #22
* Fixed issue #9
* Upgrades to [LList](https://github.com/aerospike/aerospike-client-php5/blob/master/doc/aerospike_llist.md): `update()`, `update_all()`, UDF filter arguments for `scan()`, `llist.filter` wrapped into `scan()`,  `removeRange()` implements `llist.remove_range`, `llist.remove_all` implemented as `removeMany()`
* [Deprecation notice](https://github.com/aerospike/aerospike-client-php5/blob/master/doc/aerospike_ldt.md) for LMap, LSet, LStack
* Enhanced the [docs](https://github.com/aerospike/aerospike-client-php5/blob/master/doc/README.md) and [examples](https://github.com/aerospike/aerospike-client-php5/tree/master/examples)


## 3.3.9

* Fixes a memory leak in the increment() method.


## 3.3.8

* Fixed issue #11


## 3.3.7

* Fixed issue #17


## 3.3.6

* Documentation for bin operations clarified
* Removed mention of deprecated status ERR_BIN_TYPE from the docs
* Added a [multi-process performance testing script](https://github.com/aerospike/aerospike-client-php5/tree/master/examples/performance)
* Fixed issue #14


## 3.3.5

* Upgraded to C client 3.0.94
* Faster close() resulting in faster tests and session handling
* Fixed script that fetches the C client to work with minimal CentOS 7
* Added support for queries without a predicate.


## 3.3.4

* Fixed a bug with default serialization of unsupported types (boolean, float, etc)
* Fixed a bug where scans did not respect OPT_POLICY_KEY
* Added support for Linux Mint


## 3.3.3

* [Per-transaction consistency guarantees](http://www.aerospike.com/docs/client/c/usage/consistency.html)  OPT_POLICY_COMMIT_LEVEL, OPT_POLICY_REPLICA, OPT_POLICY_CONSISTENCY
* Fixed issue #8
* createIndex(), register() now wait till operation is confirmed
* [LDT examples](https://github.com/aerospike/aerospike-client-php5/tree/master/examples/ldt)


## 3.3.2

* [Aerospike session handler](https://github.com/aerospike/aerospike-client-php5/blob/master/doc/aerospike_sessions.md) for PHP sessions.
* Fixed issue #7


## 3.3.1

* Shared-memory cluster tending.  Load is reduced when multiple PHP processes can share the data from a single tending thread.
* Upgraded to release 3.0.90 of the C client
* Reorganized the unit tests to run faster.
* Removed deprecated status codes
 * Aerospike::ERR - now it’s just Aerospike::ERR_CLIENT
 * ERR\_RECORD
 * ERR\_THROTTLED
 * ERR\_SCAN
 * ERR\_UDF\_FILE\_NOT\_FOUND


## 3.3.0

* Batch operations - getMany() and existsMany()
* Multi-op record operations - operate()
* Compilation error fixed for OS X >= 10.9 (also tested on 10.10 "Yosemite")
* Upgraded to release 3.0.86 of the C client


## 3.2.1

* Examples cleaned up
* Fixed issue #4


## 3.2.0

* Admin methods createIndex() and dropIndex()
* Info methods info(), infoMany(), getNodes()
* Write methods support OPT_POLICY_GEN.


## 3.1.1

* Starting version >= 3.1.0: **format change for returned records** - now all records come back as an array with keys ('key','meta','bins').
* Set the C Client version to 3.0.84 (latest stable).
* Methods get(), put() fixed to support OPT_POLICY_KEY.
* Fixed apply() for case when the $returned parameter is not set.
* Fixes to the .phpt tests.


## 3.1.0

* **format change for returned records** - now all records come back as an array with keys ('key','meta','bins').
* OPT_POLICY_KEY added for read and write methods
* Support for [Large Data Types](http://www.aerospike.com/docs/guide/ldt.html) with a PHP class library \Aerospike\LDT
* [stream UDF](http://www.aerospike.com/docs/guide/stream_udf.html) methods scanApply() and aggregate()
* UDF module admin methods register(), deregister(), listRegistered(), getRegistered()
* background scan method scanApply() with OPT_SCAN_* policies to control its behavior and scanInfo() helper.
* standardized (and therefore modified) parameter lists for stream methods - query(), scan(), aggregate(), scanApply()
* Fixes for FPM and APXS SAPIs
* Extension is now built with `src/aerospike/build.sh`
* Composer support
* Integration with Travis CI


