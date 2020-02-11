---
title: ADOX （ADO）的提供者支援 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADOX provider support [ADO]
ms.assetid: 64234ce5-dc46-4c8a-a316-61956b6b9abb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2b07f4563d54254310c08c8c132d0729b8ccdc6b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67923211"
---
# <a name="provider-support-for-adox-ado"></a>ADOX (ADO) 的提供者支援
根據您的 OLE DB 資料提供者而定，不支援 ADOX 的某些功能。 [Microsoft Jet 的 OLE DB 提供者](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md)完全支援 ADOX。 適用于 SQL Server、 [microsoft OLE DB provider FOR ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)或[Microsoft OLE DB Provider for Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md)的[microsoft OLE DB 提供者](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)不支援的功能會列在下表中。 任何其他 Microsoft OLE DB 提供者都不支援 ADOX。  
  
## <a name="microsoft-ole-db-provider-for-sql-server"></a>Microsoft OLE DB Provider for SQL Server  
  
|物件或集合|使用限制|  
|--------------------------|-----------------------|  
|**資料表**集合|在物件建立之前，屬性是讀取/寫入，而在參考現有的物件時則是唯讀的。|  
|**Views**集合|不支援**Views** 。|  
|**程式**集合|不支援**附加**和**刪除**方法。|  
|**Procedure**物件|不支援**命令**屬性。|  
|**金鑰**集合|不支援**附加**和**刪除**方法。|  
|**Users**集合|不支援**使用者**。|  
|**群組**集合|不支援**群組**。|  
  
## <a name="microsoft-ole-db-provider-for-odbc"></a>Microsoft OLE DB Provider for ODBC  
  
|物件或集合|使用限制|  
|--------------------------|-----------------------|  
|**Catalog**物件|不支援**Create**方法。|  
|**資料表**集合|不支援**附加**和**刪除**方法。 在物件建立之前，屬性是讀取/寫入，而在參考現有的物件時則是唯讀的。|  
|**程式**集合|不支援**附加**和**刪除**方法。|  
|**Procedure**物件|不支援**命令**屬性。|  
|**索引**集合|不支援**附加**和**刪除**方法。|  
|**金鑰**集合|不支援**附加**和**刪除**方法。|  
|**Users**集合|不支援**使用者**。|  
|**群組**集合|不支援**群組**。|  
  
## <a name="microsoft-ole-db-provider-for-oracle"></a>Microsoft OLE DB Provider for Oracle  
  
|物件或集合|使用限制|  
|--------------------------|-----------------------|  
|**Catalog**物件|不支援**Create**方法。|  
|**資料表**集合|不支援**附加**和**刪除**方法。 在物件建立之前，屬性是讀取/寫入，而在參考現有的物件時則是唯讀的。|  
|**Views**集合|不支援**附加**和**刪除**方法。|  
|**View**物件|不支援**命令**屬性。|  
|**程式**物件|不支援**附加**和**刪除**方法。|  
|**Procedure**物件|不支援**命令**屬性。|  
|**索引**集合|不支援**附加**和**刪除**方法。|  
|**金鑰**集合|不支援**附加**和**刪除**方法。|  
|**Users**集合|不支援**使用者**。|  
|**群組**集合|不支援**群組**。|
