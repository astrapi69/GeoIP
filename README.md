GeoIP
=====

By default, CountryLookupTest expects to find the
GeoIP Country database in src/main/resources/GeoIP.dat

IMPORTANT API Change for 1.1.x users - as of GeoIP 1.1.0 the
lookupCountryXxxx methods return null if a country can not
be found (it used to return '--' or 'N/A'.  Be sure to check the
return value for null !

This is version 1.2.3 of the Java interface to GeoIP.  For more information
see http://www.maxmind.com/

As of version 1.1.4 this API is fully thread safe.

To get started for GeoIP Country, look at the code in CountryLookupTest.java.

CityLookupTest.java contains an example for the MaxMind GeoIP City database.
OrgLookupTest.java contains examples for the GeoIP Organization and ISP databases.
RegionLookupTest.java contains an example for the MaxMind GeoIP Region database.
NetspeedLookupTest.java contains an example for the MaxMind GeoIP Netspeed database.

BenchmarkGeoIP.java contains benchmarks for various databases using various options.

Note that CountryLookupTest assumes that you have the GeoIP Country database
installed at /usr/local/share/GeoIP/GeoIP.dat

A free GeoLite Country database is available from:
http://www.maxmind.com/app/geoip_country

A free GeoLite City database is available from:
http://www.maxmind.com/app/geolitecity

MaxMind GeoIP Country offers greater accuracy over the free database.
MaxMind GeoIP Country, Region, City, ISP, and Organization are available
for purchase from here:
http://www.maxmind.com/app/products

Please send any comments to support@maxmind.com


MEMORY CACHING AND OTHER OPTIONS
================================
The following options can be passed as the second parameter to the
LookupService constructor:

GEOIP_STANDARD - read database from filesystem, uses least memory.

GEOIP_MEMORY_CACHE - load database into memory, faster performance
        but uses more memory

GEOIP_CHECK_CACHE - check for updated database.  If database has been updated,
        reload filehandle and/or memory cache.

GEOIP_INDEX_CACHE - just cache
        the most frequently accessed index portion of the database, resulting
        in faster lookups than GEOIP_STANDARD, but less memory usage than
        GEOIP_MEMORY_CACHE - useful for larger databases such as
        GeoIP Organization and GeoIP City.  Note, for GeoIP Country, Region
        and Netspeed databases, GEOIP_INDEX_CACHE is equivalent to GEOIP_MEMORY_CACHE

Note the options can be combined, for example:
LookupService cl = new LookupService(dbfile, LookupService.GEOIP_MEMORY_CACHE | LookupService.GEOIP_CHECK_CACHE);

Windows Notes 
========================
If it doesn't work on Windows, try to remove or comment out all the "package com.maxmind.geoip" lines 
from all the files.
