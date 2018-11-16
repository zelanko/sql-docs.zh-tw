---
title: ISSCommandWithParameters (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- ISSCommandWithParameters (OLE DB)
apitype: COM
helpviewer_keywords:
- ISSCommandWithParameters interface
ms.assetid: 3419b7f3-36a3-4863-816e-e641e4e90496
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fc15aa5dd42edb7d9176fd2981dc291ba400b8f7
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51665278"
---
# <a name="isscommandwithparameters-ole-db"></a>ISSCommandWithParameters (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **ISSCommandWithParameters**公開支援[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]XML 和使用者定義型別 (UDT)。 這是選擇性的介面，繼承自核心的 OLE DB 介面**ICommandWithParameters**。 除了繼承自的三種方法**ICommandWithParameters**;**GetParameterInfo**， **MapParameterNames**，並**SetParameterInfo**;**ISSCommandWithParameters**提供用來處理伺服器特定資料類型的兩個新方法。  
  
> [!NOTE]  
>  **ISSCommandWithParameters**使用服務元件，但本身不會使用這個介面時，可以使用介面。  
  
|方法|描述|  
|------------|-----------------|  
|[Getparameterinfo &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-getparameterproperties-ole-db.md)|針對傳遞至命令的每個 UDT 或 XML 參數以陣列傳回一個 **SSPARAMPROPS** 屬性集結構，但不會針對其他類型的參數傳回任何項目。|  
|[Isscommandwithparameters:: Setparameterproperties &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md)|依照序數根據每個參數來設定參數的屬性，或指定 **SSPARAMPROPS** 結構的陣列來設定大量參數屬性。|  
  
## <a name="see-also"></a>另請參閱  
 [介面&#40;OLE DB&#41;](https://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)   
 [使用 XML 資料類型](../../relational-databases/native-client/features/using-xml-data-types.md)   
 [使用使用者定義型別](../../relational-databases/native-client/features/using-user-defined-types.md)  
  
  
