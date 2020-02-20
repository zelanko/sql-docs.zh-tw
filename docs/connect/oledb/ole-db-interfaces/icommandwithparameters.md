---
title: ICommandWithParameters | Microsoft Docs
description: ICommandWithParameters 介面
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 205a93fe5ce57a8b4c10fffb8648a1ef4c7b6506
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "68015457"
---
# <a name="icommandwithparameters"></a>ICommandWithParameters
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  從 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 開始，資料庫引擎的改進功能就允許 ICommandWithParameters::GetParameterInfo 針對預期的結果取得更精確的描述。 這些更精確的結果可能與舊版 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中 CommandWithParameters::GetParameterInfo 所傳回的值不同。 如需詳細資訊，請參閱[中繼資料探索](../../oledb/features/metadata-discovery.md)。  
  
 此外，從 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 開始，當您呼叫 ICommandWithParameters::SetParameterInfo 時，傳遞給 *pwszName* 參數的值必須是有效的識別碼。 如需詳細資訊，請參閱＜ [Database Identifiers](../../../relational-databases/databases/database-identifiers.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [介面 &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md) 
  
  
