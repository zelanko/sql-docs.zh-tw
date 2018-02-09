---
title: "ADOX (ADO) 提供者支援 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ADOX provider support [ADO]
ms.assetid: 64234ce5-dc46-4c8a-a316-61956b6b9abb
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a4a2a8c4f277e7e7fd4abc527e3d01a556a5295f
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="provider-support-for-adox-ado"></a>ADOX (ADO) 提供者支援
ADOX 的特定功能，不支援的視您的 OLE DB 資料提供者而定。 完全支援 ADOX [OLE DB Provider for Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md)。 不支援的功能與[Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)、 [Microsoft OLE DB Provider for ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)，或[Microsoft OLE DB Provider for Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md)是下表中列出。 ADOX 不支援的任何其他的 Microsoft OLE DB 提供者。  
  
## <a name="microsoft-ole-db-provider-for-sql-server"></a>Microsoft OLE DB Provider for SQL Server  
  
|物件或集合|使用限制|  
|--------------------------|-----------------------|  
|**資料表**集合|屬性是讀取/寫入之前建立的物件，以及唯讀時參考現有的物件。|  
|**檢視**集合|**檢視**不支援。|  
|**程序**集合|**附加**和**刪除**不支援的方法。|  
|**程序**物件|**命令**不支援屬性。|  
|**索引鍵**集合|**附加**和**刪除**不支援的方法。|  
|**使用者**集合|**使用者**不支援。|  
|**群組**集合|**群組**不支援。|  
  
## <a name="microsoft-ole-db-provider-for-odbc"></a>Microsoft OLE DB Provider for ODBC  
  
|物件或集合|使用限制|  
|--------------------------|-----------------------|  
|**目錄**物件|**建立**不支援方法。|  
|**資料表**集合|**附加**和**刪除**不支援的方法。 屬性是讀取/寫入之前建立的物件，以及唯讀時參考現有的物件。|  
|**程序**集合|**附加**和**刪除**不支援的方法。|  
|**程序**物件|**命令**不支援屬性。|  
|**索引**集合|**附加**和**刪除**不支援的方法。|  
|**索引鍵**集合|**附加**和**刪除**不支援的方法。|  
|**使用者**集合|**使用者**不支援。|  
|**群組**集合|**群組**不支援。|  
  
## <a name="microsoft-ole-db-provider-for-oracle"></a>Microsoft OLE DB Provider for Oracle  
  
|物件或集合|使用限制|  
|--------------------------|-----------------------|  
|**目錄**物件|**建立**不支援方法。|  
|**資料表**集合|**附加**和**刪除**不支援的方法。 屬性是讀取/寫入之前建立的物件，以及唯讀時參考現有的物件。|  
|**檢視**集合|**附加**和**刪除**不支援的方法。|  
|**檢視**物件|**命令**不支援屬性。|  
|**程序**物件|**附加**和**刪除**不支援的方法。|  
|**程序**物件|**命令**不支援屬性。|  
|**索引**集合|**附加**和**刪除**不支援的方法。|  
|**索引鍵**集合|**附加**和**刪除**不支援的方法。|  
|**使用者**集合|**使用者**不支援。|  
|**群組**集合|**群組**不支援。|
