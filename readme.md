﻿# Episerver Blob Provider for SQL Server
Store all blobs in the database instead of disk.

Easy deployment in load balanced environments, perfect for development teams, avoids committing your blobs into source control too.

Also works for Episerver Commerce as the assets are stored as regular media.

## Installation
If installed via NuGet, EpiserverFramework.config should be automatically transformed with the correct blob provider settings. If you need to change it manually, simply add the following to EpiserverFramework.config:

```xml
<blob defaultProvider="sqlBlobProvider">
    <providers>
      <add name="sqlBlobProvider" type="EPiCode.SqlBlobProvider.SqlBlobProvider, EPiCode.SqlBlobProvider" />
    </providers>
</blob>
```

## Local Caching
The provider can cache files on local disk to decrease the number of database calls. Set `loadFromDisk` to `true` on the blob configuration.

```xml
<blob defaultProvider="sqlBlobProvider">
    <providers>
      <add name="sqlBlobProvider" 
           type="EPiCode.SqlBlobProvider.SqlBlobProvider, EPiCode.SqlBlobProvider"
           loadFromDisk="true" 
           path="c:\my_custom_location" />
    </providers>
</blob>
```
If you do not specify the `path` attribute, it will default to `[appDataPath]\sqlProviderBlobs`

**Note!** Make sure the user configured for your application pool has write access to the local folder.

## Migration
If you are installing the SqlBlobProvider in an existing project that already uses the standard file blob provider, you will need to convert existing FileBlobs into SqlBlobs. This can easily be done with EPiCode.BlobConverter.This contains a scheduled job, which will convert all file blobs into the currently configured blob type. The conversion tool is not restricted to the SqlBlobProvider, so you could use it for other blob types as well.

## Usage
Used as any other blob provider. Install, and you are good to go.

**Important:** If you are going to serve a lot of large files on your site, memory consumption will probably increase as files will be loaded into server memory before being served.

## Support
This is an unsupported module. Use at your own risk.
