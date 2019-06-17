---
title: ADOX (ADO) 的提供者支援 |Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 0b99602eaf4f2d44548692271af2ad8af039ba0a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704403"
---
# <a name="provider-support-for-adox-ado"></a>ADOX (ADO) 的提供者支援
ADOX 的某些功能會不受支援，視您的 OLE DB 資料提供者而定。 具有完整支援 ADOX [OLE DB Provider for Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md)。 不支援的功能與[Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)，則[Microsoft OLE DB Provider for ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)，或有[Microsoft OLE DB Provider for Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md)是下表列出。 ADOX 不支援的任何其他的 Microsoft OLE DB 提供者。  
  
## <a name="microsoft-ole-db-provider-for-sql-server"></a>Microsoft OLE DB Provider for SQL Server  
  
|物件或集合|使用限制|  
|--------------------------|-----------------------|  
|**資料表**集合|參考現有的物件時，屬性是讀取/寫入之前建立的物件，且為唯讀狀態。|  
|**檢視**集合|**檢視**不支援。|  
|**程序**集合|**Append**並**刪除**不支援的方法。|  
|**程序**物件|**命令**不支援屬性。|  
|**索引鍵**集合|**Append**並**刪除**不支援的方法。|  
|**使用者**集合|**使用者**不支援。|  
|**群組**集合|**群組**不支援。|  
  
## <a name="microsoft-ole-db-provider-for-odbc"></a>Microsoft OLE DB Provider for ODBC  
  
|物件或集合|使用限制|  
|--------------------------|-----------------------|  
|**目錄**物件|**建立**不支援方法。|  
|**資料表**集合|**Append**並**刪除**不支援的方法。 參考現有的物件時，屬性是讀取/寫入之前建立的物件，且為唯讀狀態。|  
|**程序**集合|**Append**並**刪除**不支援的方法。|  
|**程序**物件|**命令**不支援屬性。|  
|**索引**集合|**Append**並**刪除**不支援的方法。|  
|**索引鍵**集合|**Append**並**刪除**不支援的方法。|  
|**使用者**集合|**使用者**不支援。|  
|**群組**集合|**群組**不支援。|  
  
## <a name="microsoft-ole-db-provider-for-oracle"></a>Microsoft OLE DB Provider for Oracle  
  
|物件或集合|使用限制|  
|--------------------------|-----------------------|  
|**目錄**物件|**建立**不支援方法。|  
|**資料表**集合|**Append**並**刪除**不支援的方法。 參考現有的物件時，屬性是讀取/寫入之前建立的物件，且為唯讀狀態。|  
|**檢視**集合|**Append**並**刪除**不支援的方法。|  
|**檢視**物件|**命令**不支援屬性。|  
|**程序**物件|**Append**並**刪除**不支援的方法。|  
|**程序**物件|**命令**不支援屬性。|  
|**索引**集合|**Append**並**刪除**不支援的方法。|  
|**索引鍵**集合|**Append**並**刪除**不支援的方法。|  
|**使用者**集合|**使用者**不支援。|  
|**群組**集合|**群組**不支援。|
