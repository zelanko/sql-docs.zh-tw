---
title: ISSCommandWithParameters （OLE DB） |Microsoft Docs
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 08291b998c0f540b56cad59d29433135993487c8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "73761967"
---
# <a name="isscommandwithparameters-ole-db"></a>ISSCommandWithParameters (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **ISSCommandWithParameters**會公開對[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] XML 和使用者定義類型（UDT）的支援。 這是選擇性的介面，繼承自核心 OLE DB 介面**ICommandWithParameters**。 除了繼承自**ICommandWithParameters**的三個方法以外，**GetParameterInfo**、 **MapParameterNames**和**SetParameterInfo**;**ISSCommandWithParameters**提供兩種新的方法，可用來處理伺服器特定的資料類型。  
  
> [!NOTE]  
>  使用服務元件時，可以使用**ISSCommandWithParameters**介面，但服務元件本身不會使用此介面。  
  
|方法|描述|  
|------------|-----------------|  
|[ISSCommandWithParameters：： GetParameterProperties &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-getparameterproperties-ole-db.md)|針對傳遞至命令的每個 UDT 或 XML 參數以陣列傳回一個 **SSPARAMPROPS** 屬性集結構，但不會針對其他類型的參數傳回任何項目。|  
|[ISSCommandWithParameters：： SetParameterProperties &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md)|根據序數，設定每個參數的參數屬性，或指定**SSPARAMPROPS**結構的陣列來設定大量參數屬性。|  
  
## <a name="see-also"></a>另請參閱  
 [介面 &#40;OLE DB&#41;](https://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)   
 [使用 XML 資料類型](../../relational-databases/native-client/features/using-xml-data-types.md)   
 [使用使用者定義型別](../../relational-databases/native-client/features/using-user-defined-types.md)  
  
  
