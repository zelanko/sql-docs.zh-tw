---
title: 第 2 課： 在容器上建立原則並產生共用存取簽章（SAS）金鑰 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 41674d9d-8132-4bff-be4d-85a861419f3d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 80bd9c253adfcf1d1a677953fef183d9109534ef
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/19/2019
ms.locfileid: "75231817"
---
# <a name="lesson-2-create-a-policy-on-container-and-generate-a-shared-access-signature-sas-key"></a>第 2 課： 在容器上建立原則並產生共用存取簽章 (SAS) 金鑰
  在這一課，您將學習如何在 Blob 容器上建立原則以及產生 SAS 金鑰。  
  
 預存的存取原則可對伺服器端的共用存取簽章提供一層額外的控制。 共用存取簽章是一個 URI，會將有限的存取權限授與容器、Blob、佇列和資料表。 使用這項新的增強功能時，您需要在容器上建立具有讀取、寫入和列出權限的原則。  
  
 您可以使用下列其中一種方法建立原則和共用存取簽章：  
  
-   Azure REST API 作業：[建立容器](https://msdn.microsoft.com/library/azure/dd179468.aspx)、[設定容器 Acl](https://msdn.microsoft.com/library/azure/dd179391.aspx)和[取得容器 acl](https://msdn.microsoft.com/library/azure/dd179469.aspx)。  
  
-   Azure SDK 中的[CloudBlobContainer Cloudblobcontainer.getsharedaccesssignature 方法](https://docs.microsoft.com/dotnet/api/microsoft.azure.storage.blob.cloudblobcontainer.getsharedaccesssignature)。  
  
    ```  
  
       string signature = blob.GetSharedAccessSignature(new SharedAccessPolicy()   
        {   
            // Specify the expiration time for the signature.   
            SharedAccessExpiryTime = DateTime.Now.Years(1),   
            // Specify the permissions granted by the signature.    
            Permissions = SharedAccessPermissions.Write | SharedAccessPermissions.Read   
        });  
  
    ```  
  
-   協力廠商的 Azure explorer 工具，例如[Azure 儲存體總管](https://azurestorageexplorer.codeplex.com/)。  
  
 **下一課：**  
  
 [第3課：建立 SQL Server 認證](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)  
  
