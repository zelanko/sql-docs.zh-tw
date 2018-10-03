---
title: ISSCommandWithParameters (OLE DB) |Microsoft Docs
description: ISSCommandWithParameters (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: reference
apiname:
- ISSCommandWithParameters (OLE DB)
apitype: COM
helpviewer_keywords:
- ISSCommandWithParameters interface
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 948650b7b50c4f79c46871900422ca44ea9e1455
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47694136"
---
# <a name="isscommandwithparameters-ole-db"></a>ISSCommandWithParameters (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  **ISSCommandWithParameters** 介面公開對 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] XML 和使用者定義型別 (UDT) 的支援。 這是選擇性的介面，繼承自核心的 OLE DB 介面 **ICommandWithParameters**。 除了繼承自 **ICommandWithParameters** 的三種方法 (**GetParameterInfo**、**MapParameterNames** 和 **SetParameterInfo**) 外，**ISSCommandWithParameters** 也提供兩種用來處理伺服器特定資料類型的新方法。  
  
> [!NOTE]  
>  在使用服務元件時，可以使用 **ISSCommandWithParameters** 介面，但服務元件本身不會使用此介面。  
  
|方法|Description|  
|------------|-----------------|  
|[Getparameterinfo &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-getparameterproperties-ole-db.md)|針對傳遞至命令的每個 UDT 或 XML 參數以陣列傳回一個 **SSPARAMPROPS** 屬性集結構，但不會針對其他類型的參數傳回任何項目。|  
|[Isscommandwithparameters:: Setparameterproperties &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md)|依照序數根據每個參數來設定參數的屬性，或指定 **SSPARAMPROPS** 結構的陣列來設定大量參數屬性。|  
  
## <a name="see-also"></a>另請參閱  
 [介面&#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)    
 [使用 XML 資料類型](../../oledb/features/using-xml-data-types.md)   
 [使用使用者定義型別](../../oledb/features/using-user-defined-types.md)  
  
  
