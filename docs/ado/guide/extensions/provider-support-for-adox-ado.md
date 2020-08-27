---
description: ADOX (ADO) 的提供者支援
title: ADOX (ADO) 的提供者支援 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADOX provider support [ADO]
ms.assetid: 64234ce5-dc46-4c8a-a316-61956b6b9abb
author: rothja
ms.author: jroth
ms.openlocfilehash: cbc2b4821ac5c57c2302892caff1afa742e829b9
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978689"
---
# <a name="provider-support-for-adox-ado"></a>ADOX (ADO) 的提供者支援
視您的 OLE DB 資料提供者而定，不支援 ADOX 的某些功能。 [OLE DB Provider For Microsoft Jet](../appendixes/microsoft-ole-db-provider-for-microsoft-jet.md)完全支援 ADOX。 [Microsoft OLE DB Provider for SQL Server](../appendixes/microsoft-ole-db-provider-for-sql-server.md)的不支援功能、適用于[ODBC 的 Microsoft OLE DB 提供者](../appendixes/microsoft-ole-db-provider-for-odbc.md)或[Microsoft OLE DB Provider for Oracle](../appendixes/microsoft-ole-db-provider-for-oracle.md)列于下表中。 任何其他 Microsoft OLE DB 提供者都不支援 ADOX。  
  
## <a name="microsoft-ole-db-provider-for-sql-server"></a>Microsoft OLE DB Provider for SQL Server  
  
|物件或集合|使用限制|  
|--------------------------|-----------------------|  
|**資料表** 集合|屬性是在物件建立之前的讀取/寫入，而在參考現有的物件時，則是唯讀的。|  
|**Views** 集合|不支援**視圖**。|  
|**程式** 集合|不支援 **附加** 和 **刪除** 方法。|  
|**Procedure** 物件|不支援 **Command** 屬性。|  
|**金鑰** 集合|不支援 **附加** 和 **刪除** 方法。|  
|**使用者** 集合|不支援**使用者**。|  
|**群組** 集合|不支援**群組**。|  
  
## <a name="microsoft-ole-db-provider-for-odbc"></a>Microsoft OLE DB Provider for ODBC  
  
|物件或集合|使用限制|  
|--------------------------|-----------------------|  
|**Catalog** 物件|不支援 **Create** 方法。|  
|**資料表** 集合|不支援 **附加** 和 **刪除** 方法。 屬性是在物件建立之前的讀取/寫入，而在參考現有的物件時，則是唯讀的。|  
|**程式** 集合|不支援 **附加** 和 **刪除** 方法。|  
|**Procedure** 物件|不支援 **Command** 屬性。|  
|**索引** 集合|不支援 **附加** 和 **刪除** 方法。|  
|**金鑰** 集合|不支援 **附加** 和 **刪除** 方法。|  
|**使用者** 集合|不支援**使用者**。|  
|**群組** 集合|不支援**群組**。|  
  
## <a name="microsoft-ole-db-provider-for-oracle"></a>Microsoft OLE DB Provider for Oracle  
  
|物件或集合|使用限制|  
|--------------------------|-----------------------|  
|**Catalog** 物件|不支援 **Create** 方法。|  
|**資料表** 集合|不支援 **附加** 和 **刪除** 方法。 屬性是在物件建立之前的讀取/寫入，而在參考現有的物件時，則是唯讀的。|  
|**Views** 集合|不支援 **附加** 和 **刪除** 方法。|  
|**View** 物件|不支援 **Command** 屬性。|  
|**程式** 物件|不支援 **附加** 和 **刪除** 方法。|  
|**Procedure** 物件|不支援 **Command** 屬性。|  
|**索引** 集合|不支援 **附加** 和 **刪除** 方法。|  
|**金鑰** 集合|不支援 **附加** 和 **刪除** 方法。|  
|**使用者** 集合|不支援**使用者**。|  
|**群組** 集合|不支援**群組**。|