---
title: ICommandWithParameters |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 66644c70-def7-46d8-8c47-b883292a0288
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8c43b41faa03ae9838cc0dcec619179d272f238e
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37408148"
---
# <a name="icommandwithparameters"></a>ICommandWithParameters
  改進 database engine 開頭的[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]允許 icommandwithparameters:: Getparameterinfo 以取得更精確的預期結果的描述。 這些更精確的結果可能不同於在舊版的 CommandWithParameters::GetParameterInfo 傳回的值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需詳細資訊，請參閱 <<c0> [ 中繼資料探索](../native-client/features/metadata-discovery.md)。  
  
 也從開始[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，當您呼叫 icommandwithparameters:: Setparameterinfo，傳遞給的值*pwszName*參數必須是有效的識別項。 如需詳細資訊，請參閱＜ [Database Identifiers](../databases/database-identifiers.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [介面&#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  
