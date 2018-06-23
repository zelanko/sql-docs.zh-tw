---
title: ISSCommandWithParameters (OLE DB) |Microsoft 文件
description: ISSCommandWithParameters (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSCommandWithParameters (OLE DB)
apitype: COM
helpviewer_keywords:
- ISSCommandWithParameters interface
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: c07f297668674c7f5f41e6ce30ff4ee692da660f
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/16/2018
ms.locfileid: "35689121"
---
# <a name="isscommandwithparameters-ole-db"></a>ISSCommandWithParameters (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  **ISSCommandWithParameters**介面會公開支援[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]XML 和使用者定義型別 (UDT)。 它是選擇性的介面繼承自核心的 OLE DB 介面**ICommandWithParameters**。 除了繼承自的三種方法**ICommandWithParameters**;**GetParameterInfo**， **MapParameterNames**，和**SetParameterInfo**;**ISSCommandWithParameters**提供兩種新方法，可用來處理伺服器特定資料型別。  
  
> [!NOTE]  
>  **ISSCommandWithParameters**時使用服務元件，但服務元件不會使用這個介面，可以使用介面。  
  
|方法|描述|  
|------------|-----------------|  
|[Getparameterinfo &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-getparameterproperties-ole-db.md)|傳回一個**SSPARAMPROPS**屬性設定為傳遞至命令，每個 UDT 或 XML 參數陣列中的結構，但對於其他類型的參數傳回 none。|  
|[Isscommandwithparameters:: &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md)|依序數，根據每個參數來設定參數屬性，或藉由指定的陣列中設定大量參數屬性**SSPARAMPROPS**結構。|  
  
## <a name="see-also"></a>另請參閱  
 [介面&#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)    
 [使用 XML 資料類型](../../oledb/features/using-xml-data-types.md)   
 [使用使用者定義型別](../../oledb/features/using-user-defined-types.md)  
  
  
