---
title: ICommandWithParameters |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 66644c70-def7-46d8-8c47-b883292a0288
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 506a5f8d716529b7b2e6fe957830355e73c7c583
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43094483"
---
# <a name="icommandwithparameters"></a>ICommandWithParameters
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  改進 database engine 開頭的[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]允許 icommandwithparameters:: Getparameterinfo 以取得更精確的預期結果的描述。 這些更精確的結果可能不同於在舊版的 CommandWithParameters::GetParameterInfo 傳回的值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需詳細資訊，請參閱 <<c0> [ 中繼資料探索](../../relational-databases/native-client/features/metadata-discovery.md)。  
  
 此外，從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 開始，當您呼叫 ICommandWithParameters::SetParameterInfo 時，傳遞給 *pwszName* 參數的值必須是有效的識別碼。 如需詳細資訊，請參閱＜ [Database Identifiers](../../relational-databases/databases/database-identifiers.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [介面&#40;OLE DB&#41;](http://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)  
  
  
