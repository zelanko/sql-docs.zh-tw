---
title: ISSCommandWithParameters (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ISSCommandWithParameters (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- ISSCommandWithParameters interface
ms.assetid: 3419b7f3-36a3-4863-816e-e641e4e90496
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ceca46260d82cc6f9a179a642821aee55e57d6e3
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37429987"
---
# <a name="isscommandwithparameters-ole-db"></a>ISSCommandWithParameters (OLE DB)
  **ISSCommandWithParameters**公開支援[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]XML 和使用者定義型別 (UDT)。 這是選擇性的介面，繼承自核心的 OLE DB 介面**ICommandWithParameters**。 除了繼承自的三種方法**ICommandWithParameters**;**GetParameterInfo**， **MapParameterNames**，並**SetParameterInfo**;**ISSCommandWithParameters**提供用來處理伺服器特定資料類型的兩個新方法。  
  
> [!NOTE]  
>  **ISSCommandWithParameters**使用服務元件，但本身不會使用這個介面時，可以使用介面。  
  
|方法|描述|  
|------------|-----------------|  
|[Getparameterinfo &#40;OLE DB&#41;](isscommandwithparameters-getparameterproperties-ole-db.md)|傳回其中一個**SSPARAMPROPS**屬性設定為傳遞至命令，每個 UDT 或 XML 參數陣列中的結構，但沒有任何會傳回其他類型的參數。|  
|[Isscommandwithparameters:: Setparameterproperties &#40;OLE DB&#41;](isscommandwithparameters-setparameterproperties-ole-db.md)|根據每個參數來設定參數屬性，依序數，或藉由指定的陣列中設定大量參數屬性**SSPARAMPROPS**結構。|  
  
## <a name="see-also"></a>另請參閱  
 [介面&#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)   
 [使用 XML 資料類型](../native-client/features/using-xml-data-types.md)   
 [使用使用者定義型別](../native-client/features/using-user-defined-types.md)  
  
  
