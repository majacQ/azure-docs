---
title: Troubleshoot the Azure Data Lake Storage connectors
titleSuffix: Azure Data Factory & Azure Synapse
description: Learn how to troubleshoot issues with the Azure Data Lake Storage Gen1 and Gen2 connectors in Azure Data Factory and Azure Synapse Analytics. 
author: jianleishen
ms.service: data-factory
ms.subservice: data-movement
ms.topic: troubleshooting
ms.date: 10/13/2021
ms.author: jianleishen
ms.custom: has-adal-ref, synapse
---

# Troubleshoot the Azure Data Lake Storage connectors in Azure Data Factory and Azure Synapse

[!INCLUDE[appliesto-adf-asa-md](includes/appliesto-adf-asa-md.md)]

This article provides suggestions to troubleshoot common problems with the Azure Data Lake Storage Gen1 and Gen2 connectors in Azure Data Factory and Azure Synapse.

## Azure Data Lake Storage Gen1

### Error message: The underlying connection was closed: Could not establish trust relationship for the SSL/TLS secure channel.

- **Symptoms**: Copy activity fails with the following error: 

    `Message: ErrorCode = UserErrorFailedFileOperation, Error Message = The underlying connection was closed: Could not establish trust relationship for the SSL/TLS secure channel.`

- **Cause**: The certificate validation failed during the TLS handshake.

- **Resolution**: As a workaround, use the staged copy to skip the Transport Layer Security (TLS) validation for Azure Data Lake Storage Gen1. You need to reproduce this issue and gather the network monitor (netmon) trace, and then engage your network team to check the local network configuration.

    :::image type="content" source="./media/connector-troubleshoot-guide/adls-troubleshoot.png" alt-text="Diagram of Azure Data Lake Storage Gen1 connections for troubleshooting issues.":::


### Error message: The remote server returned an error: (403) Forbidden

- **Symptoms**: Copy activity fail with the following error: 

   `Message: The remote server returned an error: (403) Forbidden.   
    Response details: {"RemoteException":{"exception":"AccessControlException""message":"CREATE failed with error 0x83090aa2 (Forbidden. ACL verification failed. Either the resource does not exist or the user is not authorized to perform the requested operation.)....`

- **Cause**: One possible cause is that the service principal or managed identity you use doesn't have permission to access certain folders or files.

- **Resolution**: Grant appropriate permissions to all the folders and subfolders you need to copy. For more information, see [Copy data to or from Azure Data Lake Storage Gen1](connector-azure-data-lake-store.md#linked-service-properties).

### Error message: Failed to get access token by using service principal. ADAL Error: service_unavailable

- **Symptoms**: Copy activity fails with the following error:

    `Failed to get access token by using service principal.  
    ADAL Error: service_unavailable, The remote server returned an error: (503) Server Unavailable.`

- **Cause**: When the Service Token Server (STS) that's owned by Azure Active Directory is not available, that means it's too busy to handle requests, and it returns HTTP error 503. 

- **Resolution**: Rerun the copy activity after several minutes.

## Azure Data Lake Storage Gen2

### Error code: ADLSGen2OperationFailed

- **Message**: `ADLS Gen2 operation failed for: %adlsGen2Message;.%exceptionData;.`

- **Causes and recommendations**: Different causes may lead to this error. Check below list for possible cause analysis and related recommendation.

  | Cause analysis                                               | Recommendation                                               |
  | :----------------------------------------------------------- | :----------------------------------------------------------- |
  | If Azure Data Lake Storage Gen2 throws error indicating some operation failed.| Check the detailed error message thrown by Azure Data Lake Storage Gen2. If the error is a transient failure, retry the operation. For further help, contact Azure Storage support, and provide the request ID in error message. |
  | If the error message contains the string "Forbidden", the service principal or managed identity you use might not have sufficient permission to access Azure Data Lake Storage Gen2. | To troubleshoot this error, see [Copy and transform data in Azure Data Lake Storage Gen2](./connector-azure-data-lake-storage.md#service-principal-authentication). |
  | If the error message contains the string "InternalServerError", the error is returned by Azure Data Lake Storage Gen2. | The error might be caused by a transient failure. If so, retry the operation. If the issue persists, contact Azure Storage support and provide the request ID from the error message. |

### Request to Azure Data Lake Storage Gen2 account caused a timeout error

- **Message**: 
  * Error Code = `UserErrorFailedBlobFSOperation`
  * Error Message = `BlobFS operation failed for: A task was canceled.`

- **Cause**: The issue is caused by the Azure Data Lake Storage Gen2 sink timeout error, which usually occurs on the Self-hosted Integration Runtime (IR) machine.

- **Recommendation**: 

    - Place your Self-hosted IR machine and target Azure Data Lake Storage Gen2 account in the same region, if possible. This can help avoid a random timeout error and produce better performance.

    - Check whether there's a special network setting, such as ExpressRoute, and ensure that the network has enough bandwidth. We suggest that you lower the Self-hosted IR concurrent jobs setting when the overall bandwidth is low. Doing so can help avoid network resource competition across multiple concurrent jobs.

    - If the file size is moderate or small, use a smaller block size for nonbinary copy to mitigate such a timeout error. For more information, see [Blob Storage Put Block](/rest/api/storageservices/put-block).

       To specify the custom block size, edit the property in your JSON file editor as shown here:
    
        ```
        "sink": {
            "type": "DelimitedTextSink",
            "storeSettings": {
                "type": "AzureBlobFSWriteSettings",
                "blockSizeInMB": 8
            }
        }
        ```

### The copy activity is not able to pick files from Azure Data Lake Storage Gen2

- **Symptoms**: The copy activity is not able to pick files from Azure Data Lake Storage Gen2 when the file name is "Asset_Metadata". The issue only occurs in the Parquet type dataset. Other types of datasets with the same file name work correctly.

- **Cause**: For the backward compatibility, `_metadata` is treated as a reserved substring in the file name. 

- **Recommendation**: Change the file name to avoid the reserved list for Parquet below: 
    1. The file name contains `_metadata`.
    2. The file name starts with `.` (dot).

## Next steps

For more troubleshooting help, try these resources:

- [Connector troubleshooting guide](connector-troubleshoot-guide.md)
- [Data Factory blog](https://azure.microsoft.com/blog/tag/azure-data-factory/)
- [Data Factory feature requests](/answers/topics/azure-data-factory.html)
- [Azure videos](https://azure.microsoft.com/resources/videos/index/?sort=newest&services=data-factory)
- [Microsoft Q&A page](/answers/topics/azure-data-factory.html)
- [Stack Overflow forum for Data Factory](https://stackoverflow.com/questions/tagged/azure-data-factory)
- [Twitter information about Data Factory](https://twitter.com/hashtag/DataFactory)
