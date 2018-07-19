---
title: ICommandWithParameters |Microsoft 文件
description: ICommandWithParameters 介面
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
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: c41a3885293493299f6234f3dcc0ef5edc4040be
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/16/2018
ms.locfileid: "35689111"
---
# <a name="icommandwithparameters"></a>ICommandWithParameters
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  資料庫引擎開頭的改良[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]允許 icommandwithparameters:: Getparameterinfo 以取得更精確的預期結果的描述。 這些更精確的結果，在舊版的 CommandWithParameters::GetParameterInfo 傳回的值可能會有所不同[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 如需詳細資訊，請參閱[中繼資料探索](../../oledb/features/metadata-discovery.md)。  
  
 也從[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]，當您呼叫 icommandwithparameters:: Setparameterinfo，傳遞給的值*pwszName*參數必須是有效的識別項。 如需詳細資訊，請參閱＜ [Database Identifiers](../../../relational-databases/databases/database-identifiers.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [介面&#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md) 
  
  
