---
title: ICommandWithParameters (OLE DB 驅動程式) | Microsoft Docs
description: 了解改進功能如何讓 ICommandWithParameters::GetParameterInfo 針對 OLE DB Driver for SQL Server 的預期結果取得更精確的說明。
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 21f3643737d1d6682133a252d52a072f73e81dfb
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861371"
---
# <a name="icommandwithparameters"></a>ICommandWithParameters
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  從 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 開始，資料庫引擎的改進功能就允許 ICommandWithParameters::GetParameterInfo 針對預期的結果取得更精確的描述。 這些更精確的結果可能與舊版 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中 CommandWithParameters::GetParameterInfo 所傳回的值不同。 如需詳細資訊，請參閱[中繼資料探索](../../oledb/features/metadata-discovery.md)。  
  
 此外，從 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 開始，當您呼叫 ICommandWithParameters::SetParameterInfo 時，傳遞給 *pwszName* 參數的值必須是有效的識別碼。 如需詳細資訊，請參閱＜ [Database Identifiers](../../../relational-databases/databases/database-identifiers.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [介面 &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md) 
  
  
